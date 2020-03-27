---
title: マルチサイト展開を計画する
description: このトピックは、「Windows Server 2016 のマルチサイト展開に複数のリモートアクセスサーバーを展開する」の一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8387eabe-7363-4367-b5b1-03c67baa2933
ms.author: lizross
author: eross-msft
ms.openlocfilehash: d5c189969c31ef9627dd7daee0e09162ea9aec39
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80313874"
---
# <a name="plan-a-multisite-deployment"></a>マルチサイト展開を計画する

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

 Windows Server 2016、Windows Server 2012 では、DirectAccess とルーティングとリモートアクセスサービス (RRAS) VPN を1つのリモートアクセスの役割に結合しています。 この概要では、マルチサイト構成で Windows Server 2016 または Windows Server 2012 のリモートアクセスを展開するために必要な計画手順について説明します。  
  
1.  [詳細設定を使用して単一の DirectAccess サーバーを展開](https://technet.microsoft.com/library/hh831436(v=ws.11).aspx)します。 この手順には、単一のサーバーを展開するために必要なインフラストラクチャの計画が含まれます。 これには、ネットワークとサーバーの設定、証明書の要件、DNS 設定、ネットワークロケーションサーバーの展開、DirectAccess 管理サーバー、Active Directory 設定、グループポリシーオブジェクト (Gpo) の計画が含まれます。  
  
2.  [手順2マルチサイトインフラストラクチャを計画](Step-2-Plan-the-Multisite-Infrastructure.md)します。 この手順には、Active Directory と GPO の計画、および DNS の構成が含まれます。  
  
3.  [手順 3. マルチサイト展開を計画](Step-3-Plan-the-Multisite-Deployment.md)します。 この手順には、証明書の設定、ネットワークロケーションサーバーの構成、クライアントのエントリポイントの設定、IPv6 プレフィックスの設定、および必要に応じてグローバル負荷分散の設定が含まれます。  
  
> [!NOTE]  
> リモートアクセスの高度な展開の計画に関する決定事項を記録します。 このレコードは、展開の手順の完了にかかわる全員がジョブエイドとして使用できます。  
  
これらの計画手順を完了したら、「[マルチサイト展開の構成](../configure/Configure-a-Multisite-Deployment.md)」を参照してください。  
  


