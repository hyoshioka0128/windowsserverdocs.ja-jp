---
ms.assetid: 074e63e9-976c-49da-8cba-9ae0b3325e34
title: Introduction to Active Directory Administrative Center Enhancements (Level 100)
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/07/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: a3bd82feb3a0caf827091bd0cb10edf991921b3c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71390617"
---
# <a name="introduction-to-active-directory-administrative-center-enhancements-level-100"></a>Introduction to Active Directory Administrative Center Enhancements (Level 100)

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Windows Server の Active Directory 管理センターには、次の管理機能が含まれています。

- [Active Directory のごみ箱](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#ad_recycle_bin_mgmt)
- [細かいパスワードポリシー](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#fine_grained_pswd_policy_mgmt)
- [Windows PowerShell 履歴ビューアー](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#windows_powershell_history_viewer)

## <a name="ad_recycle_bin_mgmt"></a>Active Directory のごみ箱

Active Directory ドメイン サービス (AD DS) や Active Directory ライトウェイト ディレクトリ サービス (AD LDS) のユーザーが、Active Directory オブジェクトを誤って削除してしまうことはよくあります。 Windows Server 2008 R2 では、前に、Windows Server の以前のバージョン 1 つでした Active Directory で、誤って削除されたオブジェクトは回復のソリューションは欠点がありました。

Windows Server 2008 では、Windows Server バックアップ機能と **ntdsutil** の権限ある回復コマンドを使ってオブジェクトを Authoritative とマークし、復元されたデータをドメイン全体に確実にレプリケートできました。 権限ある回復ソリューションの欠点は、これをディレクトリ サービス復元モード (DSRM) で実行しなければならなかったことです。 DSRM では、復元するドメイン コントローラーはオフラインのままにしておく必要があったので、 クライアント要求を処理できませんでした。

Windows Server 2003 の Active Directory および Windows Server 2008 の AD DS では、廃棄済みオブジェクト (Tombstone) を復元することで、削除された Active Directory オブジェクトを回復できました。 ただし、物理的に削除された復元オブジェクトのリンクされた値属性 (ユーザー アカウントのグループ メンバーシップなど)、および消去されたリンクされていない値属性は、回復されませんでした。 そのため、管理者は、誤ったオブジェクトの削除に対する最終的な解決策として、廃棄済みオブジェクト (Tombstone) に頼ることができませんでした。 廃棄済みオブジェクト (Tombstone) の復元の詳細については、「 [Active Directory の廃棄済みオブジェクトを復元する](https://go.microsoft.com/fwlink/?LinkID=125452)」を参照してください。

Windows Server 2008 R2 から導入された Active Directory のごみ箱は、既存の廃棄済みオブジェクト (Tombstone) の復元インフラストラクチャを基にして作られており、誤って削除された Active Directory オブジェクトを保存して回復する機能が強化されています。

Active Directory のごみ箱を有効にすると、削除された Active Directory オブジェクトのリンクされた値属性とリンクされていない値属性がすべて保持されます。このようなオブジェクトは、削除される直前と同じ、論理的に一貫性が保たれている状態に完全な形で復元されます。 たとえば、復元されたユーザー アカウントは、削除される直前に保持していた所属するドメイン内外のすべてのグループ メンバーシップと、それに対応するアクセス権を自動的に回復します。 Active Directory のごみ箱は、AD DS 環境でも AD LDS 環境でも動作します。 Active Directory のごみ箱の詳細については、次を参照してください。 [AD DS の新機能: Active Directory のごみ箱](https://technet.microsoft.com/library/dd391916(WS.10).aspx)します。

**新機能** Windows Server 2012 以降では、ユーザーが削除されたオブジェクトを管理および復元するための新しいグラフィカルユーザーインターフェイスを使用して、Active Directory のごみ箱機能が強化されています。 ユーザーは削除されたオブジェクトの一覧を視覚的に探して、オブジェクトを元の場所または望む場所に復元できます。

Windows Server で Active Directory のごみ箱を有効にする予定がある場合は、次の点を考慮してください。

- Active Directory のごみ箱は既定で無効になっています。 これを有効にするには、まず、AD DS または AD LDS 環境のフォレストの機能レベルを Windows Server 2008 R2 以降に上げる必要があります。 これには、フォレスト内のすべてのドメインコントローラー、または AD LDS 構成セットのインスタンスをホストするすべてのサーバーが Windows Server 2008 R2 以降を実行している必要があります。
- Active Directory のごみ箱を有効にするプロセスは元に戻すことができません。 使用している環境で Active Directory のごみ箱を有効にした後で、そのごみ箱を無効にすることはできません。
- ユーザーインターフェイスを使用してごみ箱機能を管理するには、Windows Server 2012 に Active Directory 管理センターのバージョンをインストールする必要があります。

    > [!NOTE]
    > **サーバーマネージャー**を使用すると、リモートサーバー管理ツール (RSAT) をインストールして、正しいバージョンの Active Directory 管理センターを使用して、ユーザーインターフェイスからごみ箱を管理できます。
    >
    > RSAT のインストールの詳細については、「[リモートサーバー管理ツール](https://docs.microsoft.com/windows-server/remote/remote-server-administration-tools)」を参照してください。

### <a name="active-directory-recycle-bin-step-by-step"></a>Active Directory のごみ箱の手順

次の手順では、ADAC を使用して、Windows Server 2012 で、次の Active Directory のごみ箱のタスクを実行します。

- [手順 1: フォレストの機能レベルを上げる](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_raise_ffl)
- [手順 2: ごみ箱を有効にする](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_enable_recycle_bin)
- [手順 3: テストユーザー、グループ、組織単位を作成する](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_test_env)
- [手順 4: 削除されたオブジェクトを復元する](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_restore_del_obj)

> [!NOTE]
> 以下の手順を実行するには、Enterprise Admins グループのメンバーシップ、またはそれと同等のアクセス許可が必要です。

### <a name="bkmk_raise_ffl"></a>手順 1: フォレストの機能レベルを上げる

この手順では、フォレストの機能レベルを上げます。 Active Directory のごみ箱を有効にする前に、少なくとも Windows Server 2008 R2 であるターゲット フォレストの機能レベルを上げる必要があります。

#### <a name="to-raise-the-functional-level-on-the-target-forest"></a>ターゲット フォレストの機能レベルを上げるには

1. Windows PowerShell アイコンを右クリックして、クリックして **管理者として実行** と種類 **dsac.exe** ADAC を開きます。

2. **[管理]** 、 **[ナビゲーション ノードの追加]** の順にクリックし、 **[ナビゲーション ノードの追加]** ダイアログ ボックスで適切なターゲット ドメインを選択して **[OK]** をクリックします。

3. 左側のナビゲーション ウィンドウでターゲット ドメインをクリックし、 **[タスク]** ウィンドウの **[フォレストの機能レベルの昇格]** をクリックします。 少なくとも、フォレストの機能レベルを選択して Windows Server 2008 R2 またはそれ以降順にクリック **OK**します。

![AD 管理センターの](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>Windows PowerShell の同等のコマンド</em>の概要***

以下の Windows PowerShell コマンドレットは、前述の手順と同じ機能を実行します。 ここでは書式上の制約のために、折り返されて複数の行にわたって表示される場合もありますが、各コマンドレットは 1 行に入力します。

```powershell
Set-ADForestMode -Identity contoso.com -ForestMode Windows2008R2Forest -Confirm:$false
```

**-Identity**引数には、完全修飾 DNS ドメイン名を指定します。

### <a name="bkmk_enable_recycle_bin"></a>手順 2: ごみ箱を有効にする

この手順では、削除された AD DS のオブジェクトを復元するためにごみ箱を有効にします。

#### <a name="to-enable-active-directory-recycle-bin-in-adac-on-the-target-domain"></a>ADAC でターゲット ドメインの Active Directory のごみ箱を有効にするには

1. Windows PowerShell アイコンを右クリックして、クリックして **管理者として実行** と種類 **dsac.exe** ADAC を開きます。

2. **[管理]** 、 **[ナビゲーション ノードの追加]** の順にクリックし、 **[ナビゲーション ノードの追加]** ダイアログ ボックスで適切なターゲット ドメインを選択して **[OK]** をクリックします。

3. **[タスク]** ウィンドウで、 **[タスク]** ウィンドウの **[ごみ箱の有効化]** をクリックし、警告メッセージ ボックスで **[OK]** をクリックしてから **[OK]** をクリックすると、ADAC の更新メッセージが表示されます。

4. F5 キーを押して ADAC を更新します。

![AD 管理センターの](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>Windows PowerShell の同等のコマンド</em>の概要***

以下の Windows PowerShell コマンドレットは、前述の手順と同じ機能を実行します。 ここでは書式上の制約のために、折り返されて複数の行にわたって表示される場合もありますが、各コマンドレットは 1 行に入力します。

```powershell
Enable-ADOptionalFeature -Identity 'CN=Recycle Bin Feature,CN=Optional Features,CN=Directory Service,CN=Windows NT,CN=Services,CN=Configuration,DC=contoso,DC=com' -Scope ForestOrConfigurationSet -Target 'contoso.com'
```

### <a name="bkmk_create_test_env"></a>手順 3: テストユーザー、グループ、組織単位を作成する

この手順では、テスト ユーザーを 2 つ作成します。 その後テスト グループを作成し、テスト ユーザーをこのグループに追加します。 さらに OU を作成します。

#### <a name="to-create-test-users"></a>テスト ユーザーを作成するには

1. Windows PowerShell アイコンを右クリックして、クリックして **管理者として実行** と種類 **dsac.exe** ADAC を開きます。

2. **[管理]** 、 **[ナビゲーション ノードの追加]** の順にクリックし、 **[ナビゲーション ノードの追加]** ダイアログ ボックスで適切なターゲット ドメインを選択して **[OK]** をクリックします。

3. **[タスク]** ウィンドウの **[新規]** をクリックし、 **[ユーザー]** をクリックします。

    ![AD 管理センターの入門ページ](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/ADDS_ADACNewUser.gif)

4. **[アカウント]** に次の情報を入力して [OK] をクリックします。

   - フル ネーム: test1
   - ユーザー SAM アカウント名ログオン: test1
   - パスワード: p@ssword1
   - パスワードの確認入力: p@ssword1

5. 前の手順を繰り返して 2 つ目のユーザー test2 を作成します。

#### <a name="to-create-a-test-group-and-add-users-to-the-group"></a>テスト グループを作成してユーザーをグループに追加するには

1. Windows PowerShell アイコンを右クリックして、クリックして **管理者として実行** と種類 **dsac.exe** ADAC を開きます。
2. **[管理]** 、 **[ナビゲーション ノードの追加]** の順にクリックし、 **[ナビゲーション ノードの追加]** ダイアログ ボックスで適切なターゲット ドメインを選択して **[OK]** をクリックします。
3. **[タスク]** ウィンドウの **[新規]** をクリックし、 **[グループ]** をクリックします。
4. **[グループ]** に次の情報を入力して **[OK]** をクリックします。

    -   **グループ名: group1**

5. **[group1]** をクリックし、 **[タスク]** ウィンドウの **[プロパティ]** をクリックします。
6. **[メンバー]** 、 **[追加]** の順にクリックし、「**test1;test2**」と入力して、 **[OK]** をクリックします。

![AD 管理センターの](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>Windows PowerShell の同等のコマンド</em>の概要***

以下の Windows PowerShell コマンドレットは、前述の手順と同じ機能を実行します。 ここでは書式上の制約のために、折り返されて複数の行にわたって表示される場合もありますが、各コマンドレットは 1 行に入力します。

```powershell
Add-ADGroupMember -Identity group1 -Member test1
```

#### <a name="to-create-an-organizational-unit"></a>組織単位を作成するには

1. Windows PowerShell アイコンを右クリックして、クリックして **管理者として実行** と種類 **dsac.exe** ADAC を開きます。
2. **管理** をクリックし、**ナビゲーションノードの追加** をクリックして、**ナビゲーションノードの追加** ダイアログボックスで適切なターゲットドメインを選択し、OK をクリックします。
3. **[タスク]** ウィンドウの **[新規]** をクリックし、 **[組織単位]** をクリックします。
4. **[組織単位]** に次の情報を入力して **[OK]** をクリックします。

   - **NameOU1**

![AD 管理センターの](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>Windows PowerShell の同等のコマンド</em>の概要***

以下の Windows PowerShell コマンドレットは、前述の手順と同じ機能を実行します。 ここでは書式上の制約のために、折り返されて複数の行にわたって表示される場合もありますが、各コマンドレットは 1 行に入力します。

```powershell
1..2 | ForEach-Object {New-ADUser -SamAccountName test$_ -Name "test$_" -Path "DC=fabrikam,DC=com" -AccountPassword (ConvertTo-SecureString -AsPlainText "p@ssword1" -Force) -Enabled $true}
New-ADGroup -Name "group1" -SamAccountName group1 -GroupCategory Security -GroupScope Global -DisplayName "group1"
New-ADOrganizationalUnit -Name OU1 -Path "DC=fabrikam,DC=com"
```

### <a name="bkmk_restore_del_obj"></a>手順 4: 削除されたオブジェクトを復元する

この手順では、削除されたオブジェクトを **[Deleted Objects]** コンテナーから元の場所および別の場所に復元します。

#### <a name="to-restore-deleted-objects-to-their-original-location"></a>削除されたオブジェクトを元の場所に復元するには

1. Windows PowerShell アイコンを右クリックして、クリックして **管理者として実行** と種類 **dsac.exe** ADAC を開きます。

2. **[管理]** 、 **[ナビゲーション ノードの追加]** の順にクリックし、 **[ナビゲーション ノードの追加]** ダイアログ ボックスで適切なターゲット ドメインを選択して **[OK]** をクリックします。

3. ユーザー **[test1]** および **[test2]** を選択し、 **[タスク]** ウィンドウの **[削除]** をクリックし、 **[はい]** をクリックして削除を確定します。

    ![AD 管理センターの](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>Windows PowerShell の同等のコマンド</em>の概要***

    以下の Windows PowerShell コマンドレットは、前述の手順と同じ機能を実行します。 ここでは書式上の制約のために、折り返されて複数の行にわたって表示される場合もありますが、各コマンドレットは 1 行に入力します。

    ```powershell
    Get-ADUser -Filter 'Name -Like "*test*"'|Remove-ADUser -Confirm:$false
    ```

4. **[Deleted Objects]** コンテナーに移動し、 **[test2]** および **[test1]** を選択し、 **[タスク]** ウィンドウの **[復元]** をクリックします。

5. オブジェクトが元の場所に復元されたことを確認するために、ターゲット ドメインに移動してユーザー アカウントが表示されていることを確認します。

    > [!NOTE]
    > ユーザー アカウント **[test1]** および **[test2]** の **[プロパティ]** に移動して **[所属するグループ]** をクリックすると、グループ メンバーシップも復元されていることを確認できます。

以下の Windows PowerShell コマンドレットは、前述の手順と同じ機能を実行します。 ここでは書式上の制約のために、折り返されて複数の行にわたって表示される場合もありますが、各コマンドレットは 1 行に入力します。

![AD 管理センターの](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>Windows PowerShell の同等のコマンド</em>の概要***

```powershell
Get-ADObject -Filter 'Name -Like "*test*"' -IncludeDeletedObjects | Restore-ADObject
```

#### <a name="to-restore-deleted-objects-to-a-different-location"></a>削除されたオブジェクトを別の場所に復元するには

1. Windows PowerShell アイコンを右クリックして、クリックして **管理者として実行** と種類 **dsac.exe** ADAC を開きます。

2. **[管理]** 、 **[ナビゲーション ノードの追加]** の順にクリックし、 **[ナビゲーション ノードの追加]** ダイアログ ボックスで適切なターゲット ドメインを選択して **[OK]** をクリックします。

3. ユーザー **[test1]** および **[test2]** を選択し、 **[タスク]** ウィンドウの **[削除]** をクリックし、 **[はい]** をクリックして削除を確定します。

4. **[Deleted Objects]** コンテナーに移動し、 **[test2]** および **[test1]** を選択し、 **[タスク]** ウィンドウの **[復元先]** をクリックします。

5. **[OU1]** を選択して **[OK]** をクリックします。

6. オブジェクトが **[OU1]** に復元されたことを確認するために、ターゲット ドメインに移動して **[OU1]** をダブルクリックし、ユーザー アカウントが表示されていることを確認します。

![AD 管理センターの](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>Windows PowerShell の同等のコマンド</em>の概要***

以下の Windows PowerShell コマンドレットは、前述の手順と同じ機能を実行します。 ここでは書式上の制約のために、折り返されて複数の行にわたって表示される場合もありますが、各コマンドレットは 1 行に入力します。

```powershell
Get-ADObject -Filter 'Name -Like "*test*"' -IncludeDeletedObjects | Restore-ADObject -TargetPath "OU=OU1,DC=contoso,DC=com"
```

## <a name="fine_grained_pswd_policy_mgmt"></a>細かいパスワードポリシー

Windows Server 2008 オペレーティング システムでは、ドメイン内の異なるユーザー グループに対して個別にパスワード ポリシーやアカウント ロックアウト ポリシーを定義する手段を提供しています。 Windows Server 2008 より前の Active Directory ドメインでは、ドメイン内のすべてのユーザーに対して 1 つのパスワード ポリシーおよびアカウント ロックアウト ポリシーしか適用できませんでした。 これらのポリシーは、Default Domain Policy の中でドメインに対して指定していました。 この結果、異なるユーザー グループに対して個別にパスワードやアカウント ロックアウトを設定したい組織では、パスワード フィルターを作成するか複数ドメインを採用する必要がありました。 どちらもコストがかかる選択肢です。

細かい設定が可能なパスワード ポリシーを使用すると、1 つのドメイン内に複数のパスワード ポリシーを指定したり、ドメイン内の異なるユーザー グループに対してパスワード ポリシーやアカウント ロックアウト ポリシーによる制限を個別に適用したりできます。 たとえば、特権アカウントにはより厳しい設定を適用し、他のユーザー アカウントにはあまり厳しくない設定を適用することができます。 別の例として、他のデータ ソースと同期するパスワードを持つアカウントには特別なパスワード ポリシーを適用することもできます。 細かいパスワード ポリシーの詳細については、次を参照してください [AD DS: 細かいパスワード ポリシー。](https://technet.microsoft.com/library/cc770394(WS.10).aspx)

**新機能**

Windows Server 2012 以降では、細かい構成が可能なパスワードポリシーの管理は、AD DS 管理者が ADAC で管理するためのユーザーインターフェイスを提供することで、より簡単で視覚的になりました。 管理者ようになりました指定されたユーザーのポリシーの結果を表示、表示し、指定されたドメイン内のすべてのパスワード ポリシーを並べ替えるして個々 のパスワード ポリシーを視覚的に管理します。

Windows Server 2012 で細かいパスワードポリシーを使用する場合は、次の点を考慮してください。

- 細かい設定が可能なパスワードポリシーは、グローバルセキュリティグループとユーザーオブジェクト (または、ユーザーオブジェクトの代わりに使用される場合は inetOrgPerson オブジェクト) にのみ適用されます。 既定では、Domain Admins グループのメンバーのみが細かい設定が可能なパスワード ポリシーを設定できます。 ただし、このポリシーを設定する権限を他のユーザーに委任することもできます。 ドメインの機能レベルが Windows Server 2008 以上である必要があります。

- グラフィカルユーザーインターフェイスを使用して細かいパスワードポリシーを管理するには、Windows Server 2012 以降のバージョンの Active Directory 管理センターを使用する必要があります。

    > [!NOTE]
    > **サーバーマネージャー**を使用すると、リモートサーバー管理ツール (RSAT) をインストールして、正しいバージョンの Active Directory 管理センターを使用して、ユーザーインターフェイスからごみ箱を管理できます。
    >
    > RSAT のインストールの詳細については、「[リモートサーバー管理ツール](https://docs.microsoft.com/windows-server/remote/remote-server-administration-tools)」を参照してください。

### <a name="fine-grained-password-policy-step-by-step"></a>細かい設定が可能なパスワード ポリシーの手順

以下のステップでは、ADAC を使用して細かい設定が可能なパスワード ポリシーのタスクを実行します。

- [手順 1: ドメインの機能レベルを上げる](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_raise_dfl)
- [手順 2: テストユーザー、グループ、および組織単位を作成する](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk2_test_fgpp)
- [手順 3: 新しい細かい細かいパスワードポリシーを作成する](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp)
- [手順 4: ユーザーのポリシーの結果セットを表示する](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_view_resultant_fgpp)
- [手順 5: 細かい変更が可能なパスワードポリシーを編集する](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_edit_fgpp)
- [手順 6: 細かい細かいパスワードポリシーを削除する](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_delete_fgpp)

> [!NOTE]
> 以下の手順を実行するには、Domain Admins グループのメンバーシップ、またはそれと同等のアクセス許可が必要です。

#### <a name="bkmk_raise_dfl"></a>手順 1: ドメインの機能レベルを上げる

次の手順では Windows Server 2008 またはそれ以降は、移行先ドメインのドメインの機能レベルが発生します。 詳細なパスワード ポリシーを有効にするには、Windows Server 2008 以降のドメイン機能レベルが必要です。

##### <a name="to-raise-the-domain-functional-level"></a>ドメインの機能レベルを上げるには

1. Windows PowerShell アイコンを右クリックして、クリックして **管理者として実行** と種類 **dsac.exe** ADAC を開きます。

2. **[管理]** 、 **[ナビゲーション ノードの追加]** の順にクリックし、 **[ナビゲーション ノードの追加]** ダイアログ ボックスで適切なターゲット ドメインを選択して **[OK]** をクリックします。

3. 左側のナビゲーション ウィンドウでターゲット ドメインをクリックし、 **[タスク]** ウィンドウの **[ドメインの機能レベルの昇格]** をクリックします。 少なくとも、フォレストの機能レベルを選択してクリックして Windows Server 2008 以降 **OK**します。

![AD 管理センターの](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>Windows PowerShell の同等のコマンド</em>の概要***

以下の Windows PowerShell コマンドレットは、前述の手順と同じ機能を実行します。 ここでは書式上の制約のために、折り返されて複数の行にわたって表示される場合もありますが、各コマンドレットは 1 行に入力します。

```powershell
Set-ADDomainMode -Identity contoso.com -DomainMode 3
```

#### <a name="bkmk2_test_fgpp"></a>手順 2: テストユーザー、グループ、および組織単位を作成する

この手順に必要なテストユーザーとグループを作成するには、次の手順に従います。[手順 3: テストユーザー、グループ、組織単位を作成](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_test_env)する (詳細なパスワードポリシーを示すために OU を作成する必要はありません)。

#### <a name="bkmk_create_fgpp"></a>手順 3: 新しい細かい細かいパスワードポリシーを作成する

この手順では、ADAC の UI を使用して新しい細かい設定が可能なパスワード ポリシーを作成します。

##### <a name="to-create-a-new-fine-grained-password-policy"></a>新しい細かい設定が可能なパスワード ポリシーを作成するには

1. Windows PowerShell アイコンを右クリックして、クリックして **管理者として実行** と種類 **dsac.exe** ADAC を開きます。

2. **[管理]** 、 **[ナビゲーション ノードの追加]** の順にクリックし、 **[ナビゲーション ノードの追加]** ダイアログ ボックスで適切なターゲット ドメインを選択して **[OK]** をクリックします。

3. ADAC のナビゲーション ウィンドウで、 **[System]** コンテナーを展開して **[Password Settings Container]** をクリックします。

4. **[タスク]** ウィンドウの **[新規作成]** をクリックし、 **[パスワードの設定]** をクリックします。

    [プロパティ] ページ内のフィールドに入力するかまたは編集して、新しい **[パスワードの設定]** オブジェクトを作成します。 **"名前"** と **"優先順位"** フィールドが必要です。

    ![AD 管理センターの入門ページ](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/ADDS_ADACNewFGPP.gif)

5. [ **直接の適用先**, 、] をクリックして **追加**, 、型 **group1**, 、順にクリック **OK**します。

    これによりパスワード ポリシー オブジェクトが、テスト環境用に作成したグローバル グループのメンバーに関連付けられます。

6. **[OK]** をクリックして作成を送信します。

![AD 管理センターの](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>Windows PowerShell の同等のコマンド</em>の概要***

以下の Windows PowerShell コマンドレットは、前述の手順と同じ機能を実行します。 ここでは書式上の制約のために、折り返されて複数の行にわたって表示される場合もありますが、各コマンドレットは 1 行に入力します。

```powershell
New-ADFineGrainedPasswordPolicy TestPswd -ComplexityEnabled:$true -LockoutDuration:"00:30:00" -LockoutObservationWindow:"00:30:00" -LockoutThreshold:"0" -MaxPasswordAge:"42.00:00:00" -MinPasswordAge:"1.00:00:00" -MinPasswordLength:"7" -PasswordHistoryCount:"24" -Precedence:"1" -ReversibleEncryptionEnabled:$false -ProtectedFromAccidentalDeletion:$true
Add-ADFineGrainedPasswordPolicySubject TestPswd -Subjects group1
```

#### <a name="bkmk_view_resultant_fgpp"></a>手順 4: ユーザーのポリシーの結果セットを表示する

この手順では、「[手順 3: 新しい細かい設定が可能なパスワード ポリシーを作成する](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp)」でポリシーを割り当てたグループのメンバーであるユーザーの、結果のパスワード設定を表示します。

##### <a name="to-view-a-resultant-set-of-policies-for-a-user"></a>ユーザーのポリシーの結果セットを表示するには

1. Windows PowerShell アイコンを右クリックして、クリックして **管理者として実行** と種類 **dsac.exe** ADAC を開きます。

2. **[管理]** 、 **[ナビゲーション ノードの追加]** の順にクリックし、 **[ナビゲーション ノードの追加]** ダイアログ ボックスで適切なターゲット ドメインを選択して **[OK]** をクリックします。

3. ユーザーを選択 **test1** 、グループに属する **group1** で詳細なパスワード ポリシーを関連付けた [手順 3: 新しいきめ細かなパスワード ポリシーを作成](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp)します。

4. **[タスク]** ウィンドウの **[結果のパスワード設定の表示]** をクリックします。

5. パスワード設定ポリシーを確認して **[キャンセル]** をクリックします。

![AD 管理センターの](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>Windows PowerShell の同等のコマンド</em>の概要***

以下の Windows PowerShell コマンドレットは、前述の手順と同じ機能を実行します。 ここでは書式上の制約のために、折り返されて複数の行にわたって表示される場合もありますが、各コマンドレットは 1 行に入力します。

```powershell
Get-ADUserResultantPasswordPolicy test1
```

#### <a name="bkmk_edit_fgpp"></a>手順 5: 細かい変更が可能なパスワードポリシーを編集する

この手順では、「[手順 3: 新しい細かい設定が可能なパスワード ポリシーを作成する](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp)」で作成した細かい設定が可能なパスワード ポリシーを編集します。

##### <a name="to-edit-a-fine-grained-password-policy"></a>細かい設定が可能なパスワード ポリシーを編集するには

1. Windows PowerShell アイコンを右クリックして、クリックして **管理者として実行** と種類 **dsac.exe** ADAC を開きます。

2. **[管理]** 、 **[ナビゲーション ノードの追加]** の順にクリックし、 **[ナビゲーション ノードの追加]** ダイアログ ボックスで適切なターゲット ドメインを選択して **[OK]** をクリックします。

3. ADAC の **[ナビゲーション ウィンドウ]** で、 **[System]** を展開して **[Password Settings Container]** をクリックします。

4. 「[手順 3: 新しい細かい設定が可能なパスワード ポリシーを作成する](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp)」で作成した細かい設定が可能なパスワード ポリシーを選択し、 **[タスク]** ウィンドウの **[プロパティ]** をクリックします。

5. **[パスワードの履歴を記録する]** の **[記録するパスワードの数]** の値を「 **30**」に変更します。

6. **[OK]** をクリックします。

![AD 管理センターの](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>Windows PowerShell の同等のコマンド</em>の概要***

以下の Windows PowerShell コマンドレットは、前述の手順と同じ機能を実行します。 ここでは書式上の制約のために、折り返されて複数の行にわたって表示される場合もありますが、各コマンドレットは 1 行に入力します。

```powershell
Set-ADFineGrainedPasswordPolicy TestPswd -PasswordHistoryCount:"30"
```

#### <a name="bkmk_delete_fgpp"></a>手順 6: 細かい細かいパスワードポリシーを削除する

##### <a name="to-delete-a-fine-grained-password-policy"></a>細かい設定が可能なパスワード ポリシーを削除するには

1. Windows PowerShell アイコンを右クリックして、クリックして **管理者として実行** と種類 **dsac.exe** ADAC を開きます。

2. **[管理]** 、 **[ナビゲーション ノードの追加]** の順にクリックし、 **[ナビゲーション ノードの追加]** ダイアログ ボックスで適切なターゲット ドメインを選択して **[OK]** をクリックします。

3. ADAC の [ナビゲーション ウィンドウ] で、 **[System]** を展開して **[Password Settings Container]** をクリックします。

4. 「[手順 3: 新しい細かい設定が可能なパスワード ポリシーを作成する](../../../ad-ds/get-started/adac/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-.md#bkmk_create_fgpp)」で作成した細かい設定が可能なパスワード ポリシーを選択し、 **[タスク]** ウィンドウの **[プロパティ]** をクリックします。

5. **[誤って削除されないように保護する]** チェック ボックスをオフにして、 **[OK]** をクリックします。

6. 細かい設定が可能なパスワード ポリシーを選択し、 **[タスク]** ウィンドウの **[削除]** をクリックします。

7. 確認のダイアログで、 **[OK]** をクリックします。

![AD 管理センターの](media/Introduction-to-Active-Directory-Administrative-Center-Enhancements--Level-100-/PowerShellLogoSmall.gif)***<em>Windows PowerShell の同等のコマンド</em>の概要***

以下の Windows PowerShell コマンドレットは、前述の手順と同じ機能を実行します。 ここでは書式上の制約のために、折り返されて複数の行にわたって表示される場合もありますが、各コマンドレットは 1 行に入力します。

```powershell
Set-ADFineGrainedPasswordPolicy -Identity TestPswd -ProtectedFromAccidentalDeletion $False
Remove-ADFineGrainedPasswordPolicy TestPswd -Confirm
```

## <a name="windows_powershell_history_viewer"></a>Windows PowerShell 履歴ビューアー

ADAC は Windows PowerShell の上に構築されたユーザー インターフェイス ツールです。 Windows Server 2012 以降では、IT 管理者は ADAC を利用して、windows PowerShell 履歴ビューアーを使用して Active Directory コマンドレット用の Windows PowerShell について学習することができます。 ユーザー インターフェイスでアクションが実行されると、対応する Windows PowerShell コマンドが Windows PowerShell 履歴ビューアーに表示されます。 これにより、管理者は自動化されたスクリプトを作成でき、繰り返しのタスクを減らして IT 生産性を向上できます。 また、この機能は、Active Directory 用 Windows PowerShell の学習に時間が短縮され、自動化スクリプトが正しいかどうか、ユーザーの信頼性が向上します。

Windows Server 2012 以降で Windows PowerShell 履歴ビューアーを使用する場合は、次の点を考慮してください。

- Windows PowerShell スクリプトビューアーを使用するには、Windows Server 2012 以降のバージョンの ADAC を使用する必要があります。

    > [!NOTE]
    > **サーバーマネージャー**を使用すると、リモートサーバー管理ツール (RSAT) をインストールして、正しいバージョンの Active Directory 管理センターを使用して、ユーザーインターフェイスからごみ箱を管理できます。
    >
    > RSAT のインストールの詳細については、「[リモートサーバー管理ツール](https://docs.microsoft.com/windows-server/remote/remote-server-administration-tools)」を参照してください。

- Windows PowerShell についての基本的な知識があること。 たとえば、Windows PowerShell のパイプ処理についての知識が必要です。 Windows PowerShell のパイプ処理の詳細については、「 [Piping and the Pipeline in Windows PowerShell (Windows PowerShell のパイプ処理とパイプライン)](https://technet.microsoft.com/library/ee176927.aspx)」を参照してください。

### <a name="windows-powershell-history-viewer-step-by-step"></a>Windows PowerShell 履歴ビューアーの手順

この手順では、ADAC の Windows PowerShell 履歴ビューアーを使用して Windows PowerShell スクリプトを作成します。  この手順を始める前に、グループ **[group1]** からユーザー **[test1]** を削除してください。

#### <a name="to-construct-a-script-using-powershell-history-viewer"></a>PowerShell 履歴ビューアーを使用してスクリプトを作成するには

1. Windows PowerShell アイコンを右クリックして、クリックして **管理者として実行** と種類 **dsac.exe** ADAC を開きます。

2. **[管理]** 、 **[ナビゲーション ノードの追加]** の順にクリックし、 **[ナビゲーション ノードの追加]** ダイアログ ボックスで適切なターゲット ドメインを選択して **[OK]** をクリックします。

3. ADAC 画面の下にある **[Windows PowerShell 履歴]** ウィンドウを広げます。

4. ユーザー **[test1]** を選択します。

5. クリックして **グループに追加...** で、 **タスク** ウィンドウです。

6. **[group1]** を選択し、ダイアログ ボックスで **[OK]** をクリックします。

7. **[Windows PowerShell 履歴]** ウィンドウに移動し、今生成されたコマンドを探します。

8. このコマンドをコピーし、スクリプトの作成に使用するエディターに貼り付けます。

    このコマンドを変更して、たとえば別のユーザーを **[group1]** に追加したり、 **[test1]** を別のグループに追加したりできます。

## <a name="see-also"></a>参照

[Active Directory 管理センター &#40;レベル200を使用した高度な AD DS 管理&#41;](Advanced-AD-DS-Management-Using-Active-Directory-Administrative-Center--Level-200-.md)
