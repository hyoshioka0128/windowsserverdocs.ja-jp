---
title: インストールに必要なハードウェアとデバイス ドライバーを収集する
description: MultiPoint Services をインストールする必要があるドライバーに関する情報
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: a9d902e2599cdcd69e156d1fabec87a067b1d8ea
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833423"
---
# <a name="collect-hardware-and-device-drivers-needed-for-the-installation"></a>インストールに必要なハードウェアとデバイス ドライバーを収集する
MultiPoint Services システムの展開を開始する前にする必要があります。  
  
-   **サーバーのハードウェア コンポーネント**-この時点で、追加のビデオ カードまたはその他のシステム コンポーネントをインストールします。  
  
-   **ステーションのハードウェア コンポーネント**については、環境の計画のステーションを参照してください - [MultiPoint Services システムのハードウェアを選択すると](Selecting-Hardware-for-Your-MultiPoint-services-System.md)します。
-   **ビデオ カードの最新のドライバー** -、OEM またはデバイス製造元では、これら提供しませんでした、デバイスの製造元の web サイトからダウンロードする必要があります。  
  
-   **最新の USB ゼロ クライアント ドライバー** -USB ゼロ クライアント ステーションを使用している場合は、最新の USB ゼロ クライアント ドライバーをインストールする必要があります。  
  
    > [!IMPORTANT]  
    > MultiPoint Services のインストールでは、すべてのドライバーの 64 ビット バージョンをインストールする必要があります。  
  
> [!TIP]  
> 別のバージョンの Windows を既にインストールされているコンピューターで MultiPoint Services をインストールする場合を調べますビデオ カードの製造元とモデル デバイス マネージャーで、Windows Server のインストールを開始してドライバーを取得することを確認する前にWindows Server 2016 で使用できます。 デバイス マネージャーを開き、開いている**コンピュータの管理**から、**開始**画面。 次に、コンソール ツリーで、クリックして**デバイス マネージャー**します。