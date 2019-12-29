---
title: autochk
description: Windows コマンドの**autochk** -コンピューターが起動されたときと、windows Server の前にファイルシステムの論理的な整合性の検証を開始するときに実行します。
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 76e54d14879cefd4661a1ca7f1c3b8ee7ec58de2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382354"
---
# <a name="autochk"></a>autochk



コンピューターが起動したとき、および Windows Server® 2008 R2 より前に、ファイルシステムの論理的な整合性の検証を開始するときに実行されます。

**Autochk.exe**は、NTFS ディスク上でのみ実行され、Windows Server 2008 R2 が開始される前にのみ実行される**Chkdsk**のバージョンです。 コマンドラインから**Autochk**を直接実行することはできません。 代わりに、次のような状況で**Autochk**が実行されます。
-   ブートボリュームで**Chkdsk**を実行しようとすると、
-   **Chkdsk**でボリュームを排他的に使用できない場合
-   ボリュームにダーティのフラグが設定されている場合

## <a name="remarks"></a>コメント

> -   [!WARNING]
>     **Autochk**コマンドラインツールは、コマンドラインから直接実行することはできません。 代わりに、 **Chkntfs**コマンドラインツールを使用して、起動時に**Autochk**を実行する方法を構成します。
> -   **Chkntfs**を **/x**パラメーターと共に使用すると、 **Autochk**が特定のボリュームまたは複数のボリュームで実行されないようにすることができます。
> -   **Chkntfs**コマンドラインツールと **/t**パラメーターを使用して、Autochk 遅延時間を0秒から最大3日 (259200 秒) に変更します。 ただし、長い遅延とは、時間が経過するまで、またはキーを押して**Autochk**をキャンセルするまで、コンピューターが起動しないことを意味します。

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)

[Chkdsk](chkdsk.md)

[Chkntfs](chkntfs.md)

[ディスクとファイルシステムのトラブルシューティング](https://go.microsoft.com/fwlink/?LinkId=4527)