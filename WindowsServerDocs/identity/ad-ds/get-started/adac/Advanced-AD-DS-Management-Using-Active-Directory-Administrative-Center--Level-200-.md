---
ms.assetid: 4d21d27d-5523-4993-ad4f-fbaa43df7576
title: "Active Directory 管理センター (レベル 200) を使用して高度な AD DS の管理"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 19e83ce0123bd484c61d5a4522ebdd90cd40241e
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="advanced-ad-ds-management-using-active-directory-administrative-center-level-200"></a>Active Directory 管理センター (レベル 200) を使用して高度な AD DS の管理

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックでは、アーキテクチャ、一般的なタスクの例を含む、およびトラブルシューティングに関する情報の詳細に、更新された Active Directory 管理センターで、新しい Active Directory のごみ箱、細かいパスワード ポリシー、および Windows PowerShell 履歴ビューアーについて説明します。 概要については、次を参照してください。 [Introduction to Active Directory 管理センターの強化 (&) #40 です。Level 100 & #41 です。](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md).  
  
-   [Active Directory 管理センターのアーキテクチャ](../../../ad-ds/get-started/adac/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md#BKMK_Arch)  
  
-   [有効化と管理の Active Directory のごみ箱の Active Directory 管理センターを使用します。](../../../ad-ds/get-started/adac/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md#BKMK_EnableRecycleBin)  
  
-   [構成および Active Directory 管理センターを使用して、詳細なパスワード ポリシーを管理します。](../../../ad-ds/get-started/adac/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md#BKMK_FGPP)  
  
-   [Active Directory 管理センターの Windows PowerShell 履歴ビューアーを使用](../../../ad-ds/get-started/adac/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md#BKMK_HistoryViewer)  
  
-   [AD DS 管理のトラブルシューティング](../../../ad-ds/get-started/adac/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md#BKMK_Tshoot)  
  
## <a name="BKMK_Arch"></a>Active Directory 管理センターのアーキテクチャ  
  
### <a name="adprep-executables-dlls"></a>ADPrep の実行可能ファイル、Dll  
モジュールと Active Directory 管理センターの基盤となるアーキテクチャは、新しいごみ箱、FGPP、履歴ビューアーの機能と変更されていません。  
  
-   Microsoft.ActiveDirectory.Management.UI.dll  
  
-   Microsoft.ActiveDirectory.Management.UI.resources.dll  
  
-   Microsoft.ActiveDirectory.Management.dll  
  
-   Microsoft.ActiveDirectory.Management.resources.dll  
  
-   ActiveDirectoryPowerShellResources.dll  
  
基盤となる Windows PowerShell と新しいごみ箱機能の操作の層は、次に示します。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/adds_adrestore.png)  
  
## <a name="BKMK_EnableRecycleBin"></a>有効化と管理の Active Directory のごみ箱の Active Directory 管理センターを使用します。  
  
### <a name="capabilities"></a>機能  
  
-   Windows Server 2012 Active Directory 管理センターを使用すると、構成および Active Directory のごみ箱のフォレスト内の任意のドメイン パーティションを管理できます。 Windows PowerShell または Ldp.exe を使用して、Active Directory のごみ箱を有効またはドメイン パーティション内のオブジェクトを復元する必要はありません。  
  
-   Active Directory 管理センターは、フィルタ リング条件、大規模な環境で多くの意図的に削除されたオブジェクトを対象となる復元に簡単に高度なします。  
  
### <a name="limitations"></a>制限事項  
  
-   Active Directory 管理センターは、ドメイン パーティションのみを管理できる、ので (スキーマ パーティションからオブジェクトを削除できません) の構成、DNS、ドメインまたはフォレスト DNS パーティションから削除済みオブジェクトを復元することはできません。 ドメイン パーティション以外からオブジェクトを復元するには使用[Restore-adobject](https://technet.microsoft.com/library/ee617262.aspx)します。  
  
-   Active Directory 管理センターは、単一の操作でオブジェクトのサブツリーを復元できません。 たとえば、入れ子になった Ou、ユーザー、グループ、およびコンピューターの OU を削除した場合、ベース OU を復元は復元されません子オブジェクト。  
  
    > [!NOTE]  
    > Active Directory 管理センターの一括復元操作は「最善の努力」削除済みオブジェクトのソート*のみ選択範囲内*ため、保護者の方が復元の一覧については、子の前に配置されます。 単純なテスト_ケースでオブジェクトのサブツリーを 1 回の操作で復元があります。 不完全なツリーのいくつかの削除された親ノードが見つからないツリーに含まれるようになどのコーナー ケースかエラーの場合などの子オブジェクトをスキップする場合、親の復元が失敗した場合、期待どおりに動作しない可能性があります。 このため、必要があります常に復元するオブジェクトのサブツリーを単独の操作として親オブジェクトを復元した後です。  
  
Active Directory のごみ箱は、Windows Server 2008 R2 フォレストの機能レベルを必要として、Enterprise Admins グループのメンバーがあります。 有効にすると、Active Directory のごみ箱を無効にすることはできません。 Active Directory のごみ箱は、Active Directory データベース (NTDS のサイズを大きくします。。DIT) フォレスト内のすべてのドメイン コント ローラーにします。 ごみ箱によって使用されるディスク領域オブジェクトとすべての属性データを保存時間の経過と共に増加し続けます。  
  
詳細については、次を参照してください。 [Active Directory のごみ箱ステップ バイ ステップ ガイド](https://technet.microsoft.com/library/dd392261(v=WS.10).aspx)と[(Active Directory のごみ箱) のハードウェア要件を評価](https://technet.microsoft.com/library/cc753439(WS.10).aspx)します。  
  
できます*低い*、フォレストとドメインの機能レベルから Windows Server 2012 から Windows Server 2008 R2、Active Directory のごみ箱を有効にした後もします。 使用する必要があります、 **Set-adforestmode**と**Set-addomainmode** Active Directory コマンドレット。  
  
例えば：  
  
```  
Set-AdForestMode -identity corp.contoso.com -server dc1.corp.contoso.com -forestmode Windows2008R2Forest  
Set-AdDomainMode -identity research.corp.contoso.com -server dc3.research.corp.contoso.com -domainmode Windows2008R2Domain  
  
```  
  
Active Directory 管理センターを使用してこの変更を行うことはできません - の機能レベルを上げる操作のみです。  
  
### <a name="enabling-active-directory-recycle-bin-using-active-directory-administrative-center"></a>Active Directory のごみ箱 Active Directory 管理センターを使用して有効にします。  
Active Directory のごみ箱を有効にするには開きます、 **Active Directory 管理センター**ナビゲーション ウィンドウで、フォレストの名前をクリックします。 **タスク**] ウィンドウで、をクリックして**ごみ箱の有効化**します。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_EnableRecycleBin.png)  
  
Active Directory 管理センターを示しています、**ごみ箱の確認を有効にする**ダイアログします。 このダイアログ ボックスでは、ごみ箱を有効にすると元に戻せる状態ではないことを警告が表示されます。 をクリックして**OK**を Active Directory のごみ箱を有効にします。 Active Directory 管理センターでは、すべてのドメイン コント ローラーが、構成の変更をレプリケートするまでには、Active Directory のごみ箱が完全に機能しないことを通知する別のダイアログを表示します。  
  
> [!IMPORTANT]  
> Active Directory のごみ箱を有効にするオプションは使用しない場合。  
>   
> -   フォレストの機能レベルが Windows Server 2008 R2 より小さい  
> -   既に有効になっています。  
  
それと同等の Active Directory Windows PowerShell コマンドレットにも示します。  
  
```  
Enable-ADOptionalFeature  
```  
  
Windows PowerShell を使用して、Active Directory のごみ箱を有効にする方法の詳細については、次を参照してください。、 [Active Directory のごみ箱ステップ バイ ステップ ガイド](https://technet.microsoft.com/library/dd392261(v=WS.10).aspx)します。  
  
### <a name="managing-active-directory-recycle-bin-using-active-directory-administrative-center"></a>Active Directory のごみ箱 Active Directory 管理センターを使用して管理します。  
このセクションでは、という名前の既存のドメインの例を使用して**corp.contoso.com**します。このドメインは、親という名前の OU にユーザーを整理**UserAccounts**します。 **UserAccounts** OU に含まれている各さらに Ou、ユーザー、およびグループ部門別、という名前の 3 つの子 Ou が含まれています。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_EnableRecycleBinExampleOU.png)  
  
#### <a name="storage-and-filtering"></a>ストレージとフィルター  
Active Directory のごみ箱は、フォレストで削除されたすべてのオブジェクトを保持します。 に従ってこれらのオブジェクトを保存、 **Msds-deletedobjectlifetime**属性は、既定では、一致するように設定、 **tombstoneLifetime** 、フォレストの属性です。 すべてのフォレストに Windows Server 2003 SP1 を使用して作成された以降の値**tombstoneLifetime**は既定で 180 日間に設定します。 Windows 2000 からアップグレードまたは Windows Server 2003 (サービス パックなし) にインストールされている任意のフォレストでは、既定の tombstoneLifetime 属性が設定されていないし、そのため、Windows は 60 日間の内部の既定値を使用します。 これはすべては構成できます。Active Directory 管理センターを使用して、フォレストのドメイン パーティションから削除されたオブジェクトを復元することができます。 コマンドレットを使用して続ける必要があります**Restore-adobject**有効化すると、Active Directory のごみ箱など、他のパーティションから削除されたオブジェクトを**削除済みオブジェクト**コンテナーの Active Directory 管理センターですべてのドメイン パーティションの下に表示します。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_DeletedObjectsContainer.png)  
  
**削除済みオブジェクト**コンテナーでは復元可能なオブジェクトはすべて、そのドメイン パーティションにします。 削除されたオブジェクトよりも古い**Msds-deletedobjectlifetime**リサイクルされたオブジェクトと呼ばれます。 Active Directory 管理センターでは、リサイクルされたオブジェクトは表示されず、Active Directory 管理センターを使用してこれらのオブジェクトを復元することはできません。  
  
ごみ箱のアーキテクチャと処理ルールに関する詳細について、次を参照してください。 [AD のごみ箱: 理解、実装、ベスト プラクティス、およびトラブルシューティング](http://blogs.technet.com/b/askds/archive/2009/08/27/the-ad-recycle-bin-understanding-implementing-best-practices-and-troubleshooting.aspx)します。  
  
Active Directory 管理センターは、意図的 20,000 個のオブジェクトをコンテナーから返されるオブジェクトの既定の数を制限します。 をクリックして、この制限を 100,000 オブジェクトとしてを増やすことができます、**管理**メニューで、[**管理の一覧のオプション**します。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_MgmtList.png)  
  
#### <a name="restoration"></a>復元  
  
##### <a name="filtering"></a>フィルタ リング  
Active Directory 管理センターでは、強力な条件およびおく必要がありますを理解して実際の復元に使用する前に、フィルター オプションを提供します。 ドメインは、その有効期間を意図的に多くのオブジェクトを削除します。削除された可能性がありますオブジェクト有効期間は 180 日間の事故が発生したときにすべてのオブジェクトを単に復元できません。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_AddCriteria.png)  
  
複雑な LDAP フィルターを作成し、日付と時刻の UTC 値に変換するのではなく、基本および詳細を使用して**フィルター**メニューを関連するオブジェクトのみを一覧表示します。 削除の日がわかっている場合、オブジェクトの名前、またはその他のキーのデータを使ってアプリを得策フィルタ リングします。 検索ボックスの右側にあるシェブロンをクリックして、詳細フィルター オプションを切り替えます。  
  
復元操作には、すべての標準のフィルター条件オプション、他の検索と同じがサポートしています。 組み込みのフィルターのオブジェクトを復元するための重要なものは、通常です。  
  
-   *ANR (あいまいな名前解決に記載されていない、メニューがで入力したときに使用されるもの、* * * フィルター * * * ボックス)*  
  
-   最後の変更が指定の期間内  
  
-   オブジェクトは、ユーザー/inetorgperson/コンピューター/グループ/組織単位  
  
-   名  
  
-   削除します。  
  
-   最後に確認された親  
  
-   種類  
  
-   説明  
  
-   都市  
  
-   国/地域  
  
-   部門  
  
-   社員 ID  
  
-   最初の名前  
  
-   ジョブのタイトル  
  
-   姓、名  
  
-   Sam アカウント名  
  
-   都道府県  
  
-   電話番号  
  
-   UPN  
  
-   郵便番号  
  
複数の条件を追加することができます。 たとえば、年 9 月 24日で削除されたすべてのユーザー オブジェクトを検索できます<sup>th</sup>マネージャーの役職、東京から 2012 します。  
  
追加することも、変更、または回復するには、どのオブジェクトを評価するときに、詳細を提供する列ヘッダーの順序を変更します。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_ColumnHeaders.png)  
  
あいまいな名前解決の詳細については、次を参照してください。 [ANR 属性](https://msdn.microsoft.com/library/ms675092(VS.85).aspx)します。  
  
##### <a name="single-object"></a>1 つのオブジェクト  
削除されたオブジェクトを復元すると、1 回の操作を常にされています。  Active Directory 管理センターでは、その操作を簡単にできます。 1 人のユーザーなど、削除されたオブジェクトを復元するには。  
  
1.  Active Directory 管理センターのナビゲーション ウィンドウで、ドメイン名をクリックします。  
  
2.  ダブルクリック**削除済みオブジェクト**管理の一覧でします。  
  
3.  オブジェクトを右クリックし、をクリックして**復元**、] をクリックしてまたは**復元**から、**タスク**ウィンドウ。  
  
オブジェクトは、元の場所に復元します。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_RestoreSingle.gif)  
  
をクリックして**を復元しています.**復元場所を変更します。 これは、削除されたオブジェクトの親コンテナーも削除されており、親を復元したくない場合に便利です。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_RestoreToSingle.gif)  
  
##### <a name="multiple-peer-objects"></a>複数のピア オブジェクト  
OU 内のすべてのユーザーなど、複数のピア レベル オブジェクトを復元することができます。 CTRL キーを押しながらを復元する 1 つまたは複数の削除済みオブジェクト] をクリックします。 をクリックして**復元**[タスク] ウィンドウ。 Ctrl キーを押し、A キーを押したまま表示されているすべてのオブジェクトを選択することもやさまざまなオブジェクト] をクリックして、shift キーを使用します。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_RestorePeers.png)  
  
