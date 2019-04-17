---
title: "AD フォレストの回復 - Windows Server 2003 の回復"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 5a291f65-794e-4fc3-996e-094c5845a383
ms.technology: identity-adfs
ms.openlocfilehash: daebbc65b9864554fde839c3865f507ab787e6b6
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="ad-forest-recovery---windows-server-2003-recovery"></a>AD フォレストの回復 - Windows Server 2003 の回復

>適用対象: Windows Server 2003

このトピックには、Windows Server 2003 を実行するドメイン コントローラー (Dc) のフォレストの回復手順が含まれています。 フォレストの回復のための一般的なプロセスは、Windows Server 2003 Dc と違いはありませんが、さまざまなツールのための具体的な手順が異なることができます。 たとえば、バックアップし、Windows Server 2008 が実行されている Dc の使用またはそれ以降は、Windows Server バックアップまたは Wbadmin.exe 一方、Windows Server 2003 Dc が実行されている Dc を復元する Ntdsutil.exe を使用できます。  
  
-   [システム状態データをバックアップします。](#Backing-up-the-System-State-data)  
  
-   [非 authoritative restore を実行します。](#Performing-a-nonauthoritative restore)  
  
-   [インストールして、DNS サーバー サービスを構成します。](#Install-and-configure-the-DNS-Server-service)  
  
  
## <a name="backing-up-the-system-state-data"></a>システム状態データをバックアップします。  
 Windows Server 2003 を実行している DC の現在のバックアップ操作用に選択したその他のデータと共に、システム状態データをバックアップするには、次の手順を使用します。 Windows Server 2003 には、システム状態データのバックアップに使用できる Ntbackup ツールが含まれています。  
  
 メンバーシップ**管理者**または**Backup Operators**、またはそれと同等のファイルとフォルダーをバックアップするために必要な最低限です。   
  
 システム状態データをテープにバックアップするバックアップ プログラムことを示していない未使用のメディア利用可能な場合は、リムーバブル記憶域を使用する必要があります。 これは、テープを追加、空きメディア プールそのバックアップが使用できるようにします。  
  
 ローカル コンピューター上のシステム状態データをバックアップすることのみことができます。 リモート コンピューターで、それをバックアップできません。  
  
### <a name="to-back-up-the-system-state-data-on-a-domain-controller-that-runs-windows-server-2003"></a>Windows Server 2003 を実行するドメイン コントローラーのシステム状態データをバックアップするのには  
  
1.  をクリックして**開始**、] をポイント**すべてのプログラム**、] をポイント**アクセサリ**、] をポイント**システム ツール**、] をクリックし、**バックアップ**します。  
  
2.  **ようこそ**] ページで [**詳細モード**します。  
  
3.  **バックアップ**] タブで、ドライブ、フォルダー、またはバックアップするファイルのチェック ボックスをオンにします。  
  
4.  選択、**システム状態**チェック ボックスをオンします。  
  
5.  をクリックして**バックアップを開始**します。  
  
  
## <a name="performing-a-nonauthoritative-restore"></a>非 authoritative restore を実行します。  
 Windows Server 2003 を実行している DC の権限のない状態の復元を実行するのにには、次の手順を使用します。 を Windows Server 2003 の Active Directory で非 authoritative restore を実行することと、SYSVOL の権限のない状態の復元が自動的に実行します。 追加の手順は必要ありません。  
  
