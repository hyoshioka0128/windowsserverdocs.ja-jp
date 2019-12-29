---
ms.assetid: ad61c586-ba8a-4534-8824-b45994d60c6b
title: フェデレーション サーバーが正常に動作していることを確認する
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 6d27c8d69affe001630d8deaa2c21f334f8f86ad
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408312"
---
# <a name="verify-that-a-federation-server-is-operational"></a>フェデレーション サーバーが正常に動作していることを確認する


以下の手順を使用して、フェデレーション サーバーが動作可能であること (つまり、同じネットワーク上のクライアントから新しいフェデレーション サーバーにアクセスできること) を確認します。  
  
この手順を実行するには、少なくとも **Users**、 **Backup Operators**、 **Power Users**、または **Administrators** グループのメンバーであるか、そのメンバーと同等の権限が必要になります。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
### <a name="procedure-1-to-verify-that-a-federation-server-is-operational"></a>手順 1:フェデレーション サーバーが正常に動作していることを確認するには  
  
1.  フェデレーションサーバーでインターネットインフォメーションサービス\(IIS\)が正しく構成されていることを確認するには、フェデレーションサーバーと同じフォレストにあるクライアントコンピューターにログオンします。  
  
2.  ブラウザーウィンドウを開き、アドレスバーにフェデレーションサーバーの DNS ホスト名を入力し、新しいフェデレーションサーバーに/adfs/fs/federationserverservice.asmx を追加します。次に例を示します。  
  
    **https://fs1.fabrikam.com/adfs/fs/federationserverservice.asmx**  
  
3.  Enter キーを押し、フェデレーション サーバー コンピューターの次の手順を完了します。 **[この web サイトのセキュリティ証明書に問題があり]** ます というメッセージが表示された場合は、 **[このサイトの使用を続行する]** をクリックします。  
  
    期待される表示出力は、サービス内容に関する XML ドキュメントです。 このページが表示されたら、フェデレーション サーバーの IIS は動作可能であり、正常にページを提供します。  
  
この手順を実行するには、ローカル コンピューターの **Administrators**グループのメンバーシップか、それと同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
### <a name="procedure-2-to-verify-that-a-federation-server-is-operational"></a>手順 2:フェデレーション サーバーが正常に動作していることを確認するには  
  
1.  新しいフェデレーションサーバーに管理者としてログオンします。  
  
2.  **スタート**画面で、「**イベントビューアー**」と入力し、enter キーを押します。  
  
3.  詳細ウィンドウで、 **[アプリケーションとサービスログ]** をダブル\-クリック\-し、 **[AD FS イベント]** をダブルクリックして、 **[管理者]** をクリックします。  
  
4.  **[イベント id]** 列で、イベント id 100 を探します。 フェデレーションサーバーが適切に構成されている場合は、イベントビューアーのアプリケーションログに、イベント ID 100 の新しいイベントが表示されます。 このイベントは、フェデレーションサーバーがフェデレーションサービスと正常に通信できることを確認します。  
  
## <a name="additional-references"></a>その他の参照情報  
[チェックリスト:フェデレーション サーバーのセットアップ](Checklist--Setting-Up-a-Federation-Server.md)  
  