##### <a name="multiple-parent-and-child-objects"></a>複数の親と子オブジェクト  
Active Directory 管理センターは、単一の操作で削除されたオブジェクトの入れ子になったツリーを復元できないために、複数の親/子復元の復元プロセスを理解する必要があります。  
  
1.  ツリーの最上位の削除済みオブジェクトを復元します。  
  
2.  その親オブジェクトの直下の子を復元します。  
  
3.  これらの親オブジェクトの直下の子を復元します。  
  
4.  すべてのオブジェクトを復元するまでは、必要に応じて繰り返します。  
  
その親を復元する前に、子オブジェクトを復元することはできません。 この復元しようとすると、次のエラーが返されます。  
  
**オブジェクトの親がインスタンス、または削除されたために、操作を実行できませんでした。**  
  
**最後に確認された親**属性は、各オブジェクトの親との関係を示しています。 **最後に確認された親**親オブジェクトを復元した後は、Active Directory 管理センターを更新すると、削除された場所から属性が復元された場所に変更します。 したがって、親オブジェクトの位置情報が表示されなくなった削除済みオブジェクト コンテナーの識別名とその子オブジェクトを復元できます。  
  
ここで、管理者を削除してしまった子 Ou およびユーザーが含まれて Sales OU シナリオを検討してください。  
  
