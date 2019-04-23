---
title: bitsadmin wrap
description: Windows コマンド」のトピック**bitsadmin ラップ**-出力テキストは次の行にコマンド ウィンドウの右端の端を超えて拡張の任意の行をラップします。
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 4834a8a17c72394b6ee8f051ec76919af9880124
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881673"
---
# <a name="bitsadmin-wrap"></a>bitsadmin wrap

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

コマンド ウィンドウに収まるように出力をラップします。

## <a name="syntax"></a>構文

```
bitsadmin /Wrap Job
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------|--------|
|Job|ジョブの表示名または GUID|

## <a name="remarks"></a>注釈

その他のスイッチの前に指定します。 既定ですべてのスイッチを除く、 [bitsadmin モニター](bitsadmin-monitor.md)スイッチ、出力をラップします。

## <a name="BKMK_examples"></a>例

次の例では、という名前のジョブの情報を取得する*myDownloadJob*し、出力をラップします。

```
C:\>bitsadmin /Wrap /Info myDownloadJob /verbose
```

#### <a name="additional-references"></a>その他の参照

[コマンドライン構文キー](command-line-syntax-key.md)
