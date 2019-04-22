---
ms.assetid: 4d21d27d-5523-4993-ad4f-fbaa43df7576
title: Advanced AD DS Management Using Active Directory Administrative Center (Level 200)
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/07/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: fc2aaa9f7c7c42b6e94995ff473a580ce560ed93
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820003"
---
# <a name="advanced-ad-ds-management-using-active-directory-administrative-center-level-200"></a>Advanced AD DS Management Using Active Directory Administrative Center (Level 200)

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

このトピックでは、更新された Active Directory 管理センターと、そこで使用できる新しい Active Directory のごみ箱、細かい設定が可能なパスワード ポリシー、および Windows PowerShell 履歴ビューアーについて詳しく説明します。これには、アーキテクチャ、一般的なタスクの例、トラブルシューティング情報などが含まれます。 概要については、次を参照してください。 [Active Directory 管理センターの強化の概要&#40;レベル 100&#41;](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md)します。  
  
- [Active Directory 管理センターのアーキテクチャ](../../../ad-ds/get-started/adac/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md#BKMK_Arch)  
- [有効化と管理の Active Directory のごみ箱の Active Directory 管理センターを使用して](../../../ad-ds/get-started/adac/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md#BKMK_EnableRecycleBin)  
- [構成と Active Directory 管理センターを使用して、きめ細かなパスワード ポリシーの管理](../../../ad-ds/get-started/adac/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md#BKMK_FGPP)  
- [Active Directory 管理センターの Windows PowerShell 履歴ビューアーを使用してください。](../../../ad-ds/get-started/adac/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md#BKMK_HistoryViewer)  
- [AD DS の管理のトラブルシューティング](../../../ad-ds/get-started/adac/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md#BKMK_Tshoot)  
  
## <a name="BKMK_Arch"></a>Active Directory 管理センターのアーキテクチャ  
  
### <a name="active-directory-administrative-center-executables-dlls"></a>Active Directory 管理センター実行可能ファイル、Dll  

Active Directory 管理センターのモジュールと基盤となるアーキテクチャは、新しいごみ箱、細かい設定が可能なパスワード ポリシー (FGPP)、および履歴ビューアーの機能では変更されていません。  
  
- Microsoft.ActiveDirectory.Management.UI.dll  
- Microsoft.ActiveDirectory.Management.UI.resources.dll  
- Microsoft.ActiveDirectory.Management.dll  
- Microsoft.ActiveDirectory.Management.resources.dll  
- ActiveDirectoryPowerShellResources.dll  
  
基盤となる Windows PowerShell と新しいごみ箱の機能の操作レイヤーを次に示します。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/adds_adrestore.png)  
  
## <a name="BKMK_EnableRecycleBin"></a>有効化と管理の Active Directory のごみ箱の Active Directory 管理センターを使用して  
  
### <a name="capabilities"></a>機能  
  
- Windows Server 2012 または新しい Active Directory 管理センターを使用すると、構成して、Active Directory のごみ箱のフォレスト内の任意のドメイン パーティションを管理できます。 Active Directory のごみ箱の有効化や、ドメイン パーティション内のオブジェクトの復元を行うために Windows PowerShell または Ldp.exe を使用する必要はなくなりました。
- Active Directory 管理センターは高度なフィルター条件を備えており、大規模な環境で意図的に削除された多数のオブジェクトがある場合でも、必要なオブジェクトを簡単に復元できます。
  
### <a name="limitations"></a>制限事項  
  
- Active Directory 管理センターが管理できるのはドメイン パーティションのみであるため、構成パーティション、ドメイン DNS パーティション、フォレスト DNS パーティションで削除されたオブジェクトは復元できません (スキーマ パーティションのオブジェクトは削除できません)。 ドメイン パーティション以外からオブジェクトを復元するには、 [Restore-ADObject](https://technet.microsoft.com/library/ee617262.aspx)を使用します。  

- Active Directory 管理センターでは、オブジェクトのサブツリーを 1 回の操作で復元することはできません。 たとえば、入れ子になった OU、ユーザー、グループ、およびコンピューターを含む OU を削除した場合、ベース OU を復元しても、子オブジェクトは復元されません。  
  
    > [!NOTE]  
    > Active Directory 管理センターのバッチの復元操作は「ベスト エフォート」削除済みオブジェクトの*のみ選択内*のため、親は、復元の一覧の子の前に並べ替えられます。 単純なテスト ケースでは、オブジェクトのサブツリーを 1 回の操作で復元できることもあります。 一部不足している削除済みの親ノードのツリーの一部のツリーが含まれる選択などのコーナー ケースまたはエラーの場合、親の復元が失敗した場合が想定どおりに機能しない場合、子オブジェクトをスキップするなど。 このため、常に親オブジェクトを復元した後に、そのオブジェクトのサブツリーを個別の操作で復元してください。  
  
Active Directory のごみ箱には、Windows Server 2008 R2 フォレストの機能レベルが必要として、Enterprise Admins グループのメンバーがあります。 Active Directory のごみ箱は、一度有効にすると無効にすることはできません。 Active Directory のごみ箱は、フォレスト内のすべてのドメイン コントローラー上の Active Directory データベース (NTDS.DIT) のサイズを増加させます。 ごみ箱によって使用されるディスク領域は、オブジェクトとそのすべての属性データを保存するため、時間と共に増加し続けます。  
  
### <a name="enabling-active-directory-recycle-bin-using-active-directory-administrative-center"></a>Active Directory 管理センターを使用して Active Directory のごみ箱を有効化する

Active Directory のごみ箱を有効化するには、 **Active Directory 管理センター** を開いて、ナビゲーション ウィンドウでフォレストの名前をクリックします。 **[タスク]** ウィンドウで、 **[ごみ箱の有効化]** をクリックします。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_EnableRecycleBin.png)  
  
Active Directory 管理センターに **[ごみ箱の確認を有効化]** ダイアログ ボックスが表示されます。 このダイアログ ボックスには、ごみ箱を有効化すると元に戻せないことを警告するメッセージが表示されます。 **[OK]** をクリックして、Active Directory のごみ箱を有効化します。 Active Directory 管理センターに別のダイアログ ボックスが表示され、すべてのドメイン コントローラーが構成の変更をレプリケートするまで Active Directory のごみ箱は完全には機能しないことが通知されます。  
  
> [!IMPORTANT]  
> 次の場合、Active Directory のごみ箱を有効化するオプションは使用できません。  
>
> - フォレストの機能レベルが Windows Server 2008 R2 より低い  
> - Active Directory のごみ箱が既に有効になっている  

等価の Active Directory Windows PowerShell コマンドレットは次のとおりです。  

```powershell
Enable-ADOptionalFeature  
```

Windows PowerShell を使用して Active Directory のごみ箱を有効化する手順の詳細については、「 [Active Directory のごみ箱の手順ガイド](https://docs.microsoft.com/windows-server/identity/ad-ds/get-started/adac/introduction-to-active-directory-administrative-center-enhancements--level-100-#active-directory-recycle-bin-step-by-step)」を参照してください。  
  
### <a name="managing-active-directory-recycle-bin-using-active-directory-administrative-center"></a>Active Directory 管理センターを使用して Active Directory のごみ箱を管理する

このセクションでは、**corp.contoso.com** という名前の既存のドメインを例として使用します。 このドメインでは、ユーザーを **UserAccounts**という名前の親 OU にまとめています。 **UserAccounts** OU には部門の名前が付いた 3 つの子 OU が含まれており、それぞれの子 OU にはさらに OU、ユーザー、およびグループが含まれています。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_EnableRecycleBinExampleOU.png)  
  
#### <a name="storage-and-filtering"></a>ストレージとフィルター

Active Directory のごみ箱には、フォレストで削除されたすべてのオブジェクトが保存されます。 これらのオブジェクトは **msDS-deletedObjectLifetime** 属性に基づいて保存されます。既定では、この属性はフォレストの **tombstoneLifetime** 属性と同じ値に設定されています。 Windows Server 2003 SP1 以降を使用して作成されたフォレストでは、 **tombstoneLifetime** の値は、既定では 180 日に設定されています。 Windows 2000 からアップグレードしたフォレスト、または Windows Server 2003 (Service Pack なし) がインストールされたフォレストでは、既定の tombstoneLifetime 属性は設定されていないため、Windows 内部の既定値である 60 日が使用されます。 これらの設定はすべて構成可能です。Active Directory 管理センターを使用して、フォレストのドメイン パーティションから削除された任意のオブジェクトを復元できます。 構成パーティションなど、他のパーティションで削除されたオブジェクトを復元するには、引き続き **Restore-ADObject** コマンドレットを使用する必要があります。Active Directory のごみ箱を有効化すると、Active Directory 管理センターのすべてのドメイン パーティションに、**[削除済みオブジェクト]** コンテナーが表示されます。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_DeletedObjectsContainer.png)  
  
**[削除済みオブジェクト]** コンテナーには、そのドメイン パーティションで復元可能なすべてのオブジェクトが表示されます。 **msDS-deletedObjectLifetime** で指定された期間より前に削除されたオブジェクトは、リサイクルされたオブジェクトと呼ばれます。 Active Directory 管理センターには、リサイクルされたオブジェクトは表示されないため、Active Directory 管理センターを使用してこれらのオブジェクトを復元することはできません。  
  
ごみ箱のアーキテクチャと処理ルールに関する詳細については、次を参照してください。 [AD のごみ箱。理解、実装、ベスト プラクティス、およびトラブルシューティング](http://blogs.technet.com/b/askds/archive/2009/08/27/the-ad-recycle-bin-understanding-implementing-best-practices-and-troubleshooting.aspx)します。  
  
Active Directory 管理センターでは、コンテナーから返される既定のオブジェクト数を 20,000 に制限しています。 **[管理]** メニューの **[管理の一覧のオプション]** をクリックすると、この制限を 100,000 オブジェクトに増やすことができます。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_MgmtList.png)  
  
#### <a name="restoration"></a>復元  
  
##### <a name="filtering"></a>フィルター

Active Directory 管理センターは、強力な条件およびフィルター オプションを備えています。実際の復元作業で使用する前に、これらのオプションについて理解しておく必要があります。 ドメインは、有効期間が過ぎたオブジェクトを削除します。有効期間が 180 日のオブジェクトが削除されると、問題が発生した場合にすべてのオブジェクトを簡単に復元することはできません。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_AddCriteria.png)  
  
複雑な LDAP フィルターを作成し、UTC 値を日付と時刻に変換する代わりに、基本および詳細な **[フィルター]** メニューを使用して、関連するオブジェクトのみを一覧表示します。 削除した日、オブジェクトの名前、またはキーとなるその他のデータがわかっている場合、フィルターを作成する際にそれらのデータが役立ちます。 検索ボックスの右側にあるシェブロンをクリックすると、詳細フィルター オプションに切り替わります。  
  
他の検索と同様に、復元操作では標準のフィルター条件オプションがすべてサポートされています。 組み込みのフィルターのうち、一般にオブジェクトを復元する際に重要となるフィルターを次に示します。  
  
- *ANR (name resolution - 表示されていません、メニューに入力するときに使用されているもの、* * * フィルター * * * ボックス)*  
- 最後の変更が指定の期間内  
- オブジェクトの種類が、ユーザー/inetOrgPerson/コンピューター/グループ/組織単位  
- 名前  
- 削除するとき  
- 最後に確認された親  
- 種類  
- 説明  
- City  
- 国/地域  
- 部署  
- 社員 ID  
- 名  
- 役職  
- 姓  
- SAM アカウント名  
- 都道府県  
- 電話番号  
- UPN  
- 郵便番号  

複数の条件を追加できます。 たとえば、役職がマネージャーにイリノイ州シカゴから 2012 年 9 月 24 日に削除されたすべてのユーザー オブジェクトを検索できます。
  
列ヘッダーの追加、変更、並べ替えを行って、どのオブジェクトを復旧するかを判断する際に詳しい情報を表示することもできます。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_ColumnHeaders.png)  
  
あいまいな名前解決の詳細については、「 [ANR Attributes (ANR の属性)](https://msdn.microsoft.com/library/ms675092(VS.85).aspx)」を参照してください。  
  
##### <a name="single-object"></a>単一のオブジェクト

削除済みオブジェクトの復旧は、常に 1 回の操作で行われていました。  Active Directory 管理センターでは、この操作がさらに簡単になります。 単一ユーザーなど、1 つの削除済みオブジェクトを復旧するには、次の手順を実行します。  
  
1. Active Directory 管理センターのナビゲーション ウィンドウで、ドメイン名をクリックします。  
2. 管理の一覧で、 **[削除済みオブジェクト]** をダブルクリックします。  
3. オブジェクトを右クリックして **[復元]** をクリックするか、または **[タスク]** ウィンドウの **[復元]** をクリックします。  
  
オブジェクトが元の場所に復元されます。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_RestoreSingle.gif)  
  
クリックして**を復元しています.** 復元場所を変更します。 これは、機能は、削除されたオブジェクトの親コンテナーが削除されても、親を復元したくない場合に便利です。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_RestoreToSingle.gif)  
  
##### <a name="multiple-peer-objects"></a>複数のピア オブジェクト

OU 内のすべてのユーザーなど、複数のピア レベル オブジェクトを復元できます。 Ctrl キーを押しながら、復元する必要がある 1 つ以上の削除済みオブジェクトをクリックします。 [タスク] ウィンドウの **[復元]** をクリックします。 Ctrl キーを押しながら A キーを押して、表示されているすべてのオブジェクトを選択するか、または Shift キーを使用してクリックし、特定の範囲のオブジェクトを選択できます。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_RestorePeers.png)  
  
