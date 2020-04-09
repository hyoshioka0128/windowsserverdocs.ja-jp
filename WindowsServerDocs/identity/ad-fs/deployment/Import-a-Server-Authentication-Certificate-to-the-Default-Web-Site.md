---
ms.assetid: e1f2ce2d-b24f-4ccd-8add-9e69419fc6c1
title: サーバー認証証明書を既定の Web サイトにインポートする
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 3f02358167b024247f934a46218028575e393ba9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855405"
---
# <a name="import-a-server-authentication-certificate-to-the-default-web-site"></a>サーバー認証証明書を既定の Web サイトにインポートする

証明機関 \(CA\)からサーバー認証証明書を取得した後、サーバーファーム内の各フェデレーションサーバーまたはフェデレーションサーバープロキシの既定の Web サイトにその証明書を手動でインストールする必要があります。  
  
Web サーバーの場合、適切な Web サイトまたはフェデレーション アプリケーションが常駐する仮想ディレクトリに、サーバー認証証明書を手動でインストールする必要があります。  
  
ファームをセットアップする場合は、ファーム内の各サーバー上で、まったく同じ設定を使って、この同じ手順を実行してください。  
  
> [!NOTE]  
> の AD FS 管理スナップ\-は、サービス通信証明書としてのフェデレーションサーバーのサーバー認証証明書を参照します。  
  
この手順を完了するには、ローカル コンピューター上の **Administrators** または同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
### <a name="to-import-a-server-authentication-certificate-to-the-default-web-site"></a>サーバー認証証明書を既定の Web サイトにインポートするには  
  
1.  **[スタート]** 画面で、「**インターネットインフォメーションサービス \(IIS\) Manager**」と入力し、enter キーを押します。  
  
2.  コンソール ツリーで、 **[コンピューター名]** をクリックします。  
  
3.  中央のウィンドウで、 **[サーバー証明書]** をダブル\-クリックします。  
  
4.  **[アクション]** ペインで、 **[インポート]** をクリックします。  
  
5.  **[証明書のインポート]** ダイアログボックスで、. **[.]** をクリックします。 ボタンをクリックします。  
  
6.  pfx 証明書ファイルの場所に移動し、ファイルを強調表示し、 **[開く]** をクリックします。  
  
7.  証明書のパスワードを入力し、 **[OK]** をクリックします。  
  
## <a name="additional-references"></a>その他の参照情報  
[チェックリスト: フェデレーションサーバーのセットアップ](Checklist--Setting-Up-a-Federation-Server.md)  
  
[チェックリスト: フェデレーションサーバープロキシの設定](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[フェデレーション サーバーの証明書の要件](https://technet.microsoft.com/library/dd807040.aspx)  
  
[フェデレーション サーバー プロキシの証明書の要件](https://technet.microsoft.com/library/dd807054.aspx)  
   
  

