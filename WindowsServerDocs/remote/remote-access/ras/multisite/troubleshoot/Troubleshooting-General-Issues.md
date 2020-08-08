---
title: 一般的な問題のトラブルシューティング
description: このトピックは、「Windows Server 2016 のマルチサイト展開に複数のリモートアクセスサーバーを展開する」の一部です。
manager: brianlic
ms.topic: article
ms.assetid: 354ae5e3-bae1-44f9-afd7-7eaba70f2346
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 911d12088acc5071e18e7e24000364d9fe539250
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87958480"
---
# <a name="troubleshooting-general-issues"></a>一般的な問題のトラブルシューティング

>適用先:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、リモートアクセスに関連する一般的な問題のトラブルシューティングについて説明します。

## <a name="gpo-retrieval-error"></a>GPO の取得エラー
**エラーを受信しました**。 DirectAccess サーバーの GPO 設定を取得できません。 GPO の編集アクセス許可があることを確認します。

このエラーを受信した後、リモートアクセス管理コンソールは応答しません。

**原因**

DirectAccess は、展開内のいずれかのエントリポイントの GPO にアクセスできないため、構成の読み込みに失敗します。

**ソリューション**

展開内の各エントリポイントがドメインコントローラー上に対応する GPO を持っていることを確認し、ログオンしたユーザーに、リモートアクセスの展開で構成されているすべての Gpo に対する読み取りおよび書き込みのアクセス許可があることを確認します。

回避策として、リモートアクセス管理コンソールを使用する代わりに、構成コマンドレットを使用します。たとえば、とを使用し `Get-RemoteAccess` `Get-DAEntryPoint` ます。

> [!NOTE]
> このシナリオは、現在のエントリポイントのサーバー GPO が使用できない場合には発生しません。

コマンドレットを使用して、 `Get-DAEntryPointDC` サーバー gpo を格納しているすべてのドメインコントローラーを一覧表示し、 `Get-DAMultiSite` `Get-RemoteAccess` 展開内のサーバー gpo の完全な一覧を取得するためにと共に使用できます。 例:

```
$ServerGpos = Get-DAEntryPointDC | ForEach-Object {
   @{
       GpoName = (Get-RemoteAccess -EntryPoint $_.EntryPointName).ServerGpoName;
        DC = $_.DomainControllerName }
}
$ServerGpos | ForEach-Object { $GpoName = $_['GpoName'] ; $DC = $_['DC'] ; Write-Host "Server GPO '$GpoName' on DC '$DC'" }
```

## <a name="windows-7-to-windows-8-or-10-client-upgrade"></a>Windows 7 から Windows 8 または10クライアントへのアップグレード
**症状**。 Windows 7 クライアントがマルチサイト展開で Windows 10 または Windows 8 にアップグレードされた後、DirectAccess 接続は [ネットワーク] の一覧に表示されません。

**原因**

マルチサイト展開の Windows 7 Gpo には、Windows 8 Network Connectivity Assistant の構成が含まれていません。

 Windows 7 クライアントは、DirectAccess 接続アシスタントを使用して、Windows 7 クライアント Gpo で個別の手動構成を必要とする DirectAccess 接続の状態を監視する必要があります。 Windows 7 クライアントを Windows 10 または Windows 8 にアップグレードしても、Windows 7 クライアントの GPO が適用されている場合、Network Connectivity Assistant は機能しません。

**ソリューション**

DirectAccess 接続アシスタントの設定が Windows 7 Gpo で構成されている場合は、次の PowerShell コマンドレットを使用して Windows 7 Gpo を変更することで、クライアントコンピューターをアップグレードする前にこの問題を解決できます。

```
Set-GPRegistryValue -Name <Windows7GpoName> -Domain <DomainName> -Key "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\NetworkConnectivityAssistant" -ValueName "TemporaryValue" -Type Dword -Value 1
Remove-GPRegistryValue -Name <Windows7GpoName> -Domain <DomainName> -Key "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\NetworkConnectivityAssistant"
```

クライアントが既にアップグレードされている場合、または DCA が構成されていない場合は、クライアントコンピューターを Windows 10 または Windows 8 セキュリティグループに移動します。

## <a name="general-cmdlet-errors"></a>コマンドレットの一般的なエラー

-   **問題 1**

    **エラーを受信しました**。 <server_name または entry_point_name> のドメインコントローラー <domain_controller> に到達できません。

    **原因**

    マルチサイト展開で構成の一貫性を維持するためには、各 GPO が単一のドメイン コントローラーによって管理されるようにすることが重要です。 エントリポイントのサーバー GPO を管理するドメインコントローラーを使用できない場合、リモートアクセスの構成設定を読み取りまたは変更することはできません。

    **ソリューション**

    「2.4」で説明されている「サーバーの Gpo を管理するドメインコントローラーを変更するには」の手順に従い[ます。Gpo を構成する](assetId:///b1960686-a81e-4f48-83f1-cc4ea484df43#ConfigGPOs)。

-   **問題 2**

    **エラーを受信しました**。 ドメイン <domain_name> のプライマリドメインコントローラに到達できません。

    **原因**

    マルチサイト展開で構成の一貫性を維持するためには、各 GPO が単一のドメイン コントローラーによって管理されるようにすることが重要です。 クライアント GPO は、プライマリ ドメイン コントローラーで管理されます。 プライマリ ドメイン コントローラーを利用できない場合、リモート アクセスの構成設定を読み取ったり変更したりすることはできません。

    **ソリューション**

    「2.4」で説明されている「PDC エミュレーターの役割を転送するには」の手順に従い[ます。Gpo を構成する](assetId:///b1960686-a81e-4f48-83f1-cc4ea484df43#ConfigGPOs)。



