---
title: autochk
description: Windows コマンド」のトピック**autochk** - コンピューターの起動時に実行し、Windows Server の前に、ファイル システムの論理整合性を確認して開始します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8787e6a3-f023-4ea5-b2d1-61c6876d8aff
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 023bd81b93106a091fb9f26d97cf7eda75f0f633
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888463"
---
# <a name="autochk"></a>autochk



コンピューターの起動時に実行と Windows Server® 2008 R2 する前に、ファイル システムの論理整合性を検証を開始しています。

**Autochk.exe**のバージョンは、 **Chkdsk** NTFS ディスク上にのみ、および Windows Server 2008 R2 を開始する前にのみ実行します。 **Autochk**コマンドラインから直接実行することはできません。 代わりに、 **Autochk**は、次の状況で実行されます。
-   実行しようとする場合**Chkdsk**ブート ボリュームで
-   場合**Chkdsk**ボリュームを排他的に使用することができません
-   ボリュームがダーティとしてフラグが設定された場合

## <a name="remarks"></a>注釈

> -   [!WARNING]
>     **Autochk**コマンド ライン ツールは、コマンドラインから直接実行できません。 代わりに、使用、 **Chkntfs**方法を構成するコマンド ライン ツール**Autochk**スタートアップ時に実行します。
-   使用することができます**Chkntfs**で、 **/x**を防ぐためにパラメーター **Autochk**特定または複数のボリュームで実行されているからです。
-   使用して、 **Chkntfs.exe**とコマンド ライン ツール、 **/t** Autochk 遅延を 0 秒から 3 日 (259, 200 秒) に変更するパラメーター。 ただし、長時間の遅延は、時間が経過するまで、またはキャンセルするキーを押すと、コンピューターが起動しないことを意味**Autochk**します。

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)

[chkdsk](chkdsk.md)

[chkntfs](chkntfs.md)

[ディスクとファイル システムのトラブルシューティング](https://go.microsoft.com/fwlink/?LinkId=4527)