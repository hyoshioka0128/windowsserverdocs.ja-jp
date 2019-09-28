---
title: tzutil
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 347254bd5a00a8bfb4a80f20d518f1e0e8b593bf
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392301"
---
# <a name="tzutil"></a>tzutil

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Windows タイムゾーンユーティリティを表示します。 
## <a name="syntax"></a>構文
```
tzutil [/?] [/g] [/s <timeZoneID>[_dstoff]] [/l]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/?|コマンド プロンプトにヘルプを表示します。|
|/g|現在のタイムゾーン ID を表示します。|
|/s \<timeZoneID > [/dstoff]|指定されたタイムゾーン ID を使用して、現在のタイムゾーンを設定します。 (該当する場合) タイムゾーンの夏時間調整が無効になります ( **_d** )。|
|/l|有効なタイムゾーン Id と表示名をすべて一覧表示します。 出力は次のようになります。<br /><br />-    @ no__t-1 表示名 ><br />-    @ no__t-1time ゾーン ID >|

## <a name="remarks"></a>コメント
終了コード**0**は、コマンドが正常に完了したことを示します。

## <a name="BKMK_Examples"></a>例
現在のタイムゾーン ID を表示するには、次のように入力します。
```
tzutil /g
```
現在のタイムゾーンを太平洋標準時に設定するには、次のように入力します。
```
tzutil /s Pacific Standard time
```
現在のタイムゾーンを太平洋標準時に設定し、夏時間調整を無効にするには、次のように入力します。
```
tzutil /s Pacific Standard time_dstoff
```
## <a name="additional-references"></a>その他の参照情報
-   [コマンド ライン構文の記号](command-line-syntax-key.md)

