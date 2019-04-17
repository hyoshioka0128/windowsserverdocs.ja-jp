---
ms.assetid: 074e63e9-976c-49da-8cba-9ae0b3325e34
title: "Active Directory 管理センターの強化 (レベル 100) の概要"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 7f52b22ec74ba12c383952e68b412f871a56474c
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="introduction-to-active-directory-administrative-center-enhancements-level-100"></a>Active Directory 管理センターの強化 (レベル 100) の概要

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Windows Server 2012 での ADAC には、次の管理機能が含まれています。

-   [Active Directory のごみ箱](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#ad_recycle_bin_mgmt)

-   [詳細なパスワード ポリシー](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#fine_grained_pswd_policy_mgmt)

-   [Windows PowerShell 履歴ビューアー](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#windows_powershell_history_viewer)

## <a name="ad_recycle_bin_mgmt"></a>Active Directory のごみ箱
Active Directory オブジェクトが誤って削除は、ユーザーの Active Directory ドメイン サービス (AD DS) と Active Directory ライトウェイト ディレクトリ サービス (AD LDS) ユーザーが頻繁に発生します。 Windows Server 2008 R2 では、前に、Windows Server の以前のバージョン 1 つでした Active directory は、誤って削除されたオブジェクトは回復ソリューションは欠点がありました。

Windows Server 2008、Windows Server バックアップ機能を使用する可能性があります、**ntdsutil**権限ある回復コマンドをマークするオブジェクトを authoritative と確実に復元されたデータは、ドメイン全体でレプリケートできました。 権限ある回復ソリューションの欠点は、ディレクトリ サービス復元モード (DSRM) で実行することがあったことでした。 DSRM、中に復元されているドメイン コントローラーがオフラインのままにする必要があります。 そのため、クライアント要求を処理できませんでした。

Windows Server 2003 の Active Directory と Windows Server 2008 AD DS では、廃棄済みから削除された Active Directory オブジェクトを回復する可能性があります。 ただし、オブジェクトのリンクされた値属性 (たとえば、ユーザー アカウントのグループ メンバーシップ) 物理的に削除されたをあるおよび消去されたリンクされた値の属性は回復されませんでした。 そのため、管理者は、誤ったオブジェクトの削除を最終的な解決策として廃棄済みに依存しませんでした。 廃棄済みオブジェクトの復元の詳細については、次を参照してください。[Active Directory 廃棄 (tombstone) オブジェクトを復元する](https://go.microsoft.com/fwlink/?LinkID=125452)します。

Active Directory のごみ箱、以降では、Windows Server 2008 R2 は、既存の廃棄済みオブジェクトの復元インフラストラクチャにビルドされ、保持し、誤って削除された Active Directory オブジェクトを回復する機能が拡張されます。

Active Directory のごみ箱、すべてのリンクされた値を有効にして削除された Active Directory オブジェクトのリンクされた値属性が保持され、オブジェクトは、同じ一貫性のある論理れている状態で削除される直前を完全に復元されます。 たとえば、復元されたユーザー アカウントは、すべてのグループ メンバーシップとドメイン内外の削除される直前に保持していた対応するアクセス権を自動的に回復します。 Active Directory のごみ箱は、AD DS および AD LDS 環境の両方で機能します。 Active Directory のごみ箱の詳細については、次を参照してください。[AD DS の新: Active Directory のごみ箱](https://technet.microsoft.com/library/dd391916(WS.10).aspx)します。

**新着情報ですか。** Windows Server 2012 では、ユーザーの管理し、削除されたオブジェクトを復元するための新しいグラフィカル ユーザー インターフェイスで、Active Directory のごみ箱機能が強化されています。 ユーザーできますようになりました視覚的に削除されたオブジェクトの一覧を見つけてを元のまたは目的の場所に復元します。

Active Directory のごみ箱 Windows Server 2012 で有効にする場合は、次の操作を考慮してください。

-   既定では、Active Directory のごみ箱は無効です。 これを有効にするには、AD DS または AD LDS 環境に Windows Server 2008 R2、またはそれ以上のフォレストの機能レベルを上げる必要があります。 これである必要があります、フォレスト内のすべてのドメイン コントローラーまたは AD LDS 構成セットのインスタンスをホストするすべてのサーバー Windows Server 2008 R2 を実行またはそれ以降。

-   Active Directory のごみ箱を有効にするプロセスは、元に戻せる状態ではありません。 環境内で Active Directory のごみ箱を有効にした後は、無効にすることはできません。

-   ユーザー インターフェイスからごみ箱機能を管理するには、Windows Server 2012 で Active Directory 管理センターのバージョンをインストールする必要があります。

    > [!NOTE]
    > 使用することができます**サーバー マネージャー**正しいバージョンの Active Directory 管理センターを使用してユーザー インターフェイスからごみ箱を管理する Windows Server 2012 コンピューターにリモート サーバー管理ツール (RSAT) をインストールします。
    > 
    > 使用することができます[RSAT](https://go.microsoft.com/fwlink/?LinkID=238560) windows&reg; 8 台のコンピューターで正しいバージョンの Active Directory 管理センターを使用してユーザー インターフェイスからごみ箱を管理します。

### <a name="active-directory-recycle-bin-step-by-step"></a>Active Directory のごみ箱ステップ バイ ステップ
次の手順では、ADAC を使用して Windows Server 2012 で、次の Active Directory のごみ箱のタスクを実行します。

-   [手順 1: フォレストの機能レベルを上げる](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_raise_ffl)

-   [手順 2: ごみ箱を有効にします。](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_enable_recycle_bin)

-   [手順 3: テスト用のユーザー、グループ、および組織単位を作成します。](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_test_env)

-   [手順 4: 削除されたオブジェクトの復元](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_restore_del_obj)

> [!NOTE]
> 次の手順を実行するには、Enterprise Admins グループまたはそれと同等のアクセス許可のメンバーシップが必要です。

### <a name="bkmk_raise_ffl"></a>手順 1: フォレストの機能レベルを上げる
この手順では、フォレストの機能レベルを生成します。 Active Directory のごみ箱を有効にする前に、少なくとも Windows Server 2008 R2 であるターゲット フォレストの機能レベルを上げる必要があります。

##### <a name="to-raise-the-functional-level-on-the-target-forest"></a>ターゲット フォレストの機能レベルを上げる

1.  Windows PowerShell アイコンを右クリックして] をクリックして**管理者として実行**と種類**dsac.exe** ADAC を開きます。

2.  をクリックして**管理**、] をクリックして**ナビゲーション ノードの追加**で適切なターゲット ドメインを選択し、**ナビゲーション ノードの追加**] ダイアログ ボックスをクリック**OK**します。

3.  左側のナビゲーション ウィンドウとでターゲット ドメインをクリックして、**タスク**] ウィンドウで、をクリックして**フォレスト機能レベルを上げる**します。 少なくとも、フォレストの機能レベルを選択して Windows Server 2008 R2 またはそれ以上の順にクリック**[OK]**します。

![AD 管理センターの概要](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell と同等のコマンド * * *

次の Windows PowerShell コマンドレットまたはコマンドレットは、前の手順と同じ機能を実行します。 表示される場合でも可能性があります複数行に改行書式上の制約のためには、各コマンドレットを 1 つの行を入力します。

```
Set-ADForestMode -Identity contoso.com -ForestMode Windows2008R2Forest -Confirm:$false
```

**-Identity**引数、完全修飾 DNS 名を指定します。

### <a name="bkmk_enable_recycle_bin"></a>手順 2: ごみ箱を有効にします。
この手順では、AD DS から削除されたオブジェクトをごみ箱を有効にします。

##### <a name="to-enable-active-directory-recycle-bin-in-adac-on-the-target-domain"></a>Active Directory のごみ箱 adac でターゲット ドメインを有効にするには

1.  Windows PowerShell アイコンを右クリックして] をクリックして**管理者として実行**と種類**dsac.exe** ADAC を開きます。

2.  をクリックして**管理**、] をクリックして**ナビゲーション ノードの追加**で適切なターゲット ドメインを選択し、**ナビゲーション ノードの追加**] ダイアログ ボックスをクリック**OK**します。

