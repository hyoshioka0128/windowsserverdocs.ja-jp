---
title: bcdboot
description: Bcdboot コマンドのリファレンストピック。システムパーティションをすばやく設定するか、システムパーティションにあるブート環境を修復します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e62a250e-08e9-47f6-89d1-e6002560ab57
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 67aacb3a575e0cdd08af5372b403916961d223c6
ms.sourcegitcommit: ef089864980a1d4793a35cbf4cbdd02ce1962054
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/28/2020
ms.locfileid: "84149775"
---
# <a name="bcdboot"></a>bcdboot

を使用すると、システムパーティションをすばやく設定したり、システムパーティションにあるブート環境を修復したりできます。 システムパーティションは、単純な一連のブート構成データ (BCD) ファイルを既存の空のパーティションにコピーすることによって設定されます。

## <a name="syntax"></a>構文

```
bcdboot <source> [/l] [/s]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| ソース | ブート環境ファイルをコピーするためのソースとして使用する Windows ディレクトリの場所を指定します。 |
| /l | ロケールを指定します。 既定のロケールは英語 (米国) です。 |
| /s | システムパーティションのボリューム文字を指定します。 既定値は、ファームウェアによって識別されるシステムパーティションです。 |

## <a name="examples"></a>例

このコマンドの使用方法の詳細と使用例については、「Bcdboot の[コマンドラインオプション](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/hh824874(v=win.10))」を参照してください。

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)
