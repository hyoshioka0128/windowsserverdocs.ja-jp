---
title: chcp
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dc7b1c71-7b80-443d-9cf1-9bcf305aa1fd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 622d4b64128c7e39cc761e4f5e9d69cf54383760
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819203"
---
# <a name="chcp"></a>chcp



コンソールのアクティブなコード ページを変更します。 パラメーターを指定せずに使用されている場合**chcp**コンソールのアクティブなコード ページの数が表示されます。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
chcp [<NNN>]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<NNN>|コード ページを指定します。|
|/?|コマンド プロンプトにヘルプを表示します。|

次の表では、各サポートされているコード ページおよび国/地域や言語を示します。

|コード ページ|国/地域や言語|
|---------|--------------------------|
|437|米国|
|850|多言語 (ラテン I)|
|852|スラブ語 (ラテン II)|
|855|キリル語 (ロシア語)|
|857|トルコ語|
|860|ポルトガル語|
|861|アイスランド語|
|863|カナダ フランス語|
|865|北欧|
|866|ロシア語|
|869|モダン ギリシャ語|
|936|中国語|

## <a name="remarks"></a>注釈

-   ラスター フォントを使用するコマンド プロンプト ウィンドウでは、Windows と共にインストールされる original equipment manufacturer (OEM) コード ページのみが正しく表示されます。 全画面表示モードまたは TrueType フォントを使用してコマンド プロンプト ウィンドウで、他のコード ページは正しく表示されます。
-   (MS-DOS) のようにコード ページを準備する必要はありません。
-   後に起動したプログラムは、新しいコード ページに新しいコード ページの使用を割り当てます。 ただしを起動する前にする (Cmd.exe) を除くプログラムは、元のコード ページのコード ページの新しい使用割り当てられます。

## <a name="BKMK_examples"></a>例

アクティブなコード ページの設定を表示するには、次のように入力します。
```
chcp
```
次のようなメッセージが表示されます。

`Active code page: 437`

現在のコード ページ 850 (多言語) を変更するには、次のように入力します。
```
chcp 850
```
指定したコード ページが有効でない場合は、次のエラー メッセージが表示されます。

`Invalid code page`

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)
