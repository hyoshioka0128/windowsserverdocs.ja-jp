---
title: QoS のよく寄せられる質問
description: このトピックでは、Windows Server 2016 でのサービスの品質 (QoS) ポリシーに関する質問への回答を提供します。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 74c97a14-b957-4568-b48e-8963a674fdb3
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f9fb54cc3bda9a259188ae02fb2ef2836dd8718d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833753"
---
# <a name="qos-policy-frequently-asked-questions"></a>QoS ポリシーについてよく寄せられる質問

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

質問と回答 – QoS ポリシーのような質問に、次がよく寄せられます。
  
1.  **ドメイン コント ローラーで QoS ポリシーを使用して実行している必要があるのオペレーティング システムですか。**
  
     Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、または Windows Server 2008

2.  **どのようなオペレーティング システムでは、QoS ポリシーのアプリケーションのユーザーまたはコンピューターをサポートしますか。**

     ユーザーまたは Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8、Windows Server 2008 R2、Windows Server 2008、および Windows Vista を実行しているコンピューターには、QoS ポリシーを適用できます。

3.  **QoS ポリシーは送信者または受信者のトラフィックに適用されますか。**

     送信元のコンピューターにその送信トラフィックの影響を与える上 QoS ポリシーを適用する必要があります。 2 台のコンピューターの双方向のトラフィックの影響を与えたりするには、QoS ポリシーは、両方のコンピューターに適用する必要があります。

4.  **競合する QoS ポリシーは、同じコンピューターに展開するとどうなりますか。**  
  
     複数のポリシーが適用されます、特定の QoS ポリシーが優先されます。 たとえば、ホスト アドレス (192.168.4.12) を示すポリシーは、特定性の低いネットワーク アドレス (192.168.0.0/16) の代わりに適用されます。 コンピューター レベルおよびユーザー レベル ポリシーは、同じ特異性がある場合は、コンピューター レベルの QoS ポリシーではなく、ユーザー レベルの QoS ポリシーが適用されます。 

5.  **QoS ポリシーは既定で有効にしますか。**

     いいえ、QoS ポリシーは既定で有効になっていません。 QoS を有効にするには、手動で QoS ポリシーを作成する必要があります。  詳細については、次を参照してください。 [QoS ポリシーの管理](qos-policy-manage.md)します。

このガイドの最初のトピックを参照してください。[サービスの品質 (QoS) ポリシー](qos-policy-top.md)します。
