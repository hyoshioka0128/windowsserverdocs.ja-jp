---
title: bitsadmin wrap
description: Bitsadmin wrap の Windows コマンドトピックでは、コマンドウィンドウの右端から次の行まで拡張する出力テキストの行をラップしています。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 14e57522-539d-4621-ad15-09f7a44ccab7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 009a0452f44c4944ae110ca6b9e0570793c32a72
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848755"
---
# <a name="bitsadmin-wrap"></a>bitsadmin wrap

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

コマンドウィンドウの右端から次の行まで拡張する出力テキストの行をラップします。

## <a name="syntax"></a>構文

```
bitsadmin /Wrap Job
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------|--------|
|Job|ジョブの表示名または GUID|

## <a name="remarks"></a>コメント

他のスイッチの前に指定します。 既定では、 [bitsadmin monitor](bitsadmin-monitor.md)スイッチを除くすべてのスイッチが出力をラップします。

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、 *Mydownloadjob*という名前のジョブの情報を取得し、出力をラップします。

```
C:\>bitsadmin /Wrap /Info myDownloadJob /verbose
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
