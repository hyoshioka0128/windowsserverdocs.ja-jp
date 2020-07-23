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
ms.openlocfilehash: 3205085f11f84d96513d31da6dbe0853c686429f
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86960034"
---
# <a name="import-a-server-authentication-certificate-to-the-default-web-site"></a>サーバー認証証明書を既定の Web サイトにインポートする

証明機関の CA からサーバー認証証明書を取得した後 \( \) 、サーバーファーム内の各フェデレーションサーバーまたはフェデレーションサーバープロキシの既定の Web サイトに、その証明書を手動でインストールする必要があります。  
  
Web サーバーの場合、適切な Web サイトまたはフェデレーション アプリケーションが常駐する仮想ディレクトリに、サーバー認証証明書を手動でインストールする必要があります。  
  
ファームをセットアップする場合は、ファーム内の各サーバー上で、まったく同じ設定を使って、この同じ手順を実行してください。  
  
> [!NOTE]  
> AD FS 管理スナップインは、 \- サービス通信証明書としてのフェデレーションサーバーのサーバー認証証明書を参照します。  
  
この手順を完了するには、ローカル コンピューター上の **Administrators** または同等のメンバーシップが最低限必要です。  適切なアカウントおよびグループメンバーシップの使用方法の詳細については、「[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)」を参照してください。   
  
### <a name="to-import-a-server-authentication-certificate-to-the-default-web-site"></a>サーバー認証証明書を既定の Web サイトにインポートするには  
  
1.  **スタート**画面で、「**インターネットインフォメーションサービス \( IIS \) Manager**」と入力し、enter キーを押します。  
  
2.  コンソール ツリーで、[**コンピューター名**] をクリックします。  
  
3.  中央のウィンドウで、 \- [**サーバー証明書**] をダブルクリックします。  
  
4.  [**アクション**] ペインで、[**インポート**] をクリックします。  
  
5.  [**証明書のインポート**] ダイアログボックスで、[.. **.** ] をクリックします。 ボタンを選択します。  
  
6.  pfx 証明書ファイルの場所に移動し、ファイルを強調表示し、[**開く**] をクリックします。  
  
7.  証明書のパスワードを入力し、[**OK**] をクリックします。  
  
## <a name="additional-references"></a>その他のリファレンス  
[チェックリスト:フェデレーション サーバーのセットアップ](Checklist--Setting-Up-a-Federation-Server.md)  
  
[チェックリスト:フェデレーション サーバー プロキシのセットアップ](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[フェデレーション サーバーの証明書の要件](../design/certificate-requirements-for-federation-servers.md)  
  
[フェデレーション サーバー プロキシの証明書の要件](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807054(v=ws.11))  
   
  
