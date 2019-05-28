---
ms.assetid: 10d6723e-c857-43da-9d2d-acb5641d3da8
title: コンピューターをドメインに参加させる
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 02df9659ee3a1121c0cee3f7c5fa21b91c36b87c
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192052"
---
# <a name="join-a-computer-to-a-domain"></a>コンピューターをドメインに参加させる

Active Directory フェデレーション サービスの\(AD FS\)に機能するようにフェデレーション サーバーをドメインに参加する必要がありますが機能する各コンピューターにします。 フェデレーション サーバー プロキシは、ドメインに参加させることがありますが、これは必須ではありません。  
  
Web サーバーが要求をホストしている場合は、Web サーバーをドメインに参加する必要はありません\-対応のアプリケーションのみです。  
  
この手順を実行するには、ローカル コンピューターの **Administrators**グループのメンバーシップか、それと同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
### <a name="to-join-a-computer-to-a-domain"></a>コンピューターをドメインに参加させる  
  
1.  **開始**画面で「**コントロール パネルの** し、ENTER キーを押します。  
  
2.  移動します**システムとセキュリティ**、 をクリックし、**システム**します。  
  
3.  **[コンピューター名、ドメインおよびワークグループの設定]** で **[設定の変更]** をクリックします。  
  
4.  **[コンピューター名]** タブで、 **[変更]** をクリックします。  
  
5.  [**のメンバー**、] をクリックして**ドメイン**、このコンピューターをクリックして、参加を希望するドメインの名前を入力**OK**します。  
  
6.  をクリックして**OK**、コンピューターを再起動します。  
  
## <a name="additional-references"></a>その他の参照情報  
[チェックリスト:フェデレーション サーバーのセットアップ](Checklist--Setting-Up-a-Federation-Server.md)  
  
[チェックリスト:フェデレーション サーバー プロキシのセットアップ](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  

