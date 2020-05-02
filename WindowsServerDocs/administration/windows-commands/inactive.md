---
title: 非アクティブ
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f4fb4695-4e66-4166-b4ab-2c86a4605580
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4f1c0e0cd5ebbf92638a221852bc3133116f4911
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724832"
---
# <a name="inactive"></a>非アクティブ



ベーシック マスター ブート レコード (MBR) ディスク上で、フォーカスのあるシステム パーティションまたはブート パーティションを非アクティブとしてマークします。

## <a name="syntax"></a>構文

```
inactive
```

## <a name="remarks"></a>Remarks

> [!CAUTION]
> アクティブ パーティションがないコンピューターは、起動しない可能性があります。 システムまたはブートパーティションを非アクティブとしてマークしないでください。経験豊富なユーザーが Windows ファミリのオペレーティングシステムを十分に理解していることを確認してください。</br>>、システムまたはブートパーティションを非アクティブとしてマークした後にコンピューターを起動できない場合は、cd-rom ドライブに Windows セットアップ CD を挿入し、コンピューターを再起動してから、回復コンソールの**fixmbr**コマンドと**fixboot**コマンドを使用してパーティションを修復します。
> -   システムパーティションまたはブートパーティションを非アクティブとしてマークした後、コンピューターは、CD-ROM ドライブやプリブート実行環境 (PXE) など、BIOS で指定されている次のオプションから起動します。
> -   この操作を成功させるには、アクティブなシステムまたはブートパーティションを選択する必要があります。 **[パーティションの選択**] コマンドを使用してアクティブなパーティションを選択し、それにフォーカスを移動します。

## <a name="examples"></a>例

```
inactive
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

