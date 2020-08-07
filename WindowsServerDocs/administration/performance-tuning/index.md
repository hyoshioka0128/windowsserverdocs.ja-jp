---
title: Windows Server 2016 のパフォーマンス チューニング ガイドライン
description: Windows Server 2016 のパフォーマンス チューニング ガイドライン
ms.topic: landing-page
ms.author: phstee
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 69b65e9a7cb5e935a8c6b1a8ab500e33307a092d
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87896693"
---
# <a name="performance-tuning-guidelines-for-windows-server-2016"></a>Windows Server 2016 のパフォーマンス チューニング ガイドライン

組織内でサーバー システムを実行するときに、既定のサーバー設定の使用ではビジネス ニーズが満たされない場合があります。 たとえば、サーバー上で可能な最小のエネルギー消費量、可能な最短の待機時間、または可能な最大スループットが必要な場合があります。 このガイドでは、Windows Server 2016 内のサーバー設定を調整し、特に、時間が経過してもワークロードの性質がほとんど変化しない場合に、パフォーマンスを改善して、エネルギー効率を向上させるための一連のガイドラインを提供します。

チューニングの変更では、ハードウェア、ワークロード、電力の割り当て、およびサーバーのパフォーマンス目標を考慮することが重要です。 このガイドでは、各設定とその潜在的な効果について説明し、システム、ワークロード、パフォーマンス、およびエネルギー使用量の目標との関連性について情報に基づく意思決定を行えるようにします。

> [!warning]
> レジストリ設定とチューニング パラメーターは、Windows Server のバージョン間で大幅に変更されます。 予期しない結果を回避するために、必ず最新のチューニング ガイドラインを使用してください。

## <a name="in-this-guide"></a>このガイドの内容
このガイドでは、Windows Server 2016 のパフォーマンスとチューニングのガイダンスを 3 つのカテゴリに整理しています。

|サーバー ハードウェア | サーバーの役割 | サーバー サブシステム |
|:---:|:---:|:---:|
|[ハードウェア パフォーマンスに関する考慮事項](hardware/index.md) |[Active Directory サーバー](role/active-directory-server/index.md) |[キャッシュとメモリの管理](subsystem/cache-memory-management/index.md)|
|[ハードウェアの電源に関する考慮事項](hardware/power.md)|[ファイル サーバー](role/file-server/index.md)|[ネットワーク サブシステム](../../networking/technologies/network-subsystem/net-sub-performance-top.md)|
||[Hyper-V サーバー](role/hyper-v-server/index.md)|[記憶域スペース ダイレクト](subsystem/storage-spaces-direct/index.md)|
||[リモート デスクトップ サービス](role/remote-desktop/session-hosts.md)|[ソフトウェア定義ネットワーク (SDN)](subsystem/software-defined-networking/index.md)|
||[Web サーバー](role/web-server/index.md)||
||[Windows Server コンテナー](role/windows-server-container/index.md)||


## <a name="changes-in-this-version"></a>このバージョンでの変更点

### <a name="sections-added"></a>追加されたセクション
- [Nano Server のインストールの種類の構成に関する考慮事項](../../get-started/getting-started-with-nano-server.md)


- [HNV](subsystem/software-defined-networking/hnv-gateway-performance.md) や [SLB ゲートウェイの構成ガイド](subsystem/software-defined-networking/slb-gateway-performance.md)などの[ソフトウェア定義ネットワーク](subsystem/software-defined-networking/index.md)

- [記憶域スペース ダイレクト](subsystem/storage-spaces-direct/index.md)

- [HTTP1.1 と HTTP2](role/web-server/http-performance.md)

- [Windows Server コンテナー](role/windows-server-container/index.md)

### <a name="sections-changed"></a>変更されたセクション

- [Active Directory ガイダンス](role/active-directory-server/index.md)のセクションに対する更新

- [ファイル サーバー ガイダンス](role/file-server/index.md)のセクションに対する更新

- [Web サーバー ガイダンス](role/web-server/index.md)のセクションに対する更新

- [ハードウェア電源ガイダンス](hardware/power.md)のセクションに対する更新

- [PowerShell チューニング ガイダンス](powershell/index.md)のセクションに対する更新

- [Hyper-V ガイダンス](role/hyper-v-server/index.md)のセクションに対する大幅な更新

- "*ワークロードのパフォーマンス チューニングが削除され*"、[追加のチューニング リソースに関する記事](additional-resources.md)に関連リソースへのポインターを追加

- 新しい[記憶域スペース ダイレクト](subsystem/storage-spaces-direct/index.md)のセクションと正規の Technet コンテンツを優先して "*専用記憶域のセクションを削除*"

- 正規の Technet のコンテンツを優先して "*専用ネットワークのセクションを削除*"
