---
ms.assetid: cd4d4902-dcdf-49dd-8059-82a56bf4b585
title: "サーバー認証証明書の秘密キー部分のエクスポートします。"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: c968f0702d56b56d0a80459e5cf0c9e658c56741
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="export-the-private-key-portion-of-a-server-authentication-certificate"></a>サーバー認証証明書の秘密キー部分のエクスポートします。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Active Directory フェデレーション サービス \(AD FS\) ファーム内のすべてのフェデレーション サーバー、サーバー認証証明書の秘密キーへのアクセスが必要です。 フェデレーション サーバーまたは Web サーバーのサーバー ファームを実装する場合は、1 つの認証証明書が必要です。 この証明書を発行する必要があります、エンタープライズ証明機関によって \(CA\) と、エクスポート可能な秘密キーが必要です。 それが利用できる、ファーム内のすべてのサーバーにできるように、サーバー認証証明書の秘密キーがエクスポートできる必要があります。  
  
これと同じ考え方は、ファーム内のすべてのフェデレーション サーバー プロキシが同じサーバー認証証明書の秘密キー部分を共有する必要がありますという意味でフェデレーション サーバー プロキシ ファームの場合は true です。  
  
> [!NOTE]  
> AD FS 管理スナップインでは、フェデレーション サーバーのサーバー認証証明書をサービス通信証明書と呼びます。  
  
このコンピューターが果たす役割、に応じて秘密キーを持つサーバー認証証明書をインストールしたフェデレーション サーバー コンピューターまたはフェデレーション サーバー プロキシ コンピューターでこの手順に従います。 手順を完了するときに、ファーム内の各サーバーの既定の Web サイトでこの証明書をインポートできます。 詳細については、次を参照してください。[サーバー認証証明書を既定の Web サイトにインポート](Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md)します。  
  
メンバーシップ**管理者**、相当するもので、ローカル コンピューターでは、この手順を完了するために必要な最低限またはします。  適切なアカウントの使用に関する詳細を確認し、グループ メンバーシップ[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
### <a name="to-export-the-private-key-portion-of-a-server-authentication-certificate"></a>サーバー認証証明書の秘密キー部分をエクスポートするには  
  
1.  **開始**画面で「**インターネット インフォメーション サービス \(IIS\) Manager**、し、ENTER キーを押します。  
  
2.  コンソール ツリーでクリックして**ComputerName**します。  
  
3.  中央のウィンドウでダブルクリック**サーバー証明書**します。  
  
4.  中央のウィンドウに、エクスポート、およびをクリックする証明書を右クリックで**エクスポート**します。  
  
5.  **証明書のエクスポート**ダイアログ ボックスで、をクリックして、**.** ボタンをクリックします。  
  
6.  **ファイル名**、種類**C:\\***NameofCertificate*、] をクリックし、**開く**します。  
  
7.  証明書のパスワードを入力、および確認し、をクリックして**OK**します。  
  
8.  指定したファイルが指定された場所に作成されたことを確認することによって、エクスポートの成功を検証します。  
  
    > [!IMPORTANT]  
    > この証明書は、新しいサーバー上のローカル証明書ストアにインポートできるようには、物理メディアにファイルを転送し、新しいサーバーへの転送中にそのセキュリティを保護する必要があります。 これは秘密キーのセキュリティを保護するために非常に重要です。 このキーが侵害された場合、全体の AD FS 展開のセキュリティ \ (リソース パートナー organizations\ で、組織内のリソースを含む) に欠陥があります。  
  
9. フェデレーション サービスをインストールする前に、新しいサーバーで証明書ストアにエクスポートされたサーバー認証証明書をインポートします。 証明書をインポートする方法については、サーバー証明書のインポートを参照してください \ ([http:///\/go.microsoft.com\/fwlink\/ですか?。LinkId\ = 108283](https://go.microsoft.com/fwlink/?LinkId=108283)\)。  
  
## <a name="additional-references"></a>その他の参照  
[チェックリスト: フェデレーション サーバーのセットアップ](Checklist--Setting-Up-a-Federation-Server.md)  
  
[チェックリスト: フェデレーション サーバー プロキシのセットアップ](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[フェデレーション サーバーの証明書の要件](https://technet.microsoft.com/library/dd807040.aspx)  
  
[フェデレーション サーバー プロキシの証明書の要件](https://technet.microsoft.com/library/dd807054.aspx)  
  