値を最初に、確認、**最後に確認された親**削除されたすべてのユーザーの属性を読み取る方法* *OU = \0adel:*< guid + 削除済みオブジェクト コンテナーの識別名 >** *。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_LastKnownParent.gif)  
  
フィルターを復元するの削除済みの OU を返す、あいまいな名前「Sales:  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_LastKnownParentSales.png)  
  
復元された Sales OU の識別名を変更、削除されたユーザー オブジェクトの最後に確認された親属性を表示するには、Active Directory 管理センターを更新します。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_LastKnownParentSalesRestored.gif)  
  
すべての Sales ユーザーでフィルター処理します。 削除されたすべての Sales ユーザーを選択するのには、CTRL キーを押しながら A キー。 をクリックして**復元**からオブジェクトを移動する、**削除済みオブジェクト**Sales OU のグループ メンバーシップと属性は保持するコンテナー。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_LastKnownParentSalesUndelete.png)  
  
場合、 **Sales** OU に、独自の子 Ou が含まれているし、まずその子を復元する前に子 Ou を復元具合です。  
  
削除された親コンテナーを指定して、入れ子になったすべての削除済みオブジェクトを復元するを参照してください。[付録 b: 復元複数、削除済みの Active Directory オブジェクト (サンプル スクリプト)](https://technet.microsoft.com/library/dd379504(WS.10).aspx)します。  
  
削除されたオブジェクトを復元するため、Active Directory Windows PowerShell コマンドレットは次のとおりです。  
  
```  
Restore-adobject  
  
```  
  
**Restore-adobject**コマンドレットの機能は Windows Server 2008 R2 と Windows Server 2012 の間で違いはありません。  
  
##### <a name="server-side-filtering"></a>サーバー側のフィルター処理  
時間の経過と共に削除済みオブジェクト コンテナーは中規模および大規模の企業に 20,000 (または 100,000) オブジェクトが蓄積して難易度のすべてのオブジェクトを表示できます。 Active Directory 管理センターのフィルター メカニズムは、クライアント側のフィルター処理に依存している、ために、これらの他のオブジェクトを表示できません。 このような制限を回避するのにには、サーバー側の検索を実行するのに、次の手順を使用します。  
  
1.  右クリックし、**削除済みオブジェクト**コンテナーとクリック**このノード配下の検索**します。  
  
2.  シェブロンをクリックして、 **+ 条件の追加**] メニューを選択し、追加**最後の変更が指定の期間内**します。 最終更新時刻 (、 **whenChanged**属性) は、削除時間; の近いほとんどの環境では同一です。 このクエリでは、サーバー側の検索を実行します。  
  
