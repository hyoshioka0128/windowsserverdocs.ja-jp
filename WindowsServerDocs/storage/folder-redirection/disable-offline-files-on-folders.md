---
title: 個々 のリダイレクトされたフォルダーでオフライン ファイルを無効にします。
description: フォルダー リダイレクトを使用して、ネットワーク共有にリダイレクトされている個々 のフォルダーでオフライン ファイルのキャッシュを無効にする方法について説明します。
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: adc93906cb7ff958fc1db7b00abdc557623e764e
ms.sourcegitcommit: 9ed4c9fe04ebf3ef488170503c9a354c992b6fde
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/03/2018
ms.locfileid: "4339310"
---
# 個々 のリダイレクトされたフォルダーでオフライン ファイルを無効にします。

>適用対象: Windows 10、Windows 8、Windows 8.1、Windows Server 2012、Windows Server 2012 R2、Windows Server 2016

このトピックでは、フォルダー リダイレクトを使用して、ネットワーク共有にリダイレクトされている個々 のフォルダーでオフライン ファイルのキャッシュを無効にする方法について説明します。 これにより、ローカルにキャッシュから除外するフォルダーを指定する機能、オフライン ファイルのキャッシュを減らすことサイズと時間必要なオフライン ファイルを同期します。

>[!NOTE]
>このトピックでは、上記の手順の一部を自動化するために使用できるサンプル Windows PowerShell コマンドレットを使用します。 詳細については、 [Windows PowerShell の基本](https://docs.microsoft.com/powershell/scripting/getting-started/fundamental/windows-powershell-basics?view=powershell-6)を参照してください。

## 前提条件

オフライン ファイルは、特定のリダイレクトされたフォルダーのキャッシュを無効にするには、環境が次の前提条件を満たす必要があります。

- ドメインに参加しているクライアント コンピューターとの Active Directory ドメイン サービス (AD DS) ドメイン。 フォレストまたはドメイン機能レベルの要件やスキーマの要件はありません。
- Windows 10、Windows 8.1、Windows 8、Windows Server 2016、Windows Server 2012 R2、または Windows Server 2012 を実行しているクライアント コンピューター。
- グループ ポリシーの管理がインストールされているコンピューター。

## 個々 のリダイレクトされたフォルダーでオフライン ファイルを無効にします。

オフライン ファイルは、特定のリダイレクトされたフォルダーのキャッシュを無効にするのにには、**利用可能な特定のリダイレクトされたフォルダーをオフラインように自動的に**このポリシー設定の適切なグループ ポリシー オブジェクト (GPO) を有効にするのにグループ ポリシーを使用します。 このポリシー設定を**無効**または**未構成**によりすべてのリダイレクトされたフォルダーでオフラインできます。

>[!NOTE]
>ドメイン管理者、エンタープライズ管理者、およびグループ ポリシーの作成者所有者グループのメンバーは、Gpo を作成できます。

### 特定のリダイレクトされたフォルダーでオフライン ファイルを無効にするには

1. **グループ ポリシーの管理**を開きます。
2. 必要に応じて指定できるユーザーにオフライン使用から除外するフォルダーをリダイレクトする必要がありますが、新しい GPO を作成するには、適切なドメインまたは組織単位 (OU) を右クリックし、**このドメインに GPO を作成して選びリンクします。**.
3. コンソール ツリーで、フォルダー リダイレクトの設定を構成し、**編集**を選択する GPO を右クリックします。 グループ ポリシー管理エディターに表示されます。
4. コンソール ツリーで、[**ユーザーの構成****ポリシー**を展開、**管理用**テンプレート**システム**を展開し、**フォルダー リダイレクト**を展開します。
5. **自動的にオフラインで利用可能な特定のリダイレクトされたフォルダー**を右クリックし、**編集**します。 **利用可能な特定のリダイレクトされたフォルダーをオフラインように自動的に**ウィンドウが表示されます。
6. **[有効]** を選びます。 **オプション**のウィンドウでない可能になります。 オフライン該当するチェック ボックスを選択しているフォルダーを選択します。 **[OK]** を選択します。

### 同等の Windows PowerShell コマンド

次の Windows PowerShell コマンドレットまたはコマンドレットは、[無効にすると、オフライン ファイル個々 のリダイレクトされたフォルダー](#disabling-offline-files-on-individual-redirected-folders)で説明する手順と同じ機能を実行します。 表示される場合でも可能性がありますワード ラップ複数行を以下に間での制約を書式設定のために、1 つの行で各コマンドレットを入力します。

この例は、 *contoso.com*ドメインで*MyOu*組織単位に*オフライン ファイルの設定*をという名前の新しい GPO を作成します (LDAP 識別名が"ou = MyOU、dc = contoso, dc = com")。 ビデオのリダイレクトされたフォルダーのオフライン ファイル、無効にします。

```PowerShell
New-GPO -Name "Offline Files Settings" | New-Gplink -Target "ou=MyOu,dc=contoso,dc=com" -LinkEnabled Yes

Set-GPRegistryValue –Name "Offline Files Settings" –Key
"HKCU\Software\Policies\Microsoft\Windows\NetCache\{18989B1D-99B5-455B-841C-AB7C74E4DDFC}" -ValueName DisableFRAdminPinByFolder –Type DWORD –Value 1
```

各リダイレクトされたフォルダーに使用するレジストリ キー名 (フォルダーの Guid) の一覧については、次の表を参照してください。

|リダイレクトされたフォルダー|レジストリ キー名 (フォルダーの GUID)|
|---|---|
|AppData(Roaming)|{3EB685DB-65F9-4CF6-A03A-E3EF65729F3D}|
|Desktop|{B4BFCC3A-DB2C-424C-B029-7FE99A87C641}|
|[スタート] メニュー|{625B53C3-AB48-4EC1-BA1F-A1EF4146FC19}|
|ドキュメント|{FDD39AD0-238F-46AF-ADB4-6C85480369C7}|
|ピクチャ|{33E28130-4E1E-4676-835A-98395C3BC3BB}|
|ミュージック|{4BD8D571-6D19-48D3-BE97-422220080E43}|
|ビデオ|{18989B1D-99B5-455B-841C-AB7C74E4DDFC}|
|お気に入り|{1777F761-68AD-4D8A-87BD-30B759FA33DD}|
|連絡先|{56784854-C6CB-462b-8169-88E350ACB882}|
|ダウンロード|{374DE290-123F-4565-9164-39C4925E467B}|
|Links|{BFB9D5E0-C6A9-404C-B2B2-AE6DB6AF4968}|
|検索|{7D1D3A04-DEBB-4115-95CF-2F29DA2920DA}|
|保存したゲーム|{4C5C32FF-BB9D-43B0-B5B4-2D72E54EAAA4}|

## 詳細

- [フォルダー リダイレクト、オフライン ファイル、および移動ユーザー プロファイルの概要](folder-redirection-rup-overview.md)
- [フォルダー リダイレクトとオフライン ファイルを展開します。](deploy-folder-redirection.md)