> [!NOTE]
>  Windows Server 2003 オペレーティング システムを再インストールも場合するが、コンピューターをドメインに参加しない場合があり、オペレーティング システムのセットアップ中に、コンピューターに任意の名前を付けることができます。 Active Directory はインストールされません。 オペレーティング システムを再インストールした後は、手順 4 に直接移動します。  
  
 システム状態のデータのみを復元した Windows Server 2003 ドメイン コントローラーでも回復する前にドメイン コントローラーで実行されていたソフトウェア アプリケーションを再インストールする必要があります。 両者がシステム状態データの一部であるために、レジストリを復元も、ドメインの最初の DC では AD DS を復元します。 これらの Dc で実行されているすべてのアプリケーションがあった場合、およびレジストリに保存されたあらゆる情報を保持していた場合は、この点に留意してください。  
  
 ソフトウェアを再インストールに必要な時間を節約するには、かどうか、ドメイン コントローラーにインストールする必要があるアプリケーションは仮想 DC の複製と互換性を確認します。 このようなアプリケーションは、時間と、複製された仮想ドメイン コントローラーにインストールに必要な作業を保存するために複製前に、ソース ドメイン コントローラーにインストールできます。  
  
#### <a name="to-perform-a-nonauthoritative-restore"></a>非 authoritative restore を実行するには  
  
1.  ドメイン コントローラーを開始した後は、ディレクトリ サービス復元モード (DSRM) でコンピューターを再起動する F8 キーを押します。  
  
2.  選択**ディレクトリ サービス復元モード (Windows ドメイン コントローラーのみ)**します。  
  
3.  復元モードで起動するオペレーティング システムを選択します。  
  
4.  (するのみドメイン ログオン オプションがない、ローカル コンピューター アカウントを使用することができます)、管理者としてログオンします。  
  
5.  コマンド プロンプトで次のように入力します。**ntbackup**、し、Enter キーを押します。  
  
6.  **ようこそ**] ページで [**詳細モード**、し、[、**復元メディアと管理**タブ (選択しないでください**復元ウィザード**.)  
  
7.  復元していることを確認する適切なバックアップ ファイルを選択、**システム ディスク**と**システム状態**チェック ボックスがオンにします。  
  
8.  をクリックして**復元の開始**します。  
  
9. 復元操作が完了したら、コンピューターを再起動します。  
  
 Windows Server 2003 を実行している DC で SYSVOL の権限のある (プライマリとも呼ばれます) 復元を実行するのにには、次の手順を使用します。 ドメイン内に復元された最初の Windows Server 2003 DC でのみ、この手順を実行します。  
  
### <a name="to-perform-an-authoritative-restore-of-sysvol"></a>SYSVOL の authoritative restore を実行するには  
  
1.  前の手順では、手順 1 ~ 8 を実行します。  
  
2.  **復元の確認**ダイアログ ボックスで、] をクリックして**詳細**します。  
  
3.  SYSVOL の authoritative restore を実行する] チェック ボックスをオンに**を復元するには、データ セットが複製される、復元されたデータのすべてのレプリカのプライマリ データとしてマーク**します。  
  
    > [!NOTE]
    >  バックアップ内のプライマリ データは設定に相当に復元されたデータのマークを付ける、**BurFlags** D4 に次のレジストリ サブキーの下のエントリ。  
    >   
    >  **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NtFrs\Parameters\Cumulative レプリカ Sets\\***GUID*  
  
4.  復元操作が完了したら、コンピューターを再起動します。  
  
 
## <a name="install-and-configure-the-dns-server-service"></a>インストールして、DNS サーバー サービスを構成します。  
 バックアップから復元された DC が Windows Server 2003 を実行している場合は、DC を任意のネットワークに接続しなくても DNS サーバーをインストールできます。  
  
### <a name="to-install-and-configure-the-dns-server-service"></a>インストールして、DNS サーバー サービスを構成するには  
  
1.  Windows コンポーネント ウィザードを開きます。 ウィザードを開きます。  
  
    -   をクリックして**開始**、] をクリックして**コントロール パネルの [**、] をクリックし、**プログラム追加と削除**します。  
  
    -   をクリックして**Windows コンポーネントの追加/削除**します。  
  
2.  **コンポーネント**を選択、**ネットワーク サービス**チェック ボックスをオンし、**詳細**します。  
  
