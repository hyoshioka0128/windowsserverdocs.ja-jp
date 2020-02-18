---
title: リダイレクトされた個々のフォルダーのオフライン ファイルを無効にする
description: フォルダー リダイレクトを使用してネットワーク共有にリダイレクトされた個々のフォルダーでオフライン ファイル キャッシュを無効にする方法。
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: c2614c0180b32a0215454f2d725d6a962986ef1f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71394396"
---
# <a name="disable-offline-files-on-individual-redirected-folders"></a>リダイレクトされた個々のフォルダーのオフライン ファイルを無効にする

>適用先:Windows 10、Windows 8、Windows 8.1、Windows Server 2019、Windows Server 2016、Windows Server 2012、Windows Server 2012 R2、Windows (半期チャネル)

このトピックでは、フォルダーリダイレクトを使用してネットワーク共有にリダイレクトされた個々のフォルダーでオフライン ファイル キャッシュを無効にする方法について説明します。 これにより、ローカル キャッシュに保存しないフォルダーを指定できるようになり、オフライン ファイル キャッシュのサイズを縮小し、オフライン ファイルの同期に必要な時間を短縮できます。

>[!NOTE]
>このトピックでは、説明した手順の一部を自動化するのに使用できる Windows PowerShell コマンドレットのサンプルを示します。 詳細については、「[Windows PowerShell の基礎](https://docs.microsoft.com/powershell/scripting/getting-started/fundamental/windows-powershell-basics?view=powershell-6)」を参照してください。

## <a name="prerequisites"></a>前提条件

リダイレクトされた特定のフォルダーのオフライン ファイル キャッシュを無効にするには、環境が次の前提条件を満たしている必要があります。

- Active Directory Domain Services (AD DS) ドメインが存在し、クライアント コンピューターがこのドメインに参加していること。 フォレストおよびドメインの機能レベルの要件やスキーマの要件はありません。
- Windows 10、Windows 8.1、Windows 8、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012 または Windows (半期チャネル) を実行しているクライアント コンピューター。
- グループ ポリシー管理がインストールされたコンピューター。

## <a name="disabling-offline-files-on-individual-redirected-folders"></a>リダイレクトされた個々のフォルダーのオフライン ファイルを無効にする

リダイレクトされた個々のフォルダーのオフライン ファイル キャッシュを無効にするには、グループ ポリシーを使用して、該当するグループ ポリシーオブジェクト (GPO) の **[リダイレクトされた特定のフォルダーを自動的にオフライン利用できるようにしない]** ポリシー設定を有効にします。 このポリシー設定を **[無効]** または **[未構成]** に構成すると、リダイレクトされたすべてのフォルダーがオフラインで使用できるようになります。

>[!NOTE]
>Domain Administrators、Enterprise Administrators、および Group Policy Creator Owners の各グループのメンバーのみが GPO を作成できます。

### <a name="to-disable-offline-files-on-specific-redirected-folders"></a>リダイレクトされた個々のフォルダーのオフライン ファイルを無効にするには

1. **[グループ ポリシーの管理]** を開きます。
2. 必要に応じて、リダイレクトされたフォルダーをオフライン利用できないユーザーを指定する新しい GPO を作成するには、該当するドメインまたは組織単位 (OU) を右クリックし、 **[このドメインに GPO を作成し、このコンテナーにリンクする]** をクリックします。
3. コンソール ツリーで、フォルダー リダイレクト設定を構成する GPO を右クリックし、 **[編集]** を選択します。 グループ ポリシー管理エディターが表示されます。
4. コンソール ツリーの **[ユーザーの構成]** で、 **[ポリシー]** 、 **[管理用テンプレート]** 、 **[システム]** 、 **[フォルダー リダイレクト]** の順に展開します。
5. **[リダイレクトされた特定のフォルダーを自動的にオフライン利用できるようにしない]** を右クリックし、 **[編集]** を選択します。 **[リダイレクトされた特定のフォルダーを自動的にオフライン利用できるようにしない]** ウィンドウが表示されます。
6. **[有効]** をクリックします。 **[オプション]** ペインで、該当するチェック ボックスをオンにして、オフラインで使用できないようにするフォルダーを選択します。 **[OK]** を選択します。

### <a name="windows-powershell-equivalent-commands"></a>Windows PowerShell の同等のコマンド

次の Windows PowerShell コマンドレットは、「[リダイレクトされた個々のフォルダーのオフライン ファイルを無効にする](#disabling-offline-files-on-individual-redirected-folders)」で説明されている手順と同じ機能を実行します。 各コマンドレットを単一行に入力します。ただし、ここでは、書式上の制約があるために、複数行に改行されて表示される場合があります。

この例では、*contoso.com* ドメインの *MyOu* 組織単位に *Offline Files Settings* という名前の新しい GPO を作成します (LDAP 識別名は "ou=MyOU,dc=contoso,dc=com")。 その後、ビデオのリダイレクト フォルダーのオフライン ファイルを無効にします。

```PowerShell
New-GPO -Name "Offline Files Settings" | New-Gplink -Target "ou=MyOu,dc=contoso,dc=com" -LinkEnabled Yes

Set-GPRegistryValue –Name "Offline Files Settings" –Key
"HKCU\Software\Policies\Microsoft\Windows\NetCache\{18989B1D-99B5-455B-841C-AB7C74E4DDFC}" -ValueName DisableFRAdminPinByFolder –Type DWORD –Value 1
```

リダイレクトされる各フォルダーに使用するレジストリ キー名 (フォルダー GUID) の一覧については、次の表を参照してください。

|リダイレクトされるフォルダー|レジストリ キー名 (フォルダー GUID)|
|---|---|
|AppData(Roaming)|{3EB685DB-65F9-4CF6-A03A-E3EF65729F3D}|
|デスクトップ|{B4BFCC3A-DB2C-424C-B029-7FE99A87C641}|
|スタート メニュー|{625B53C3-AB48-4EC1-BA1F-A1EF4146FC19}|
|ドキュメント|{FDD39AD0-238F-46AF-ADB4-6C85480369C7}|
|ピクチャ|{33E28130-4E1E-4676-835A-98395C3BC3BB}|
|ミュージック|{4BD8D571-6D19-48D3-BE97-422220080E43}|
|ビデオ|{18989B1D-99B5-455B-841C-AB7C74E4DDFC}|
|お気に入り|{1777F761-68AD-4D8A-87BD-30B759FA33DD}|
|連絡先|{56784854-C6CB-462b-8169-88E350ACB882}|
|ダウンロード|{374DE290-123F-4565-9164-39C4925E467B}|
|リンク|{BFB9D5E0-C6A9-404C-B2B2-AE6DB6AF4968}|
|検索|{7D1D3A04-DEBB-4115-95CF-2F29DA2920DA}|
|保存したゲーム|{4C5C32FF-BB9D-43B0-B5B4-2D72E54EAAA4}|

## <a name="more-information"></a>説明を見る

- [フォルダー リダイレクト、オフライン ファイル、移動ユーザー プロファイルの概要](folder-redirection-rup-overview.md)
- [オフライン ファイルを使用してフォルダー リダイレクトを展開する](deploy-folder-redirection.md)