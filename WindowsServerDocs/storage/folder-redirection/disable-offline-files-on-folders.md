---
title: リダイレクトされた個々のフォルダーのオフラインファイルを無効にする
description: フォルダーリダイレクトを使用してネットワーク共有にリダイレクトされる個々のフォルダーでオフラインファイルキャッシュを無効にする方法。
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: c2614c0180b32a0215454f2d725d6a962986ef1f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71394396"
---
# <a name="disable-offline-files-on-individual-redirected-folders"></a>リダイレクトされた個々のフォルダーのオフラインファイルを無効にする

>適用対象:Windows 10、windows 8、Windows 8.1、Windows Server 2019、Windows Server 2016、Windows Server 2012、Windows Server 2012 R2、Windows (半期チャネル)

このトピックでは、フォルダーリダイレクトを使用してネットワーク共有にリダイレクトされる個々のフォルダーでオフラインファイルキャッシュを無効にする方法について説明します。 これにより、ローカルでキャッシュから除外するフォルダーを指定し、オフラインファイルの同期に必要なオフラインファイルキャッシュサイズと時間を短縮できます。

>[!NOTE]
>このトピックでは、サンプル Windows PowerShell コマンドレットを紹介します。ここで説明する手順の一部はこのコマンドレットで自動化できます。 詳細については、「 [Windows PowerShell の基礎](https://docs.microsoft.com/powershell/scripting/getting-started/fundamental/windows-powershell-basics?view=powershell-6)」を参照してください。

## <a name="prerequisites"></a>前提条件

リダイレクトされた特定のフォルダーのオフラインファイルキャッシュを無効にするには、環境が次の前提条件を満たしている必要があります。

- クライアントコンピューターがドメインに参加している Active Directory Domain Services (AD DS) ドメイン。 フォレストまたはドメインの機能レベルの要件やスキーマの要件はありません。
- Windows 10、Windows 8.1、Windows 8、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012 または Windows (半期チャネル) を実行しているクライアントコンピューター。
- グループポリシー管理がインストールされているコンピューター。

## <a name="disabling-offline-files-on-individual-redirected-folders"></a>リダイレクトされた個々のフォルダーのオフラインファイルを無効にする

リダイレクトされた特定のフォルダーのオフラインファイルキャッシュを無効にするには、グループポリシーを使用して、適切なグループポリシーオブジェクト (GPO) に対して [**特定のリダイレクトフォルダーを自動的にオフライン利用できる**ようにする] ポリシー設定を有効にします。 このポリシー設定を**無効**または**未構成**に構成すると、リダイレクトされたすべてのフォルダーがオフラインで使用できるようになります。

>[!NOTE]
>ドメイン管理者、エンタープライズ管理者、およびグループポリシー creator owners グループのメンバーのみが Gpo を作成できます。

### <a name="to-disable-offline-files-on-specific-redirected-folders"></a>リダイレクトされた特定のフォルダーでオフラインファイルを無効にするには

1. **グループポリシー管理**を開きます。
2. 必要に応じて、リダイレクトされたフォルダーをオフラインで利用できないようにするユーザーを指定する新しい GPO を作成するには、適切なドメインまたは組織単位 (OU) を右クリックし、[**このドメインに GPO を作成し、このコンテナーにリンクする] を選択します。** .
3. コンソールツリーで、フォルダーリダイレクト設定を構成する GPO を右クリックし、 **[編集]** を選択します。 グループポリシー管理エディターが表示されます。
4. コンソールツリーの ユーザーの **[構成]** で、 **[ポリシー]** 、 **[管理用テンプレート]** の順に展開し、 **[システム]** 、 **[フォルダーリダイレクト]** の順に展開します。
5. **[リダイレクトされた特定のフォルダーを自動的にオフライン利用できるように]** する を右クリックし、 **[編集]** を選択します。 [リダイレクトされた**特定のフォルダーを自動的にオフラインに**する] ウィンドウが表示されます。
6. **[有効]** を選びます。 **[オプション]** ウィンドウで、適切なチェックボックスをオンにして、オフラインで使用できないようにするフォルダーを選択します。 **[OK]** を選択します。

### <a name="windows-powershell-equivalent-commands"></a>Windows PowerShell と同等のコマンド

次の Windows PowerShell コマンドレットまたはコマンドレットは、「[個々のリダイレクトフォルダーでのオフラインファイルの無効化](#disabling-offline-files-on-individual-redirected-folders)」で説明されている手順と同じ機能を実行します。 ここでは書式上の制約のために、折り返されて複数の行にわたって表示される場合もありますが、各コマンドレットは 1 行に入力します。

この例では、 *contoso.com*ドメインの*myou*組織単位に*オフラインファイル Settings*という名前の新しい GPO を作成します (LDAP 識別名は "ou = myou, dc = contoso, dc = com")。 その後、ビデオリダイレクトフォルダーのオフラインファイルを無効にします。

```PowerShell
New-GPO -Name "Offline Files Settings" | New-Gplink -Target "ou=MyOu,dc=contoso,dc=com" -LinkEnabled Yes

Set-GPRegistryValue –Name "Offline Files Settings" –Key
"HKCU\Software\Policies\Microsoft\Windows\NetCache\{18989B1D-99B5-455B-841C-AB7C74E4DDFC}" -ValueName DisableFRAdminPinByFolder –Type DWORD –Value 1
```

リダイレクトされる各フォルダーに使用するレジストリキー名 (フォルダー Guid) の一覧については、次の表を参照してください。

|リダイレクトされたフォルダー|レジストリキー名 (フォルダー GUID)|
|---|---|
|AppData(Roaming)|{3EB685DB65F947 CF6-A03E3EF65729F3D}|
|Desktop|B4BFCC3A-DB2C-424C-B029-7FE99A87C641|
|スタート メニュー|{625B53C3-AB48-4EC1-BA1F-A1EF4146FC19}|
|Documents|{FDD39AD0-238F-46AF-ADB4-6C85480369C7}|
|画像|{33E2813047 E1E4-676835A9898395C3BC3BB}|
|音楽|{4BD8D571-6D19-48D3-BE97-422220080E43}|
|ビデオ|{18989B1D-99B5-455B-841C-AB7C74E4DDFC}|
|Favorites|{1777F761-68AD-4D8A-87BD-30B759FA33DD}|
|連絡先|{56784854-C6CB-462b-8169-88 E350ACB88 2}|
|ダウンロード|{374DE290-123F4565-916439C4925E467B}|
|リンク|{BFB9D5E0-C6A9-404C-B2B2-AE6DB6AF4968}|
|検索|{7D1D3A04(DEBB47 115) 00 分の3分の1|
|保存したゲーム|{4C5C32FF-BB9D-43B0-B5B4-2D72E54EAAA4}|

## <a name="more-information"></a>詳細情報

- [フォルダーリダイレクト、オフラインファイル、移動ユーザープロファイルの概要](folder-redirection-rup-overview.md)
- [オフラインファイルでフォルダーリダイレクトを展開する](deploy-folder-redirection.md)