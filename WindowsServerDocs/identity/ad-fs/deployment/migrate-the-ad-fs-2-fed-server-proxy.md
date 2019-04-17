---
title: "AD FS 2.0 フェデレーション サーバー プロキシを移行します。"
description: "Windows Server 2012 への AD FS フェデレーション サーバー プロキシの移行について説明します。"
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 98e28c9be808f63ed39a3ac24dd95014b388d001
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="migrate-the-ad-fs-20-federation-server-proxy"></a>AD FS 2.0 フェデレーション サーバー プロキシを移行します。
このドキュメントでは、Windows Server 2012 への AD FS 2.0 フェデレーション プロキシ サーバーの移行の詳細を提供します。

## <a name="migrate-the-proxy"></a>プロキシを移行します。

AD FS 2.0 フェデレーション サーバー プロキシを Windows Server 2012 に移行するには、次の手順を実行します。  
  
1.  Windows Server 2012 への移行を計画している各フェデレーション サーバー プロキシには、確認し、手順を実行[移行、AD FS 2.0 フェデレーション サーバー プロキシの準備](prepare-to-migrate-ad-fs-fed-proxy.md)します。  
  
2.  フェデレーション サーバー プロキシをロード バランサーから削除します。  
  
3.  このサーバーから Windows Server 2008 R2 または Windows Server 2012 への Windows Server 2008 では、オペレーティング システムのインプレース アップグレードを実行します。 詳細については、次を参照してください。[Windows Server 2012 のインストール](https://technet.microsoft.com/library/jj134246.aspx)します。  
  
> [!IMPORTANT]
>  オペレーティング システムのアップグレードの結果、このサーバーの AD FS プロキシ構成が失われたと AD FS 2.0 サーバーの役割が削除されます。 Windows Server 2012 の AD FS サーバーの役割が代わりに、インストールされているが構成されていません。 手動で元の AD FS プロキシ構成を作成して、フェデレーション サーバー プロキシの移行を完了する他の AD FS プロキシ設定を復元する必要があります。  
  
4.  使用して、元の AD FS プロキシ構成を作成、**AD FS フェデレーション サーバー プロキシ構成ウィザード**します。 詳細については、次を参照してください。[for Federation Server Proxy Role Configure a Computer](configure-a-computer-for-the-federation-server-proxy-role.md)します。 ウィザードを実行すると、収集した情報準備」の移行、AD fs 2.0 フェデレーション サーバー プロキシ次のようを使用します。  
  
 
|**フェデレーション サーバー プロキシのウィザードのオプション**|**次の値を使用してください。**|
|-----|-----|  
|**フェデレーション サービス名**|Proxyproperties.txt ファイルの BaseHostName 値を入力します|  
|**このフェデレーションに要求を送信するときに HTTP プロキシ サーバーを使用して**サービス] チェック ボックス|Proxyproperties.txt ファイルに ForwardProxyUrl プロパティの値が含まれている場合、チェック ボックスをオン|  
|**HTTP プロキシ サーバーのアドレス**|Proxyproperties.txt ファイルの ForwardProxyUrl 値を入力します|  
|資格情報プロンプト|AD FS フェデレーション サーバーの管理者であるアカウントまたは AD FS フェデレーション サービスを実行するサービス アカウントの資格情報を入力します。|  
  
5.  このサーバー上で、AD FS Web ページを更新します。 バックアップした場合、カスタマイズされた AD FS プロキシ Web ページ、フェデレーション サーバー プロキシの移行の準備中に、既定では既定で作成された AD FS Web ページを上書きする、バックアップ データを使用して、**%systemdrive%\inetpub\adfs\ls** Windows Server 2012 で AD FS プロキシ構成の結果としてディレクトリ。  
  
6.  このサーバーをロード バランサーに追加します。  
  
7.  その他の AD FS 2.0 フェデレーション サーバー プロキシに移行する場合は、残りのフェデレーション サーバー プロキシ コンピューターに手順 2 ~ 6 を繰り返します。  
  
  
## <a name="next-steps"></a>次の手順
 [AD FS 2.0 フェデレーション サーバーの移行を準備します。](prepare-to-migrate-ad-fs-fed-server.md)   
 [AD FS 2.0 フェデレーション サーバー プロキシの移行を準備します。](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [AD FS 2.0 フェデレーション サーバーを移行します。](migrate-the-ad-fs-fed-server.md)   
 [AD FS 2.0 フェデレーション サーバー プロキシを移行します。](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [AD FS 1.1 Web エージェントを移行します。](migrate-the-ad-fs-web-agent.md)