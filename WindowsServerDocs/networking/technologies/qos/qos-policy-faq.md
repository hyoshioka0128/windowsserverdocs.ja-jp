---
title: QoS のよく寄せられる質問
description: このトピックでは、Windows Server 2016 でのサービスの品質 (QoS) ポリシーに関する質問への回答を示します。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 74c97a14-b957-4568-b48e-8963a674fdb3
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e63cd00a2016411e9f2c532c0e4c301dabdfd816
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="qos-policy-frequently-asked-questions"></a>QoS ポリシーについてよく寄せられる質問

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

次は、– の質問と回答それらの質問に対する – QoS ポリシーに頻繁にように求められます。
  
1.  **どのようなオペレーティング システムの QoS ポリシーを使用して実行されているドメイン コントローラーが必要か。**
  
     Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、または Windows Server 2008

2.  **どのようなオペレーティング システムでは、QoS ポリシーのユーザーまたはコンピューターにアプリケーションをサポートしますか。**

     QoS ポリシーは、ユーザーまたは Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8、Windows Server 2008 R2、Windows Server 2008、および Windows Vista を実行しているコンピューターに適用できます。

3.  **QoS ポリシーは、送信者またはトラフィックの受信側には適用ですか。**

     QoS ポリシーは、その送信トラフィックに影響する送信元コンピューターに適用する必要があります。 2 台のコンピューターの双方向のトラフィックに影響するために、QoS ポリシーは、両方のコンピューターに適用する必要があります。

4.  **競合する QoS ポリシーが同じコンピューターに展開するとどうなりますか。**  
  
     複数のポリシーを適用する特定の QoS ポリシーが優先されます。 たとえば、ポリシーいるホストの状態に対処する (192.168.4.12) を適用するのではなく、特定性の低いネットワーク アドレス (192.168.0.0/16)。 コンピューター レベルとユーザー レベルのポリシーがある同じ特異性は、コンピューター レベルの QoS ポリシーではなく、ユーザー レベルの QoS ポリシーが適用されます。 

5.  **QoS ポリシーは既定で有効にしますか。**

     いいえ、QoS ポリシーは、既定では無効です。 QoS を有効にするには、手動で QoS ポリシーを作成する必要があります。  詳細については、次を参照してください。[QoS ポリシーの管理](qos-policy-manage.md)します。

このガイドで最初のトピックを参照してください。[サービスの品質 (QoS) ポリシー](qos-policy-top.md)します。
