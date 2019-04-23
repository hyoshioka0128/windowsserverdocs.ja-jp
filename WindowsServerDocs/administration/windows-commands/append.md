---
title: append
description: 'Windows コマンド」のトピック '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9c3fea20-9502-40ad-a442-7a927aad88eb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: abf7713b3fd5bbb6172969ca1cc39cbbbbafafc6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881983"
---
# <a name="append"></a>append



として格納されている場合、現在のディレクトリに指定したディレクトリ内のデータ ファイルを開くプログラムを許可します。 パラメーターを指定せずに使用されている場合**追加**追加されたディレクトリの一覧が表示されます。

> [!NOTE]
> このコマンドでは、Windows 10 でサポートされていません。
>

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
append [[<Drive>:]<Path>[;...]] [/x[:on|:off]] [/path:[:on|:off] [/e] 
append ;
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|[\<ドライブ >:]<Path>|ドライブと追加するディレクトリを指定します。|
|/x:on|ファイルの検索および起動するアプリケーションに追加されたディレクトリを適用します。|
|/x:off|追加されたディレクトリをファイルを開く要求のみに適用されます。</br>**/x: オフ**既定の設定です。|
|/path:on|追加されたディレクトリを既にパスを指定する要求をファイルに適用されます。 **/path: で**既定の設定です。|
|/path:off|効果をオフに **/path: で**します。|
|/e|追加をという名前の環境変数に追加されたディレクトリの一覧のコピーを格納します。 **/e**初めてに使用するときにのみ使用できます**追加**後、システムを起動します。|
|;|追加されたディレクトリの一覧をクリアします。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="BKMK_examples"></a>例

追加されたディレクトリの一覧を消去するには、次のように入力します。
```
append ;
```
追加のという環境変数に追加されたディレクトリのコピーを保存するには、次のように入力します。
```
append /e
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)
