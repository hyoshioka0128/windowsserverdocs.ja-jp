---
title: Azure ファイル Sync を使用して、ファイル サーバー、クラウドとの同期します。
description: Azure ファイル Sync を使用して、柔軟性、パフォーマンス、およびオンプレミス ファイル サーバーとの互換性を維持しながら、azure では、組織のファイル共有を一元化します。 Azure ファイル同期は、Windows Server を省略可能なクラウドの階層化機能を使用して Azure ファイル共有のクイック キャッシュに変換します。
ms.technology: manage
ms.topic: article
author: fauhse
ms.author: fauhse
ms.date: 04/12/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 93cfa469a3c14410d95b0b224cbf59b913ec9f7e
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296970"
---
# Azure ファイル Sync を使用して、ファイル サーバー、クラウドとの同期します。

>適用対象: Windows Admin Center、Windows Admin Center Preview

Azure ファイル Sync を使用して、柔軟性、パフォーマンス、およびオンプレミス ファイル サーバーとの互換性を維持しながら、azure では、組織のファイル共有を一元化します。 Azure ファイル同期は、Windows Server を省略可能なクラウドの階層化機能を使用して Azure ファイル共有のクイック キャッシュに変換します。 SMB、NFS、FTPS など、ローカルでのデータにアクセスする Windows Server で使用可能な任意のプロトコルを使用できます。

同期し、コンテンツをローカルにキャッシュするのと同じ Azure ファイル共有に複数のサーバーを接続するには、ファイルは、クラウドに同期が、いったん-権限 (Acl) が常に転送されるもします。 Azure ファイルには、Azure のファイル共有の差分のスナップショットを生成できるスナップショット機能が用意されています。 これらのスナップショットを簡単な閲覧と復元の SMB を通じて読み取り専用のネットワーク ドライブとしてマウントもできます。 クラウドの階層化と組み合わせることにより、オンプレミス ファイル サーバーを実行している容易になりました。

詳しくは、 [Azure ファイル同期展開の計画](https://aka.ms/afs)を参照してください。