3.  さらに表示フィルター、並べ替え、結果で使用して復元する削除済みオブジェクトを見つけてし、それらを通常どおりに復元します。  
  
## <a name="BKMK_FGPP"></a>構成および Active Directory 管理センターを使用して、詳細なパスワード ポリシーを管理します。  
  
### <a name="configuring-fine-grained-password-policies"></a>詳細なパスワード ポリシーを構成します。  
Active Directory 管理センターでは、細かいパスワード ポリシー (FGPP) オブジェクトを作成および管理できます。 Windows Server 2008 に導入された FGPP 機能が Windows Server 2012、最初のグラフィカル管理インターフェイスのことです。 ドメイン レベルで細かいパスワード ポリシーを適用して、Windows Server 2003 で必要なパスワードを 1 つのドメインをオーバーライドすることができます。 さまざまな FGPP を異なる設定を作成する個々 のユーザーまたはグループはドメインにに対して異なるパスワード ポリシーを取得します。  
  
細かいパスワード ポリシーについては、次を参照してください。 [AD DS の細かいパスワードとアカウント ロックアウト ポリシーのステップ バイ ステップ ガイド (Windows Server 2008 R2)](https://technet.microsoft.com/library/cc770842(WS.10).aspx)します。  
  
ナビゲーション ウィンドウで、ツリーの表示] をクリックして、[ドメイン] をクリックして、] をクリックして**システム**、] をクリックして**Password Settings Container**、タスク ウィンドウで、クリックして**新規**と**パスワード設定**します。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_PasswordSettings.png)  
  
