---
title: 一般的な問題のトラブルシューティング
description: このトピックは、ガイドの一部複数リモート アクセス サーバーの展開で Windows Server 2016 の Multisite 展開します。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 354ae5e3-bae1-44f9-afd7-7eaba70f2346
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 87614ac3b83eaacefb4ac5f9fddef238ed500953
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67282551"
---
# <a name="troubleshooting-general-issues"></a>一般的な問題のトラブルシューティング

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

このトピックでには、リモート アクセスに関連する一般的な問題のトラブルシューティング情報が含まれています。  
  
## <a name="gpo-retrieval-error"></a>GPO の取得エラー  
**表示されるエラー**します。 DirectAccess サーバー GPO の設定を取得することはできません。 GPO の編集アクセス許可があることを確認します。  
  
このエラーを受信した後、リモート アクセス管理コンソールが応答しません。  
  
**原因**  
  
DirectAccess 展開でエントリ ポイントの 1 つの GPO にアクセスできないし、その結果、構成の読み込みに失敗します。  
  
**ソリューション**  
  
展開内の各エントリ ポイントが、ドメイン コント ローラー上の対応する GPO を持っているかどうかを確認し、ログオン ユーザーに読み取りし、書き込みのアクセス許可、リモート アクセス展開で構成されているすべての Gpo ことを確認します。  
  
この問題を回避するには、リモート アクセス管理コンソールを使用する代わりに構成コマンドレットを使用して、たとえばを使用して`Get-RemoteAccess`と`Get-DAEntryPoint`します。  
  
> [!NOTE]  
> このシナリオでは、現在のエントリ ポイントのサーバーの GPO を利用できない場合は発生しません。  
  
使用することができます、`Get-DAEntryPointDC`サーバー Gpo を保存するすべてのドメイン コント ローラーの一覧を表示するコマンドレットと`Get-DAMultiSite`と組み合わせて`Get-RemoteAccess`展開内のサーバー Gpo の完全な一覧を取得します。 次に、例を示します。  
  
```  
$ServerGpos = Get-DAEntryPointDC | ForEach-Object {   
   @{   
       GpoName = (Get-RemoteAccess -EntryPoint $_.EntryPointName).ServerGpoName;   
        DC = $_.DomainControllerName }   
}  
$ServerGpos | ForEach-Object { $GpoName = $_['GpoName'] ; $DC = $_['DC'] ; Write-Host "Server GPO '$GpoName' on DC '$DC'" }  
```  
  
## <a name="windows-7-to-windows-8-or-10-client-upgrade"></a>Windows 8、Windows 7 または 10 クライアントのアップグレード  
**現象**します。 Windows 7 クライアントのマルチサイト展開で Windows 10 または Windows 8 にアップグレードした後は、DirectAccess 接続は、ネットワークの一覧に表示されません。  
  
**原因**  
  
マルチサイト展開では、Windows 7 の Gpo では、Windows 8 Network Connectivity Assistant の構成は含まれません。  
  
 Windows 7 クライアントは、Windows 7 クライアント Gpo で個別の手動構成を必要とする DirectAccess 接続の状態を監視するのに DirectAccess Connectivity Assistant を使用する必要があります。 Windows 7 クライアントをアップグレードするには Windows 10 または Windows 8 に、Network Connectivity Assistant は機能しません、Windows 7 クライアント GPO がまだ適用されている場合。  
  
**ソリューション**  
  
DirectAccess Connectivity Assistant の設定が構成され、Windows 7 の Gpo の場合は、次の PowerShell コマンドレットを使用して Windows 7 の Gpo を変更することにより、クライアント コンピューターをアップグレードする前にこの問題を解決できます。  
  
```  
Set-GPRegistryValue -Name <Windows7GpoName> -Domain <DomainName> -Key "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\NetworkConnectivityAssistant" -ValueName "TemporaryValue" -Type Dword -Value 1  
Remove-GPRegistryValue -Name <Windows7GpoName> -Domain <DomainName> -Key "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\NetworkConnectivityAssistant"  
```  
  
場合は、クライアントがアップグレードされているか、DCA が構成されていない、クライアント コンピューターを Windows 10 または Windows 8 のセキュリティ グループに移動します。  
  
## <a name="general-cmdlet-errors"></a>コマンドレットの一般的なエラー  
  
-   **問題 1**  
  
    **表示されるエラー**します。 < サーバー名または名 > の < 表示される > のドメイン コント ローラーに到達できません。  
  
    **原因**  
  
    マルチサイト展開で構成の一貫性を維持するためには、各 GPO が単一のドメイン コントローラーによって管理されるようにすることが重要です。 エントリ ポイントのサーバーの GPO を管理するドメイン コント ローラーが利用できない場合は、リモート アクセスの構成設定の読み取りまたは変更できません。  
  
    **ソリューション**  
  
    サーバーの Gpo を管理するドメイン コント ローラーの変更"するには」で説明されている手順に従って[2.4 します。Gpo を構成する](assetId:///b1960686-a81e-4f48-83f1-cc4ea484df43#ConfigGPOs)します。  
  
-   **問題 2**  
  
    **表示されるエラー**します。 < Domain_name > ドメインでプライマリ ドメイン コント ローラーに到達できません。  
  
    **原因**  
  
    マルチサイト展開で構成の一貫性を維持するためには、各 GPO が単一のドメイン コントローラーによって管理されるようにすることが重要です。 クライアント GPO は、プライマリ ドメイン コントローラーで管理されます。 プライマリ ドメイン コントローラーを利用できない場合、リモート アクセスの構成設定を読み取ったり変更したりすることはできません。  
  
    **ソリューション**  
  
    PDC エミュレーターの役割を転送するには"するには」で説明されている手順に従って[2.4 します。Gpo を構成する](assetId:///b1960686-a81e-4f48-83f1-cc4ea484df43#ConfigGPOs)します。  
  


