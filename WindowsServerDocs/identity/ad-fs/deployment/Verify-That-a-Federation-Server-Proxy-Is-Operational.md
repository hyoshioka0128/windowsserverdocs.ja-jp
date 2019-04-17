---
ms.assetid: d555041a-709e-42c7-920a-8dfd2c7e0488
title: "フェデレーション サーバー プロキシが動作可能であることを確認します。"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 4900d8621b94a514a07bba55b2f7f3df5dd36353
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="verify-that-a-federation-server-proxy-is-operational"></a>フェデレーション サーバー プロキシが動作可能であることを確認します。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

次の手順を使用すると、フェデレーション サーバー プロキシは、Active Directory フェデレーション サービス \(AD FS\) 内のフェデレーション サービスと通信できることを確認します。 実行した後、この手順を実行する、 **AD FS フェデレーション サーバー プロキシ構成ウィザード**、フェデレーション サーバー プロキシの役割を実行するコンピューターを構成します。 このウィザードを実行する方法の詳細については、次を参照してください。 [for Federation Server Proxy Role Configure a Computer](Configure-a-Computer-for-the-Federation-Server-Proxy-Role.md)します。  
  
> [!IMPORTANT]  
> このテストの結果は、イベント ビューアーで、フェデレーション サーバー プロキシ コンピューターの特定のイベントが正しく生成です。  
  
メンバーシップ**管理者**、相当するもので、ローカル コンピューターでは、この手順を完了するために必要な最低限またはします。  適切なアカウントの使用に関する詳細を確認し、グループ メンバーシップ[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
### <a name="to-verify-that-a-federation-server-proxy-is-operational"></a>フェデレーション サーバー プロキシが動作可能であることを確認するには  
  
1.  管理者としてフェデレーション サーバー プロキシにログオンします。  
  
2.  **開始**画面で「**イベント ビューアー**し、ENTER キーを押します。  
  
3.  詳細ウィンドウで、ダブルクリック**アプリケーションとサービス ログ**をダブルクリック**AD FS イベント**、] をクリックし、 **Admin**します。  
  
4.  **イベント ID**列で、イベント ID 198 を探します。  
  
    フェデレーション サーバー プロキシが正しく構成されている場合、イベント ID が 198 のイベント ビューアーのアプリケーション ログに新しいイベントを参照してください。 このイベントは、フェデレーション サーバー プロキシ サービスが正常に起動し、現在はオンラインことを確認します。  
  
## <a name="additional-references"></a>その他の参照  
[チェックリスト: フェデレーション サーバー プロキシのセットアップ](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  

