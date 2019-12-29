---
title: graftabl
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: ac7748b43eb8859a17a2c61ef9ef4444019ad51b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375629"
---
# <a name="graftabl"></a>graftabl



Windows オペレーティングシステムで、拡張文字セットをグラフィックモードで表示できるようにします。 パラメーターを指定せずに**graftabl**を使用すると、前のコードページと現在のコードページが表示されます。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
graftabl <CodePage>
graftabl /status
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<CodePage >|グラフィックスモードで拡張文字の外観を定義するコードページを指定します。</br>有効なコードページ id 番号は次のとおりです。</br>437:米国</br>850:多言語 (ラテン I)</br>852:スラブ語 (ラテン II)</br>855:キリル語 (ロシア)</br>857:トルコ語</br>860:ポルトガル語</br>861:アイスランド語</br>863:カナダ-フランス語</br>865:北欧</br>866:ロシア語</br>869:モダンギリシャ語|
|/status|**Graftabl**が使用している現在のコードページを表示します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>コメント

-   **Graftabl**は、指定したコードページの拡張文字のモニター表示のみに影響します。 実際のコンソール入力コードページは変更されません。 コンソールの入力コードページを変更するには、 **mode**または**chcp**コマンドを使用します。
-   次の表に、各終了コードとその簡単な説明を示します。  
    |終了コード|説明|
    |---------|-----------|
    |0|文字セットが正常に読み込まれました。 前のコードページが読み込まれませんでした。|
    |1|正しくないパラメーターが指定されました。 何も処理されませんでした。|
    |2|ファイルエラーが発生しました。|
-   バッチプログラムで ERRORLEVEL 環境変数を使用すると、 **graftabl**によって返される終了コードを処理できます。

## <a name="BKMK_examples"></a>例

**Graftabl**によって使用される現在のコードページを表示するには、次のように入力します。
```
graftabl /status
```
コードページ 437 (米国) のグラフィックス文字セットをメモリに読み込むには、次のように入力します。
```
graftabl 437
```
コードページ 850 (多言語) のグラフィックス文字セットをメモリに読み込むには、次のように入力します。
```
graftabl 850
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)

[Freedisk](freedisk.md)

[Chcp](chcp.md)