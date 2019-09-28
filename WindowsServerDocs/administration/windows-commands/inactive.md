---
title: 稼動
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f4fb4695-4e66-4166-b4ab-2c86a4605580
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9ce91b6a024c165e3aa63148b9ad6dfcc4db7a7c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375374"
---
# <a name="inactive"></a>稼動



ベーシックマスタブートレコード (MBR) ディスクでは、はシステムパーティションまたはブートパーティションを非アクティブとしてマークします。

## <a name="syntax"></a>構文

```
inactive
```

## <a name="remarks"></a>コメント

> [!CAUTION]
> アクティブなパーティションがないと、コンピューターが起動しない可能性があります。 システムまたはブートパーティションを非アクティブとしてマークしないでください。経験豊富なユーザーが Windows ファミリのオペレーティングシステムを十分に理解していることを確認してください。</br>>、システムまたはブートパーティションを非アクティブとしてマークした後にコンピューターを起動できない場合は、cd-rom ドライブに Windows セットアップ CD を挿入し、コンピューターを再起動してから、次**のコマンドを使用して**、パーティションを修復**します。** 回復コンソール。
> -   システムパーティションまたはブートパーティションを非アクティブとしてマークした後、コンピューターは、CD-ROM ドライブやプリブート実行環境 (PXE) など、BIOS で指定されている次のオプションから起動します。
> -   この操作を成功させるには、アクティブなシステムまたはブートパーティションを選択する必要があります。 **[パーティションの選択**] コマンドを使用してアクティブなパーティションを選択し、それにフォーカスを移動します。

## <a name="BKMK_examples"></a>例

```
inactive
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)

