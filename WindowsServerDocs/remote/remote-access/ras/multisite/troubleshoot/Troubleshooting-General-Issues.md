---
title: 一般的な問題のトラブルシューティング
description: このトピックは、「Windows Server 2016 のマルチサイト展開に複数のリモートアクセスサーバーを展開する」の一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 354ae5e3-bae1-44f9-afd7-7eaba70f2346
ms.author: pashort
author: shortpatti
ms.openlocfilehash: a2b8d7decad482ca8756aa4d82baa35abf16f5fe
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404449"
---
# <a name="troubleshooting-general-issues"></a>一般的な問題のトラブルシューティング

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、リモートアクセスに関連する一般的な問題のトラブルシューティングについて説明します。  
  
## <a name="gpo-retrieval-error"></a>GPO の取得エラー  
**エラーを受信しました**。 DirectAccess サーバーの GPO 設定を取得できません。 GPO の編集アクセス許可があることを確認します。  
  
このエラーを受信した後、リモートアクセス管理コンソールは応答しません。  
  
**原因**  
  
DirectAccess は、展開内のいずれかのエントリポイントの GPO にアクセスできないため、構成の読み込みに失敗します。  
  
**ソリューション**  
  
展開内の各エントリポイントがドメインコントローラー上に対応する GPO を持っていることを確認し、ログオンしたユーザーに、リモートアクセスの展開で構成されているすべての Gpo に対する読み取りおよび書き込みのアクセス許可があることを確認します。  
  
回避策として、リモートアクセス管理コンソールを使用する代わりに、構成コマンドレットを使用します。たとえば、`Get-RemoteAccess` と `Get-DAEntryPoint`を使用します。  
  
> [!NOTE]  
> このシナリオは、現在のエントリポイントのサーバー GPO が使用できない場合には発生しません。  
  
`Get-DAEntryPointDC` コマンドレットを使用して、サーバー Gpo を格納 `Get-DAMultiSite` しているすべてのドメインコントローラーの一覧を表示し、`Get-RemoteAccess` と組み合わせて展開内のサーバー Gpo の完全な一覧を取得することができます。 次に、例を示します。  
  
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
  
-   **問題1**  
  
    **エラーを受信しました**。 < Server_name または entry_point_name > のドメインコントローラー < domain_controller > に到達できません。  
  
    **原因**  
  
    マルチサイト展開で構成の一貫性を維持するためには、各 GPO が単一のドメイン コントローラーによって管理されるようにすることが重要です。 エントリポイントのサーバー GPO を管理するドメインコントローラーを使用できない場合、リモートアクセスの構成設定を読み取りまたは変更することはできません。  
  
    **ソリューション**  
  
    「2.4」で説明されている「サーバーの Gpo を管理するドメインコントローラーを変更するには」の手順に従い[ます。Gpo を構成する](assetId:///b1960686-a81e-4f48-83f1-cc4ea484df43#ConfigGPOs)。  
  
-   **問題2**  
  
    **エラーを受信しました**。 ドメイン < domain_name > のプライマリドメインコントローラに到達できません。  
  
    **原因**  
  
    マルチサイト展開で構成の一貫性を維持するためには、各 GPO が単一のドメイン コントローラーによって管理されるようにすることが重要です。 クライアント GPO は、プライマリ ドメイン コントローラーで管理されます。 プライマリ ドメイン コントローラーを利用できない場合、リモート アクセスの構成設定を読み取ったり変更したりすることはできません。  
  
    **ソリューション**  
  
    「2.4」で説明されている「PDC エミュレーターの役割を転送するには」の手順に従い[ます。Gpo を構成する](assetId:///b1960686-a81e-4f48-83f1-cc4ea484df43#ConfigGPOs)。  
  