3.  **タスク**] ウィンドウで、をクリックして**ごみ箱の有効化しています.**で、**タスク**] ウィンドウで、] をクリックして**OK**をクリックし、警告メッセージ ボックスで、**[OK]**更新 ADAC メッセージにします。

4.  F5 キーを押して ADAC を更新します。

![AD 管理センターの概要](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell と同等のコマンド * * *

次の Windows PowerShell コマンドレットまたはコマンドレットは、前の手順と同じ機能を実行します。 表示される場合でも可能性があります複数行に改行書式上の制約のためには、各コマンドレットを 1 つの行を入力します。

```
Enable-ADOptionalFeature -Identity 'CN=Recycle Bin Feature,CN=Optional Features,CN=Directory Service,CN=Windows NT,CN=Services,CN=Configuration,DC=contoso,DC=com' -Scope ForestOrConfigurationSet -Target 'contoso.com'
```

### <a name="bkmk_create_test_env"></a>手順 3: テスト用のユーザー、グループ、および組織単位を作成します。
次の手順では、次の 2 つのテスト ユーザーを作成します。 テスト グループを作成し、テスト ユーザーをグループに追加されます。 さらに、OU を作成します。

##### <a name="to-create-test-users"></a>テスト ユーザーを作成するには

1.  Windows PowerShell アイコンを右クリックして] をクリックして**管理者として実行**と種類**dsac.exe** ADAC を開きます。