### <a name="managing-fine-grained-password-policies"></a>詳細なパスワード ポリシーの管理  
新しい FGPP を作成または既存の権利を編集する表示、**パスワード設定**エディターします。 ここは内にある、Windows Server 2008 または Windows Server 2008 R2 でのみようになりました専用のエディターを使用してすべての必要なパスワード ポリシーを構成します。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_CreatePasswordSettings.png)  
  
(赤いアスタリスク付き) のすべての必須フィールドと任意のオプションのフィールドに入力し、をクリックして**追加**をユーザーまたはグループがこのポリシーを受信を設定します。 FGPP は、指定されたセキュリティ プリンシパルの既定のドメイン ポリシー設定を上書きします。 上記の図では、セキュリティ侵害を防ぐために、ビルトイン Administrator アカウントにのみ、非常に厳しいポリシーが適用されます。 ポリシーは複雑すぎるに準拠する標準のユーザーが、IT プロフェッショナルのみで使用される危険度の高いアカウントに最適。  
  
優先順位を設定して、指定されたドメイン内のユーザーとグループにポリシーが適用されます。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_Precedence.png)  
  
細かいパスワード ポリシー用の Active Directory Windows PowerShell コマンドレットは次のとおりです。  
  
```  
Add-ADFineGrainedPasswordPolicySubject  
Get-ADFineGrainedPasswordPolicy  
Get-ADFineGrainedPasswordPolicySubject  
New-ADFineGrainedPasswordPolicy  
Remove-ADFineGrainedPasswordPolicy  
Remove-ADFineGrainedPasswordPolicySubject  
Set-ADFineGrainedPasswordPolicy  
  
```  
  
詳細なパスワード ポリシーのコマンドレットの機能は、Windows Server 2008 R2 と Windows Server 2012 の間で違いはありません。 必要に応じては、次の図は、関連するコマンドレットの引数を示します。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_FGPP.gif)  
  
Active Directory 管理センターでは、特定のユーザーに適用された FGPP の結果セットを検索することもできます。 すべてのユーザーを右クリックし、をクリックして**結果のパスワード設定を表示しています.**を開くには、*パスワード設定*暗黙的または明示的な割り当てを通じてそのユーザーに適用されるページ。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_RSOP.png)  
  
調べること、**プロパティ**の任意のユーザーまたはグループの表示、**直接関連付けられているパスワードの設定**、これは、明示的に割り当てられた fgpp です。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_FGPPSettings.gif)  
  
暗黙的な FGPP 割り当ては表示されません。その場合は、使用する必要があります、**結果のパスワード設定を表示しています.**オプションです。  
  
## <a name="BKMK_HistoryViewer"></a>Active Directory 管理センターの Windows PowerShell 履歴ビューアーを使用  
将来の Windows 管理では、Windows PowerShell です。 タスク自動化フレームワークの上にグラフィカル ツールを階層化では、複雑な分散システムの管理は、一貫性と効率性となります。 最大限に発揮し、コンピューティングへの投資を最大化するために Windows PowerShell のしくみを理解する必要があります。  
  
