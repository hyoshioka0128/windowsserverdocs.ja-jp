---
title: reg export
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0ad9526f-1e29-4fa5-9d2d-feaa92f12d7c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5901014511fed0c17a641e1ed183ddbf40dd44c8
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80836495"
---
# <a name="reg-export"></a>reg export



他のサーバーに転送するためのファイルに指定されたサブキー、エントリ、およびローカル コンピューターの値をコピーします。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
Reg export KeyName FileName [/y]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<KeyName >|サブキーの完全なパスを指定します。 エクスポート操作は、ローカル コンピューターでのみ機能します。 られているキー名では、有効なルート キーを含める必要があります。 有効なルート キー: HKLM、HKCU、HKCR、HKU、および HKCC します。|
|\<ファイル名 >|操作中に作成されるファイルのパスと名前を指定します。 拡張子が .reg のファイルが必要です。|
|/y|名前の既存のファイルを上書き *FileName* 確認を求めずにします。|
|/?|ヘルプを表示 **reg エクスポート** コマンド プロンプト。|

## <a name="remarks"></a>コメント

次の表に、戻り値の **reg エクスポート** 操作します。

|値|説明|
|-----|-----------|
|0|成功|
|1|失敗|

## <a name="examples"></a><a name=BKMK_examples></a>例

すべてのサブキーの内容は、MyApp キーの値を AppBkUp.reg ファイルをエクスポートするには、次のように入力します。
```
reg export HKLM\Software\MyCo\MyApp AppBkUp.reg
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)