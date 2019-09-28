---
title: append
description: 'の Windows コマンドに関するトピック '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: fdc4243bee8055888b023a56921cef757dda6b7e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382755"
---
# <a name="append"></a>append



指定したディレクトリ内のデータファイルを、現在のディレクトリにあるかのように開くことをプログラムに許可します。 パラメーターを指定せずに使用した場合は、追加されたディレクトリの一覧が**追加**されます。

> [!NOTE]
> このコマンドは、Windows 10 ではサポートされていません。
>

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
append [[<Drive>:]<Path>[;...]] [/x[:on|:off]] [/path:[:on|:off] [/e] 
append ;
```

## <a name="parameters"></a>パラメーター

|     パラメーター     |                                                                                 説明                                                                                 |
|-------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [\<Drive >:] <Path> |                                                                 追加するドライブとディレクトリを指定します。                                                                  |
|       /x: オン       |                                                  追加されたディレクトリをファイル検索に適用し、アプリケーションを起動します。                                                  |
|      /x: off       |                                     ファイルを開く要求のみに追加されたディレクトリを適用します。</br>**/x: off**が既定の設定です。                                     |
|     /path: on      |                               既にパスを指定しているファイル要求に追加されたディレクトリを適用します。 **/path: on**は既定の設定です。                               |
|     /path: オフ     |                                                                    **/Path: on**の効果をオフにします。                                                                    |
|        /e         | 追加されたディレクトリリストのコピーを APPEND という名前の環境変数に格納します。 **/e**は、システムを起動した後に**append**を初めて使用するときにのみ使用できます。 |
|         ;         |                                                                     追加されたディレクトリの一覧をクリアします。                                                                     |
|        /?         |                                                                    コマンド プロンプトにヘルプを表示します。                                                                     |

## <a name="BKMK_examples"></a>例

追加されたディレクトリの一覧を消去するには、次のように入力します。
```
append ;
```
追加されたディレクトリのコピーを APPEND という名前の環境変数に格納するには、次のように入力します。
```
append /e
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)
