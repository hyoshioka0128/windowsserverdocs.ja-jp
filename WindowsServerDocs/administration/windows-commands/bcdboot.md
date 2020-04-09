---
title: bcdboot
description: Windows**コマンドのトピックでは、システム**パーティションを迅速に設定するか、システムパーティションにあるブート環境を修復します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e62a250e-08e9-47f6-89d1-e6002560ab57
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 637170cbd8ee4f3c11ee1dc77a0cd49b5dfa3038
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851085"
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
| source | ブート環境ファイルをコピーするためのソースとして使用する Windows ディレクトリの場所を指定します。 |
| /l | ロケールを指定します。 既定のロケールは英語 (米国) です。 |
| /s | システム パーティションのボリューム文字を指定します。 既定値は、ファームウェアによって識別されるシステムパーティションです。 |

## <a name="examples"></a><a name=BKMK_examples></a>例

このコマンドの使用方法の詳細と使用例については、「Bcdboot の[コマンドラインオプション](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/hh824874(v=win.10)x)」を参照してください。

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)