2.  をクリックして**管理**、] をクリックして**ナビゲーション ノードの追加**で適切なターゲット ドメインを選択し、**ナビゲーション ノードの追加**] ダイアログ ボックスをクリック**OK**します。

3.  **タスク**] ウィンドウで、をクリックして**新規**] をクリックし、**ユーザー**します。

    ![AD 管理センターの概要](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/ADDS_ADACNewUser.gif)

4.  下にある次の情報を入力**アカウント**し、[OK] をクリックします。

    -   フル_ネーム: test1

    -   [ユーザー SamAccountName ログオン: test1

    -   パスワード:p@ssword1

    -   パスワードを確認します。p@ssword1

5.  2 番目のユーザー test2 を作成する前の手順を繰り返します。

##### <a name="to-create-a-test-group-and-add-users-to-the-group"></a>テスト グループを作成し、グループにユーザーを追加するには

1.  Windows PowerShell アイコンを右クリックして] をクリックして**管理者として実行**と種類**dsac.exe** ADAC を開きます。

2.  をクリックして**管理**、] をクリックして**ナビゲーション ノードの追加**で適切なターゲット ドメインを選択し、**ナビゲーション ノードの追加**] ダイアログ ボックスをクリック**OK**します。

3.  **タスク**] ウィンドウで、をクリックして**新規**] をクリックし、**グループ**します。

4.  下にある次の情報を入力**グループ**] をクリックし、**OK**:

    -   **グループ名: group1]**

5.  をクリックして**group1**、し、**タスク**] ウィンドウで、をクリックして**プロパティ**します。

6.  をクリックして**メンバー**、] をクリックして**追加**、種類**test1; test2**、] をクリックし、**OK**します。

![AD 管理センターの概要](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell と同等のコマンド * * *

次の Windows PowerShell コマンドレットまたはコマンドレットは、前の手順と同じ機能を実行します。 表示される場合でも可能性があります複数行に改行書式上の制約のためには、各コマンドレットを 1 つの行を入力します。

```
Add-ADGroupMember -Identity group1 -Member test1
```

##### <a name="to-create-an-organizational-unit"></a>組織単位を作成するには

1.  Windows PowerShell アイコンを右クリックして] をクリックして**管理者として実行**と種類**dsac.exe** ADAC を開きます。

2.  をクリックして**管理**、] をクリックして**ナビゲーション ノードの追加**で適切なターゲット ドメインを選択し、**ナビゲーション ノードの追加**] ダイアログ ボックスをクリック**OK**します。

3.  **タスク**] ウィンドウで、をクリックして**新規**] をクリックし、**組織単位**します。

4.  下にある次の情報を入力**組織単位**] をクリックし、**OK**:

    -   **NameOU1**