##### <a name="multiple-parent-and-child-objects"></a>複数の親および子オブジェクト

Active Directory 管理センターでは、削除済みオブジェクトの入れ子になっているツリーを 1 回の操作では復元できないため、複数の親/子オブジェクトの復元プロセスを理解しておくことが重要です。  
  
1. ツリーの最上位にある削除済みオブジェクトを復元します。  
2. その親オブジェクトの直下にある子オブジェクトを復元します。  
3. それらの子オブジェクトが親となっている、直下の子オブジェクトを復元します。  
4. 必要に応じて、すべてのオブジェクトが復元されるまで繰り返します。  
  
親オブジェクトを復元する前に、その子オブジェクトを復元することはできません。 そのような復元を試行すると、次のエラーが返されます。  
  
**オブジェクトの親のインスタンスが作成されていないか削除されているため、操作は実行できませんでした。**  
  
**[最後に確認された親]** 属性には、各オブジェクトの親との関係が表示されます。 親オブジェクトを復元した後に Active Directory 管理センターを更新すると、**[最後に確認された親]** 属性の値が、削除された場所から復元された場所に変更されます。 そのため、親オブジェクトの場所が不要になった削除済みオブジェクト コンテナーの識別名を表示するときに、その子オブジェクトを復元できます。  
  
