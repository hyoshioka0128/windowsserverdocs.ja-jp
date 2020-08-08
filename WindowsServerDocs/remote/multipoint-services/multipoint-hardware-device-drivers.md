---
title: インストールに必要なハードウェアとデバイスのドライバーを収集します。
description: MultiPoint Services にインストールする必要があるドライバーに関する情報
ms.topic: article
ms.assetid: 4cf5fdbe-b871-4360-b003-d65ac43b491e
author: evaseydl
manager: scottman
ms.author: evas
ms.date: 08/04/2016
ms.openlocfilehash: d66c7fe216d5c2503f536e387b4e013e74092745
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87992778"
---
# <a name="collect-hardware-and-device-drivers-needed-for-the-installation"></a>インストールに必要なハードウェアとデバイスのドライバーを収集します。
MultiPoint Services システムの展開を開始する前に、次のものが必要です。

-   **サーバーのハードウェアコンポーネント**-この時点で、追加のビデオカードまたはその他のシステムコンポーネントをインストールします。

-   **ステーションのハードウェアコンポーネント**-環境のステーションを計画する方法については、「 [MultiPoint Services システムのハードウェアの選択](./select-hardware-mps.md)」を参照してください。
-   **ビデオカードの最新のドライバー** -OEM またはデバイスの製造元がこれらを提供していない場合は、デバイスの製造元の web サイトからダウンロードする必要があります。

-   **最新の usb ゼロクライアントドライバー** -usb ゼロクライアントステーションを使用している場合は、最新の usb ゼロクライアントドライバーをインストールする必要があります。

    > [!IMPORTANT]
    > MultiPoint Services をインストールするには、64ビット版のドライバーをインストールする必要があります。

> [!TIP]
> 異なるバージョンの Windows が既にインストールされているコンピューターに MultiPoint Services をインストールする場合は、Windows Server のインストールを開始する前に、デバイスマネージャーのビデオカードの製造元とモデルを確認して、Windows Server 2016 で使用可能なドライバーを取得できるようにする必要があります。 デバイスマネージャーを開き、**スタート**画面から [**コンピューターの管理**] を開きます。 次に、コンソールツリーで、[**デバイスマネージャー**] をクリックします。