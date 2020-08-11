---
title: Windows Server Version 1809 の新機能
description: Windows Server Version 1809 の新機能
ms.topic: article
author: jasongerend
ms.author: jgerend
ms.date: 05/21/2019
ms.localizationpriority: high
ms.openlocfilehash: cb3bf10b0c89f60a5cebb7109ebc4a7de46f8961
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87941641"
---
# <a name="whats-new-in-windows-server-version-1809"></a>Windows Server Version 1809 の新機能

>適用先:Windows Server (半期チャネル)

Windows の最新の機能については、「[Windows Server の新機能](whats-new-in-windows-server.md)」を参照してください。 このトピックでは、Windows Server Version 1809 の新機能の一部について説明します。

## <a name="container-networking-with-kubernetes"></a>Kubernetes を使用したコンテナー ネットワーク

Windows Server 2019 の [Kubernetes を使用したコンテナー ネットワーク](../networking/sdn/technologies/containers/container-networking-overview.md)機能により、プラットフォームのネットワーク回復性とコンテナー ネットワーク プラグインのサポートが強化され、Windows での Kubernetes の使いやすさが大幅に向上します。
さらに、ワークロードを Kubernetes に展開すると、ネットワーク セキュリティを使用して、埋め込みツールにより Linux と Windows の両方のサービスを保護できます。

## <a name="group-managed-service-accounts-for-containers"></a>コンテナー用グループ管理サービス アカウント

Windows Server Version 1809 では、グループ管理サービス アカウント (gMSA) を使用してネットワーク リソースにアクセスするコンテナーの拡張性と信頼性が向上しています。

## <a name="host-device-access-for-containers"></a>ホスト デバイスからコンテナーへのアクセス

プロセス分離された Windows Server のコンテナーには、単純なバスを割り当てることができます。
コンテナー内で実行されているアプリケーションは、必要であれば SPI、I2C、GPIO、UART/COM を使用して通信できるようになりました。

## <a name="additional-features"></a>追加機能
Windows Server Version 1809 の新機能のほか、[Windows Server 2019](../get-started-19/get-started-19.md) の次の新機能も Windows Server Version 1809 に適用されます。

* コンテナーの機能強化
* HTTP/2
* Kubernetes サポート
* Windows 上の Linux コンテナー
* [Low Extra Delay Background Transport (LEDBAT)](https://techcommunity.microsoft.com/t5/networking-blog/bg-p/NetworkingBlog)
* 仮想ワークロードに関するネットワーク パフォーマンスの向上
* [Server Core アプリ互換性オンデマンド機能 (FOD)](../get-started-19/install-fod-19.md)
* [ストレージ移行サービス (SMS)](../storage/whats-new-in-storage.md#storage-spaces-direct)
* 記憶域レプリカ
* システム インサイト
* Windows Defender Advanced Threat Protection (ATP)
* Windows Defender ATP Exploit Guard
* [Windows タイム サービス](../networking/windows-time-service/insider-preview.md)
