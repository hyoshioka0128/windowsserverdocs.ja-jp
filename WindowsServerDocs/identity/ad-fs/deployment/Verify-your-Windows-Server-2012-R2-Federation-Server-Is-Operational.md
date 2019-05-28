---
ms.assetid: 1115d276-00f6-4c23-9278-eedcc31295d8
title: Windows Server 2012 R2 フェデレーション サーバーが稼働中であることを確認します。
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 7cab415cc599f388c2bb5966d45998874ce56987
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66191838"
---
# <a name="verify-your-windows-server-2012-r2-federation-server-is-operational"></a>Windows Server 2012 R2 フェデレーション サーバーが稼働中であることを確認します。



以下の手順を使用して、フェデレーション サーバーが動作可能であること (つまり、同じネットワーク上のクライアントから新しいフェデレーション サーバーにアクセスできること) を確認します。  
  
この手順を実行するには、少なくとも **Users**、 **Backup Operators**、 **Power Users**、または **Administrators** グループのメンバーであるか、そのメンバーと同等の権限が必要になります。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
### <a name="procedure-1-to-verify-that-a-federation-server-is-operational"></a>手順 1:フェデレーション サーバーが正常に動作していることを確認するには  
  
1.  インターネット インフォメーション サービスのことを確認する\(IIS\)フェデレーション サーバーでは、フェデレーション サーバーと同じフォレストにあるクライアント コンピューターにログオンが正しく構成されています。  
  
2.  ブラウザー ウィンドウを開き、アドレス バーに、フェデレーション サーバーの DNS のホスト名を入力および追加\/adfs\/fs\/例については、新しいフェデレーション サーバー用に federationserverservice.asmx:  
  
    **https:\/\/fs1.fabrikam.com\/adfs\/fs\/federationserverservice.asmx**  
  
3.  Enter キーを押し、フェデレーション サーバー コンピューターの次の手順を完了します。 メッセージが表示された場合**この web サイトのセキュリティ証明書に問題がある**、 をクリックして**このサイトの閲覧を続行する**します。  
  
    期待される表示出力は、サービス内容に関する XML ドキュメントです。 このページが表示されたら、フェデレーション サーバーの IIS は動作可能であり、正常にページを提供します。  
  
この手順を実行するには、ローカル コンピューターの **Administrators**グループのメンバーシップか、それと同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
### <a name="procedure-2-to-verify-that-a-federation-server-is-operational"></a>手順 2:フェデレーション サーバーが正常に動作していることを確認するには  
  
1.  新しいフェデレーション サーバーに管理者としてログオンします。  
  
2.  **開始**画面で「**イベント ビューアー**し、ENTER キーを押します。  
  
3.  詳細ウィンドウでダブルクリック\-クリックして**Applications and Services Logs**、二重\- をクリックして**AD FS Eventing**、順にクリックします**管理者**。  
  
4.  **イベント ID**列で、イベント ID 100 を探します。 新しいイベントを参照してください、フェデレーション サーバーが正しく構成されている場合: イベント ビューアーのアプリケーション ログ: イベント ID 100。 このイベントは、フェデレーション サーバーがフェデレーション サービスと正常に通信できることを確認します。  
  
## <a name="see-also"></a>関連項目 

[AD FS 展開](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS 展開ガイドします。](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[フェデレーション サーバー ファームの展開](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
   
  

