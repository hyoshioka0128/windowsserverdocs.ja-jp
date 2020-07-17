---
ms.assetid: cd4d4902-dcdf-49dd-8059-82a56bf4b585
title: サーバー認証証明書の秘密キーの部分をエクスポートする
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 6baa734e3fc346d94f4387e2ed54d3e707e5af75
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855425"
---
# <a name="export-the-private-key-portion-of-a-server-authentication-certificate"></a>サーバー認証証明書の秘密キーの部分をエクスポートする

Active Directory フェデレーションサービス (AD FS) \(AD FS\) ファーム内のすべてのフェデレーションサーバーは、サーバー認証証明書の秘密キーへのアクセス権を持っている必要があります。 フェデレーションサーバーまたは Web サーバーのサーバーファームを実装する場合は、1つの認証証明書が必要です。 この証明書は、エンタープライズ証明機関 \(CA\)によって発行されている必要があり、エクスポート可能な秘密キーを持っている必要があります。 サーバー認証証明書の秘密キーは、ファーム内のすべてのサーバーが利用できるように、エクスポート可能である必要があります。  
  
この同じ概念は、ファーム内のすべてのフェデレーションサーバープロキシが同じサーバー認証証明書の秘密キー部分を共有する必要があるという意味で、フェデレーションサーバープロキシファームにも当てはまります。  
  
> [!NOTE]  
> の AD FS 管理スナップ\-は、サービス通信証明書としてのフェデレーションサーバーのサーバー認証証明書を参照します。  
  
このコンピューターが再生する役割に応じて、サーバー認証証明書を秘密キーと共にインストールしたフェデレーションサーバーコンピューターまたはフェデレーションサーバープロキシコンピューターで、この手順を実行します。 手順を完了すると、ファーム内の各サーバーの既定の Web サイトでこの証明書をインポートできるようになります。 詳細については、「[サーバー認証証明書を既定の Web サイトにインポートする](Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md)」を参照してください。  
  
この手順を完了するには、ローカル コンピューター上の **Administrators** または同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
### <a name="to-export-the-private-key-portion-of-a-server-authentication-certificate"></a>サーバー認証証明書の秘密キーの部分をエクスポートするには  
  
1. **[スタート]** 画面で、「**インターネットインフォメーションサービス \(IIS\) Manager**」と入力し、enter キーを押します。  
  
2. コンソール ツリーで、 **[コンピューター名]** をクリックします。  
  
3. 中央のウィンドウで、 **[サーバー証明書]** をダブル\-クリックします。  
  
4. 中央のウィンドウで、エクスポートする証明書を右\-クリックし、 **[エクスポート]** をクリックします。  
  
5. **[証明書のエクスポート]** ダイアログボックスで、. **[.]** をクリックします。 ボタンをクリックします。  
  
6. **[ファイル名]** に「 **C:\\** <em>nameofcertificate</em>」と入力し、 **[開く]** をクリックします。  
  
7. 証明書のパスワードを入力し、確認したら、 **[OK]** をクリックします。  
  
8. エクスポートが成功したかどうかを検証するには、指定したファイルが指定した場所に作成されていることを確認します。  
  
   > [!IMPORTANT]  
   > この証明書を新しいサーバー上のローカル証明書ストアにインポートできるように、ファイルを物理メディアに転送すると共に、新しいサーバーへの移送中にそのセキュリティを保護する必要があります。 秘密キーのセキュリティを保護することはきわめて重要です。 このキーが侵害された場合、組織内およびリソースパートナー組織内のリソースを含む AD FS 展開 \(のセキュリティが侵害されること\) あります。  
  
9. フェデレーション サービスをインストールする前に、新しいサーバー上の証明書ストアにサーバー認証証明書をインポートします。 証明書をインポートする方法の詳細については、「サーバー証明書のインポート \([http:\/\/go.microsoft.com\/fwlink\/?」を参照してください。LinkId\=108283](https://go.microsoft.com/fwlink/?LinkId=108283)\)。  
  
## <a name="additional-references"></a>その他の参照情報  
[チェックリスト: フェデレーションサーバーのセットアップ](Checklist--Setting-Up-a-Federation-Server.md)  
  
[チェックリスト: フェデレーションサーバープロキシの設定](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[フェデレーション サーバーの証明書の要件](https://technet.microsoft.com/library/dd807040.aspx)  
  
[フェデレーション サーバー プロキシの証明書の要件](https://technet.microsoft.com/library/dd807054.aspx)  
  

