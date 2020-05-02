---
title: wmic
description: 対話型コマンドシェル内に WMI 情報を表示する wmic のリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 76397c72-d06f-4cea-88cf-c7603315a983
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 252ba6b59c29378dd1f5e437de21a2ec4f5ec5c8
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720654"
---
# <a name="wmic"></a>wmic



対話型コマンドシェル内に WMI 情報を表示します。



## <a name="syntax"></a>構文

```
wmic </parameter>
```

## <a name="sub-commands"></a>サブコマンド

次のサブコマンドは常に使用できます。

|サブコマンド|[説明]|
|-----------|-----------|
|class|WMIC の既定のエイリアスモードをエスケープして、WMI スキーマ内のクラスに直接アクセスします。|
|path|WMIC の既定のエイリアスモードをエスケープして、WMI スキーマ内のインスタンスに直接アクセスできるようにします。|
|context|すべてのグローバルスイッチの現在の値を表示します。|
|[終了\|終了]|WMIC コマンドシェルを終了します。|

## <a name="examples"></a>例

すべてのグローバルスイッチの現在の値を表示するには、次のように入力します。
```
wmic context
```
次のような出力が表示されます。
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
コマンドラインで使用される言語 ID を英語 (ロケール ID 409) に変更するには、次のように入力します。
```
wmic /locale:ms_409
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)
