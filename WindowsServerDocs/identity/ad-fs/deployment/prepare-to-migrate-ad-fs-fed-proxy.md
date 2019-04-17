---
title: "AD FS 2.0 フェデレーション サーバー プロキシの移行を準備します。"
description: "Windows Server 2012 への AD FS サーバーのプロキシの移行の準備について説明します。"
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f207993580e6fd06c9ff185e58e5b7e81af60252
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="prepare-to-migrate-the-ad-fs-20-federation-server-proxy"></a>AD FS 2.0 フェデレーション サーバー プロキシの移行を準備します。

Windows Server 2012 への AD FS 2.0 フェデレーション サーバー プロキシの移行の準備、エクスポートして、このサーバー プロキシから AD FS 構成データをバックアップする必要があります。  このトピックの手順は、シナリオ 1 プロキシ フェデレーション サーバーまたは複数プロキシ フェデレーション サーバーに適用されます。  
  
 AD FS 構成データをエクスポートするには、次のタスクを実行します。  
  
-   [手順 1: プロキシ サービス設定のエクスポート](#step-1-export-proxy-service-settings)  
  
-   [手順 2: Web ページのカスタマイズをバックアップします。](#step-2-back-up-webpage-customizations)  
  
##  <a name="step-1-export-proxy-service-settings"></a>手順 1: プロキシ サービス設定のエクスポート  
 フェデレーション サーバー プロキシ サービスの設定をエクスポートするには、次の手順を実行します。  
  
### <a name="to-export-proxy-service-settings"></a>プロキシ サービス設定をエクスポートするには  
  
1.  Secure Sockets Layer (SSL) 証明書とその秘密キーを .pfx ファイルにエクスポートします。 詳細については、次を参照してください。[サーバー認証証明書の秘密キー部分のエクスポート](export-the-private-key-portion-of-a-server-authentication-certificate.md)します。  
  
> [!NOTE]
>  この手順は、オペレーティング システムのアップグレード中にこの証明書は保持省略可能です。  
  
2.  AD FS 2.0 フェデレーション プロキシのプロパティをファイルにエクスポートします。 Windows PowerShell を使用しているを行うことができます。  
  
Windows PowerShell を開き、AD FS のコマンドレットを Windows PowerShell セッションに追加するには、次のコマンドを実行します。`PSH:>add-pssnapin “Microsoft.adfs.powershell”`します。 フェデレーション プロキシのプロパティをファイルにエクスポートするには、次のコマンドを実行し、:`PSH:> Get-ADFSProxyProperties | out-file “.\proxyproperties.txt”`します。  
  
3.  AD FS フェデレーション サーバーの管理者であるアカウントまたは AD FS フェデレーション サービスを実行するサービス アカウントの資格情報を知ることを確認します。  この情報は、プロキシ信頼のセットアップに必要です。  
  
 AD FS フェデレーション サーバー プロキシの構成に必要な次の情報を収集するときにこの手順の結果を完了するには。  
  
-   AD FS フェデレーション サービス名  
  
-   プロキシ信頼のセットアップに必要であるドメイン アカウントの名前  
  
-   アドレスとポート (AD FS フェデレーション サーバー プロキシと AD FS フェデレーション サーバーの間で HTTP プロキシがある場合)、HTTP プロキシの  
  
##  <a name="step-2-back-up-webpage-customizations"></a>手順 2: Web ページのカスタマイズをバックアップします。  
 Web ページのカスタマイズをバックアップするには、AD FS プロキシ Web ページをコピーし、**Web.config**仮想パスにマップされているディレクトリからファイル**"/adfs/ls"** IIS でします。  既定では、**%systemdrive%\inetpub\adfs\ls**ディレクトリ。  
  
## <a name="next-steps"></a>次の手順
 [AD FS 2.0 フェデレーション サーバーの移行を準備します。](prepare-to-migrate-ad-fs-fed-server.md)   
 [AD FS 2.0 フェデレーション サーバー プロキシの移行を準備します。](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [AD FS 2.0 フェデレーション サーバーを移行します。](migrate-the-ad-fs-fed-server.md)   
 [AD FS 2.0 フェデレーション サーバー プロキシを移行します。](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [AD FS 1.1 Web エージェントを移行します。](migrate-the-ad-fs-web-agent.md)