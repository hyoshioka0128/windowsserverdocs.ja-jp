---
ms.assetid: ad61c586-ba8a-4534-8824-b45994d60c6b
title: フェデレーション サーバーが正常に動作していることを確認する
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: b9498451e8f6d7701e9ed4b3ac7d61f19d2dcdb4
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66191893"
---
# <a name="verify-that-a-federation-server-is-operational"></a>フェデレーション サーバーが正常に動作していることを確認する


以下の手順を使用して、フェデレーション サーバーが動作可能であること (つまり、同じネットワーク上のクライアントから新しいフェデレーション サーバーにアクセスできること) を確認します。  
  
この手順を実行するには、少なくとも **Users**、 **Backup Operators**、 **Power Users**、または **Administrators** グループのメンバーであるか、そのメンバーと同等の権限が必要になります。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
### <a name="procedure-1-to-verify-that-a-federation-server-is-operational"></a>手順 1:フェデレーション サーバーが正常に動作していることを確認するには  
  
1.  インターネット インフォメーション サービスのことを確認する\(IIS\)フェデレーション サーバーでは、フェデレーション サーバーと同じフォレストにあるクライアント コンピューターにログオンが正しく構成されています。  
  
2.  ブラウザー ウィンドウを開きで、アドレス バーの種類、フェデレーション サーバーの DNS ホスト名、およびしの/adfs/fs/federationserverservice.asmx を追加、新しいフェデレーション サーバーの例。  
  
    **https://fs1.fabrikam.com/adfs/fs/federationserverservice.asmx**  
  
3.  Enter キーを押し、フェデレーション サーバー コンピューターの次の手順を完了します。 メッセージが表示された場合**この web サイトのセキュリティ証明書に問題がある**、 をクリックして**このサイトの閲覧を続行する**します。  
  
    期待される表示出力は、サービス内容に関する XML ドキュメントです。 このページが表示されたら、フェデレーション サーバーの IIS は動作可能であり、正常にページを提供します。  
  
この手順を実行するには、ローカル コンピューターの **Administrators**グループのメンバーシップか、それと同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
### <a name="procedure-2-to-verify-that-a-federation-server-is-operational"></a>手順 2:フェデレーション サーバーが正常に動作していることを確認するには  
  
1.  新しいフェデレーション サーバーに管理者としてログオンします。  
  
2.  **開始**画面で「**イベント ビューアー**し、ENTER キーを押します。  
  
3.  詳細ウィンドウでダブルクリック\-クリックして**Applications and Services Logs**、二重\- をクリックして**AD FS Eventing**、順にクリックします**管理者**。  
  
4.  **イベント ID**列で、イベント ID 100 を探します。 新しいイベントを参照してください、フェデレーション サーバーが正しく構成されている場合: イベント ビューアーのアプリケーション ログ: イベント ID 100。 このイベントは、フェデレーション サーバーがフェデレーション サービスと正常に通信できることを確認します。  
  
## <a name="additional-references"></a>その他の参照情報  
[チェックリスト:フェデレーション サーバーのセットアップ](Checklist--Setting-Up-a-Federation-Server.md)  
  

