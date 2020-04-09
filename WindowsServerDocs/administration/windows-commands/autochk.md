---
title: autochk
description: Windows コマンドにおける**autochk**のトピックでは、コンピューターが起動したとき、およびファイルシステムの論理的な整合性の検証を開始する前に、windows Server の前に実行されます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8787e6a3-f023-4ea5-b2d1-61c6876d8aff
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 30ccdbb6aad6e116988ae9c782e3ff359642453e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851125"
---
# <a name="autochk"></a>autochk

コンピューターが起動したとき、および Windows Server&reg; 2008 R2 より前に、ファイルシステムの論理的な整合性の検証を開始するときに実行されます。

**Autochk.exe**は、NTFS ディスク上でのみ実行され、Windows Server 2008 R2 が開始される前にのみ実行される**Chkdsk**のバージョンです。 コマンドラインから**Autochk**を直接実行することはできません。 代わりに、次のような状況で**Autochk**が実行されます。

- ブートボリュームで**Chkdsk**を実行しようとした場合。

- **Chkdsk**でボリュームを排他的に使用できない場合。

- ボリュームにダーティのフラグが設定されている場合。

## <a name="remarks"></a>コメント

> [!WARNING]
> **Autochk**コマンドラインツールは、コマンドラインから直接実行することはできません。 代わりに、 **Chkntfs**コマンドラインツールを使用して、起動時に**Autochk**を実行する方法を構成します。
> -  **Chkntfs**を **/x**パラメーターと共に使用すると、 **Autochk**が特定のボリュームまたは複数のボリュームで実行されないようにすることができます。
>
> - **Chkntfs**コマンドラインツールと **/t**パラメーターを使用して、Autochk 遅延時間を0秒から最大3日 (259200 秒) に変更します。 ただし、長い遅延とは、時間が経過するまで、またはキーを押して**Autochk**をキャンセルするまで、コンピューターが起動しないことを意味します。

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [Chkdsk](chkdsk.md)

- [Chkntfs](chkntfs.md)

- [ディスクとファイルシステムのトラブルシューティング](https://go.microsoft.com/fwlink/?LinkId=4527)