![AD 管理センターの概要](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell と同等のコマンド * * *

次の Windows PowerShell コマンドレットまたはコマンドレットは、前の手順と同じ機能を実行します。 表示される場合でも可能性があります複数行に改行書式上の制約のためには、各コマンドレットを 1 つの行を入力します。

```
1..2 | ForEach-Object {New-ADUser -SamAccountName test$_ -Name "test$_" -Path "DC=fabrikam,DC=com" -AccountPassword (ConvertTo-SecureString -AsPlainText "p@ssword1" -Force) -Enabled $true}
New-ADGroup -Name "group1" -SamAccountName group1 -GroupCategory Security -GroupScope Global -DisplayName "group1"
New-ADOrganizationalUnit -Name OU1 -Path "DC=fabrikam,DC=com"

```

### <a name="bkmk_restore_del_obj"></a>手順 4: 削除されたオブジェクトの復元
次の手順から削除されたオブジェクトを復元する、**削除済みオブジェクト**コンテナーを元の場所および別の場所にします。

##### <a name="to-restore-deleted-objects-to-their-original-location"></a>削除されたオブジェクトを元の場所に復元するには

1.  Windows PowerShell アイコンを右クリックして] をクリックして**管理者として実行**と種類**dsac.exe** ADAC を開きます。

2.  をクリックして**管理**、] をクリックして**ナビゲーション ノードの追加**で適切なターゲット ドメインを選択し、**ナビゲーション ノードの追加**] ダイアログ ボックスをクリック**OK**します。

3.  ユーザー選択**test1**と**test2**、] をクリックして**削除**で、**タスク**ペインをクリック**[はい]**削除を確定します。

    ![AD 管理センターの概要](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell と同等のコマンド * * *

    次の Windows PowerShell コマンドレットまたはコマンドレットは、前の手順と同じ機能を実行します。 表示される場合でも可能性があります複数行に改行書式上の制約のためには、各コマンドレットを 1 つの行を入力します。

    ```
    Get-ADUser -Filter 'Name -Like "*test*"'|Remove-ADUser -Confirm:$false
    ```

4.  移動、**削除済みオブジェクト**コンテナーで、**test2**と**test1** ] をクリックし、**復元**で、**タスク**ウィンドウ。

5.  オブジェクトが元の場所に復元されたことを確認するには、ターゲット ドメインに移動し、ユーザー アカウントが表示されていることを確認します。

    > [!NOTE]
    > 移動した場合、**プロパティ**ユーザー アカウントの**test1**と**test2** ] をクリックし、**所属するグループ**、グループのメンバーシップも復元されているが表示されます。

次の Windows PowerShell コマンドレットまたはコマンドレットは、前の手順と同じ機能を実行します。 表示される場合でも可能性があります複数行に改行書式上の制約のためには、各コマンドレットを 1 つの行を入力します。

![AD 管理センターの概要](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell と同等のコマンド * * *

```
Get-ADObject -Filter 'Name -Like "*test*"' -IncludeDeletedObjects | Restore-ADObject
```

##### <a name="to-restore-deleted-objects-to-a-different-location"></a>削除されたオブジェクトを別の場所に復元するには

1.  Windows PowerShell アイコンを右クリックして] をクリックして**管理者として実行**と種類**dsac.exe** ADAC を開きます。

2.  をクリックして**管理**、] をクリックして**ナビゲーション ノードの追加**で適切なターゲット ドメインを選択し、**ナビゲーション ノードの追加**] ダイアログ ボックスをクリック**OK**します。

3.  ユーザー選択**test1**と**test2**、] をクリックして**削除**で、**タスク**ペインをクリック**[はい]**削除を確定します。

4.  移動、**削除済みオブジェクト**コンテナーで、**test2**と**test1** ] をクリックし、**復元先**で、**タスク**ウィンドウ。

5.  選択**OU1** ] をクリックし、**OK**します。

6.  オブジェクトを確認するに復元された**OU1**、ターゲット ドメインに移動し、] をダブルクリック**OU1**し、ユーザー アカウントが表示されていることを確認します。

