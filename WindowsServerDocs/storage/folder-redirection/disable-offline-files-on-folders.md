---
title: 個々 のリダイレクトされたフォルダーのオフライン ファイルを無効にします。
description: オフライン ファイル キャッシュ フォルダーのリダイレクトを使用してネットワーク共有にリダイレクトされた個々 のフォルダーを無効にする方法。
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: b006742c9256c357d9aff3fb1b765dbed087383a
ms.sourcegitcommit: ed27ddbe316d543b7865bc10590b238290a2a1ad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/09/2019
ms.locfileid: "65475883"
---
# <a name="disable-offline-files-on-individual-redirected-folders"></a>個々 のリダイレクトされたフォルダーのオフライン ファイルを無効にします。

>適用対象:Windows 10、Windows 8、Windows 8.1、Windows Server 2019、Windows Server 2016、Windows Server 2012、Windows Server 2012 R2、Windows (半期チャネル)

このトピックでは、オフライン ファイル キャッシュ フォルダーのリダイレクトを使用してネットワーク共有にリダイレクトされた個々 のフォルダーを無効にする方法について説明します。 これにより、ローカル キャッシュから除外するフォルダーを指定できる、オフライン ファイルを同期するオフライン ファイル キャッシュの削減サイズと時間必要です。

>[!NOTE]
>このトピックでは、サンプル Windows PowerShell コマンドレットを紹介します。ここで説明する手順の一部はこのコマンドレットで自動化できます。 詳細については、次を参照してください。 [Windows PowerShell の基礎](https://docs.microsoft.com/powershell/scripting/getting-started/fundamental/windows-powershell-basics?view=powershell-6)します。

## <a name="prerequisites"></a>前提条件

特定のリダイレクトされたフォルダーのオフライン ファイルのキャッシュを無効にするには、環境は、次の前提条件を満たす必要があります。

- ドメインに参加しているクライアント コンピューターとの Active Directory Domain Services (AD DS) ドメイン。 フォレストまたはドメインの機能レベル要件やスキーマの要件はありません。
- Windows 10、Windows 8.1、Windows 8、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012 または Windows (半期チャネル) を実行しているクライアント コンピューター。
- グループ ポリシー管理がインストールされているコンピューター。

## <a name="disabling-offline-files-on-individual-redirected-folders"></a>個々 のリダイレクトされたフォルダーのオフライン ファイルを無効にします。

特定のリダイレクトされたフォルダーのオフライン ファイルのキャッシュを無効にするには、有効にするグループ ポリシーを使用、**自動的にオフラインようにしないリダイレクトされたフォルダーの特定使用可能な**ポリシー設定の適切なグループ ポリシー オブジェクト (GPO)。 このポリシー設定を構成する**無効になっている**または**構成されていない**すべてのリダイレクトされたフォルダーをオフラインで使用できるようにします。

>[!NOTE]
>ドメイン管理者、enterprise administrators、およびグループ ポリシーの creator owners グループのメンバーは、Gpo を作成できます。

### <a name="to-disable-offline-files-on-specific-redirected-folders"></a>特定のリダイレクトされたフォルダーのオフライン ファイルを無効にするには

1. 開いている**グループ ポリシー管理**します。
2. 必要に応じてユーザーがオフライン使用から除外するフォルダーをリダイレクトがある必要がありますを指定する新しい GPO を作成する適切なドメインまたは組織単位 (OU) を右クリックし、**このドメインに GPO を作成し、リンクここで it**します。
3. コンソール ツリーで、フォルダー リダイレクトの設定を構成し、選択する GPO を右クリックして**編集**します。 グループ ポリシー管理エディターが表示されます。
4. コンソール ツリーで **ユーザー構成**、展開**ポリシー**、展開**管理用テンプレート**、展開**システム**と展開**フォルダー リダイレクト**します。
5. 右クリック**自動的にオフラインようにしないリダイレクトされたフォルダーの特定使用可能な**選び**編集**します。 **自動的にオフラインようにしないリダイレクトされたフォルダーの特定使用可能な**ウィンドウが表示されます。
6. **[有効]** を選びます。 **オプション** ウィンドウがない利用できるようにオフライン、該当するチェック ボックスを選択してフォルダーを選択します。 **[OK]** を選択します。

### <a name="windows-powershell-equivalent-commands"></a>Windows PowerShell と同等のコマンド

次の Windows PowerShell コマンドレットまたはコマンドレット」の手順の説明に従って、同じ関数を実行[を無効にするオフライン ファイルの個々 のリダイレクトされたフォルダー](#disabling-offline-files-on-individual-redirected-folders)します。 ここでは書式上の制約のために、折り返されて複数の行にわたって表示される場合もありますが、各コマンドレットは 1 行に入力します。

この例は、という名前の新しい GPO を作成します*オフライン ファイル設定*で、 *MyOu*内の組織単位、 *contoso.com*ドメイン (LDAP 識別名は"ou = MyOU, dc =。contoso, dc = com")。 ビデオのリダイレクト フォルダーのオフライン ファイル、無効にします。

```PowerShell
New-GPO -Name "Offline Files Settings" | New-Gplink -Target "ou=MyOu,dc=contoso,dc=com" -LinkEnabled Yes

Set-GPRegistryValue –Name "Offline Files Settings" –Key
"HKCU\Software\Policies\Microsoft\Windows\NetCache\{18989B1D-99B5-455B-841C-AB7C74E4DDFC}" -ValueName DisableFRAdminPinByFolder –Type DWORD –Value 1
```

リダイレクトされたフォルダーごとに使用するレジストリ キー名 (フォルダーの Guid) の一覧については、次の表を参照してください。

|リダイレクトされたフォルダー|レジストリ キーの名前 (フォルダーの GUID)|
|---|---|
|AppData(Roaming)|{3EB685DB-65F9-4CF6-A03A-E3EF65729F3D}|
|Desktop|{B4BFCC3A-DB2C-424C-B029-7FE99A87C641}|
|スタート メニュー|{625B53C3-AB48-4EC1-BA1F-A1EF4146FC19}|
|Documents|{FDD39AD0-238F-46AF-ADB4-6C85480369C7}|
|画像|{33E28130-4E1E-4676-835A-98395C3BC3BB}|
|音楽|{4BD8D571-6D19-48D3-BE97-422220080E43}|
|ビデオ|{18989B1D-99B5-455B-841C-AB7C74E4DDFC}|
|Favorites|{1777F761-68AD-4D8A-87BD-30B759FA33DD}|
|連絡先|{56784854-C6CB-462b-8169-88E350ACB882}|
|ダウンロード|{374DE290-123F-4565-9164-39C4925E467B}|
|リンク|{BFB9D5E0-C6A9-404C-B2B2-AE6DB6AF4968}|
|検索|{7D1D3A04-DEBB-4115-95CF-2F29DA2920DA}|
|保存したゲーム|{4C5C32FF-BB9D-43B0-B5B4-2D72E54EAAA4}|

## <a name="more-information"></a>詳細情報

- [フォルダー リダイレクト、オフライン ファイル、および移動ユーザー プロファイルの概要](folder-redirection-rup-overview.md)
- [フォルダー リダイレクト オフライン ファイルを展開します。](deploy-folder-redirection.md)