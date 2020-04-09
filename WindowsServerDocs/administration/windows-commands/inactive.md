---
title: 稼動
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f4fb4695-4e66-4166-b4ab-2c86a4605580
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 38a4f731bef9515a387b0343eaf4cb06142e6620
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80842125"
---
# <a name="inactive"></a>稼動



ベーシック マスター ブート レコード (MBR) ディスク上で、フォーカスのあるシステム パーティションまたはブート パーティションを非アクティブとしてマークします。

## <a name="syntax"></a>構文

```
inactive
```

## <a name="remarks"></a>コメント

> [!CAUTION]
> アクティブ パーティションがないコンピューターは、起動しない可能性があります。 システムまたはブートパーティションを非アクティブとしてマークしないでください。経験豊富なユーザーが Windows ファミリのオペレーティングシステムを十分に理解していることを確認してください。</br>>、システムまたはブートパーティションを非アクティブとしてマークした後にコンピューターを起動できない場合は、cd-rom ドライブに Windows セットアップ CD を挿入し、コンピューターを再起動してから、回復コンソールの**fixmbr**コマンドと**fixboot**コマンドを使用してパーティションを修復します。
> -   システムパーティションまたはブートパーティションを非アクティブとしてマークした後、コンピューターは、CD-ROM ドライブやプリブート実行環境 (PXE) など、BIOS で指定されている次のオプションから起動します。
> -   この操作を成功させるには、アクティブなシステムまたはブートパーティションを選択する必要があります。 **[パーティションの選択**] コマンドを使用してアクティブなパーティションを選択し、それにフォーカスを移動します。

## <a name="examples"></a><a name=BKMK_examples></a>例

```
inactive
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

