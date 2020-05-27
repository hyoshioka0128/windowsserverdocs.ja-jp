---
title: goto
description: Goto コマンドのリファレンストピックです。このコマンドは、cmd.exe をバッチプログラムのラベル付きの行に指示します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e0de1458-1f78-48ff-a746-c285a945a510
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1eb1b6b275887de535614fa5df4adabe33406a31
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2020
ms.locfileid: "83818972"
---
# <a name="goto"></a>goto

Cmd.exe をバッチプログラムのラベル付きの行に指示します。 バッチプログラム内では、このコマンドはラベルによって識別される行にコマンド処理を指示します。 ラベルが見つかると、処理が続行され、次の行で始まるコマンドが開始されます。

## <a name="syntax"></a>構文

```
goto <label>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<label>` | バッチプログラムでラベルとして使用されるテキスト文字列を指定します。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

#### <a name="remarks"></a>注釈

-  コマンド拡張機能が有効になっている場合 (既定)、target ラベルが**EOF**の**goto**コマンドを使用する場合は、現在のバッチスクリプトファイルの末尾に制御を移し、ラベルを定義せずにバッチスクリプトファイルを終了します。 このコマンドを **: EOF**ラベルと共に使用する場合は、ラベルの前にコロンを挿入する必要があります。 (例: `goto:EOF`)。

- *Label*パラメーターにはスペースを使用できますが、他の区切り記号 (セミコロン;) (;) など) を含めることはできません。または等号 (=)) にします。

- 指定する*ラベル*値は、バッチプログラムのラベルと一致する必要があります。 バッチプログラム内のラベルは、コロン (:) で始まる必要があります。 行がコロンで始まる場合は、ラベルとして扱われ、その行のすべてのコマンドは無視されます。 *ラベル*パラメーターに指定したラベルがバッチプログラムに含まれていない場合、バッチプログラムは停止し、というメッセージが表示されます `Label not found` 。

- 他のコマンドと共に**goto**を使用して、条件付き操作を実行できます。 条件付き操作に**goto**を使用する方法の詳細については、 [if コマンド](if.md)を参照してください。

## <a name="examples"></a>例

次のバッチプログラムは、ドライブ A のディスクをシステムディスクとしてフォーマットします。 操作が成功した場合、 **goto**コマンドは処理を**終了**ラベルに渡します。

```
echo off
format a: /s
if not errorlevel 1 goto end
echo An error occurred during formatting.
:end
echo End of batch program.
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [cmd コマンド](cmd.md)

- [if コマンド](if.md)