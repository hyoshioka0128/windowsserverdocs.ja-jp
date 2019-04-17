---
ms.assetid: e1f2ce2d-b24f-4ccd-8add-9e69419fc6c1
title: "既定の Web サイトにサーバー認証証明書をインポートします。"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 7bc890c744de5cd86d4e8b0418e75512518f656c
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="import-a-server-authentication-certificate-to-the-default-web-site"></a>既定の Web サイトにサーバー認証証明書をインポートします。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

証明機関から、サーバー認証証明書を取得した後、\(CA\) 必要があります手動でインストールする証明書を各フェデレーション サーバーまたはサーバー ファームにフェデレーション サーバー プロキシの既定の Web サイトにします。  
  
Web サーバーでは、適切な Web サイトまたはフェデレーション アプリケーションの存在する仮想ディレクトリで、サーバー認証証明書を手動でインストールする必要があります。  
  
ファームをセットアップする場合は、同じようにこの手順を実行することを確認する —、まったく同じ設定を使用して、、ファーム内のサーバーの各します。  
  
> [!NOTE]  
> AD FS 管理スナップインでは、フェデレーション サーバーのサーバー認証証明書をサービス通信証明書と呼びます。  
  
メンバーシップ**管理者**、相当するもので、ローカル コンピューターでは、この手順を完了するために必要な最低限またはします。  適切なアカウントの使用に関する詳細を確認し、グループ メンバーシップ[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
### <a name="to-import-a-server-authentication-certificate-to-the-default-web-site"></a>既定の Web サイトにサーバー認証証明書をインポートするには  
  
1.  **開始**画面で「**インターネット インフォメーション サービス \(IIS\) Manager**、し、ENTER キーを押します。  
  
2.  コンソール ツリーでクリックして**ComputerName**します。  
  
3.  中央のウィンドウでダブルクリック**サーバー証明書**します。  
  
4.  **アクション**] ウィンドウで、をクリックして**インポート**します。  
  
5.  **証明書のインポート**ダイアログ ボックスで、をクリックして、 **.** ボタンをクリックします。  
  
6.  Pfx 証明書ファイルの場所を参照し、[強調表示して、[クリックして**開く**します。  
  
7.  証明書のパスワードを入力し、をクリックして**OK**します。  
  
## <a name="additional-references"></a>その他の参照  
[チェックリスト: フェデレーション サーバーのセットアップ](Checklist--Setting-Up-a-Federation-Server.md)  
  
[チェックリスト: フェデレーション サーバー プロキシのセットアップ](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[フェデレーション サーバーの証明書の要件](https://technet.microsoft.com/library/dd807040.aspx)  
  
[フェデレーション サーバー プロキシの証明書の要件](https://technet.microsoft.com/library/dd807054.aspx)  
   
  