![AD 管理センターの概要](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell と同等のコマンド * * *

次の Windows PowerShell コマンドレットまたはコマンドレットは、前の手順と同じ機能を実行します。 表示される場合でも可能性があります複数行に改行書式上の制約のためには、各コマンドレットを 1 つの行を入力します。

```
Get-ADObject -Filter 'Name -Like "*test*"' -IncludeDeletedObjects | Restore-ADObject -TargetPath "OU=OU1,DC=contoso,DC=com"
```

## <a name="fine_grained_pswd_policy_mgmt"></a>詳細なパスワード ポリシー
Windows Server 2008 オペレーティング システムのドメインに別のパスワードとアカウント ロックアウトのポリシーのユーザーのセットを定義する方法を提供します。 Windows Server 2008 より前の Active Directory ドメインで 1 つだけのパスワード ポリシーおよびアカウント ロックアウトのポリシーをドメイン内のすべてのユーザーに適用される。 これらのポリシーは、ドメインの既定のドメイン ポリシーに指定されています。 その結果、募集の異なるユーザーのパスワードとアカウント ロックアウト設定が別の組織では、パスワード フィルターを作成するか、複数のドメインを展開する必要があります。 両方は、コストのかかるオプションです。

詳細なパスワード ポリシーを使用して、単一ドメイン内の複数のパスワード ポリシーを指定し、さまざまなドメイン内のユーザーにパスワードとアカウント ロックアウトのポリシーに別の制限を適用することができます。 たとえば、他のユーザー アカウントには、特権アカウントをより厳密な設定と少ない厳密な設定を適用できます。 それ以外の場合とその他のデータ ソースを同期するパスワードを持つアカウントの特別なパスワード ポリシーを適用する場合があります。 細かいパスワード ポリシーの詳細については、次を参照してください[AD DS: 細かいパスワード ポリシー。](https://technet.microsoft.com/library/cc770394(WS.10).aspx)

**新着情報ですか。** 、Windows Server 2012 で詳細なパスワード ポリシーの管理が簡単になり詳細に関するビジュアル ADAC で管理する AD DS 管理者のユーザー インターフェイスを提供することでします。 管理者ことができますようになりました特定のユーザーのポリシーの結果を表示、表示および指定されたドメイン内のすべてのパスワード ポリシーを並べ替えるおよび個々 のパスワード ポリシーを視覚的に管理します。

Windows Server 2012 で詳細なパスワード ポリシーを使用する場合は、次の操作を考慮してください。

-   詳細なパスワード ポリシーは、のみグローバル セキュリティ グループとユーザー オブジェクト (またはユーザー オブジェクトの代わりに使用されている inetOrgPerson オブジェクト) に適用されます。 既定では、Domain Admins グループのメンバーのみに詳細なパスワード ポリシーを設定できます。 ただし、他のユーザーにこれらのポリシーを設定する機能を委任することもできます。 ドメインの機能レベルは、Windows Server 2008 以上である必要があります。

-   Active Directory 管理センターの Windows Server 2012 バージョンを使用して、グラフィカル ユーザー インターフェイスを使って詳細なパスワード ポリシーを管理する必要があります。

    > [!NOTE]
    > 使用することができます**サーバー マネージャー**正しいバージョンの Active Directory 管理センターを使用してユーザー インターフェイスからごみ箱を管理する Windows Server 2012 コンピューターにリモート サーバー管理ツール (RSAT) をインストールします。
    > 
    > 使用することができます[RSAT](https://go.microsoft.com/fwlink/?LinkID=238560) windows&reg; 8 台のコンピューターで正しいバージョンの Active Directory 管理センターを使用してユーザー インターフェイスからごみ箱を管理します。

### <a name="fine-grained-password-policy-step-by-step"></a>ステップ バイ ステップの詳細なパスワード ポリシー
次の手順では ADAC を使用して、次の詳細なパスワード ポリシー タスクを実行します。

-   [手順 1: ドメインの機能レベルを上げる](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_raise_dfl)

-   [手順 2: テスト用のユーザー、グループ、および組織単位を作成します。](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk2_test_fgpp)

-   [手順 3: 新しい詳細なパスワード ポリシーを作成します。](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp)

-   [手順 4: ユーザーのポリシーの結果セットを表示します。](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_view_resultant_fgpp)

-   [手順 5: 詳細なパスワード ポリシーを編集します。](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_edit_fgpp)

-   [手順 6: 詳細なパスワード ポリシーを削除します。](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_delete_fgpp)

> [!NOTE]
> 次の手順を実行するには、Domain Admins グループまたはそれと同等のアクセス許可のメンバーシップが必要です。

#### <a name="bkmk_raise_dfl"></a>手順 1: ドメインの機能レベルを上げる
次の手順では、ターゲット ドメインを Windows Server 2008、またはそれ以上のドメインの機能レベルを生成します。 詳細なパスワード ポリシーを有効にするには、Windows Server 2008 以降のドメイン機能レベルが必要です。

###### <a name="to-raise-the-domain-functional-level"></a>ドメインの機能レベルを上げる

1.  Windows PowerShell アイコンを右クリックして] をクリックして**管理者として実行**と種類**dsac.exe** ADAC を開きます。

2.  をクリックして**管理**、] をクリックして**ナビゲーション ノードの追加**で適切なターゲット ドメインを選択し、**ナビゲーション ノードの追加**] ダイアログ ボックスをクリック**OK**します。

