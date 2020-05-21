---
title: endlocal
description: Endlocal コマンドのリファレンストピック。バッチファイル内の環境の変更のローカライズを終了し、対応する setlocal コマンドが実行される前に環境変数を値に復元します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 765fae3c-0c0a-4639-99a4-cf613489b949
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 229914ddbfa7361738cad79903630be9e749c795
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2020
ms.locfileid: "83436887"
---
# <a name="endlocal"></a>endlocal

バッチファイル内の環境の変更のローカライズを終了し、対応する**setlocal**コマンドが実行される前に環境変数を値に復元します。

## <a name="syntax"></a>構文

```
endlocal
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| /? | コマンド プロンプトにヘルプを表示します。 |

#### <a name="remarks"></a>解説

- **Endlocal**コマンドは、スクリプトまたはバッチファイルの外部には影響しません。

- バッチファイルの末尾には、暗黙的な**endlocal**コマンドがあります。

- コマンド拡張機能が有効になっている場合 (コマンド拡張機能が既定で有効になっている場合)、 **endlocal**コマンドを実行すると、コマンド拡張機能 (有効または無効) の状態が、対応する**setlocal**コマンドが実行される前の状態に復元されます。

> [!NOTE]
> コマンド拡張機能の有効化と無効化の詳細については、「 [Cmd コマンド](cmd.md)」を参照してください。

### <a name="examples"></a>例

環境変数はバッチファイルでローカライズできます。 たとえば、次のプログラムは、ネットワーク上で*superapp*バッチプログラムを開始し、出力をファイルに送信して、メモ帳でファイルを表示します。

```
@echo off
setlocal
path=g:\programs\superapp;%path%
call superapp>c:\superapp.out
endlocal
start notepad c:\superapp.out
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)
