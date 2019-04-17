---
ms.assetid: 1115d276-00f6-4c23-9278-eedcc31295d8
title: "Windows Server 2012 R2 フェデレーション サーバーが稼働中であることを確認します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 2df8a00a953196d7ca19ea0d164abbbf6eefd829
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="verify-your-windows-server-2012-r2-federation-server-is-operational"></a>Windows Server 2012 R2 フェデレーション サーバーが稼働中であることを確認します。

>適用対象: Windows Server 2016、Windows Server 2012 R2

次の手順を使用するには、フェデレーション サーバーが運用; であることを確認するにはつまり、同じネットワーク上のどのクライアントが新しいフェデレーション サーバーに到達できること。  
  
メンバーシップ**ユーザー**、 **Backup Operators**、 **Power Users**、**管理者**相当するもので、ローカル コンピューターでは、この手順を完了するために必要な最低限またはします。  適切なアカウントの使用に関する詳細を確認し、グループ メンバーシップ[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
### <a name="procedure-1-to-verify-that-a-federation-server-is-operational"></a>手順 1: フェデレーション サーバーが動作可能であることを確認するには  
  
1.  フェデレーション サーバーで、インターネット インフォメーション サービス \(IIS\) が正しく構成されていることを確認するには、フェデレーション サーバーと同じフォレストに配置されているクライアント コンピューターにログオンします。  
  
2.  ブラウザー ウィンドウを開き、アドレス バーの種類、フェデレーション サーバーの DNS ホスト名、およびし \/adfs\/fs\/federationserverservice.asmx に追加して、新しいフェデレーション サーバーの例。  
  
    **https:\/\/fs1.fabrikam.com\/adfs\/fs\/federationserverservice.asmx**  
  
3.  キーを押しし、フェデレーション サーバー コンピューターで、次の手順を完了します。 メッセージが表示された場合**この web サイトのセキュリティ証明書に問題がある**、] をクリックして**この web サイトにあっても続行**します。  
  
    想定される出力は、サービスの説明のドキュメントと XML の表示です。 このページが表示されたら、サービスを提供して、運用上のページが正常には、フェデレーション サーバーの IIS です。  
  
メンバーシップ**管理者**、相当するもので、ローカル コンピューターでは、この手順を完了するために必要な最低限またはします。  適切なアカウントの使用に関する詳細を確認し、グループ メンバーシップ[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
### <a name="procedure-2-to-verify-that-a-federation-server-is-operational"></a>手順 2: フェデレーション サーバーが動作可能であることを確認するには  
  
1.  新しいフェデレーション サーバーに管理者としてログオンします。  
  
2.  **開始**画面で「**イベント ビューアー**し、ENTER キーを押します。  
  
3.  詳細ウィンドウで、ダブルクリック**アプリケーションとサービス ログ**をダブルクリック**AD FS イベント**、] をクリックし、 **Admin**します。  
  
4.  **イベント ID**列で、イベント ID が 100 を探します。 新しいイベントを参照してください、フェデレーション サーバーが正しく構成されている場合、イベント ビューアーのアプリケーション ログに: イベント ID が 100 にします。 このイベントは、フェデレーション サーバーが、フェデレーション サービスと正常に通信できたことを確認します。  
  
## <a name="see-also"></a>参照してください。 

[AD FS の展開](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS 展開ガイドします。](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[フェデレーション サーバー ファームを展開します。](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
   
  