管理者が誤って Sales OU を削除してしまった場合を考えてみましょう。Sales OU には、子 OU およびユーザーが含まれています。  
  
値を最初に、確認、**最後に確認された親**削除済みのすべてのユーザー属性とどのように読み取る **OU = \0adel:*< guid + 削除済みオブジェクト コンテナー識別名 > * * *。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_LastKnownParent.gif)  
  
あいまいな名前「Sales」でフィルターすると、削除済みの OU が返されるので、これを復元します。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_LastKnownParentSales.png)  
  
復元された Sales OU の識別名を変更、削除されたユーザー オブジェクトの最後に確認された親属性を表示する Active Directory 管理センターを更新します。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_LastKnownParentSalesRestored.gif)  
  
すべての Sales ユーザーでフィルターします。 Ctrl キーを押しながら A キーを押して、削除済みの Sales ユーザーをすべて選択します。 **[復元]** をクリックすると、選択したオブジェクトが **[削除済みオブジェクト]** コンテナーから Sales OU に移動します。オブジェクトのグループ メンバーシップと属性は保持されます。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_LastKnownParentSalesUndelete.png)  
  
**Sales** OU に子 OU が含まれていた場合は、最初に子 OU を復元してから、その子オブジェクトを復元します。さらに階層がある場合は、親から順次、復元していきます。  
  
