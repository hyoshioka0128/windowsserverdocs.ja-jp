---
title: 確認
description: Verify の Windows コマンドに関するトピック。ファイルがディスクに正しく書き込まれたことを確認するかどうかを**cmd**に指示します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: dfe8bc91-d948-4e47-84ad-a79a60506ffa
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 91a0777999a604a23e2de83eda6b89c926cb241c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80830055"
---
# <a name="verify"></a>確認



指示 **cmd** をディスクにファイルが正しく書き込まれたことを確認するかどうか。 パラメーターを指定せずに使用する場合 **確認** 現在の設定が表示されます。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
verify [on | off]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|[on \| off]|スイッチ、 **確認** オンまたはオフに設定します。|
|/?|コマンド プロンプトでヘルプを表示します。|

## <a name="examples"></a><a name=BKMK_examples></a>例

現在の表示を **ことを確認** 入力を設定する。
```
verify
```
するには、 **確認** に設定を入力します。
```
Verify on
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)