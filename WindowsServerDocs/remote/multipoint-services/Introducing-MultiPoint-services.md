---
title: MultiPoint Services の概要
description: 複数のユーザーがシステムを共有できるようにするための、MultiPoint Services の概要について説明します。
ms.date: 07/22/2016
ms.topic: article
ms.assetid: 1cbef744-4661-4ba9-9e2b-0bbd8854fd5c
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 663b3d4afade9b4fb459f34120d1e6b18984285a
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87997423"
---
# <a name="introducing-multipoint-services"></a>MultiPoint Services の概要
Windows Server 2016 の MultiPoint Services ロールを使用すると、複数のユーザーが独自の独立した使い慣れた Windows エクスペリエンスを持つことで、1台のコンピューターを同時に共有できます。ユーザーがセッションにアクセスするには、いくつかの方法があります。 1つの方法として、任意のデバイスで[リモートデスクトップアプリ](../remote-desktop-services/clients/remote-desktop-clients.md)を使用してサーバーにリモート処理を行う方法があります。 もう1つの方法は、MultiPoint server に接続されているステーションが物理ステーションを使用することです。

-   コンピューターのビデオポートに直接接続します。

-   特殊な usb ゼロクライアント (多機能 USB ハブとも呼ばれます) と同様の USB オーバーイーサネットデバイス。

-   ローカルエリアネットワーク (LAN) 経由

これらの各方法の詳細については、このドキュメントの「 [MultiPoint Services ステーション](MultiPoint-services-Stations.md)」を参照してください。

このドキュメントでは、MultiPoint Services の展開を計画する際に考慮する必要がある次の要素について説明します。

-   MultiPoint Services システムで使用するデスクトップの種類: セッション、仮想マシン、または Windows Pc は必要ですか。

-   [MultiPoint Services システムのハードウェアを選択](./select-hardware-mps.md)する: どのようなハードウェアを決定する必要がありますか。

-   [ハードウェア要件とパフォーマンスに関する推奨事項](./hardware-and-performance-recommendations.md): MultiPoint サービスに必要なハードウェアは何ですか。

-   [Multipoint Services サイトの計画](MultiPoint-services-Site-Planning.md): multipoint services を実行しているコンピューターとそのステーションが配置される場所、およびそれらはどのように構成されますか。

-   [ネットワークに関する考慮事項とユーザーアカウント](Network-Considerations-and-User-Accounts.md): MultiPoint Services システムが展開されるネットワーク環境は、ユーザーアカウントの管理方法に影響を与える可能性があります。 ネットワーク環境とは何ですか。 ユーザーアカウントはどのように管理されますか。

-   [MultiPoint Services を使用したファイルの保存](Storing-Files-with-MultiPoint-services.md): ユーザーファイルの保存場所とアクセス方法を指定します。

-   [展開前のチェックリスト](Predeployment-Checklist.md)