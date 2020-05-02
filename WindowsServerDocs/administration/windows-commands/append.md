---
title: append
description: '[追加] コマンドのリファレンストピック。これにより、プログラムは、現在のディレクトリにあるかのように、指定されたディレクトリ内のデータファイルを開くことができます。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9c3fea20-9502-40ad-a442-7a927aad88eb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 562a13c6b1a47e43bb66548902f0b8e57e789a34
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718995"
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

| パラメーター | [説明] |
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

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)