3.  左側のナビゲーション ウィンドウとでターゲット ドメインをクリックして、**タスク**] ウィンドウで、をクリックして**ドメイン機能レベルを上げる**します。 少なくとも、フォレストの機能レベルを選択してクリックして Windows Server 2008 以降**OK**します。

![AD 管理センターの概要](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell と同等のコマンド * * *

次の Windows PowerShell コマンドレットまたはコマンドレットは、前の手順と同じ機能を実行します。 表示される場合でも可能性があります複数行に改行書式上の制約のためには、各コマンドレットを 1 つの行を入力します。

```
Set-ADDomainMode -Identity contoso.com -DomainMode 3
```

#### <a name="bkmk2_test_fgpp"></a>手順 2: テスト用のユーザー、グループ、および組織単位を作成します。
テスト ユーザーを作成し、この手順の必要性をグループ化にある手順に従います。[手順 3: テスト用のユーザー、グループ、および組織単位を作成する](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_test_env)(詳細なパスワード ポリシーを試すために OU を作成する必要はありません)。

#### <a name="bkmk_create_fgpp"></a>手順 3: 新しい詳細なパスワード ポリシーを作成します。
次の手順では、ADAC の UI を使用して新しい詳細なパスワード ポリシーを作成します。

###### <a name="to-create-a-new-fine-grained-password-policy"></a>新しい細かい設定が可能なパスワード ポリシーを作成するには

1.  Windows PowerShell アイコンを右クリックして] をクリックして**管理者として実行**と種類**dsac.exe** ADAC を開きます。

2.  をクリックして**管理**、] をクリックして**ナビゲーション ノードの追加**で適切なターゲット ドメインを選択し、**ナビゲーション ノードの追加**] ダイアログ ボックスをクリック**OK**します。

3.  ADAC のナビゲーション ウィンドウで開き、**システム**コンテナーとクリック**Password Settings Container**します。

4.  **タスク**] ウィンドウで、] をクリックして**新規**、] をクリックし、**パスワード設定**します。

    入力するか、新しく作成するプロパティ ページ内のフィールドを編集**パスワード設定**オブジェクト。 **名**と**優先順位**フィールドが必要です。

    ![AD 管理センターの概要](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/ADDS_ADACNewFGPP.gif)

5.  下にある**直接適用先**、] をクリックして**追加**、種類**group1**、] をクリックし、**OK**します。

    これは、パスワード ポリシー オブジェクトは、テスト環境用に作成したグローバル グループのメンバーを関連付けます。

6.  をクリックして**OK**作成を送信します。

![AD 管理センターの概要](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell と同等のコマンド * * *

次の Windows PowerShell コマンドレットまたはコマンドレットは、前の手順と同じ機能を実行します。 表示される場合でも可能性があります複数行に改行書式上の制約のためには、各コマンドレットを 1 つの行を入力します。

```
New-ADFineGrainedPasswordPolicy TestPswd -ComplexityEnabled:$true -LockoutDuration:"00:30:00" -LockoutObservationWindow:"00:30:00" -LockoutThreshold:"0" -MaxPasswordAge:"42.00:00:00" -MinPasswordAge:"1.00:00:00" -MinPasswordLength:"7" -PasswordHistoryCount:"24" -Precedence:"1" -ReversibleEncryptionEnabled:$false -ProtectedFromAccidentalDeletion:$true
Add-ADFineGrainedPasswordPolicySubject TestPswd -Subjects group1
```

#### <a name="bkmk_view_resultant_fgpp"></a>手順 4: ユーザーのポリシーの結果セットを表示します。
細かい設定が可能なパスワード ポリシーを割り当てたグループのメンバーあるユーザーの結果のパスワード設定を表示する次の手順で[手順 3: 新しい詳細なパスワード ポリシーを作成](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp)します。

###### <a name="to-view-a-resultant-set-of-policies-for-a-user"></a>ユーザーのポリシーの結果セットを表示するには

1.  Windows PowerShell アイコンを右クリックして] をクリックして**管理者として実行**と種類**dsac.exe** ADAC を開きます。

