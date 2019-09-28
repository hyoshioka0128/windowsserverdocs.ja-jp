---
title: インストールに必要なハードウェアとデバイス ドライバーを収集する
description: MultiPoint Services にインストールする必要があるドライバーに関する情報
ms.custom: na
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4cf5fdbe-b871-4360-b003-d65ac43b491e
author: evaseydl
manager: scottman
ms.author: evas
ms.date: 08/04/2016
ms.openlocfilehash: cfbb8c8b68768c72b869df539c93f05e7e01d256
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71394697"
---
# <a name="collect-hardware-and-device-drivers-needed-for-the-installation"></a>インストールに必要なハードウェアとデバイス ドライバーを収集する
MultiPoint Services システムの展開を開始する前に、次のものが必要です。  
  
-   **サーバーのハードウェアコンポーネント**-この時点で、追加のビデオカードまたはその他のシステムコンポーネントをインストールします。  
  
-   **ステーションのハードウェアコンポーネント**-環境のステーションを計画する方法については、「 [MultiPoint Services システムのハードウェアの選択](Selecting-Hardware-for-Your-MultiPoint-services-System.md)」を参照してください。
-   **ビデオカードの最新のドライバー** -OEM またはデバイスの製造元がこれらを提供していない場合は、デバイスの製造元の web サイトからダウンロードする必要があります。  
  
-   **最新の usb ゼロクライアントドライバー** -usb ゼロクライアントステーションを使用している場合は、最新の usb ゼロクライアントドライバーをインストールする必要があります。  
  
    > [!IMPORTANT]  
    > MultiPoint Services をインストールするには、64ビット版のドライバーをインストールする必要があります。  
  
> [!TIP]  
> 異なるバージョンの Windows が既にインストールされているコンピューターに MultiPoint Services をインストールする場合は、Windows Server のインストールを開始する前に、ビデオカードの製造元とモデルをデバイスマネージャーして、ドライバーを取得できることを確認する必要があります。Windows Server 2016 で使用できます。 デバイスマネージャーを開き、**スタート**画面から **[コンピューターの管理]** を開きます。 次に、コンソールツリーで、 **[デバイスマネージャー]** をクリックします。