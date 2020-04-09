---
title: chcp
description: Windows コマンドの chcp に関するトピックでは、アクティブなコンソールのコードページを変更します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: dc7b1c71-7b80-443d-9cf1-9bcf305aa1fd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e644cf8544d135c5d21c344b0fd0a3364c7f89c1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80847945"
---
# <a name="chcp"></a>chcp

アクティブなコンソールのコードページを変更します。 パラメーターを指定せずに使用した場合、 **chcp**には、アクティブなコンソールコードページの数が表示されます。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
chcp [<NNN>]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<NNN >|コードページを指定します。|
|/?|コマンド プロンプトでヘルプを表示します。|

次の表に、サポートされているコードページとその国/地域または言語を示します。

|コードページ|国/地域または言語|
|---------|--------------------------|
|437|米国|
|850|多言語 (ラテン I)|
|852|スラブ語 (ラテン II)|
|855|キリル語 (ロシア)|
|857|トルコ語|
|860|ポルトガル語|
|861|アイスランド語|
|863|カナダ-フランス語|
|865|北欧|
|866|ロシア語|
|869|モダンギリシャ語|
|936|中国語|

## <a name="remarks"></a>コメント

-   Windows と共にインストールされる相手先ブランド供給 (OEM) コードページのみが、ラスターフォントを使用するコマンドプロンプトウィンドウに正しく表示されます。 他のコードページは、全画面表示モードまたは TrueType フォントを使用するコマンドプロンプトウィンドウで正しく表示されます。
-   (MS-DOS の場合と同様に) コードページを準備する必要はありません。
-   新しいコードページを割り当てた後に起動するプログラムでは、新しいコードページが使用されます。 ただし、新しいコードページを割り当てる前に開始したプログラム (Cmd.exe を除く) は、元のコードページを使用します。

## <a name="examples"></a><a name=BKMK_examples></a>例

アクティブなコードページの設定を表示するには、次のように入力します。
```
chcp
```
次のようなメッセージが表示されます。

`Active code page: 437`

アクティブなコードページを 850 (多言語) に変更するには、次のように入力します。
```
chcp 850
```
指定したコードページが無効な場合は、次のエラーメッセージが表示されます。

`Invalid code page`

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
