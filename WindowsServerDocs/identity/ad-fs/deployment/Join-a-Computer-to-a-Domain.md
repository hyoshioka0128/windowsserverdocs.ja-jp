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
ms.openlocfilehash: 811f5296143637974cf82e59d57665f8a96f1c8c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59884113"
---
# <a name="join-a-computer-to-a-domain"></a>コンピューターをドメインに参加させる

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

Active Directory フェデレーション サービスの\(AD FS\)に機能するようにフェデレーション サーバーをドメインに参加する必要がありますが機能する各コンピューターにします。 フェデレーション サーバー プロキシは、ドメインに参加させることがありますが、これは必須ではありません。  
  
Web サーバーが要求をホストしている場合は、Web サーバーをドメインに参加する必要はありません\-対応のアプリケーションのみです。  
  
この手順を実行するには、ローカル コンピューターの **Administrators**グループのメンバーシップか、それと同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
### <a name="to-join-a-computer-to-a-domain"></a>コンピューターをドメインに参加させる  
  
1.  **開始**画面で「**コントロール パネルの **し、ENTER キーを押します。  
  
2.  移動します**システムとセキュリティ**、 をクリックし、**システム**します。  
  
3.  **[コンピューター名、ドメインおよびワークグループの設定]** で **[設定の変更]** をクリックします。  
  
4.  **[コンピューター名]** タブで、 **[変更]** をクリックします。  
  
5.  [**のメンバー**、] をクリックして**ドメイン**、このコンピューターをクリックして、参加を希望するドメインの名前を入力**OK**します。  
  
6.  をクリックして**OK**、コンピューターを再起動します。  
  
## <a name="additional-references"></a>その他の参照情報  
[チェックリスト:フェデレーション サーバーを設定します。](Checklist--Setting-Up-a-Federation-Server.md)  
  
[チェックリスト:フェデレーション サーバー プロキシを設定します。](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  