2.  をクリックして**管理**、] をクリックして**ナビゲーション ノードの追加**で適切なターゲット ドメインを選択し、**ナビゲーション ノードの追加**] ダイアログ ボックスをクリック**OK**します。

3.  ユーザーを選択**test1**、グループに属している**group1**内で詳細なパスワード ポリシーを関連付けた[手順 3: 新しい詳細なパスワード ポリシーを作成](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp)します。

4.  をクリックして**ビューの結果のパスワード設定**で、**タスク**ウィンドウ。

5.  パスワード ポリシーの設定を確認し、クリックして**キャンセル**します。

![AD 管理センターの概要](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell と同等のコマンド * * *

次の Windows PowerShell コマンドレットまたはコマンドレットは、前の手順と同じ機能を実行します。 表示される場合でも可能性があります複数行に改行書式上の制約のためには、各コマンドレットを 1 つの行を入力します。

```
Get-ADUserResultantPasswordPolicy test1
```

#### <a name="bkmk_edit_fgpp"></a>手順 5: 詳細なパスワード ポリシーを編集します。
次の手順で作成した細かい設定が可能なパスワード ポリシーを編集する[手順 3: 新しい詳細なパスワード ポリシーを作成します。](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp)

###### <a name="to-edit-a-fine-grained-password-policy"></a>詳細なパスワード ポリシーを編集するには

1.  Windows PowerShell アイコンを右クリックして] をクリックして**管理者として実行**と種類**dsac.exe** ADAC を開きます。

2.  をクリックして**管理**、] をクリックして**ナビゲーション ノードの追加**で適切なターゲット ドメインを選択し、**ナビゲーション ノードの追加**] ダイアログ ボックスをクリック**OK**します。

3.  Adac**ナビゲーション ウィンドウ**、展開**システム**] をクリックし、**Password Settings Container**します。

4.  作成した細かい設定が可能なパスワード ポリシーを選択[手順 3: 新しい詳細なパスワード ポリシーを作成](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp)] をクリック**プロパティ**で、**タスク**ウィンドウ。

5.  **パスワード履歴を記録する**の値を変更**記憶するパスワードの数**に**30**します。

6.  をクリックして**OK**します。

![AD 管理センターの概要](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell と同等のコマンド * * *

次の Windows PowerShell コマンドレットまたはコマンドレットは、前の手順と同じ機能を実行します。 表示される場合でも可能性があります複数行に改行書式上の制約のためには、各コマンドレットを 1 つの行を入力します。

```
Set-ADFineGrainedPasswordPolicy TestPswd -PasswordHistoryCount:"30"
```

#### <a name="bkmk_delete_fgpp"></a>手順 6: 詳細なパスワード ポリシーを削除します。

###### <a name="to-delete-a-fine-grained-password-policy"></a>詳細なパスワード ポリシーを削除するには

1.  Windows PowerShell アイコンを右クリックして] をクリックして**管理者として実行**と種類**dsac.exe** ADAC を開きます。

2.  をクリックして**管理**、] をクリックして**ナビゲーション ノードの追加**で適切なターゲット ドメインを選択し、**ナビゲーション ノードの追加**] ダイアログ ボックスをクリック**OK**します。

3.  ADAC のナビゲーション ウィンドウで [**システム**] をクリックし、**Password Settings Container**します。

4.  作成した細かい設定が可能なパスワード ポリシーを選択[手順 3: 新しい詳細なパスワード ポリシーを作成](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp)し、[、**タスク**ウィンドウ] をクリック**プロパティ**します。

5.  クリア、**誤って削除されないように保護する**チェック ボックスをオン] をクリック**OK**します。

6.  細かい設定が可能なパスワード ポリシーを選択し、[、**タスク**ウィンドウ] をクリック**削除**します。

