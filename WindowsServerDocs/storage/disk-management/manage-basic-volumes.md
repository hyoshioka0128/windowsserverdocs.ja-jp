---
title: ベーシック ボリュームを管理する
description: この記事では、ベーシック ボリュームを管理する方法について説明します。
ms.date: 10/12/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 2eee5820891c108475c58c9ad024cd7c00391e43
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385918"
---
# <a name="manage-basic-volumes"></a>ベーシック ボリュームを管理する

> **適用対象:** Windows 10、Windows 8.1、Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ベーシック ディスクとは、プライマリ パーティション、拡張パーティション、または論理ドライブが含まれる物理ディスクです。 ベーシック ディス上のパーティションと論理ドライブはベーシック ボリュームと呼ばれます。 ベーシック ディスクにはベーシック ボリュームのみを作成できます。

既存のプライマリ パーティションや論理ドライブに空き領域を追加するには、同じディスク上にある、隣接する連続した未割り当て領域に拡張します。 ベーシック ボリュームを拡張するには、NTFS ファイル システムでフォーマットされている必要があります。 論理ドライブは、その論理ドライブが含まれる拡張パーティション内の連続した空き領域内で拡張することができます。 拡張パーティションで利用可能な空き領域を超えて論理ドライブを拡張する場合、拡張パーティションに連続した未割り当て領域が続いている場合に限り、論理ドライブを格納できるように拡張パーティションが拡大されます。

## <a name="see-also"></a>参照

-   [ドライブにマウント ポイント フォルダー パスを割り当てる](assign-a-mount-point-folder-path-to-a-drive.md)
-   [ベーシック ボリュームを拡張する](extend-a-basic-volume.md)
-   [ベーシック ボリュームを縮小する](shrink-a-basic-volume.md)