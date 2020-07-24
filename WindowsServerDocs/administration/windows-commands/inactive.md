---
title: 非アクティブ
description: 非アクティブなコマンドの参照記事。ベーシックマスターブートレコード (MBR) ディスクで、フォーカスがあるシステムパーティションまたはブートパーティションを非アクティブとしてマークします。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f4fb4695-4e66-4166-b4ab-2c86a4605580
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f7e9679dee2bb8a75da14e1d7ee6c75b80bb1ef1
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86957134"
---
# <a name="inactive"></a>非アクティブ

基本マスターブートレコード (MBR) ディスクで、フォーカスがあるシステムパーティションまたはブートパーティションを非アクティブとしてマークします。

この操作を成功させるには、アクティブなシステムまたはブートパーティションを選択する必要があります。 [[パーティションの選択] コマンド](select-partition.md)を使用してアクティブなパーティションを選択し、それにフォーカスを移動します。

> [!CAUTION]
> アクティブ パーティションがないコンピューターは、起動しない可能性があります。 システムまたはブートパーティションを非アクティブとしてマークしないでください。これは、Windows ファミリのオペレーティングシステムを十分に理解している経験豊富なユーザーでない限りです。<p>システムパーティションまたはブートパーティションを非アクティブとしてマークした後にコンピューターを起動できない場合は、cd-rom ドライブに Windows セットアップ CD を挿入し、コンピューターを再起動してから、回復コンソールの**fixmbr**コマンドと**fixboot**コマンドを使用してパーティションを修復します。
>
> システムパーティションまたはブートパーティションを非アクティブとしてマークした後、コンピューターは、CD-ROM ドライブやプリブート実行環境 (PXE) など、BIOS で指定されている次のオプションから起動します。

## <a name="syntax"></a>構文

```
inactive
```

### <a name="examples"></a>例

```
inactive
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [パーティションの選択コマンド](select-partition.md)

- [Windows の起動の問題の高度なトラブルシューティング](/windows/client-management/advanced-troubleshooting-boot-problems)
