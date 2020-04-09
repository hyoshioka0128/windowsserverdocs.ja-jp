---
title: tzutil
description: Windows タイムゾーンユーティリティを表示する tzutil の windows コマンドに関するトピック。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bcf6e007-c9b6-4df5-83c5-ed7b4b1b5913
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 330ee1eb4318df5aca1a5bb1a456711cd103c467
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80832345"
---
# <a name="tzutil"></a>tzutil

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Windows タイムゾーンユーティリティを表示します。 

## <a name="syntax"></a>構文
```
tzutil [/?] [/g] [/s <timeZoneID>[_dstoff]] [/l]
```
#### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/?|コマンド プロンプトでヘルプを表示します。|
|/g|現在のタイムゾーン ID を表示します。|
|/s \<timeZoneID > [_dstoff]|指定されたタイムゾーン ID を使用して、現在のタイムゾーンを設定します。 **_Dstoff**サフィックスは、タイムゾーンの夏時間調整を無効にします (該当する場合)。|
|/l|有効なタイムゾーン Id と表示名をすべて一覧表示します。 出力は次のようになります。<p>-   \<表示名 ><br />-   \<タイムゾーン ID >|

## <a name="remarks"></a>コメント
終了コード**0**は、コマンドが正常に完了したことを示します。

## <a name="examples"></a><a name=BKMK_Examples></a>例
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
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)

