---
title: AD FS 2.0 フェデレーション サーバー プロキシを移行します。
description: Windows Server 2012 への AD FS フェデレーション サーバー プロキシの移行に関する情報を提供します。
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 98e28c9be808f63ed39a3ac24dd95014b388d001
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881023"
---
# <a name="migrate-the-ad-fs-20-federation-server-proxy"></a>AD FS 2.0 フェデレーション サーバー プロキシを移行します。
このドキュメントでは、Windows Server 2012 への AD FS 2.0 フェデレーション プロキシ サーバーの移行に関する詳細情報を示します。

## <a name="migrate-the-proxy"></a>プロキシを移行します。

AD FS 2.0 フェデレーション サーバー プロキシを Windows Server 2012 に移行するには、次の手順を実行します。  
  
1.  Windows Server 2012 に移行する各フェデレーション サーバー プロキシには、確認し、実行手順では、 [Migrate the AD FS 2.0 フェデレーション サーバー プロキシの準備](prepare-to-migrate-ad-fs-fed-proxy.md)します。  
  
2.  フェデレーション サーバー プロキシをロード バランサーから削除します。  
  
3.  このサーバーから Windows Server 2008 R2 または Windows Server 2012 への Windows Server 2008 オペレーティング システムのインプレース アップグレードを実行します。 詳細については、「[Windows Server 2012 のインストール](https://technet.microsoft.com/library/jj134246.aspx)」を参照してください。  
  
> [!IMPORTANT]
>  オペレーティング システムをアップグレードすると、このサーバーの AD FS 構成が失われ、AD FS 2.0 サーバーの役割が削除されます。 Windows Server 2012 の AD FS サーバーの役割が代わりに、インストールされているが構成されていません。 フェデレーション サーバーの移行を完了するには、元の AD FS プロキシ構成を手動で作成し、その他の AD FS 設定を復元する必要があります。  
  
4.  **AD FS フェデレーション サーバー構成ウィザード**を使用して、元の AD FS プロキシ構成を作成します。 詳細については、「 [Configure a Computer for the Federation Server Proxy Role](configure-a-computer-for-the-federation-server-proxy-role.md)」を参照してください。 ウィザードを実行するときに、AD FS 2.0 フェデレーション サーバー プロキシを移行するための準備を行っている間に収集した情報を、次のように使用します。  
  
 
|**フェデレーション サーバー プロキシ ウィザード オプションの入力**|**次の値を使用します。**|
|-----|-----|  
|**フェデレーション サービス名**|Proxyproperties.txt ファイルの BaseHostName 値を入力します。|  
|**[このフェデレーション サービスに要求を送信するときに HTTP プロキシ サーバーを使用する]** チェックボックス|proxyproperties.txt ファイルに ForwardProxyUrl プロパティの値が含まれている場合は、このチェックボックスをオンにします。|  
|**HTTP プロキシ サーバーのアドレス**|proxyproperties.txt ファイルの ForwardProxyUrl 値を入力します。|  
|資格情報プロンプト|AD FS フェデレーション サーバーの管理者のアカウントまたは AD FS フェデレーション サービスを実行するサービス アカウントの資格情報を入力します。|  
  
5.  このサーバーで AD FS Web ページを更新します。 フェデレーション サーバー プロキシの移行の準備中に、カスタマイズされた AD FS プロキシ web ページをバックアップしている場合は、バックアップ データを使用して、AD FS web ページで既定で作成された既定値を上書きする、 **%systemdrive%\inetpub\adfs\ls** Windows Server 2012 で AD FS プロキシ構成の結果ディレクトリ。  
  
6.  このサーバーをロード バランサーに追加して戻します。  
  
7.  移行する AD FS 2.0 フェデレーション サーバー プロキシが他にもある場合は、残りのフェデレーション サーバー プロキシ コンピューターで、手順 2 から 6 を繰り返します。  
  
  
## <a name="next-steps"></a>次の手順
 [AD FS 2.0 フェデレーション サーバーの移行を準備します。](prepare-to-migrate-ad-fs-fed-server.md)   
 [AD FS 2.0 フェデレーション サーバー プロキシの移行を準備します。](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [AD FS 2.0 フェデレーション サーバーを移行します。](migrate-the-ad-fs-fed-server.md)   
 [AD FS 2.0 フェデレーション サーバー プロキシを移行します。](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [AD FS 1.1 Web エージェントを移行します。](migrate-the-ad-fs-web-agent.md)