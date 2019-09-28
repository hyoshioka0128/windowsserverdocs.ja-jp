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
ms.openlocfilehash: e97a1b3b66d7c12c96570022b7e69caaf0e92f65
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408222"
---
# <a name="migrate-the-ad-fs-20-federation-server-proxy"></a>AD FS 2.0 フェデレーションサーバープロキシの移行
このドキュメントでは、AD FS 2.0 のフェデレーションプロキシサーバーを Windows Server 2012 に移行する方法について詳しく説明します。

## <a name="migrate-the-proxy"></a>プロキシを移行する

AD FS 2.0 フェデレーションサーバープロキシを Windows Server 2012 に移行するには、次の手順を実行します。  
  
1.  Windows Server 2012 への移行を計画しているすべてのフェデレーションサーバープロキシについて、「 [AD FS 2.0 フェデレーションサーバープロキシの移行の準備](prepare-to-migrate-ad-fs-fed-proxy.md)」の手順を確認して実行します。  
  
2.  フェデレーション サーバー プロキシをロード バランサーから削除します。  
  
3.  このサーバーのオペレーティングシステムを windows server 2008 R2 または Windows Server 2008 から Windows Server 2012 にインプレースアップグレードします。 詳細については、「[Windows Server 2012 のインストール](https://technet.microsoft.com/library/jj134246.aspx)」を参照してください。  
  
> [!IMPORTANT]
>  オペレーティング システムをアップグレードすると、このサーバーの AD FS 構成が失われ、AD FS 2.0 サーバーの役割が削除されます。 代わりに、Windows Server 2012 AD FS サーバーロールがインストールされますが、構成されていません。 フェデレーション サーバーの移行を完了するには、元の AD FS プロキシ構成を手動で作成し、その他の AD FS 設定を復元する必要があります。  
  
4. **AD FS フェデレーション サーバー構成ウィザード**を使用して、元の AD FS プロキシ構成を作成します。 詳細については、次を参照してください。 [、フェデレーション サーバー プロキシ ロール用コンピューターの構成](configure-a-computer-for-the-federation-server-proxy-role.md)します。 ウィザードを実行するときに、AD FS 2.0 フェデレーション サーバー プロキシを移行するための準備を行っている間に収集した情報を、次のように使用します。  
  
 
|**フェデレーションサーバープロキシウィザードの入力オプション**|**次の値を使用します。**|
|-----|-----|  
|**フェデレーションサービス名**|Proxyproperties.txt ファイルの BaseHostName 値を入力します。|  
|**[このフェデレーション サービスに要求を送信するときに HTTP プロキシ サーバーを使用する]** チェックボックス|proxyproperties.txt ファイルに ForwardProxyUrl プロパティの値が含まれている場合は、このチェックボックスをオンにします。|  
|**HTTP プロキシサーバーのアドレス**|proxyproperties.txt ファイルの ForwardProxyUrl 値を入力します。|  
|資格情報プロンプト|AD FS フェデレーション サーバーの管理者のアカウントまたは AD FS フェデレーション サービスを実行するサービス アカウントの資格情報を入力します。|  
  
5. このサーバーで AD FS Web ページを更新します。 移行のためにフェデレーションサーバープロキシを準備しているときに、カスタマイズした AD FS プロキシ web ページをバックアップした場合は、バックアップデータを使用して、 **%systemdrive%\inetpub\adfs\ls**ディレクトリに既定で作成された既定の AD FS web ページを上書きします。Windows Server 2012 の AD FS プロキシ構成の結果として。  
  
6. このサーバーをロード バランサーに追加して戻します。  
  
7. 移行する AD FS 2.0 フェデレーション サーバー プロキシが他にもある場合は、残りのフェデレーション サーバー プロキシ コンピューターで、手順 2 から 6 を繰り返します。  
  
  
## <a name="next-steps"></a>次の手順
 [AD FS 2.0 フェデレーションサーバーの移行の準備](prepare-to-migrate-ad-fs-fed-server.md)   
 [AD FS 2.0 フェデレーションサーバープロキシの移行の準備](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [AD FS 2.0 フェデレーションサーバー](migrate-the-ad-fs-fed-server.md)  を移行します。  
 [AD FS 2.0 フェデレーションサーバープロキシ   を移行します](migrate-the-ad-fs-2-fed-server-proxy.md)。  
 [AD FS 1.1 Web エージェントの移行](migrate-the-ad-fs-web-agent.md)