削除済みの親コンテナーを指定して、入れ子になったすべての削除されたオブジェクトを復元するを参照してください[付録 b:。複数を復元する削除された Active Directory オブジェクト (サンプル スクリプト)](https://technet.microsoft.com/library/dd379504(WS.10).aspx)します。  
  
次の Active Directory Windows PowerShell コマンドレットは、削除済みオブジェクトを復元します。  

```powershell
Restore-adobject  
```

**Restore-ADObject** コマンドレットの機能は、Windows Server 2008 R2 と Windows Server 2012 の間で違いはありません。  
  
##### <a name="server-side-filtering"></a>サーバー側のフィルター

中規模および大規模なエンタープライズ環境では、時間が経つと、[削除済みオブジェクト] コンテナーに 20,000 (場合によっては 100,000) を超えるオブジェクトが蓄積され、すべてのオブジェクトを表示することが困難になる可能性があります。 Active Directory 管理センターのフィルター メカニズムでは、クライアント側のフィルターを使用しているため、上限を超えたオブジェクトを表示することはできません。 この制限を回避するには、次の手順に従ってサーバー側の検索を実行します。  
  
1. **[削除済みオブジェクト]** コンテナーを右クリックし、**[このノード配下の検索]** をクリックします。  
2. シェブロンをクリックして **[+条件の追加]** メニューを表示し、 **[最後の変更が指定の期間内]** を選択して追加します。 最終更新時刻 (**whenChanged** 属性) は、削除時間に非常に近い値であり、ほとんどの環境では同一になります。 このクエリでは、サーバー側の検索が実行されます。  
3. 結果に対し、さらに表示フィルターや並べ替えなどを使用して、復元する削除済みオブジェクトを特定し、通常の手順で復元を実行します。  
  
## <a name="BKMK_FGPP"></a>構成と Active Directory 管理センターを使用して、きめ細かなパスワード ポリシーの管理  
  
### <a name="configuring-fine-grained-password-policies"></a>細かい設定が可能なパスワード ポリシーを構成する

Active Directory 管理センターを使用すると、細かい設定が可能なパスワード ポリシー (FGPP) オブジェクトを作成して管理できます。 FGPP 機能は Windows Server 2008 で導入されましたが、Windows Server 2012 で初めて FGPP のグラフィカル管理インターフェイスが使用できるようになりました。 細かい設定が可能なパスワード ポリシーをドメイン レベルで適用すると、Windows Server 2003 で必要な単一ドメイン パスワードを上書きできます。 複数の FGPP を異なる設定で作成すると、ドメイン内の個々のユーザーまたはグループに対して異なるパスワード ポリシーを適用できます。  
  
細かい設定が可能なパスワード ポリシーの詳細については、「 [ステップ バイ ステップ ガイド - 細かい設定が可能なパスワードおよびアカウント ロックアウトのポリシー設定 (Windows Server 2008 R2)](https://technet.microsoft.com/library/cc770842(WS.10).aspx)」を参照してください。  
  
ナビゲーション ウィンドウで、ツリー ビューからドメインをクリックし、 **[システム]**、 **[パスワード設定コンテナー]** を順にクリックします。次に、[タスク] ウィンドウで、 **[新規]** 、 **[パスワードの設定]** を順にクリックします。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_PasswordSettings.png)  
  
### <a name="managing-fine-grained-password-policies"></a>細かい設定が可能なパスワード ポリシーを管理する

新しい FGPP を作成するか、または既存の FGPP の編集を選択すると、**[パスワードの設定]** エディターが表示されます。 この画面で、必要なすべてのパスワード ポリシーを構成します。Windows Server 2008 や Windows Server 2008 R2 で行うのと同様の内容ですが、ここでは専用のエディターを使用するという点のみ異なります。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_CreatePasswordSettings.png)  
  
