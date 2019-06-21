---
title: 手順 4 は、クラスターを確認します。
description: このトピックでは、Windows Server 2016 でのクラスターでのリモート アクセスの展開ガイドの一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f22dcf10-b453-4664-a9ef-e40e95c72f63
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 424c4f881c168ea691dd51cd2d86a4a234c41075
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67282988"
---
# <a name="step-4-verify-the-cluster"></a>手順 4 は、クラスターを確認します。

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

このトピックでは、DirectAccess クラスター展開が正しく構成されていることを確認する方法について説明します。  
  
### <a name="to-verify-access-to-internal-resources-through-the-cluster"></a>クラスターを通じた内部リソースへのアクセスを確認するには  
  
1.  DirectAccess クライアント コンピューターを企業ネットワークに接続し、グループ ポリシーを取得します。  
  
2.  クライアント コンピューターを外部ネットワークに接続して、内部リソースへのアクセスを試行します。  
  
    すべての企業リソースにアクセスできます。  
  
3.  オフ、または、クラスター サーバーの 1 つを除くすべての外部ネットワークから切断して、クラスター内の各サーバー経由で接続をテストします。 クライアント コンピューターでは、企業リソースにアクセスしようとします。 別のクラスター サーバーでテストを繰り返します。  
  
    各クラスター サーバーですべての企業リソースにアクセスできる必要があります。  
  


