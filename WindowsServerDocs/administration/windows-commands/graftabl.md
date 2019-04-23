---
title: graftabl
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b08351d4-3d24-490c-86f6-1252da11d923
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 395873cf3dbeb574dd9abc69f45b410bece80c25
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848443"
---
# <a name="graftabl"></a>graftabl



拡張文字セット グラフィック モードで表示する Windows オペレーティング システムを有効にします。 パラメーターを指定せずに使用されている場合**与えます**以前のバージョンと現在のコード ページが表示されます。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
graftabl <CodePage>
graftabl /status
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<CodePage>|グラフィック モードで拡張文字の外観を定義するコード ページを指定します。</br>有効なコード ページ id 番号は次のとおりです。</br>437:米国</br>850:多言語 (ラテン I)</br>852:スラブ語 (ラテン II)</br>855:キリル語 (ロシア語)</br>857:トルコ語</br>860:ポルトガル語</br>861:アイスランド語</br>863:カナダ フランス語</br>865:北欧</br>866:ロシア語</br>869:モダン ギリシャ語|
|/status|現在の表示コード ページを**与えます**を使用しています。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

-   **与えます**指定したコード ページの拡張文字のモニターの表示のみに影響します。 実際のコンソールの入力のコード ページは変更されません。 コンソールの入力のコード ページを変更するには、使用、**モード**または**chcp**コマンド。
-   次の表は、終了コードとその簡単な説明を示します。  
    |終了コード|説明|
    |---------|-----------|
    |0|文字セットが正常に読み込まれます。 前のコード ページが読み込まれません。|
    |1|無効なパラメーターが指定されました。 何も処理されませんでした。|
    |2|ファイルのエラーが発生しました。|
-   ERRORLEVEL 環境変数を使用して、によって返される終了コードを処理するバッチ プログラムで**与えます**します。

## <a name="BKMK_examples"></a>例

使用される現在のコード ページを表示する**与えます**種類。
```
graftabl /status
```
グラフィック文字をメモリにコード ページ 437 (米国) のセットを読み込むには、次のように入力します。
```
graftabl 437
```
グラフィックスの文字セットのコード ページ 850 (多言語) をメモリに読み込むには、次のように入力します。
```
graftabl 850
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)

[freedisk](freedisk.md)

[Chcp](chcp.md)