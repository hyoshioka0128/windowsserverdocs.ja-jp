---
title: 手順 8 INET1 を構成します。
description: このトピックは一部のテスト ラボ ガイド-DirectAccess マルチサイト展開の Windows Server 2016 のデモンストレーション
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 693acb5c-dffc-4484-8286-163bb67724c9
ms.author: coreyp
author: coreyp-at-msft
ms.openlocfilehash: 707591604a1d030b3abba9395081d2c2e4b7fb1c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838813"
---
# <a name="step-8-configure-inet1"></a>手順 8:INET1 を構成します。

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

インターネット経由でリモート アクセス サーバーに接続するクライアント コンピューターを有効にする、INET1 で 2 EDGE1 の DNS エントリを構成する必要があります。  
  
### <a name="to-create-the-2-edge1-dns-entry"></a>2 EDGE1 の DNS エントリを作成するには  
  
1.  **開始**画面で「**dnsmgmt.msc**、し、ENTER キーを押します。  
  
2.  コンソール ツリーで開く**前方参照ゾーン**、 をクリックして**contoso.com**、右クリックし、 **contoso.com**、順にクリックします**新しいホスト (A または AAAA)**.  
  
3.  **名前**、型**2 EDGE1**します。 **IP アドレス**、型**131.107.0.20**します。 **[ホストの追加]** をクリックし、**[OK]** をクリックして、**[完了]** をクリックします。  
  


