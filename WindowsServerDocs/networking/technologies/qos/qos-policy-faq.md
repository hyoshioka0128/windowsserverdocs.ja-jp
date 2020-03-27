---
title: QoS に関してよく寄せられる質問
description: このトピックでは、Windows Server 2016 のサービス品質 (QoS) ポリシーに関する質問への回答を示します。
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 74c97a14-b957-4568-b48e-8963a674fdb3
manager: brianlic
ms.author: lizross
author: eross-msft
ms.openlocfilehash: a2b0990bd1416032cd519c60878c389f391e053d
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80315534"
---
# <a name="qos-policy-frequently-asked-questions"></a>QoS ポリシーに関してよく寄せられる質問

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

次に、QoS ポリシーに関してよく寄せられる質問とその回答を示します。
  
1.  **QoS ポリシーを使用するには、ドメインコントローラーを実行する必要があるオペレーティングシステムを指定してください。**
  
     Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、または Windows Server 2008

2.  **ユーザーまたはコンピューターへの QoS ポリシーの適用は、どのオペレーティングシステムでサポートされていますか。**

     QoS ポリシーは、Windows Server 2016、Windows 10、Windows Server 2012 R2、Windows 8.1、Windows Server 2012、Windows 8、Windows Server 2008 R2、Windows Server 2008、および Windows Vista を実行しているユーザーまたはコンピューターに適用できます。

3.  **QoS ポリシーは、トラフィックの送信側または受信側に適用されますか。**

     送信トラフィックに影響を与えるには、QoS ポリシーを送信側のコンピューターに適用する必要があります。 2台のコンピューターの双方向トラフィックに影響を与えるには、QoS ポリシーを両方のコンピューターに適用する必要があります。

4.  **競合する QoS ポリシーが同じコンピューターに展開されるとどうなりますか。**  
  
     複数のポリシーが適用されると、より具体的な QoS ポリシーが優先されます。 たとえば、特定のネットワークアドレス (192.168.0.0/16) ではなく、ホストアドレス (192.168.4.12) を示すポリシーが適用されます。 コンピューターレベルとユーザーレベルのポリシーの特異性が同じである場合は、コンピューターレベルの QoS ポリシーではなく、ユーザーレベルの QoS ポリシーが適用されます。 

5.  **QoS ポリシーは既定で有効になっていますか?**

     いいえ、QoS ポリシーは既定では有効になっていません。 Qos ポリシーを有効にするには、手動で QoS ポリシーを作成する必要があります。  詳細については、「 [QoS ポリシーの管理](qos-policy-manage.md)」を参照してください。

このガイドの最初のトピックについては、「[サービスの品質 (QoS) ポリシー](qos-policy-top.md)」を参照してください。
