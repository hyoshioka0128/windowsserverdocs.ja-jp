---
title: tzutil
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bcf6e007-c9b6-4df5-83c5-ed7b4b1b5913
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 41a46ea7974b67cc557973484428480e7beb5484
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59876803"
---
# <a name="tzutil"></a>tzutil

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

表示、Windows は時刻ゾーン ユーティリティ。 
## <a name="syntax"></a>構文
```
tzutil [/?] [/g] [/s <timeZoneID>[_dstoff]] [/l]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/?|コマンド プロンプトにヘルプを表示します。|
|/g|現在のタイム ゾーン ID を表示します|
|/s \<timeZoneID>[_dstoff]|指定されたタイム ゾーン ID を使用して現在のタイム ゾーンの設定します。 **_Dstoff**サフィックス (該当する場合) のタイム ゾーンの夏時間調整を無効にします。|
|/l|リストのすべての有効な時刻は、ゾーンの Id と表示名。 出力になります。<br /><br />-   \<表示名 ><br />-   \<タイム ゾーン ID >|

## <a name="remarks"></a>注釈
終了コードを**0**コマンドが正常に完了したことを示します。

## <a name="BKMK_Examples"></a>例
現在のタイム ゾーン ID を表示するには、次のように入力します。
```
tzutil /g
```
現在のタイム ゾーンを太平洋標準時に設定するに次のように入力します。
```
tzutil /s Pacific Standard time
```
太平洋標準時に現在のタイム ゾーンの設定を夏時間の調整を無効にするには、次のように入力します。
```
tzutil /s Pacific Standard time_dstoff
```
## <a name="additional-references"></a>その他の参照
-   [コマンドライン構文キー](command-line-syntax-key.md)

