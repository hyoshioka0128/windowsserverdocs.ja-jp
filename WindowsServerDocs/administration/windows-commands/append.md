---
title: append
description: '[追加] コマンドの参照記事。これにより、プログラムは、現在のディレクトリにあるかのように、指定されたディレクトリ内のデータファイルを開くことができます。'
ms.topic: article
ms.assetid: 9c3fea20-9502-40ad-a442-7a927aad88eb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 887d058baf333f068b2e1fb557f085f0cfe58615
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87895571"
---
# <a name="append"></a>append

指定したディレクトリ内のデータファイルを、現在のディレクトリにあるかのように開くことをプログラムに許可します。 パラメーターを指定せずに使用した場合は、追加されたディレクトリの一覧が**追加**されます。

> [!NOTE]
> このコマンドは、Windows 10 ではサポートされていません。

## <a name="syntax"></a>構文

```
append [[<drive>:]<path>[;...]] [/x[:on|:off]] [/path:[:on|:off] [/e]
append ;
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `[\<drive>:]<path>` | 追加するドライブとディレクトリを指定します。 |
| /x: オン | 追加されたディレクトリをファイル検索に適用し、アプリケーションを起動します。 |
| /x: off | ファイルを開く要求のみに追加されたディレクトリを適用します。 **/X: off**オプションは既定の設定です。 |
| /path: on | 既にパスを指定しているファイル要求に追加されたディレクトリを適用します。 **/path: on**は既定の設定です。 |
| /path: オフ | **/Path: on**の効果をオフにします。 |
| /e | 追加されたディレクトリリストのコピーを APPEND という名前の環境変数に格納します。 **/e**は、システムを起動した後に**append**を初めて使用するときにのみ使用できます。 |
| ; | 追加されたディレクトリの一覧をクリアします。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

## <a name="examples"></a>例

追加されたディレクトリの一覧を消去するには、次のように入力します。

```
append ;
```

追加されたディレクトリのコピーを*append*という名前の環境変数に格納するには、次のように入力します。

```
append /e
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
