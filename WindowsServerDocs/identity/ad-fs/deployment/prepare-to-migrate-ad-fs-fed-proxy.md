---
title: AD FS 2.0 フェデレーション サーバー プロキシの移行準備
description: Windows Server 2012 に AD FS サーバー プロキシの移行の準備について説明します。
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f207993580e6fd06c9ff185e58e5b7e81af60252
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847833"
---
# <a name="prepare-to-migrate-the-ad-fs-20-federation-server-proxy"></a>AD FS 2.0 フェデレーション サーバー プロキシの移行準備

Windows Server 2012 への AD FS 2.0 フェデレーション サーバー プロキシの移行の準備するには、エクスポートし、このサーバー プロキシから AD FS 構成データをバックアップする必要があります。  このトピックの手順は、1 プロキシ フェデレーション サーバーまたは複数プロキシ フェデレーション サーバーのシナリオに適用されます。  
  
 AD FS の構成データをエクスポートするには、次の作業を実行します。  
  
-   [ステップ 1: プロキシ サービス設定をエクスポートします。](#step-1-export-proxy-service-settings)  
  
-   [手順 2:Web ページのカスタマイズをバックアップします。](#step-2-back-up-webpage-customizations)  
  
##  <a name="step-1-export-proxy-service-settings"></a>手順 1:プロキシ サービス設定をエクスポートする  
 フェデレーション サーバー プロキシ サービスの設定をエクスポートするには、次の手順を実行します。  
  
### <a name="to-export-proxy-service-settings"></a>プロキシ サービスの設定をエクスポートするには  
  
1.  Secure Sockets Layer (SSL) 証明書とその秘密キーを .pfx ファイルにエクスポートします。 詳細については、[サーバー認証証明書の秘密キー部分のエクスポートに関するページ](export-the-private-key-portion-of-a-server-authentication-certificate.md)を参照してください。  
  
> [!NOTE]
>  オペレーティング システムをアップグレードしても、この証明書は保持されます。したがって、この手順は省略可能です。  
  
2.  AD FS 2.0 フェデレーション プロキシのプロパティをファイルにエクスポートします。 これは、Windows PowerShell を使って行うことができます。  
  
Windows PowerShell を開き、コマンド `PSH:>add-pssnapin “Microsoft.adfs.powershell”`を実行して、AD FS コマンドレットを Windows PowerShell セッションに追加します。 次に、コマンド `PSH:> Get-ADFSProxyProperties | out-file “.\proxyproperties.txt”`を実行して、フェデレーション プロキシのプロパティをファイルにエクスポートします。  
  
3.  AD FS フェデレーション サーバーの管理者であるアカウント、または AD FS フェデレーション サービスが実行しているサービス アカウントの資格情報を把握していることを確認します。  この情報は、プロキシ信頼のセットアップに必要です。  
  
 このステップを完了すると、AD FS フェデレーション サーバー プロキシの構成に必要な次の情報が収集されています。  
  
-   AD FS フェデレーション サービス名  
  
-   プロキシ信頼のセットアップに必要なドメイン アカウント名  
  
-   HTTP プロキシのアドレスとポート (AD FS フェデレーション サーバー プロキシと AD FS フェデレーション サーバー間に HTTP プロキシがある場合)  
  
##  <a name="step-2-back-up-webpage-customizations"></a>手順 2:Web ページのカスタマイズをバックアップする  
 Web ページのカスタマイズをバックアップするには、IIS で仮想パス **“/adfs/ls”** にマップされたディレクトリから AD FS プロキシ Web ページと **web.config** ファイルをコピーします。  既定では、そのファイルは **%systemdrive%\inetpub\adfs\ls** ディレクトリにあります。  
  
## <a name="next-steps"></a>次の手順
 [AD FS 2.0 フェデレーション サーバーの移行を準備します。](prepare-to-migrate-ad-fs-fed-server.md)   
 [AD FS 2.0 フェデレーション サーバー プロキシの移行を準備します。](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [AD FS 2.0 フェデレーション サーバーを移行します。](migrate-the-ad-fs-fed-server.md)   
 [AD FS 2.0 フェデレーション サーバー プロキシを移行します。](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [AD FS 1.1 Web エージェントを移行します。](migrate-the-ad-fs-web-agent.md)