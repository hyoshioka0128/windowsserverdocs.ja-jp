---
ms.assetid: e1f2ce2d-b24f-4ccd-8add-9e69419fc6c1
title: サーバー認証証明書を既定の Web サイトにインポートする
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 7bc890c744de5cd86d4e8b0418e75512518f656c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59880943"
---
# <a name="import-a-server-authentication-certificate-to-the-default-web-site"></a>サーバー認証証明書を既定の Web サイトにインポートする

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

証明機関から、サーバー認証証明書を取得した後\(CA\)、する必要があります手動でインストールする証明書を各フェデレーション サーバーまたはサーバー ファームにフェデレーション サーバー プロキシの既定の Web サイトにします。  
  
Web サーバーの場合、適切な Web サイトまたはフェデレーション アプリケーションが常駐する仮想ディレクトリに、サーバー認証証明書を手動でインストールする必要があります。  
  
ファームをセットアップする場合は、ファーム内の各サーバー上で、まったく同じ設定を使って、この同じ手順を実行してください。  
  
> [!NOTE]  
> AD FS 管理スナップイン\-サービス通信証明書としてフェデレーション サーバーのサーバー認証証明書を参照しています。  
  
この手順を実行するには、ローカル コンピューターの **Administrators**グループのメンバーシップか、それと同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
### <a name="to-import-a-server-authentication-certificate-to-the-default-web-site"></a>サーバー認証証明書を既定の Web サイトにインポートするには  
  
1.  **開始**画面で「**インターネット インフォメーション サービス\(IIS\) Manager**、し、ENTER キーを押します。  
  
2.  コンソール ツリーで、**[コンピューター名]** をクリックします。  
  
3.  中央のウィンドウでダブルクリック\-クリックして**サーバー証明書**します。  
  
4.  **[操作]** ウィンドウで、**[インポート]** をクリックします。  
  
5.  **証明書のインポート**ダイアログ ボックスで、をクリックして、 **.** ボタンをクリックします。  
  
6.  pfx 証明書ファイルのある場所に移動し、ファイルを強調表示して、**[開く]** をクリックします。  
  
7.  証明書のパスワードを入力し、**[OK]** をクリックします。  
  
## <a name="additional-references"></a>その他の参照情報  
[チェックリスト:フェデレーション サーバーを設定します。](Checklist--Setting-Up-a-Federation-Server.md)  
  
[チェックリスト:フェデレーション サーバー プロキシを設定します。](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[フェデレーション サーバーの証明書の要件](https://technet.microsoft.com/library/dd807040.aspx)  
  
[フェデレーション サーバー プロキシの証明書の要件](https://technet.microsoft.com/library/dd807054.aspx)  
   
  

