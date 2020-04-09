---
ms.assetid: ad61c586-ba8a-4534-8824-b45994d60c6b
title: フェデレーション サーバーが正常に動作していることを確認する
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: b6ce4f826809e2c07fdbe4424d427f1244ea5172
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80814255"
---
# <a name="verify-that-a-federation-server-is-operational"></a>フェデレーション サーバーが正常に動作していることを確認する


以下の手順を使用して、フェデレーション サーバーが動作可能であること (つまり、同じネットワーク上のクライアントから新しいフェデレーション サーバーにアクセスできること) を確認します。  
  
この手順を完了するための最小要件は、ローカル コンピューター上の **[Users]** 、 **[Backup Operators]** 、 **[Power Users]** 、 **[Administrators]** または同等ユーザーのメンバーシップであることです。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
### <a name="procedure-1-to-verify-that-a-federation-server-is-operational"></a>手順 1: フェデレーションサーバーが動作可能であることを確認するには  
  
1.  インターネットインフォメーションサービス \(IIS\) がフェデレーションサーバーで正しく構成されていることを確認するには、フェデレーションサーバーと同じフォレストにあるクライアントコンピューターにログオンします。  
  
2.  ブラウザーウィンドウを開き、アドレスバーにフェデレーションサーバーの DNS ホスト名を入力し、新しいフェデレーションサーバーに/adfs/fs/federationserverservice.asmx を追加します。次に例を示します。  
  
    **https://fs1.fabrikam.com/adfs/fs/federationserverservice.asmx**  
  
3.  Enter キーを押し、フェデレーション サーバー コンピューターの次の手順を完了します。 **[この web サイトのセキュリティ証明書に問題があり]** ます というメッセージが表示された場合は、 **[このサイトの使用を続行する]** をクリックします。  
  
    期待される表示出力は、サービス内容に関する XML ドキュメントです。 このページが表示されたら、フェデレーション サーバーの IIS は動作可能であり、正常にページを提供します。  
  
この手順を完了するには、ローカル コンピューター上の **Administrators** または同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
### <a name="procedure-2-to-verify-that-a-federation-server-is-operational"></a>手順 2: フェデレーションサーバーが動作可能であることを確認するには  
  
1.  管理者として新しいフェデレーション サーバーにログオンします。  
  
2.  **[スタート]** 画面で、「**Event Viewer**」と入力して Enter キーを押します。  
  
3.  詳細ウィンドウで、**アプリケーションとサービスログ** をダブル\-クリックし、**イベント AD FS**の\-をダブルクリックして、**管理者** をクリックします。  
  
4.  **[イベント id]** 列で、イベント id 100 を探します。 フェデレーションサーバーが適切に構成されている場合は、イベントビューアーのアプリケーションログに、イベント ID 100 の新しいイベントが表示されます。 このイベントにより、フェデレーション サーバーがフェデレーション サービスと正常に通信できたことが確認されます。  
  
## <a name="additional-references"></a>その他の参照情報  
[チェックリスト: フェデレーションサーバーのセットアップ](Checklist--Setting-Up-a-Federation-Server.md)  
  