すべての必須フィールド (赤いアスタリスク付き) と、必要に応じて省略可能なフィールドに入力します。次に、 **[追加]** をクリックし、このポリシーを適用するユーザーまたはグループを設定します。 FGPP は、指定されたセキュリティ プリンシパルの既定のドメイン ポリシー設定を上書きします。 上の画面では、セキュリティを保護するために、制限が非常に厳しいポリシーを組み込みの Administrator アカウントのみに適用しています。 このポリシーは、通常のユーザーに適用するには複雑すぎる内容ですが、IT プロフェッショナルのみが使用する危険度の高いアカウントには最適です。  
  
また、優先順位を設定し、指定したドメイン内でポリシーを適用するユーザーおよびグループも設定します。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_Precedence.png)  
  
次の Active Directory Windows PowerShell コマンドレットは、細かい設定が可能なパスワード ポリシーの管理に使用できます。  
  
```powershell
Add-ADFineGrainedPasswordPolicySubject  
Get-ADFineGrainedPasswordPolicy  
Get-ADFineGrainedPasswordPolicySubject  
New-ADFineGrainedPasswordPolicy  
Remove-ADFineGrainedPasswordPolicy  
Remove-ADFineGrainedPasswordPolicySubject  
Set-ADFineGrainedPasswordPolicy  
```

細かい設定が可能なパスワード ポリシー用のコマンドレットの機能は、Windows Server 2008 R2 と Windows Server 2012 の間で違いはありません。 コマンドレットの使用時に役立つように、各設定に対応するコマンドレットの引数を次の図に示します。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_FGPP.gif)  
  
Active Directory 管理センターを使用して、特定のユーザーに適用された FGPP の結果セットを参照することもできます。 すべてのユーザーを右クリックし、をクリックして**結果のパスワードの設定を表示しています.** を開く、*パスワード設定*暗黙的または明示的な割り当てを通じてそのユーザーに適用されるページ。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_RSOP.png)  
  
任意のユーザーまたはグループの **[プロパティ]** を確認すると、 **[直接関連付けられたパスワードの設定]** が表示されます。これは、明示的に割り当てられた FGPP です。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_FGPPSettings.gif)  
  
暗黙的な FGPP 割り当ては表示されません。そのため、使用する必要があります、**結果のパスワードの設定を表示しています.** オプション。  
  
## <a name="BKMK_HistoryViewer"></a>Active Directory 管理センターの Windows PowerShell 履歴ビューアーを使用してください。

今後の Windows 管理で基盤となるのは、Windows PowerShell です。 タスク自動化フレームワークの上にグラフィカル ツールを重ねて配置することで、複雑な分散システムの管理作業を一貫して効率的に実行できるようになります。 管理能力を最大限に発揮し、コンピューティング環境への投資を最大限に活用するには、Windows PowerShell の動作について理解する必要があります。  
  
Active Directory 管理センターでは、実行されるすべての Windows PowerShell コマンドレットと、その引数と値についての完全な履歴を提供できるようになりました。 コマンドレットの履歴を別の場所にコピーして、学習に役立てたり、変更および再利用できます。 タスク メモを作成すると、Active Directory 管理センターで実行した操作がどのような Windows PowerShell コマンドになったかを切り分けるために役立ちます。 また、履歴をフィルターして関心のある部分を見つけ出すこともできます。  
  
Active Directory 管理センターの Windows PowerShell 履歴ビューアーの目的は、ユーザーが実際の操作を通じて学習できるようにすることです。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_HistoryViewer.gif)  
  
シェブロン (矢印) をクリックすると、Windows PowerShell 履歴ビューアーが表示されます。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_RaiseViewer.png)  
  
次に、ユーザーを作成するか、グループのメンバーシップを変更します。 履歴ビューアーは継続的に更新され、Active Directory 管理センターが実行した各コマンドレットと指定された引数が、折りたたまれたビューに表示されます。  
  
関心のある行の項目を展開すると、コマンドレットの引数に指定されたすべての値が表示されます。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_ViewArgs.png)  
  
