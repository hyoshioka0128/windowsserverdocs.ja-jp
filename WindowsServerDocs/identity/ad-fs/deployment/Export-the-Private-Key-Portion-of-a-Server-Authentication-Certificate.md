---
ms.assetid: cd4d4902-dcdf-49dd-8059-82a56bf4b585
title: サーバー認証証明書の秘密キーの部分をエクスポートする
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 1a7e59dd83ebc9a9eabd5bda1dc598d320f5028d
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66442504"
---
# <a name="export-the-private-key-portion-of-a-server-authentication-certificate"></a>サーバー認証証明書の秘密キーの部分をエクスポートする

Active の Directory フェデレーション サービス内のすべてのフェデレーション サーバー \(AD FS\)ファームにサーバー認証証明書の秘密キーにアクセスする必要があります。 フェデレーション サーバーまたは Web サーバーのサーバー ファームを実装する場合は、1 つの認証証明書が必要です。 エンタープライズ証明機関によってこの証明書を発行する必要があります\(CA\)、エクスポートの秘密キーが必要とします。 サーバー認証証明書の秘密キーは、ファーム内のすべてのサーバーが利用できるように、エクスポート可能である必要があります。  
  
これと同じ考え方は、ファーム内のすべてのフェデレーション サーバー プロキシが同じサーバー認証証明書の秘密キー部分を共有する必要がありますの意味では、フェデレーション サーバー プロキシ ファームの場合は true。  
  
> [!NOTE]  
> AD FS 管理スナップイン\-サービス通信証明書としてフェデレーション サーバーのサーバー認証証明書を参照しています。  
  
このコンピューターが果たす役割、に応じて秘密キーでサーバー認証証明書をインストールしたフェデレーション サーバー コンピューターまたはフェデレーション サーバー プロキシ コンピューターでこの手順に従います。 手順を完了すると、ファーム内の各サーバーの既定の Web サイトでこの証明書をインポートできるようになります。 詳細については、次を参照してください。[既定の Web サイトにサーバー認証証明書をインポート](Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md)します。  
  
この手順を実行するには、ローカル コンピューターの **Administrators**グループのメンバーシップか、それと同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
### <a name="to-export-the-private-key-portion-of-a-server-authentication-certificate"></a>サーバー認証証明書の秘密キーの部分をエクスポートするには  
  
1. **開始**画面で「**インターネット インフォメーション サービス\(IIS\) Manager**、し、ENTER キーを押します。  
  
2. コンソール ツリーで、 **[コンピューター名]** をクリックします。  
  
3. 中央のウィンドウでダブルクリック\-クリックして**サーバー証明書**します。  
  
4. 中央のウィンドウで右\-クリックして、エクスポートする証明書をクリックします。**エクスポート**します。  
  
5. **証明書のエクスポート**ダイアログ ボックスで、をクリックして、 **.** ボタンをクリックします。  
  
6. **ファイル名**、型**c:\\** <em>NameofCertificate</em>、 をクリックし、**オープン**します。  
  
7. 証明書のパスワードを入力し、確認したら、 **[OK]** をクリックします。  
  
8. エクスポートが成功したかどうかを検証するには、指定したファイルが指定した場所に作成されていることを確認します。  
  
   > [!IMPORTANT]  
   > この証明書を新しいサーバー上のローカル証明書ストアにインポートできるように、ファイルを物理メディアに転送すると共に、新しいサーバーへの移送中にそのセキュリティを保護する必要があります。 秘密キーのセキュリティを保護することはきわめて重要です。 このキーが侵害された場合、AD FS のデプロイ全体のセキュリティ\(、組織内、およびリソース パートナー組織内のリソースを含む\)が侵害された場合します。  
  
9. フェデレーション サービスをインストールする前に、新しいサーバー上の証明書ストアにサーバー認証証明書をインポートします。 証明書をインポートする方法については、サーバー証明書のインポートを参照してください。 \( [http:\/\/go.microsoft.com\/fwlink\/でしょうか。LinkId\=108283](https://go.microsoft.com/fwlink/?LinkId=108283)\)します。  
  
## <a name="additional-references"></a>その他の参照情報  
[チェックリスト:フェデレーション サーバーのセットアップ](Checklist--Setting-Up-a-Federation-Server.md)  
  
[チェックリスト:フェデレーション サーバー プロキシのセットアップ](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[フェデレーション サーバーの証明書の要件](https://technet.microsoft.com/library/dd807040.aspx)  
  
[フェデレーション サーバー プロキシの証明書の要件](https://technet.microsoft.com/library/dd807054.aspx)  
  

