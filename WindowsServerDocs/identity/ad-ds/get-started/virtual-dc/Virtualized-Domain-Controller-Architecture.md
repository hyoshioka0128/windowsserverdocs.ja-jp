---
ms.assetid: 341614c6-72c2-444f-8b92-d2663aab7070
title: 仮想化ドメイン コントローラーのアーキテクチャ
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: e8673b9e66a0aa3b6bea89b91ae5022efb26c65c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71390509"
---
# <a name="virtualized-domain-controller-architecture"></a>仮想化ドメイン コントローラーのアーキテクチャ

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

このトピックでは、仮想化ドメイン コントローラーの複製および安全な復元のアーキテクチャについて説明します。 複製と安全な復元のプロセスをフローチャートで示し、その後プロセスの各手順について詳しく取り上げます。  
  
-   [仮想化ドメインコントローラーの複製のアーキテクチャ](../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Architecture.md#BKMK_CloneArch)  
  
-   [仮想化ドメインコントローラーの安全な復元のアーキテクチャ](../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Architecture.md#BKMK_SafeRestoreArch)  
  
## <a name="BKMK_CloneArch"></a>仮想化ドメインコントローラーの複製のアーキテクチャ  
  
### <a name="overview"></a>概要  
仮想化ドメイン コントローラーの複製は、ハイパーバイザー プラットフォームを使用して **VM-Generation ID** と呼ばれる識別子を公開し、仮想マシンの作成を検出します。 この識別子の値は、ドメイン コントローラーの昇格中に、AD DS によってデータベース (NTDS.DIT) に格納されます。 仮想マシンを起動すると、その仮想マシン内の VM-Generation ID の現在値は、データベース内の値と比較されます。 2 つの値が異なる場合は、ドメイン コントローラーにより起動 ID がリセットされ、RID プールが破棄されます。これにより、USN の再利用、またはセキュリティ プリンシパルが重複して作成されるのを防ぐことができます。 次に、「[複製プロセスの詳細](../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Architecture.md#BKMK_CloneProcessDetails)」の手順 3. で示されている場所で、DCCloneConfig.xml ファイルが検索されます。 DCCloneConfig.xml ファイルが見つかった場合は、複製としてデプロイされているものと判断します。したがって、ソース メディアからコピーされた既存の NTDS.DIT および SYSVOL の内容を使用して再昇格することで複製を開始して、自身を追加のドメイン コントローラーとしてプロビジョニングします。  
  
VM-GenerationID をサポートするハイパーバイザーと、サポートしないハイパーバイザーが混在する環境では、VM-GenerationID をサポートしないハイパーバイザーに複製メディアが誤ってデプロイされる可能性があります。 DCCloneConfig.xml ファイルの存在は、DC の複製を管理しようとしていることを示します。 したがって、ブート時に DCCloneConfig.xml ファイルが見つかったのに、VM-GenerationID がホストから提供されていない場合は、環境のその他の部分が影響を受けないように、複製 DC はディレクトリ サービス復元モード (DSRM) でブートされます。 その後、VM-GenerationID をサポートするハイパーバイザーに複製メディアを移動し、複製を再試行できます。  
  
VM-GenerationID をサポートするハイパーバイザーに複製メディアがデプロイされているにもかかわらず、DCCloneConfig.xml ファイルが提供されていない場合、その DIT と新しい VM の VM-GenerationID が異なることが DC によって検出され、USN の再利用と SID の重複を防ぐためにセーフガードがトリガーされます。 ただし、複製が開始されないため、セカンダリ DC は、ソース DC と同じ ID で引き続き実行されます。 このセカンダリ DC は、環境内での不整合を避けるためにできるだけ早くネットワークから削除する必要があります。 更新が出力方向にレプリケートされるようにしながら、このセカンダリ DC を再利用する方法の詳細については、Microsoft サポート技術情報の記事 [2742970](https://support.microsoft.com/kb/2742970)を参照してください。  
  
### <a name="BKMK_CloneProcessDetails"></a>詳細な処理の複製  
次の図は、初期の複製操作および複製再試行操作のアーキテクチャを示しています。 これらのプロセスについては、このトピックでさらに詳しく後述します。  
  
**初期複製操作**  
  
![仮想化 DC のアーキテクチャ](media/Virtualized-Domain-Controller-Architecture/ADDS_VDC_InitialCloningProcess.png)  
  
**複製再試行操作**  
  
![仮想化 DC のアーキテクチャ](media/Virtualized-Domain-Controller-Architecture/ADDS_VDC_CloningRetryProcess.png)  
  
以降の手順では、プロセスについてさらに詳しく説明します。  
  
1.  VM-Generation ID をサポートするハイパーバイザーで、既存の仮想マシンのドメイン コントローラーが起動します。  
  
    1.  この VM では、昇格後の AD DS コンピューター オブジェクトに、既存の VM Generation-ID 値が設定されていません。  
  
    2.  これが NULL の場合でも、新しい VM Generation-ID が一致しないので、次のコンピューター作成では引き続き複製が行われることになります。  
  
    3.  VM Generation-ID は、DC を次回再起動したときに設定され、レプリケートされません。  
  
2.  次に、仮想マシンは、VMGenerationCounter ドライバーによって提供された VM-Generation ID を読み取り、 2 つの VM-Generation ID を比較します。  
  
    1.  ID が一致する場合、これは新しい仮想マシンではないため、複製は行われません。 DCCloneConfig.xml ファイルが存在する場合は、複製が行われないように、時間/日付スタンプが含まれるファイルの名前が変更されます。 サーバーは引き続き正常に起動されます。 Windows Server 2012 で仮想ドメイン コントローラーを再起動すると、すべてこのように動作します。  
  
    2.  2 つの ID が一致しない場合、これは、以前のドメイン コントローラーの NTDS.DIT が含まれる新しい仮想マシン (または、復元されたスナップショット) です。 DCCloneConfig.xml ファイルが存在する場合は、複製操作が続行されます。 存在しない場合は、スナップショット復元操作が引き続き行われます。 「 [Virtualized domain controller safe restore architecture](../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/../../../ad-ds/get-started/virtual-dc/Virtualized-Domain-Controller-Architecture.md#BKMK_SafeRestoreArch)」を参照してください。  
  
    3.  ハイパーバイザーが比較のための VM-Generation ID を提供していないのに、DCCloneConfig.xml ファイルが存在する場合は、ネットワークでドメイン コントローラーが重複しないようにファイル名が変更され、ゲストは DSRM でブートされます。 dccloneconfig.xml ファイルがない場合、ゲストは正常にブートされます (ネットワーク上に重複ドメイン コントローラーが存在する可能性があります)。 この重複ドメインコントローラーを再利用する方法の詳細については、Microsoft サポート技術情報の記事 [2742970](https://support.microsoft.com/kb/2742970)を参照してください。  
  
3.  NTDS サービスによって、(HKEY_Local_Machine\System\CurrentControlSet\Services\Ntds\Parameters の) VDCisCloning DWORD レジストリ値の名前がチェックされます。  
  
    1.  この名前がない場合は、この仮想マシンの複製を初めて実行しようとしたことを意味します。 ゲストは VDC オブジェクト重複セーフガードを実装することで、ローカル RID プールを無効にして、ドメイン コントローラーに対して新しいレプリケーション起動 ID を設定します。  
  
    2.  これが既に 0x1 に設定されている場合は、"再試行" 複製を行おうとしており、以前の複製操作は失敗しました。 VDC オブジェクト重複の安全対策は採られていません。この対策は既に一度実行され、不必要にゲストを複数回変更した可能性があるからです。  
  
4.  IsClone DWORD レジストリ値の名前が (Hkey_Local_Machine\System\CurrentControlSet\Services\NTDS\Parameters に) 書き込まれます。  
  
5.  NTDS サービスによりゲスト ブート フラグが変更され、以降のすべての再起動が DS 修復モードで開始されます。  
  
6.  NTDS サービスは、受理された 3 つの場所、つまりドライブのルートにある DSA 作業ディレクトリ、%windir%\NTDS、またはリムーバブル読み取り/書き込みメディアのいずれかで、ドライブ文字順に DcCloneConfig.xml を読み取ろうとします。  
  
    1.  ファイルが有効な場所にない場合は、IP アドレスが重複していないかどうかが確認されます。 IP アドレスが重複していない場合、サーバーは正常に起動されます。 重複している IP アドレスがあると、コンピューターは、ネットワークでドメイン コントローラーが重複しないように DSRM でブートされます。  
  
    2.  ファイルが有効な場所にある場合は、NTDS サービスによりその設定が検証されます。 ファイル (または特定の設定) がブランクの場合は、NTDS によってその設定の値が自動的に構成されます。  
  
    3.  DcCloneConfig.xml が存在するが、無効なエントリが含まれている場合、または読み取り不可になっている場合は、複製に失敗し、ゲストはディレクトリ サービス復元モード (DSRM) でブートされます。  
  
7.  ソース コンピューター名と IP アドレスが誤って乗っ取られないように、すべての DNS 自動登録が無効になります。  
  
8.  Netlogon サービスは、クライアントからのネットワーク AD DS 要求のアドバタイズまたは回答を防ぐために停止されます。  
  
9. NTDS は、DefaultDCCloneAllowList.xml または CustomDCCloneAllowList.xml に含まれないサービスまたはプログラムがインストールされていないことを検証します。  
  
    1.  既定の除外許可リストまたはユーザー定義の除外許可リストに含まれないサービスまたはプログラムがインストールされている場合は、複製に失敗し、ゲストは、ネットワークでドメイン コントローラーが重複しないように DSRM でブートされます。  
  
    2.  非互換性がない場合は、複製が続行します。  
  
10. DCCloneConfig.xml ネットワーク設定がブランクであることが原因で IP アドレスの自動割り当てが使用される場合は、ネットワーク アダプター上の DHCP が、IP アドレス リース、ネットワーク ルーティング、および名前解決に関する情報を取得できるように設定されます。  
  
11. ゲストが、PDC エミュレーター FSMO 役割が実行されているドメイン コントローラーを特定し、そのコントローラーに接続します。 その際、DNS および DCLocator プロトコルが使用されます。 これにより、ドメイン コントローラー コンピューター オブジェクトを複製するために、RPC 接続が確立され、IDL_DRSAddCloneDC メソッドが呼び出されます。  
  
    1.  ゲストのソース コンピューター オブジェクトに、最上位ドメイン拡張アクセス許可 "DC にそれ自身の複製の作成を許可する" がある場合、複製は続行されます。  
  
    2.  ゲストのソース コンピューター オブジェクトにその拡張アクセス許可がない場合は、複製に失敗し、ゲストは、ネットワークでドメイン コントローラーが重複しないように DSRM でブートされます。  
  
12. AD DS コンピューター オブジェクト名は、DCCloneConfig.xml で指定された名前と一致するように設定されるか (存在する場合)、PDCE で自動的に生成されます。 NTDS によって、適切な Active Directory 論理サイトに対して適切な NTDS 設定オブジェクトが作成されます。  
  
    1.  これが PDC 複製の場合は、ローカル コンピューターの名前が変更され、ゲストは再起動されます。 は、再起動後は、ここでも、手順 1 ~ 10 を通過し、手順 13. に進みます。  
  
    2.  これがレプリカ DC 複製の場合、この段階では再起動は行われません。  
  
13. ゲストが昇格の設定を DS 役割サーバー サービスに提供し、そのサービスが昇格を開始します。  
  
14. DS 役割サーバー サービスによって、すべての AD DS 関連サービス (NTDS、NTFRS/DFSR、KDC、DNS).が停止されます。  
  
15. ゲストが、(既定の Windows タイム サービス階層内で、つまり、PDCE を使用して) 他のドメイン コントローラーとの NT5DS (Windows NTP) 時間同期を強制的に実行し、 PDCE に接続します。 既存の Kerberos チケットがフラッシュします。  
  
16. ゲストが、DFSR または NTFRS サービスが自動的に実行されるように構成し、 ゲストは、すべての既存 DFSR と NTFRS データベース ファイルを削除 (既定: c:\windows\ntfrs と c:\system ボリューム information\dfsr\\ *< database_GUID >* )、サービスを開始することは、次に、権限のない SYSVOL 同期を強制するためにします。 SYSVOL のファイルの内容は、後で同期を開始するときに SYSVOL をプレシードできるように削除されません。  
  
17. ゲストの名前が変更されます。 ゲスト上の DS 役割サーバー サービスは、既存の NTDS.DIT データベース ファイルを、通常の昇格のように c:\windows\system32 に含まれているテンプレート データベースとしてではなく、ソースとして使用して、AD DS 構成 (昇格) を開始します。  
  
18. ゲストが、RID マスター FSMO 役割の保有者に接続して、新しい RID プール割り当てを取得します。  
  
19. 昇格プロセスにより新しい起動 ID が作成され、複製されたドメイン コントローラーに対して、NTDS 設定オブジェクトが再作成されます (複製に関係なく。既存の NTDS.DIT データベースを使用している場合、これはドメイン昇格の一環して行われます)。  
  
20. NTDS は、見つからないオブジェクト、新しいオブジェクト、または新しいバージョンのオブジェクトで、パートナー ドメイン コントローラーからレプリケーションを行います。 NTDS.DIT には、ソース ドメイン コントローラーがオフラインになったときからのオブジェクトが既に含まれています。受信レプリケーション トラフィックを最小限に抑えるために、このオブジェクトができる限り使用されます。 グローバル カタログ パーティションは設定されています。  
  
21. DFSR または FRS サービスが開始します。データベースがないため、SYSVOL は、レプリケーション パートナーから権限のない入力方向の同期を実行します。 このプロセスでは、ネットワーク レプリケーション トラフィックを最小限に抑えるために、SYSVOL フォルダーの既存のデータが再利用されます。  
  
22. ゲストが DNS クライアント登録を再度有効にし、コンピューターには一意の名前が付けられ、ネットワークが設定されます。  
  
23. ゲストが、以前のコンピューター名と SID をスクラブするために、DefaultDCCloneAllowList.xml <SysprepInformation> 要素で指定された SYSPREP モジュールを実行します。  
  
24. 昇格の複製が完了します。  
  
    1.  ゲストが、次回正常に再起動されるように DSRM ブート フラグを削除します。  
  
    2.  ゲストが、日付/時間が含まれる DCCloneConfig.xml の名前を変更します。これにより、次回起動時に名前が再度読み取られなくなります。  
  
    3.  ゲストが、HKEY_Local_Machine\System\CurrentControlSet\Services\NTDS\Parameters の VdcIsCloning DWORD レジストリ値の名前を削除します。  
  
    4.  ゲストが、HKEY_Local_Machine\System\CurrentControlSet\Services\NTDS\Parameters to 0x1 の "VdcCloningDone" DWORD レジストリ値の名前を設定します。 Windows ではこの値は使用されません。代わりに、この値はマーカーとしてサード パーティに提供されます。  
  
25. ゲストが、複製された独自のドメイン コントローラー オブジェクトの msDS-GenerationID 属性を、現在のゲスト VM-Generation ID に合わせて更新します。  
  
26. ゲストが再起動されます。 これで、通常のアドバタイズ ドメイン コントローラーになりました。  
  
## <a name="BKMK_SafeRestoreArch"></a>仮想化ドメインコントローラーの安全な復元のアーキテクチャ  
  
### <a name="overview"></a>概要  
AD DSは、ハイパーバイザー プラットフォームを使用して **VM-Generation ID** と呼ばれる識別子を公開し、仮想マシンのスナップショット復元を検出します。 この識別子の値は、ドメイン コントローラーの昇格中に、AD DS によってデータベース (NTDS.DIT) に格納されます。 管理者が以前のスナップショットから仮想マシンを復元するとき、仮想マシン内の VM-Generation ID の現在値がデータベース内の値と比較されます。 2 つの値が異なる場合は、ドメイン コントローラーにより起動 ID がリセットされ、RID プールが破棄されます。これにより、USN の再利用、またはセキュリティ プリンシパルが重複して作成されるのを防ぐことができます。 安全な復元が行われるシナリオは 2 つあります。  
  
-   仮想ドメイン コントローラーのシャットダウン中、スナップショットの復元後にそのコントローラーが起動されたとき  
  
-   実行中の仮想ドメイン コントローラーでスナップショットが復元されたとき  
  
    スナップショットの仮想化ドメイン コントローラーが、シャットダウンではなく中断されている状態の場合は、AD DS サービスを再開して新しい RID プール要求をトリガーする必要があります。 AD DS サービスを再開するには、サービス スナップインまたは Windows PowerShell (Restart-Service NTDS -force) を使用します。  
  
次の各セクションでは、各シナリオの安全な復元について詳しく説明します。  
  
### <a name="safe-restore-detailed-processing"></a>安全な復元の詳細なプロセス  
次のフローチャートは、仮想ドメイン コントローラーのシャットダウン中、スナップショットの復元後にそのコントローラーが起動されたときに、安全な復元がどのように行われるかを示しています。  
  
![仮想化 DC のアーキテクチャ](media/Virtualized-Domain-Controller-Architecture/ADDS_VDC_VirtualizationSafeguardsDuringNormalBoot.png)  
  
1.  スナップショットの復元後に仮想マシンが起動されると、スナップショットが復元されたことにより、その仮想マシンにはハイパーバイザー ホストによって新しい VM-Generation ID が提供されます。  
  
2.  仮想マシンの新しい VM-Generation ID はデータベースの VM-Generation ID と比較されます。 2 つの ID が一致しないと、仮想化セーフガードが適用されます (前のセクションの手順 3. を参照)。 復元による適用が完了すると、AD DS コンピューター オブジェクトに設定された VM-GenerationID が、ハイパーバイザー ホストによって適用された新しい ID に合わせて更新されます。  
  
3.  仮想化セーフガードは、次の操作によって適用されます。  
  
    1.  ローカル RID プールを無効にする。  
  
    2.  ドメイン コントローラー データベースに対して新しい起動 ID を設定する。  
  
> [!NOTE]  
> 安全な復元のこの部分は、複製プロセスと重複します。 このプロセスは、スナップショット復元後に仮想ドメイン コントローラーを起動した後の、そのドメイン コントローラーの安全な復元に関するものですが、これと同じ手順が、複製プロセスでも行われます。  
  
次の図は、実行中の仮想ドメイン コントローラーでスナップショットが復元されるときに、仮想化セーフガードが、USN ロールバックによる相違を防ぐ方法を示しています。  
  
![仮想化 DC のアーキテクチャ](media/Virtualized-Domain-Controller-Architecture/ADDS_VDC_VirtualizationSafeguardsDuringSnapShotRestore.png)  
  
> [!NOTE]  
> このイラストは、概念を説明するために簡素化されています。  
  
1.  Time T1 の時点で、ハイパーバイザー管理者は仮想 DC1 のスナップショットを取得します。 この段階の DC1 には、USN 値 (実際は**highestCommittedUsn** ) 100、InvocationId (この図では ID として示されています) A (実際は GUID) が設定されています。 savedVMGID 値は、DC の DIT ファイルの VM-GenerationID です ( **msDS-GenerationId**という名前の属性の DC のコンピューター オブジェクトに対して格納)。 VMGID は、仮想マシン ドライバーから使用できる VM-GenerationId の現在の値です。 この値は、ハイパーバイザーによって提供されます。  
  
2.  次の Time T2 で、100 人のユーザーがこの DC に追加されています (ユーザーを、Time T1 と Time T2 の間にこの DC で実行された可能性のある更新の例と考えます。実際の更新では、ユーザーの作成、グループの作成、パスワードの更新、属性の更新などが混在しています)。 この例では、更新ごとに 1 つの一意の USN が使用されます (実際は、ユーザー作成により複数の USN が使用される可能性があります)。 DC1 は、これらの更新をコミットする前に、データベースの VM-GenerationID の値 (savedVMGID) が、ドライバーから使用できる現在の値 (VMGID) と同じかどうかを確認します。 同じ場合は、ロールバックがまだ行われていないため、更新はコミットされ、USN は 200 になります。これは次の更新では USN 201 が使用されることを意味します。 InvocationId、savedVMGID、または VMGID に変更はありません。 これらの更新は、次のレプリケーション サイクルで DC2 にレプリケートされます。 DC2 は、ここで表現されている高基準値 (および**UptoDatenessVector**) を、DC1 (A) @USN = 200 として単純に更新します。 つまり、DC2 は、USN 200 を介した nvocationId A のコンテキストでは、DC1 からのすべての更新を認識します。  
  
3.  Time T3 の時点で、Time T1 で取得されたスナップショットが DC1 に適用されます。 DC1 がロールバックされたため、その USN は 100 にロールバックされます。これは、DC1 が USN を 101 から使用して、以降の更新と関連付ける可能性があることを示しています。 ただし、この時点で、VMGID の値は、VM-GenerationID をサポートするハイパーバイザーによって異なります。  
  
4.  続いて、DC1 は、更新を実行するときに、データベースの VM-GenerationId の値 (savedVMGID) が仮想マシンドライバーの値 (VMGID) と同じかどうかを確認します。 値が同じでない場合、DC1 はロールバックが行われたと推測し、仮想化セーフガードをトリガーします。つまり、その InvocationId (ID = B) をリセットして、RID プールを破棄します (この図では示されていません)。 VMGID の新しい値をそのデータベースに保存し、新しい InvocationId B のコンテキストでこれらの更新 (USN 101 - 250) をコミットします。次のレプリケーション サイクルで DC2 は何も知らず DC1 から InvocationId B のコンテキストで、InvocationID B. に関連付けられている DC1 からすべての要求その結果、スナップショットの適用後に DC1 上で実行される更新は安全に収束します。 さらに、T2 の時点で DC1 で行われた一連の更新 (スナップショットの復元後に DC1 で失われた更新) は、DC2 にレプリケートされていたため、(DC1 の点線で示すように) スケジュールされた次のレプリケーションで DC1 にレプリケートされます。  
  
ゲストが仮想化セーフガードを適用すると、NTDS は、パートナー ドメイン コントローラーから、Active Directory オブジェクト差分の権限のない入力方向レプリケーションを行います。 レプリケート先ディレクトリ サービスの最新のベクターは、それに従って更新されます。 その後、ゲストは SYSVOL を同期します。  
  
-   FRS を使用している場合、ゲストは NTFRS サービスを停止し、D2 BURFLAGS レジストリ値を設定します。 その後、可能な場合は、変更されていない既存の SYSVOL データを再利用して、NTFRS サービスを開始し、権限のない入力方向のレプリケーションを行います。  
  
-   ゲストは DFSR サービスを停止し、DFSR データベース ファイルを削除 DFSR を使用する場合 (既定の場所: %systemroot%\system ボリューム information\dfsr\\ *<database GUID>* )。 その後、可能な場合は、変更されていない既存の SYSVOL データを再利用して、DFSR サービスを開始し、権限のない入力方向のレプリケーションを行います。  
  
> [!NOTE]  
> -   ハイパーバイザーが比較のための VM-Generation ID を提供していない場合、そのハイパーバイザーでは仮想化セーフガードがサポートされていません。ゲストは、Windows Server 2008 R2 以前が実行されている仮想化ドメイン コントローラーのように動作します。 パートナー DC によって確認される最新の最大 USN を超えていない USN でレプリケーションを開始しようとすると、ゲストでは USN ロールバック検疫保護が実装されます。 USN ロールバック検疫保護の詳細については、「 [USN and USN Rollback (USN と USN ロールバック)](https://technet.microsoft.com/library/virtual_active_directory_domain_controller_virtualization_hyperv(WS.10).aspx)」を参照してください。  
  