Active Directory 管理センターを使用してオブジェクトを作成、変更、または削除する前に、**[タスクの開始]** メニューをクリックして、手動で注釈を作成します。 実行する内容を入力します。  Active Directory 管理センターによる作業が完了したら、 **[タスクの終了]** を選択します。 このタスク メモを使用すると、実行されたすべての操作が折りたたみ可能なメモにグループ化され、実行した内容を理解しやすくなります。  
  
たとえば、ユーザーのパスワードを変更し、そのユーザーをグループから削除するために使用された Windows PowerShell コマンドを、次のようなメモで確認できます。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_RemoveUser.gif)  
  
[すべて表示] チェック ボックスをオンにすると、データを取得するだけの Get-* 動詞の Windows PowerShell コマンドレットも表示されるようになります。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_ShowAll.png)  
  
履歴ビューアーには、Active Directory 管理センターで実行されたコマンドがそのまま表示されるため、一部のコマンドレットは必要がないのに実行されているように見えることがあります。 たとえば、次のコマンドレットを使用して、新しいユーザーを作成できます。  

```powershell
new-aduser
```

この際、次のようなコマンドレットを使用する必要はありません。  

```powershell
set-adaccountpassword  
enable-adaccount  
set-aduser  
```

Active Directory 管理センターの設計では、最小限のコードを使用してモジュール方式にすることが求められました。 そのため、Active Directory 管理センターでは、新しいユーザーを作成する機能セットや既存のユーザーを変更する別の機能セットを実行する代わりに、最小限の各機能を実行し、コマンドレットを使用してそれらをつなぎ合わせています。 Active Directory Windows PowerShell について学習する際は、この点に注意してください。 1 つのタスクを完了するためにどれだけ単純な Windows PowerShell を使用できるかを確認することで、学習に役立てることもできます。  
  
## <a name="BKMK_Tshoot"></a>AD DS の管理のトラブルシューティング  
  
### <a name="introduction-to-troubleshooting"></a>トラブルシューティングの概要

Active Directory 管理センターは、既存のカスタマー環境において比較的新しいツールであり、使用事例が不足しているため、トラブルシューティングのオプションは限られています。  
  
### <a name="troubleshooting-options"></a>トラブルシューティングのオプション  
  
#### <a name="logging-options"></a>ログ オプション

Active Directory 管理センターには、トレースの構成ファイルの一部として、組み込みのログ記録が含まれています。 dsac.exe と同じフォルダーに次のファイルを作成するか、ファイルが存在する場合は以下の手順に従って変更します。  
  
**dsac.exe.config**
  
次の内容を作成します。  
  
```xml
<appSettings>  
  <add key="DsacLogLevel" value="Verbose" />  
</appSettings>  
<system.diagnostics>
 <trace autoflush="false" indentsize="4">
  <listeners>
   <add name="myListener"
    type="System.Diagnostics.TextWriterTraceListener"
    initializeData="dsac.trace.log" />
   <remove name="Default" />
  </listeners>
 </trace>
</system.diagnostics>
```

**DsacLogLevel** の詳細レベルは、 **None**、 **Error**、 **Warning**、 **Info**、および **Verbose**です。 出力ファイル名は構成可能で、dsac.exe と同じフォルダーに書き込まれます。 出力には、ADAC の状態、接続しているドメイン コントローラー、実行された Windows PowerShell コマンドとその応答内容などの詳細情報が記録されます。  

たとえば、INFO レベルを使用している場合、トレース レベルの詳細を除く、次のすべての結果が返されます。  
  
- DSAC.exe の起動  
- ログの開始  
- 最初のドメイン情報を返すためのドメイン コントローラーが要求される  

   ```
   [12:42:49][TID 3][Info] Command Id, Action, Command, Time, Elapsed Time ms (output), Number objects (output)  
   [12:42:49][TID 3][Info] 1, Invoke, Get-ADDomainController, 2012-04-16T12:42:49  
   [12:42:49][TID 3][Info] Get-ADDomainController-Discover:$null-DomainName:"CORP"-ForceDiscover:$null-Service:ADWS-Writable:$null  
   ```

- Corp ドメインからドメイン コントローラー DC1 が返される  
- PS AD 仮想ドライブの読み込み  

   ```
   [12:42:49][TID 3][Info] 1, Output, Get-ADDomainController, 2012-04-16T12:42:49, 1  
   [12:42:49][TID 3][Info] Found the domain controller 'DC1' in the domain 'CORP'.  
   [12:42:49][TID 3][Info] 2, Invoke, New-PSDrive, 2012-04-16T12:42:49  
   [12:42:49][TID 3][Info] New-PSDrive-Name:"ADDrive0"-PSProvider:"ActiveDirectory"-Root:""-Server:"dc1.corp.contoso.com"  
   [12:42:49][TID 3][Info] 2, Output, New-PSDrive, 2012-04-16T12:42:49, 1  
   [12:42:49][TID 3][Info] 3, Invoke, Get-ADRootDSE, 2012-04-16T12:42:49  
   ```
  