Active Directory 管理センターでは、すべての Windows PowerShell コマンドレットを実行し、その引数と値の完全な履歴が用意されています。 コマンドレットの履歴を別の場所の学習または変更および再利用をコピーすることができます。 Windows PowerShell コマンドの結果にどのような Active Directory 管理センターの特定に役立つタスク メモを作成することができます。 関心のあるポイントを検索する履歴フィルター処理することもできます。  
  
Active Directory 管理センター Windows PowerShell 履歴ビューアーの目的は、実際の操作を通じて学習するためです。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_HistoryViewer.gif)  
  
Windows PowerShell 履歴ビューアーを表示する (矢印) を表す山形記号をクリックします。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_RaiseViewer.png)  
  
次に、ユーザーを作成またはグループのメンバーシップを変更します。 履歴ビューアーは、指定された引数を使用して Active Directory 管理センターを実行した各コマンドレットの折りたたまれたビューが継続的に更新されます。  
  
コマンドレットの引数に提供されているすべての値を表示する関心のある行の項目を展開します。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_ViewArgs.png)  
  
をクリックして、**タスクの開始**] メニューの [Active Directory 管理センターを使用して、作成、変更、またはオブジェクトを削除する前に、手動で注釈を作成します。 行っていた作業に入力します。  変更を完了したら、選択**タスクの終了**します。 タスク注: グループより深く理解するのに使用することができます、折りたたみ可能なメモにすべての操作を実行します。  
  
たとえば、ユーザーのパスワードを変更し、彼のグループから削除するために使用する Windows PowerShell コマンドを参照してください。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_RemoveUser.gif)  
  
すべてを表示する] チェック ボックスを選択すると表示も get-* 動詞のみデータを取得する Windows PowerShell コマンドレット。  
  
![高度な AD DS の管理](media/Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-/ADDS_ADAC_TR_ShowAll.png)  
  
履歴ビューアーは、コマンドは、Active Directory 管理センターで実行され、不必要を実行する一部のコマンドレットが表示されていることに注意して可能性があります、リテラルを示しています。 たとえばで新しいユーザーを作成できます。  
  
```  
new-aduser   
```  
  
使用する必要はありません。  
  
```  
set-adaccountpassword  
enable-adaccount  
set-aduser  
  
```  
  
Active Directory 管理センターの設計は、最小限のコードを使用してモジュール方式に必要です。 したがって、一連の新しいユーザーを作成する機能と既存のユーザーを変更する別のセットでは、代わりに、各関数を最小限に抑えるには、し、それらをつなぎ合わせてコマンドレット。 Active Directory Windows PowerShell を学習するときに、この点に留意してください。 として使用できる学習方法、Windows PowerShell を使用して、1 つのタスクを完了する方法だけで表示します。  
  
## <a name="BKMK_Tshoot"></a>AD DS 管理のトラブルシューティング  
  
### <a name="introduction-to-troubleshooting"></a>トラブルシューティングの概要  
その相対的な事例が不足して既存のカスタマー環境での使用、のため、Active Directory 管理センターにトラブルシューティングのオプションが制限されます。  
  
### <a name="troubleshooting-options"></a>トラブルシューティングのオプション  
  
#### <a name="logging-options"></a>ログ オプション  
Active Directory 管理センターでは、トレース設定ファイルの一部としての Windows Server 2012 の組み込みのログを含まれています。 Dsac.exe と同じフォルダーに次のファイルを作成または変更します。  
  
**dsac.exe.config**  
  
次の内容を作成します。  
  
