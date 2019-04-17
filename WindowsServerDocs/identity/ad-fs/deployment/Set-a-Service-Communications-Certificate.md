---
ms.assetid: 638c89bd-87e6-484b-9d2e-8ae2a74227e5
title: "サービス通信証明書を設定します。"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 0d630372d82cf1519da82397a9c90d6a28903ed0
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="set-a-service-communications-certificate"></a>サービス通信証明書を設定します。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Active Directory フェデレーション サービス \(AD FS\) 内のフェデレーション サーバーでは、サービス通信証明書を使用して、Web クライアントまたはフェデレーション サーバー プロキシの Secure Sockets Layer \(SSL\) 通信用の Web サービス トラフィックをセキュリティで保護します。 これは、インターネット インフォメーション サービス \(IIS\) で SSL 証明書としてフェデレーション サーバーを使用する同じ証明書です。  
  
AD FS 管理スナップインで、サービス通信証明書を変更するのには、次の手順を使用できます。  
  
> [!NOTE]  
> AD FS 管理スナップインでは、フェデレーション サーバーのサーバー認証証明書をサービス通信証明書と呼びます。  
  
メンバーシップ**管理者**、相当するもので、ローカル コンピューターでは、この手順を完了するために必要な最低限またはします。  適切なアカウントの使用に関する詳細を確認し、グループ メンバーシップ[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)\ (http:///\/go.microsoft.com\/fwlink\/ですか?LinkId\ = 83477\)。   
  
### <a name="to-set-a-service-communications-certificate"></a>サービス通信証明書を設定するには  
  
1.  **開始**画面で「**AD FS 管理**、し、Enter キーを押します。  
  
2.  コンソール ツリーで、ダブルクリック**サービス**、] をクリックし、**証明書**します。  
  
3.  **アクション**] ウィンドウで、をクリックして、**サービス通信証明書の設定**リンクします。  
  
4.  **サービス通信証明書を選択**] ダイアログ ボックスで、サービス通信証明書として設定、証明書ファイルを選択し、クリックする証明書ファイルを移動**開く**します。  
  
## <a name="additional-references"></a>その他の参照  
[チェックリスト: フェデレーション サーバーのセットアップ](Checklist--Setting-Up-a-Federation-Server.md)  
  
[フェデレーション サーバーの証明書の要件](https://technet.microsoft.com/library/dd807040.aspx)  
  

