---
title: set_2
description: シャドウコピーの作成に使用するコンテキスト、オプション、詳細モード、およびメタデータファイルを設定する set_2 の参照記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: acf24663-1a50-4321-b48d-1717655e9476
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1b25b30ad729eb4e1cbf455f02cdacc76c0a3ab3
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85934636"
---
# <a name="set_2"></a>set_2

コンテキスト、オプション、詳細出力モード、およびシャドウ コピーの作成のメタデータ ファイルを設定します。 パラメーターを指定せずに使用する場合 **設定** すべて現在の設定を一覧表示します。

## <a name="syntax"></a>Syntax

```
set
set context {clientaccessible | persistent [nowriters] | volatile [nowriters]}
set option {[differential | plex] [transportable] [[rollbackrecover] [txfrecover] | [noautorecover]]}
set verbose {on|off}
set metadata <MetaData.cab>
```

## <a name="set-sub-commands"></a>サブコマンドの設定

|サブコマンド|説明|
|-----------|-----------|
|context|シャドウ コピーの作成のコンテキストを設定します。 参照してください [セット コンテキスト](set-context.md) 構文およびパラメーターについてです。|
|オプション|シャドウ コピーの作成のオプションを設定します。 参照してください [オプション設定](set-option.md) 構文およびパラメーターについてです。|
|verbose|詳細出力モードを有効または無効にします。 参照してください [が詳細設定](set-verbose.md) 構文およびパラメーターについてです。|
|metadata|シャドウの作成のメタデータ ファイルの場所と名前を設定します。 参照してください [メタデータ設定](set-metadata.md) 構文およびパラメーターについてです。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)