```  
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
  
詳細レベル**DsacLogLevel**は**None**、**エラー**、**警告**、**情報**、および**Verbose**します。 出力ファイル名は、構成可能な dsac.exe と同じフォルダーに書き込みます。 出力には、詳細 adac の状態、どのドメイン コント ローラーに接続されると、どのような Windows PowerShell コマンドを実行、その応答内容、およびさらに詳細がわかります。  
  
たとえば、INFO レベルを使用しているときに、トレース レベルの詳細を除くすべての結果を返します。  
  
-   DSAC.exe を起動します。  
  
-   ログの開始  
  
-   最初のドメイン情報を返すように要求されるドメイン コント ローラー  
  
    ```  
    [12:42:49][TID 3][Info] Command Id, Action, Command, Time, Elapsed Time ms (output), Number objects (output)  
    [12:42:49][TID 3][Info] 1, Invoke, Get-ADDomainController, 2012-04-16T12:42:49  
    [12:42:49][TID 3][Info] Get-ADDomainController-Discover:$null-DomainName:"CORP"-ForceDiscover:$null-Service:ADWS-Writable:$null  
    ```  
  
-   Corp ドメインからドメイン コント ローラー DC1 が返される  
  
-   PS AD 仮想ドライブが読み込まれる  
  
    ```  
    [12:42:49][TID 3][Info] 1, Output, Get-ADDomainController, 2012-04-16T12:42:49, 1  
    [12:42:49][TID 3][Info] Found the domain controller 'DC1' in the domain 'CORP'.  
    [12:42:49][TID 3][Info] 2, Invoke, New-PSDrive, 2012-04-16T12:42:49  
    [12:42:49][TID 3][Info] New-PSDrive-Name:"ADDrive0"-PSProvider:"ActiveDirectory"-Root:""-Server:"dc1.corp.contoso.com"  
    [12:42:49][TID 3][Info] 2, Output, New-PSDrive, 2012-04-16T12:42:49, 1  
    [12:42:49][TID 3][Info] 3, Invoke, Get-ADRootDSE, 2012-04-16T12:42:49  
  
    ```  
  
-   ドメイン ルート DSE 情報を取得します。  
  
    ```  
    [12:42:49][TID 3][Info] Get-ADRootDSE  
    -Server:"dc1.corp.contoso.com"  
    [12:42:49][TID 3][Info] 3, Output, Get-ADRootDSE, 2012-04-16T12:42:49, 1  
    [12:42:49][TID 3][Info] 4, Invoke, Get-ADOptionalFeature, 2012-04-16T12:42:49  
  
    ```  
  
-   ドメインの AD のごみ箱の情報を取得します。  
  
    ```  
    [12:42:49][TID 3][Info] Get-ADOptionalFeature  
    -LDAPFilter:"(msDS-OptionalFeatureFlags=1)"  
    -Server:"dc1.corp.contoso.com"  
    [12:42:49][TID 3][Info] 4, Output, Get-ADOptionalFeature, 2012-04-16T12:42:49, 1  
    [12:42:49][TID 3][Info] 5, Invoke, Get-ADRootDSE, 2012-04-16T12:42:49  
    [12:42:49][TID 3][Info] Get-ADRootDSE  
    -Server:"dc1.corp.contoso.com"  
    [12:42:49][TID 3][Info] 5, Output, Get-ADRootDSE, 2012-04-16T12:42:49, 1  
    [12:42:49][TID 3][Info] 6, Invoke, Get-ADRootDSE, 2012-04-16T12:42:49  
    [12:42:49][TID 3][Info] Get-ADRootDSE  
    -Server:"dc1.corp.contoso.com"  
    [12:42:49][TID 3][Info] 6, Output, Get-ADRootDSE, 2012-04-16T12:42:49, 1  
    [12:42:49][TID 3][Info] 7, Invoke, Get-ADOptionalFeature, 2012-04-16T12:42:49  
    [12:42:49][TID 3][Info] Get-ADOptionalFeature  
    -LDAPFilter:"(msDS-OptionalFeatureFlags=1)"  
    -Server:"dc1.corp.contoso.com"  
    [12:42:50][TID 3][Info] 7, Output, Get-ADOptionalFeature, 2012-04-16T12:42:50, 1  
    [12:42:50][TID 3][Info] 8, Invoke, Get-ADForest, 2012-04-16T12:42:50  
  
    ```  
  
-   AD フォレストを取得します。  
  
    ```  
    [12:42:50][TID 3][Info] Get-ADForest  
    -Identity:"corp.contoso.com"  
    -Server:"dc1.corp.contoso.com"  
    [12:42:50][TID 3][Info] 8, Output, Get-ADForest, 2012-04-16T12:42:50, 1  
    [12:42:50][TID 3][Info] 9, Invoke, Get-ADObject, 2012-04-16T12:42:50  
  
    ```  
  
-   サポートされている暗号化の種類、FGPP、特定のユーザー情報に対するスキーマ情報を取得します。  
  
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
  
-   ドメイン ヘッドをクリックした管理者に表示するためのドメイン オブジェクトに関するすべての情報を取得します。  
  
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
  
各関数の .NET スタック、Verbose レベルの設定も示されますが、これらは、した場合のトラブルシューティングの問題、アクセス違反やクラッシュの発生して Dsac.exe 特に役に立つための十分なデータは含まれません。  
  
> [!IMPORTANT]  
> という名前のサービスの帯域外のバージョンがセットアップされても、 [Active Directory 管理ゲートウェイ](https://www.microsoft.com/download/en/details.aspx?displaylang=en&id=2852)、Windows Server 2008 SP2 および Windows Server 2003 SP2 上で実行します。  
  
この問題の 2 つの原因は次のとおりです。  
  
-   ADWS サービスがアクセス可能なドメイン コント ローラーで実行されていません。  
  
-   Active Directory 管理センターを実行しているコンピューターから ADWS サービスへのネットワーク通信がブロックされています。  
  
Active Directory Web Services インスタンスが使用できないときに表示されるエラーは次のとおりです。  
  
|||  
|-|-|  
|エラー|操作|  
|"任意のドメインに接続できません。 リフレッシュまたは接続が利用可能な場合にもう一度やり直してください"|Active Directory 管理センター アプリケーションの開始時に表示|  
|"で、利用可能なサーバーを見つけられない、 * <NetBIOS domain name> * Active Directory Web サービス (ADWS) を実行しているドメイン"|Active Directory 管理センター アプリケーションでドメイン ノードを選択しているときに表示されます。|  
  
この問題をトラブルシューティングするには、次の手順を使用します。  
  
1.  ドメイン内の少なくとも 1 つのドメイン コント ローラー (可能であればすべてのドメイン内のコント ローラー、フォレストと) サービスが開始されて、Active Directory Web サービスを検証します。 すべてのドメイン コント ローラーをも自動的に開始する設定されていることを確認します。  
  
2.  Active Directory 管理センターを実行するコンピューターから次の NLTest.exe コマンドを実行して、ADWS を実行するサーバーを特定できることを検証します。  
  
    ```  
    nltest /dsgetdc:<domain NetBIOS name> /ws /force   
    nltest /dsgetdc:<domain fully qualified DNS name> /ws /force  
  
    ```  
  
    ADWS サービスが実行されている場合でもこれらのテストに失敗する場合は、名前解決または LDAP といない ADWS または Active Directory 管理センターに問題があります。 このテストがエラーで失敗"1355 0x54berror_no_such_domain して"ADWS 実行されていない場合、ドメイン コント ローラー上でも、何らかの結論に至る前に再確認ようにします。  
  
3.  NLTest で返されたドメイン コント ローラー、コマンドを使用してリスニング ポートの一覧をダンプします。  
  
    ```  
    Netstat -anob > ports.txt  
  
    ```  
  
    Ports.txt ファイルを確認し、ADWS サービスがポート 9389 でリッスンしていることを検証します。 例:  
  
    ```  
    TCP    0.0.0.0:9389    0.0.0.0:0    LISTENING    1828  
    [Microsoft.ActiveDirectory.WebServices.exe]  
  
    TCP    [::]:9389       [::]:0       LISTENING    1828  
    [Microsoft.ActiveDirectory.WebServices.exe]  
  
    ```  
  
    Windows ファイアウォールの規則を検証し、9389 TCP できることを確認、リッスンしている場合は、受信します。 既定では、ドメイン コント ローラーは、「Active Directory Web サービス (TCP で)」のファイアウォール規則を有効にします。 リッスンしていない場合、このサーバー上で、サービスが実行されていることを再確認し、それを再起動します。 その他のプロセスが既にリッスンしているないポート 9389 で検証します。  
  
4.  NLTEST で返されたドメイン コント ローラーと Active Directory 管理センターを実行しているコンピューターでは、NetMon または他のネットワーク キャプチャ ユーティリティをインストールします。 ネットワーク キャプチャを同時に Active Directory 管理センターを起動し、キャプチャーを停止する前に、エラーを参照してください、両方のコンピューターから収集します。 クライアントがポート TCP 9389 でドメイン コント ローラーから送受信できることを検証します。 パケットが送信されますが、到着していない場合、または到着し、ドメイン コント ローラーの応答がクライアントに到達しない場合は、そのポート パケットを破棄して、ネットワーク上のコンピューター間にファイアウォールがある可能性がありますをお勧めします。 このファイアウォールは、ソフトウェア、またはハードウェア可能性があり、サード パーティ製エンドポイント保護 (ウイルス対策) ソフトウェアの一部となる可能性があります。  
  
#### <a name="knownlikely-issues-and-support-scenarios"></a>正常および可能性の高い問題とサポートのシナリオ  
Active Directory 管理センターで可能性のある唯一の問題は、接続に、Active Directory Web サービス (ADWS) Windows Server 2012 または Windows Server 2008 R2 のドメイン コント ローラーで実行されているが無効です。  
  
## <a name="see-also"></a>参照してください。  
[Active Directory 管理センターの強化 (&) #40; の概要Level 100 & #41 です。](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md)  
  

