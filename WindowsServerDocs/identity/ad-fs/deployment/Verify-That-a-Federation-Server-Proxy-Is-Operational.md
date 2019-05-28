---
ms.assetid: d555041a-709e-42c7-920a-8dfd2c7e0488
title: フェデレーション サーバー プロキシが正常に動作していることを確認する
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 26b0ae4f331607d83c6b94a2655ddc9eded8a356
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66191868"
---
# <a name="verify-that-a-federation-server-proxy-is-operational"></a>フェデレーション サーバー プロキシが正常に動作していることを確認する


次の手順を使用するには、フェデレーション サーバー プロキシは、Active Directory フェデレーション サービスでフェデレーション サービスと通信できることを確認する\(AD FS\)します。 実行した後、この手順を実行する、 **AD FS フェデレーション サーバー プロキシ構成ウィザード**フェデレーション サーバー プロキシ ロールで実行するコンピューターを構成します。 このウィザードを実行する方法の詳細については、次を参照してください。 [、フェデレーション サーバー プロキシ ロール用コンピューターの構成](Configure-a-Computer-for-the-Federation-Server-Proxy-Role.md)します。  
  
> [!IMPORTANT]  
> このテスト結果は、フェデレーション サーバー プロキシ コンピューターのイベント ビューアーに、特定の成功イベントとして生成されます。  
  
この手順を実行するには、ローカル コンピューターの **Administrators**グループのメンバーシップか、それと同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
### <a name="to-verify-that-a-federation-server-proxy-is-operational"></a>フェデレーション サーバー プロキシが動作することを確認するには  
  
1.  管理者としてフェデレーション サーバー プロキシにログオンします。  
  
2.  **開始**画面で「**イベント ビューアー**し、ENTER キーを押します。  
  
3.  詳細ウィンドウでダブルクリック\-クリックして**Applications and Services Logs**、二重\- をクリックして**AD FS Eventing**、順にクリックします**管理者**。  
  
4.  **イベント ID**列で、イベント ID 198 を探します。  
  
    フェデレーション サーバー プロキシが正しく構成されている場合、イベント ID 198 のイベント ビューアーのアプリケーション ログに新しいイベントを参照してください。 このイベントは、フェデレーション サーバー プロキシ サービスが正常に開始し、現在はオンラインことを確認します。  
  
## <a name="additional-references"></a>その他の参照情報  
[チェックリスト:フェデレーション サーバー プロキシのセットアップ](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  