7.  をクリックして**OK**確認のダイアログ ボックス。

![AD 管理センターの概要](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)Windows PowerShell と同等のコマンド * * *

次の Windows PowerShell コマンドレットまたはコマンドレットは、前の手順と同じ機能を実行します。 表示される場合でも可能性があります複数行に改行書式上の制約のためには、各コマンドレットを 1 つの行を入力します。

```
Set-ADFineGrainedPasswordPolicy -Identity TestPswd -ProtectedFromAccidentalDeletion $False
Remove-ADFineGrainedPasswordPolicy TestPswd -Confirm
```

## <a name="windows_powershell_history_viewer"></a>Windows PowerShell 履歴ビューアー
ADAC は、Windows PowerShell 上に構築されるユーザー インターフェイス ツールです。  Windows Server 2012 では、IT 管理者は ADAC を Windows PowerShell 履歴ビューアーを使用して Active Directory コマンドレットの Windows PowerShell の学習を活用できます。 ユーザー インターフェイスでアクションが実行されるため、それと同等の Windows PowerShell コマンドが Windows PowerShell 履歴ビューアー内のユーザーに表示されます。 これにより、管理者は自動スクリプトを作成し、したがって IT 生産性を向上させ、繰り返しのタスクを削減できます。  また、この機能は、Active Directory 用 Windows PowerShell の学習に時間を削減して、自動化スクリプトが正しいかどうか、ユーザーの信頼性が向上します。

Windows Server 2012 で Windows PowerShell 履歴ビューアーを使用する場合は、次を考慮してください。

-   Windows PowerShell スクリプト ビューアーを使用するには、ADAC の Windows Server 2012 バージョンを使用する必要があります。

    > [!NOTE]
    > 使用することができます**サーバー マネージャー**正しいバージョンの Active Directory 管理センターを使用してユーザー インターフェイスからごみ箱を管理する Windows Server 2012 コンピューターにリモート サーバー管理ツール (RSAT) をインストールします。
    > 
    > 使用することができます[RSAT](https://go.microsoft.com/fwlink/?LinkID=238560) windows&reg; 8 台のコンピューターで正しいバージョンの Active Directory 管理センターを使用してユーザー インターフェイスからごみ箱を管理します。

-   Windows PowerShell の基本的な知識があります。 たとえば、Windows PowerShell のパイプ処理のしくみを理解する必要があります。 Windows PowerShell のパイプ処理の詳細については、次を参照してください。[パイプ処理と Windows PowerShell でパイプライン](https://technet.microsoft.com/library/ee176927.aspx)します。

### <a name="windows-powershell-history-viewer-step-by-step"></a>Windows PowerShell 履歴ビューアーの詳細な手順
次の手順では ADAC の Windows PowerShell 履歴ビューアーを使用して Windows PowerShell スクリプトを作成します。  この手順を開始する前にユーザーを削除**test1**グループから**group1**します。

##### <a name="to-construct-a-script-using-powershell-history-viewer"></a>PowerShell 履歴ビューアーを使用してスクリプトを作成するには

1.  Windows PowerShell アイコンを右クリックして] をクリックして**管理者として実行**と種類**dsac.exe** ADAC を開きます。

2.  をクリックして**管理**、] をクリックして**ナビゲーション ノードの追加**で適切なターゲット ドメインを選択し、**ナビゲーション ノードの追加**] ダイアログ ボックスをクリック**OK**します。

3.  展開、**Windows PowerShell 履歴**ADAC 画面の下部のウィンドウ。

4.  ユーザーの選択、**test1**します。

5.  をクリックして**グループに追加しています.**で、**タスク**ウィンドウ。

6.  移動**group1** ] をクリック**OK** ] ダイアログ ボックスでします。

7.  移動、**Windows PowerShell 履歴**ウィンドウを今生成されたコマンドを見つけます。

8.  コマンドをコピーし、スクリプトの作成に必要なエディターに貼り付けます。

    たとえば、別のユーザーを追加するコマンドを変更できます**group1**、または追加**test1**を別のグループ。

## <a name="see-also"></a>参照してください。
[Active Directory 管理センター (&) #40; を使用して高度な AD DS の管理レベル 200 & #41 です。](Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md)


