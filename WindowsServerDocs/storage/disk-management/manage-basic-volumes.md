---
title: ベーシック ボリュームを管理する
description: この記事では、ベーシック ボリュームを管理する方法について説明します。
ms.date: 10/12/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: c75d887a6427673319999522b890d523f4276871
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870963"
---
# <a name="manage-basic-volumes"></a>ベーシック ボリュームを管理する

> **適用対象します。** Windows 10、Windows 8.1、Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ベーシック ディスクとは、プライマリ パーティション、拡張パーティション、または論理ドライブが含まれる物理ディスクです。 ベーシック ディス上のパーティションと論理ドライブはベーシック ボリュームと呼ばれます。 ベーシック ディスクにはベーシック ボリュームのみを作成できます。

既存のプライマリ パーティションや論理ドライブに空き領域を追加するには、同じディスク上にある、隣接する連続した未割り当て領域に拡張します。 ベーシック ボリュームを拡張するには、NTFS ファイル システムでフォーマットされている必要があります。 論理ドライブは、その論理ドライブが含まれる拡張パーティション内の連続した空き領域内で拡張することができます。 拡張パーティションで利用可能な空き領域を超えて論理ドライブを拡張する場合、拡張パーティションに連続した未割り当て領域が続いている場合に限り、論理ドライブを格納できるように拡張パーティションが拡大されます。

## <a name="see-also"></a>関連項目

-   [マウント ポイント フォルダー パスをドライブに割り当てる](assign-a-mount-point-folder-path-to-a-drive.md)
-   [ベーシック ボリュームを拡張します。](extend-a-basic-volume.md)
-   [ベーシック ボリュームを圧縮します。](shrink-a-basic-volume.md)