- ドメインのルート DSE 情報の取得  

   ```
   [12:42:49][TID 3][Info] Get-ADRootDSE -Server:"dc1.corp.contoso.com"  
   [12:42:49][TID 3][Info] 3, Output, Get-ADRootDSE, 2012-04-16T12:42:49, 1  
   [12:42:49][TID 3][Info] 4, Invoke, Get-ADOptionalFeature, 2012-04-16T12:42:49  
   ```

- ドメインの AD のごみ箱の情報の取得  

   ```
   [12:42:49][TID 3][Info] Get-ADOptionalFeature -LDAPFilter:"(msDS-OptionalFeatureFlags=1)" -Server:"dc1.corp.contoso.com"
   [12:42:49][TID 3][Info] 4, Output, Get-ADOptionalFeature, 2012-04-16T12:42:49, 1
   [12:42:49][TID 3][Info] 5, Invoke, Get-ADRootDSE, 2012-04-16T12:42:49
   [12:42:49][TID 3][Info] Get-ADRootDSE -Server:"dc1.corp.contoso.com"
   [12:42:49][TID 3][Info] 5, Output, Get-ADRootDSE, 2012-04-16T12:42:49, 1
   [12:42:49][TID 3][Info] 6, Invoke, Get-ADRootDSE, 2012-04-16T12:42:49
   [12:42:49][TID 3][Info] Get-ADRootDSE -Server:"dc1.corp.contoso.com"
   [12:42:49][TID 3][Info] 6, Output, Get-ADRootDSE, 2012-04-16T12:42:49, 1
   [12:42:49][TID 3][Info] 7, Invoke, Get-ADOptionalFeature, 2012-04-16T12:42:49
   [12:42:49][TID 3][Info] Get-ADOptionalFeature -LDAPFilter:"(msDS-OptionalFeatureFlags=1)" -Server:"dc1.corp.contoso.com"
   [12:42:50][TID 3][Info] 7, Output, Get-ADOptionalFeature, 2012-04-16T12:42:50, 1
   [12:42:50][TID 3][Info] 8, Invoke, Get-ADForest, 2012-04-16T12:42:50
   ```

- AD フォレストの取得  

   ```  
   [12:42:50][TID 3][Info] Get-ADForest -Identity:"corp.contoso.com" -Server:"dc1.corp.contoso.com"
   [12:42:50][TID 3][Info] 8, Output, Get-ADForest, 2012-04-16T12:42:50, 1  
   [12:42:50][TID 3][Info] 9, Invoke, Get-ADObject, 2012-04-16T12:42:50  
   ```

- サポートされている暗号化の種類、FGPP、特定のユーザー情報に対するスキーマ情報の取得  

   ```
   [12:42:50][TID 3][Info] Get-ADObject  
   -LDAPFilter:"(|(ldapdisplayname=msDS-PhoneticDisplayName)(ldapdisplayname=msDS-PhoneticCompanyName)(ldapdisplayname=msDS-PhoneticDepartment)(ldapdisplayname=msDS-PhoneticFirstName)(ldapdisplayname=msDS-PhoneticLastName)(ldapdisplayname=msDS-SupportedEncryptionTypes)(ldapdisplayname=msDS-PasswordSettingsPrecedence))"  
   -Properties:lDAPDisplayName  
   -ResultPageSize:"100"  
   -ResultSetSize:$null  
   -SearchBase:"CN=Schema,CN=Configuration,DC=corp,DC=contoso,DC=com"  
   -SearchScope:"OneLevel"  
   -Server:"dc1.corp.contoso.com"  
   [12:42:50][TID 3][Info] 9, Output, Get-ADObject, 2012-04-16T12:42:50, 7  
   [12:42:50][TID 3][Info] 10, Invoke, Get-ADObject, 2012-04-16T12:42:50  
   ```

- ドメイン ヘッドをクリックした管理者に表示されるドメイン オブジェクトに関するすべての情報の取得  

   ```
   [12:42:50][TID 3][Info] Get-ADObject  
   -IncludeDeletedObjects:$false  
   -LDAPFilter:"(objectClass=*)"  
   -Properties:allowedChildClassesEffective,allowedChildClasses,lastKnownParent,sAMAccountType,systemFlags,userAccountControl,displayName,description,whenChanged,location,managedBy,memberOf,primaryGroupID,objectSid,msDS-User-Account-Control-Computed,sAMAccountName,lastLogonTimestamp,lastLogoff,mail,accountExpires,msDS-PhoneticCompanyName,msDS-PhoneticDepartment,msDS-PhoneticDisplayName,msDS-PhoneticFirstName,msDS-PhoneticLastName,pwdLastSet,operatingSystem,operatingSystemServicePack,operatingSystemVersion,telephoneNumber,physicalDeliveryOfficeName,department,company,manager,dNSHostName,groupType,c,l,employeeID,givenName,sn,title,st,postalCode,managedBy,userPrincipalName,isDeleted,msDS-PasswordSettingsPrecedence  
   -ResultPageSize:"100"  
   -ResultSetSize:"20201"  
   -SearchBase:"DC=corp,DC=contoso,DC=com"  
   -SearchScope:"Base"  
   -Server:"dc1.corp.contoso.com"  
   ```

