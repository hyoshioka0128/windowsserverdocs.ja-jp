---
title: online volume
description: オンラインボリュームコマンドのリファレンストピック。オフラインボリュームをオンライン状態にします。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5da073fd-578d-4691-ad0f-605ba66e0c7e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 83a1e4bf1d6afe9485ab71c9af372166797900b3
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85472668"
---
# <a name="online-disk"></a>online disk

オフラインボリュームをオンライン状態にします。 このコマンドは、障害が発生しているか、失敗したか、冗長状態になっているボリュームに対して機能します。

> [!NOTE]
> **オンラインボリューム**コマンドを正常に実行するには、ボリュームを選択する必要があります。 使用して、 [ボリュームを選択して](select-volume.md) コマンドのボリュームを選択し、それにフォーカスをします。

> [!IMPORTANT]
> 読み取り専用ディスクで使用されている場合、このコマンドは失敗します。

## <a name="syntax"></a>構文

```
online volume [noerr]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
|--|--|
| noerr | スクリプト専用です。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。 |

### <a name="examples"></a>例

フォーカスがあるボリュームをオンラインにするには、次のように入力します。

```
online volume
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)
