---
title: create
description: Create コマンドのリファレンストピックでは、ディスク上のパーティションまたはシャドウパーティション、1つまたは複数のディスク上のボリューム、または仮想ハードディスク (VHD) を作成します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b45acde1-8f4f-4ec3-b905-d8188f884af8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f371bee591e29a45b1488b2c36112b55ed54d3f8
ms.sourcegitcommit: fad2ba64bbc13763772e21ed3eabd010f6a5da34
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/09/2020
ms.locfileid: "82993189"
---
# <a name="create"></a>create

ディスク上のパーティションまたはシャドウ、1つ以上のディスク上のボリューム、または仮想ハードディスク (VHD) を作成します。 このコマンドを使用してシャドウディスクにボリュームを作成している場合は、シャドウコピーセットに少なくとも1つのボリュームが既に存在している必要があります。

## <a name="syntax"></a>構文

```
create partition
create volume
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| [create partition primary コマンド](create-partition-primary.md) | フォーカスがあるベーシックディスク上にプライマリパーティションを作成します。 |
| [create partition efi コマンド](create-partition-efi.md) | Itanium ベースのコンピューター上の GUID パーティションテーブル (gpt) ディスクに、拡張ファームウェアインターフェイス (EFI) システムパーティションを作成します。 |
| [create partition extended コマンド](create-partition-extended.md) | フォーカスがあるディスクに拡張パーティションを作成します。 |
| [create partition logical コマンド](create-partition-logical.md) | 既存の拡張パーティションに論理パーティションを作成します。 |
| [パーティション msr の作成コマンド](create-partition-msr.md) | GUID パーティションテーブル (gpt) ディスクに Microsoft 予約 (MSR) パーティションを作成します。 |
| [create volume simple コマンド](create-volume-simple.md) | 指定されたダイナミックディスクにシンプルボリュームを作成します。 |
| [ボリュームミラーの作成コマンド](create-volume-mirror.md) | 指定された2つのダイナミックディスクを使用してボリュームミラーを作成します。 |
| [ボリューム raid の作成コマンド](create-volume-raid.md) | 指定された3つ以上のダイナミックディスクを使用して RAID-5 ボリュームを作成します。 |
| [ボリュームストライプの作成コマンド](create-volume-stripe.md) | 2つ以上の指定されたダイナミックディスクを使用してストライプボリュームを作成します。 |

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)
