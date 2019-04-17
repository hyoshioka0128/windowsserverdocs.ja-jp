---
ms.assetid: 10d6723e-c857-43da-9d2d-acb5641d3da8
title: "コンピューターをドメインに参加させる"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 641a1541143206d06973a6a0f11c689390abea21
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="join-a-computer-to-a-domain"></a>コンピューターをドメインに参加させる

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Active Directory フェデレーション サービスの \(AD FS\) 関数に、フェデレーション サーバーとして機能する各コンピューターをドメインに参加する必要があります。 フェデレーション サーバー プロキシは、ドメインに参加することがありますが、これは必須ではありません。  
  
Web サーバーでのみ claims\ に対応するアプリケーションをホストしている場合は、Web サーバーをドメインに参加する必要はありません。  
  
メンバーシップ**管理者**、相当するもので、ローカル コンピューターでは、この手順を完了するために必要な最低限またはします。  適切なアカウントの使用に関する詳細を確認し、グループ メンバーシップ[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
### <a name="to-join-a-computer-to-a-domain"></a>コンピューターをドメインに参加させる  
  
1.  **開始**画面で「**コントロール パネルの [**し、Enter キーを押します。  
  
2.  移動**システムとセキュリティ**、] をクリックし、**システム**します。  
  
3.  [**コンピューター名、ドメインおよびワークグループの設定**、] をクリックして**設定を変更する**します。  
  
4.  **コンピューター名**] タブ、[**変更**します。  
  
5.  [**のメンバー**、] をクリックして**ドメイン**、このコンピューターに参加し、[ドメインの名前を入力**OK**します。  
  
6.  をクリックして**OK**、コンピューターを再起動します。  
  
## <a name="additional-references"></a>その他の参照  
[チェックリスト: フェデレーション サーバーのセットアップ](Checklist--Setting-Up-a-Federation-Server.md)  
  
[チェックリスト: フェデレーション サーバー プロキシのセットアップ](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  

