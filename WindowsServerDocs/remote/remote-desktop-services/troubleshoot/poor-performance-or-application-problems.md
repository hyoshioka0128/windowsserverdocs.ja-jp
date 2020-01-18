---
title: リモート デスクトップ接続時のパフォーマンスの低下またはアプリケーションの問題
description: リモート デスクトップ接続時のパフォーマンスの低下またはアプリケーションの問題のトラブルシューティング。
audience: itpro
ms.custom: na
ms.reviewer: rklemen
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: troubleshooting
ms.assetid: ''
author: kaushika-msft
manager: dcscontentpm
ms.author: delhan
ms.date: 07/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: bcf2c8163123cbb71162f8ee44d283c532bd01a8
ms.sourcegitcommit: c5709021aa98abd075d7a8f912d4fd2263db8803
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/18/2020
ms.locfileid: "76265924"
---
# <a name="poor-performance-or-application-problems-during-remote-desktop-connection"></a>リモート デスクトップ接続時のパフォーマンスの低下またはアプリケーションの問題

この記事では、ユーザーがリモート デスクトップ機能を使うときに発生する可能性があるいくつかの一般的な問題について説明します。

### <a name="intermittent-problems-with-new-microsoft-azure-virtual-machines"></a>新しい Microsoft Azure 仮想マシンでの断続的な問題

この問題は、最近プロビジョニングされた仮想マシンに影響します。 ユーザーが仮想マシンに接続した後、リモート デスクトップ セッションにおいてユーザーの一部の設定が正しく読み込まれません。

この問題を回避するには、仮想マシンから切断し、少なくとも 20 分間待ってから、再接続します。

この問題を解決するには、必要に応じて、次の更新プログラムを仮想マシンに適用します。

  - Windows 10 および Windows Server 2016: KB 4343884、[2018 年 8 月 30 日 — KB4343884 (OS ビルド 14393.2457)](https://support.microsoft.com/help/4343884/windows-10-update-kb4343884)
  - Windows Server 2012 R2KB 4343891、[2018 年 8 月 30 日 — KB4343891 (マンスリー ロールアップのプレビュー)](https://support.microsoft.com/help/4343891/windows-81-update-kb4343891)

### <a name="video-playback-issues-on-windows-10-version-1709"></a>Windows 10 バージョン 1709 でのビデオ再生の問題

この問題は、Windows 10 バージョン 1709 が実行されているリモート コンピューターにユーザーが接続すると発生します。 これらのユーザーが VMR9 (Video Mixing Renderer 9) コーデックを使ってビデオを再生すると、プレーヤーに黒いウィンドウだけが表示されます。

これは、Windows 10 バージョン 1709 での既知の問題です。 この問題は、Windows 10 バージョン 1703 では発生しません。

### <a name="desktop-sharing-issues-on-windows-10"></a>Windows 10 でのデスクトップ共有の問題

この問題は、ユーザーがキオスク シナリオのように読み取り専用のユーザー プロファイル (および関連するレジストリ ハイブ) を使用している場合に発生します。 このようなユーザーは、Windows 10 バージョン 1803 が実行されているリモート コンピューターに接続すると、自分のデスクトップを共有できません。

この問題を解決するには、Windows 10 更新プログラム 4340917、[2018 年 7 月 24 日 — KB4340917 (OS ビルド 17134.191)](https://support.microsoft.com/help/4340917/windows-10-update-kb4340917) を適用します。

### <a name="performance-issues-when-mixing-versions-of-windows-10-if-nla-is-disabled"></a>NLA が無効になっている場合に Windows 10 のバージョンが混在するときのパフォーマンスの問題

この問題は、NLA が無効になっているときに、Windows 10 が実行されているリモート デスクトップ クライアント コンピューターで、異なるバージョンの Windows 10 が実行されているリモート デスクトップに接続すると発生します。 Windows 10 バージョン 1709 以前が実行されているコンピューターのリモート デスクトップ クライアントのユーザーが、Windows 10 バージョン 1803 以降が実行されているリモート デスクトップに接続すると、パフォーマンスの低下が発生します。

これは、NLA が無効になっていると、古いクライアント コンピューターでは、Windows 10 バージョン 1803 以降に接続するときに、低速のプロトコルが使われるために発生します。

この問題を解決するには、KB 4340917、[2018 年 7 月 24 日 — KB4340917 (OS ビルド 17134.191)](https://support.microsoft.com/help/4340917/windows-10-update-kb4340917) を適用します。

### <a name="black-screen-issue"></a>黒い画面の問題

この問題は、Windows 8.0、Windows 8.1、Windows 10 RTM、および Windows Server 2012 R2 で発生します。 ユーザーは、リモート デスクトップで複数のアプリケーションを起動した後、セッションから切断します。 ユーザーは、定期的にリモート デスクトップに再接続してアプリケーションと対話し、再び切断します。 ある時点で、ユーザーが再接続すると、リモート デスクトップ セッションに黒い画面だけが表示されます。 セッションが再び正常に表示されるようにするには、ユーザーがリモート コンピューターのコンソールまたは RDSH サーバー コンソールからセッションを終了し、セッションのアプリケーションを停止する必要があります。

この問題を解決するには、必要に応じて次の更新プログラムを適用します。

  - Windows 8 および Windows Server 2012: KB4103719、[2018 年 5 月 17 日 — KB4103719 (マンスリー ロールアップのプレビュー)](https://support.microsoft.com/help/4103719/windows-server-2012-update-kb4103719)
  - Windows 8.1 および Windows Server 2012 R2: KB4103724、[2018 年 5 月 17 日 — KB4103724 (マンスリー ロールアップのプレビュー)](https://support.microsoft.com/help/4103724/windows-81-update-kb4103724) および KB 4284863、[2018 年 6 月 21 日 — KB4284863 (マンスリー ロールアップのプレビュー)](https://support.microsoft.com/help/4284863/windows-81-update-kb4284863)
  - Windows 10:KB4284860、[2018 年 6 月 12 日 — KB4284860 (OS ビルド 10240.17889)](https://support.microsoft.com/help/4284860/windows-10-update-kb4284860) で修正されました
