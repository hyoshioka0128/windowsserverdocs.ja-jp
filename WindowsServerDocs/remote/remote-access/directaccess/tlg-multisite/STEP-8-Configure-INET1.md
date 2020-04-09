---
title: 手順 8. INET1 を構成する
description: このトピックは、「Windows Server 2016 用の DirectAccess マルチサイト展開のテストラボガイド」の一部です。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: 693acb5c-dffc-4484-8286-163bb67724c9
ms.author: coreyp
author: coreyp-at-msft
ms.openlocfilehash: ca8a49e612bef9c4a72c47e8d0e147a900686f84
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861545"
---
# <a name="step-8-configure-inet1"></a>手順 8: INET1 を構成する

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

クライアントコンピューターがインターネット経由でリモートアクセスサーバーに接続できるようにするには、INET1 で EDGE1 の DNS エントリを構成する必要があります。  
  
### <a name="to-create-the-2-edge1-dns-entry"></a>2 EDGE1 DNS エントリを作成するには  
  
1.  **スタート**画面で「**dnsmgmt.msc**」と入力し、enter キーを押します。  
  
2.  コンソールツリーで、 **[前方参照ゾーン]** を開き、 **[contoso.com]** をクリックします。次に、 **[contoso.com]** を右クリックし、 **[新しいホスト (A または AAAA)]** をクリックします。  
  
3.  **[名前]** に「 **2-EDGE1**」と入力します。 **[IP アドレス]** に、「 **131.107.0.20**」と入力します。 **[ホストの追加]** をクリックし、 **[OK]** をクリックして、 **[完了]** をクリックします。  
  