3.  **ネットワーク サービスのサブコンポーネント**を選択、**ドメイン ネーム システム (DNS)**チェック ボックスをオン] をクリックして**OK**、] をクリックし、**[次へ]**します。  
  
4.  求められた場合で**からファイルをコピー**、配布ファイルの完全なパスを入力し、[クリックして**OK**します。  
  
     インストールの後、DNS サーバーを構成するのには、次の手順を完了します。  
  
5.  をクリックして**開始**、] をポイント**すべてのプログラム**、] をポイント**管理ツール**、] をクリックし、**DNS**します。  
  
6.  重要な誤動作する前に、DNS サーバーでホストされている同じ DNS ドメイン名の DNS ゾーンを作成します。 詳細については、追加の前方参照ゾーンを参照してください ([https://go.microsoft.com/fwlink/?LinkId=74574](https://go.microsoft.com/fwlink/?LinkId=74574))。  
  
7.  重要な誤動作する前に存在していた DNS データを構成します。 例えば：  
  
    -   AD DS に格納する DNS ゾーンを構成します。 詳細については、変更、ゾーンの種類を参照してください ([https://go.microsoft.com/fwlink/?LinkId=74579](https://go.microsoft.com/fwlink/?LinkId=74579))。  
  
    -   保護された動的更新を許可するようにドメイン コントローラー ロケーター (DC ロケーター) リソース レコードに対する権限を持つ DNS ゾーンを構成します。 詳細については、許可をセキュリティで保護動的更新のみを参照してください ([https://go.microsoft.com/fwlink/?LinkId=74580](https://go.microsoft.com/fwlink/?LinkId=74580))。  
  
8.  親 DNS ゾーンにこの DNS サーバーでホストされている子ゾーンの委任リソース レコード (ネーム サーバー (NS) とグルー ホスト (A) リソース レコード) が含まれていることを確認します。 詳細については、ゾーンの委任を作成するを参照してください ([https://go.microsoft.com/fwlink/?LinkId=74562](https://go.microsoft.com/fwlink/?LinkId=74562))。  
  
9. DNS を構成した後は、コマンド プロンプトで、次のコマンドを入力し、Enter キーを押します。  
  
     **Net stop netlogon**  
  
10. 次のコマンドを入力し、Enter キーを押します。  
  
     **Net start netlogon**  
  
    > [!NOTE]
    >  この DC の DNS に、net Logon は DC ロケーターのリソース レコードを登録します。 子ドメイン内のサーバーで、DNS サーバー サービスをインストールする場合は、この DC は、そのレコードをすぐに登録することはできません。 これは、回復プロセスとのプライマリ DNS サーバーの一部は、フォレスト ルート DNS サーバーは現在切り離されているためです。 DC サービス ルックアップの失敗を回避する障害前と同じ IP アドレスでは、このコンピューターを構成します。

## <a name="next-steps"></a>次の手順
-   [AD フォレストの回復の前提条件](AD-Forest-Recovery-Prerequisties.md)  
-   [AD フォレストの回復 - カスタム フォレスト回復計画を立てる](AD-Forest-Recovery-Devising-a-Plan.md)  
- [AD フォレストの回復 - 問題の特定](AD-Forest-Recovery-Identify-the-Problem.md)
-   [AD フォレストの回復 - を回復する方法を決定します。](AD-Forest-Recovery-Determine-how-to-Recover.md)
-   [AD フォレストの回復 - 最初の回復を実行](AD-Forest-Recovery-Perform-initial-recovery.md)  
-   [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md)  
-   [AD フォレストの回復のよく寄せられる質問](AD-Forest-Recovery-FAQ.md)  
-   [AD フォレストの回復であれば、マルチ ドメイン フォレスト内で 1 つのドメインの回復](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
-   [AD フォレストの回復 - Windows Server 2003 ドメイン コントローラーとフォレストの回復](AD-Forest-Recovery-Windows-Server-2003.md) 
