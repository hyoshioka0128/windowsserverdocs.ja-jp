---
title: wmic
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 76397c72-d06f-4cea-88cf-c7603315a983
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6c68866fbe0c8f5b16dae77e2121331f06cdc726
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59885843"
---
# <a name="wmic"></a>wmic



対話型コマンド シェル内で WMI 情報を表示します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
command </parameter>
```

## <a name="sub-commands"></a>サブ コマンド

次のサブ コマンドは、常に使用できます。

|サブ コマンド|説明|
|-----------|-----------|
|クラス|WMI スキーマ内のクラスに直接アクセスする WMIC の既定のエイリアス モードからエスケープします。|
|path|WMI スキーマのインスタンスに直接アクセスする WMIC の既定のエイリアス モードからエスケープします。|
|コンテキスト|すべてのグローバル スイッチの現在の値が表示されます。|
|[終了\|終了]|終了、WMIC はコマンド シェルです。|

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|</parameter>|\<簡潔な説明が始まる動詞 >。|
|</param2>|\<もう 1 つの簡潔な説明が始まる動詞 >。|


## <a name="BKMK_examples"></a>例

すべてのグローバル スイッチの現在の値を表示するには、次のように入力します。
```
wmic context
```
次のような出力:
```
NAMESPACE    : root\cimv2
ROLE         : root\cli
NODE(S)      : BOBENTERPRISE
IMPLEVEL     : IMPERSONATE
[AUTHORITY   : N/A]
AUTHLEVEL    : PKTPRIVACY
LOCALE       : ms_409
PRIVILEGES   : ENABLE
TRACE        : OFF
RECORD       : N/A
INTERACTIVE  : OFF
FAILFAST     : OFF
OUTPUT       : STDOUT
APPEND       : STDOUT
USER         : N/A
AGGREGATE    : ON
```
言語を変更するのには、ID は、型を英語 (ロケール ID 409) するためのコマンドラインで使用。
```
wmic /locale:ms_409
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)