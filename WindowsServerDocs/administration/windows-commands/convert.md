---
title: convert
description: ディスクの種類をディスクから別のディスクに変換する convert コマンドの参照記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ae151297-af21-4701-bd69-21d775518e03
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f93f2b16838a6f54af3f28b7e0883808a6cd013a
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928901"
---
# <a name="convert"></a>convert

ディスクをディスクの種類別に変換します。

## <a name="syntax"></a>構文

```
convert basic
convert dynamic
convert gpt
convert mbr
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| [基本コマンドの変換](convert-basic.md) | 空のダイナミック ディスクをベーシック ディスクに変換します。 |
| [動的コマンドの変換](convert-dynamic.md) | ベーシック ディスクをダイナミック ディスクに変換します。 |
| [gpt コマンドの変換](convert-gpt.md) | マスター ブート レコード (MBR) パーティション スタイルを持つ空のベーシック ディスクを、GUID パーティション テーブル (GPT) パーティション スタイルを持つベーシック ディスクに変換します。 |
| [mbr コマンドの変換](convert-mbr.md) | GUID パーティションテーブル (GPT) パーティションスタイルを持つ空のベーシックディスクを、マスターブートレコード (MBR) パーティションスタイルを持つベーシックディスクに変換します。 |

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
