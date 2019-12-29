---
title: bitsadmin wrap
description: '**Bitsadmin wrap**の Windows コマンドトピックでは、コマンドウィンドウの右端から次の行まで拡張する出力テキストの行をラップします。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 14e57522-539d-4621-ad15-09f7a44ccab7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5609fb6f38716795a545e0c7fe3939f893a8c8d5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380683"
---
# <a name="bitsadmin-wrap"></a>bitsadmin wrap

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

コマンドウィンドウに合わせるために出力をラップします。

## <a name="syntax"></a>構文

```
bitsadmin /Wrap Job
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------|--------|
|Job|ジョブの表示名または GUID|

## <a name="remarks"></a>コメント

他のスイッチの前に指定します。 既定では、 [bitsadmin monitor](bitsadmin-monitor.md)スイッチを除くすべてのスイッチが出力をラップします。

## <a name="BKMK_examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブの情報を取得し、出力をラップします。

```
C:\>bitsadmin /Wrap /Info myDownloadJob /verbose
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)