Verbose レベルに設定すると、各関数の .NET スタックも表示されますが、これらの情報には、Dsac.exe でアクセス違反やクラッシュが発生した場合のトラブルシューティングに役立つデータしか含まれていません。 この問題の原因として、次の 2 つが考えられます。
  
- アクセス可能なドメイン コントローラー上で ADWS サービスが実行されていない
- Active Directory 管理センターを実行しているコンピューターから ADWS サービスへのネットワーク通信がブロックされます。

> [!IMPORTANT]  
> [Active Directory 管理ゲートウェイ](https://www.microsoft.com/download/en/details.aspx?displaylang=en&id=2852)と呼ばれるアウトオブバンド バージョンのサービスもあります。これは、Windows Server 2008 SP2 および Windows Server 2003 SP2 で動作します。
>

Active Directory Web Services インスタンスが使用できない場合は、次のエラーが表示されます。  
  
|エラー|操作|
| --- | --- |  
|"どのドメインにも接続できません。 接続できるようになったら、更新するか、再試行してください"|Active Directory 管理センター アプリケーションの開始時に表示されます|
|"で使用可能なサーバーを見つけることができません、 *<NetBIOS domain name>* Active Directory Web サービス (ADWS) を実行しているドメイン"|Active Directory 管理センター アプリケーションでドメイン ノードの選択を試行したときに表示されます|
  
この問題のトラブルシューティングを行うには、次の手順に従います。  
  
1. ドメイン内の少なくとも 1 つのドメイン コントローラー (可能であれば、フォレスト内のすべてのドメイン コントローラー) で Active Directory Web Services サービスが開始していることを確認します。 また、すべてのドメイン コントローラーで ADWS サービスが自動で開始するように設定されていることを確認します。
2. Active Directory 管理センターが実行されているコンピューターで、次の NLTest.exe コマンドを実行して、ADWS が実行されているサーバーを特定できることを確認します。  

   ```
   nltest /dsgetdc:<domain NetBIOS name> /ws /force
   nltest /dsgetdc:<domain fully qualified DNS name> /ws /force
   ```

   ADWS サービスが実行されていても、これらのテストに失敗する場合、この問題は、ADWS および Active Directory 管理センターではなく、名前解決または LDAP に関連しています。 ADWS がどのドメイン コントローラーでも実行されていない場合、このテストは "1355 0x54B ERROR_NO_SUCH_DOMAIN" エラーを出力して失敗します。何らかの結論に至る前に、この点をダブルチェックしてください。  
  
3. NLTest で返されたドメイン コントローラー上で、次のコマンドを使用してリスニング ポートの一覧をダンプします。  

   ```
   Netstat -anob > ports.txt  
   ```

   ports.txt ファイルを調査して、ADWS サービスがポート 9389 でリッスン中であることを確認します。 以下に例を示します。  

   ```
   TCP    0.0.0.0:9389    0.0.0.0:0    LISTENING    1828  
   [Microsoft.ActiveDirectory.WebServices.exe]  

   TCP    [::]:9389       [::]:0       LISTENING    1828  
   [Microsoft.ActiveDirectory.WebServices.exe]  
   ```

   リッスン中である場合、Windows ファイアウォールの規則で 9389 TCP の受信が許可されていることを確認します。 既定では、ドメイン コントローラーは "Active Directory Web サービス (TCP-受信)" という名前のファイアウォールの規則を有効化します。 リッスン中でない場合は、このサーバー上で ADWS サービスが実行されていることを再確認して、サービスを再起動します。 ポート 9389 で既にリッスン中である他のプロセスがないことを確認してください。  
  
4. Active Directory 管理センターが実行されているコンピューターと、NLTEST で返されたドメイン コントローラーに、NetMon または他のネットワーク キャプチャ ユーティリティをインストールします。 両方のコンピューターからネットワーク キャプチャを同時に収集し、その状態で Active Directory 管理センターを起動して、エラーを確認したらキャプチャを停止します。 クライアントが TCP ポート 9389 でドメイン コントローラーと送受信できることを確認します。 パケットが送信されているが到着していない場合、またはパケットが到着しているがドメイン コントローラーの応答がクライアントに到着していない場合は、ネットワーク上のコンピューター間に存在するファイアウォールがそのポートのパケットを破棄している可能性があります。 このファイアウォールは、ソフトウェア、ハードウェア、またはサードパーティ エンドポイント保護 (ウイルス対策) ソフトウェアの一部である可能性があります。  
  
## <a name="see-also"></a>関連項目

[AD のごみ箱、きめ細かなパスワード ポリシー、および PowerShell の履歴](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md)  
