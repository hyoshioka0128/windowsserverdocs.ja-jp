---
title: AD FS 2.0 フェデレーションサーバープロキシの移行
description: AD FS フェデレーションサーバープロキシを Windows Server 2012 に移行する方法について説明します。
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: d7b08b28f33bbab5d3e573b10195528c47f6cc6c
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86966234"
---
# <a name="migrate-the-ad-fs-20-federation-server-proxy"></a>AD FS 2.0 フェデレーションサーバープロキシの移行
このドキュメントでは、AD FS 2.0 のフェデレーションプロキシサーバーを Windows Server 2012 に移行する方法について詳しく説明します。

## <a name="migrate-the-proxy"></a>プロキシを移行する

AD FS 2.0 フェデレーションサーバープロキシを Windows Server 2012 に移行するには、次の手順を実行します。  
  
1.  Windows Server 2012 への移行を計画しているすべてのフェデレーションサーバープロキシについて、「 [AD FS 2.0 フェデレーションサーバープロキシの移行の準備](prepare-to-migrate-ad-fs-fed-proxy.md)」の手順を確認して実行します。  
  
2.  フェデレーション サーバー プロキシをロード バランサーから削除します。  
  
3.  このサーバーのオペレーティングシステムを windows server 2008 R2 または Windows Server 2008 から Windows Server 2012 にインプレースアップグレードします。 詳細については、「[Windows Server 2012 のインストール](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj134246(v=ws.11))」を参照してください。  
  
> [!IMPORTANT]
>  オペレーティング システムをアップグレードすると、このサーバーの AD FS 構成が失われ、AD FS 2.0 サーバーの役割が削除されます。 代わりに、Windows Server 2012 AD FS サーバーロールがインストールされますが、構成されていません。 フェデレーション サーバーの移行を完了するには、元の AD FS プロキシ構成を手動で作成し、その他の AD FS 設定を復元する必要があります。  
  
4. **AD FS フェデレーション サーバー構成ウィザード**を使用して、元の AD FS プロキシ構成を作成します。 詳細については、「 [Configure a Computer for the Federation Server Proxy Role](configure-a-computer-for-the-federation-server-proxy-role.md)」を参照してください。 ウィザードを実行するときに、AD FS 2.0 フェデレーション サーバー プロキシを移行するための準備を行っている間に収集した情報を、次のように使用します。  
  
 
|**フェデレーション サーバー構成ウィザードのオプション**|**使用する値**|
|-----|-----|  
|**フェデレーションサービス名**|Proxyproperties.txt ファイルの BaseHostName 値を入力します。|  
|[**このフェデレーション サービスに要求を送信するときに HTTP プロキシ サーバーを使用する**] チェックボックス|proxyproperties.txt ファイルに ForwardProxyUrl プロパティの値が含まれている場合は、このチェックボックスをオンにします。|  
|**プロキシ サーバーのアドレス**|proxyproperties.txt ファイルの ForwardProxyUrl 値を入力します。|  
|資格情報プロンプト|AD FS フェデレーション サーバーの管理者のアカウントまたは AD FS フェデレーション サービスを実行するサービス アカウントの資格情報を入力します。|  
  
5. このサーバーで AD FS Web ページを更新します。 移行のためにフェデレーションサーバープロキシを準備しているときに、カスタマイズされた AD FS プロキシ web ページをバックアップした場合は、バックアップデータを使用して、Windows Server 2012 の AD FS プロキシ構成の結果として **%systemdrive%\inetpub\adfs\ls**ディレクトリに既定で作成された既定の AD FS web ページを上書きします。  
  
6. このサーバーをロード バランサーに追加して戻します。  
  
7. 移行する AD FS 2.0 フェデレーション サーバー プロキシが他にもある場合は、残りのフェデレーション サーバー プロキシ コンピューターで、手順 2 から 6 を繰り返します。  
  
  
## <a name="next-steps"></a>次の手順
 [AD FS 2.0 フェデレーションサーバーの移行の準備](prepare-to-migrate-ad-fs-fed-server.md)   
 [AD FS 2.0 フェデレーションサーバープロキシの移行の準備](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [AD FS 2.0 フェデレーションサーバーの移行](migrate-the-ad-fs-fed-server.md)   
 [AD FS 2.0 フェデレーションサーバープロキシの移行](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [AD FS 1.1 Web エージェントの移行](migrate-the-ad-fs-web-agent.md)
