---
title: 手順 8. INET1 を構成する
description: このトピックは、「Windows Server 2016 用の DirectAccess マルチサイト展開のテストラボガイド」の一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 693acb5c-dffc-4484-8286-163bb67724c9
ms.author: coreyp
author: coreyp-at-msft
ms.openlocfilehash: 54674adc33f45a58f2515d07fed4c8a070ded5a1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404708"
---
# <a name="step-8-configure-inet1"></a>手順 8:INET1 を構成する

>適用先:Windows Server (半期チャネル)、Windows Server 2016

クライアントコンピューターがインターネット経由でリモートアクセスサーバーに接続できるようにするには、INET1 で EDGE1 の DNS エントリを構成する必要があります。  
  
### <a name="to-create-the-2-edge1-dns-entry"></a>2 EDGE1 DNS エントリを作成するには  
  
1.  **スタート**画面で「**dnsmgmt.msc**」と入力し、enter キーを押します。  
  
2.  コンソールツリーで、 **[前方参照ゾーン]** を開き、 **[contoso.com]** をクリックします。次に、 **[contoso.com]** を右クリックし、 **[新しいホスト (A または AAAA)]** をクリックします。  
  
3.  **[名前]** に「 **2-EDGE1**」と入力します。 **[IP アドレス]** に、「 **131.107.0.20**」と入力します。 **[ホストの追加]** をクリックし、 **[OK]** をクリックして、 **[完了]** をクリックします。  
  


