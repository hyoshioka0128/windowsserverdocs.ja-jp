---
title: convert
description: Windows コマンドに関するトピックでは、ディスクをあるディスクの種類から別のディスクの種類に変換します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ae151297-af21-4701-bd69-21d775518e03
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b1b5c62b7e51b497faac77a13185f844de230d67
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80847185"
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

|パラメーター|説明|
|---------|-----------|
|[基本の変換](convert-basic.md)|空のダイナミック ディスクをベーシック ディスクに変換します。|
|[動的変換](convert-dynamic.md)|ベーシック ディスクをダイナミック ディスクに変換します。|
|[Gpt の変換](convert-gpt.md)|マスター ブート レコード (MBR) パーティション スタイルを持つ空のベーシック ディスクを、GUID パーティション テーブル (GPT) パーティション スタイルを持つベーシック ディスクに変換します。|
|[Mbr の変換](convert-mbr.md)|GUID パーティションテーブル (GPT) パーティションスタイルを持つ空のベーシックディスクを、マスターブートレコード (MBR) パーティションスタイルを持つベーシックディスクに変換します。|

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

