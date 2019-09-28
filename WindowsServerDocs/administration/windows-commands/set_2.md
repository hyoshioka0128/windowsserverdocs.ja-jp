---
title: set_2
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: acf24663-1a50-4321-b48d-1717655e9476
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e91bee5f0d351e461d16ccd22478d67f26887728
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71370912"
---
# <a name="set_2"></a>set_2



コンテキスト、オプション、詳細出力モード、およびシャドウ コピーの作成のメタデータ ファイルを設定します。 パラメーターを指定せずに使用する場合 **設定** すべて現在の設定を一覧表示します。

## <a name="syntax"></a>構文

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
|コンテキスト|シャドウ コピーの作成のコンテキストを設定します。 参照してください [セット コンテキスト](set-context.md) 構文およびパラメーターについてです。|
|オプション|シャドウ コピーの作成のオプションを設定します。 参照してください [オプション設定](set-option.md) 構文およびパラメーターについてです。|
|詳細|詳細出力モードを有効または無効にします。 参照してください [が詳細設定](set-verbose.md) 構文およびパラメーターについてです。|
|メタデータ (metadata)|シャドウの作成のメタデータ ファイルの場所と名前を設定します。 参照してください [メタデータ設定](set-metadata.md) 構文およびパラメーターについてです。|
|/?|コマンド プロンプトにヘルプを表示します。|

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)