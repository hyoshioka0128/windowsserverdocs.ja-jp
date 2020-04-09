---
title: dispdiag
description: Dispdiag の Windows コマンドに関するトピックでは、ファイルに情報を表示します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5079e1dd-b57c-44ed-970f-e6b409369e03
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 498294aa6678cc4904880128bca55d7900c91db5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80845385"
---
# <a name="dispdiag"></a>dispdiag

ログには、ファイルの情報が表示されます。

## <a name="syntax"></a>構文

```
dispdiag [-testacpi] [-d] [-delay <Seconds>] [-out <FilePath>]
```

#### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|-testacpi|ホットキー診断テストを実行します。 テスト中に押されたキーのキー名、コード、およびスキャンコードを表示します。|
|-d|テスト結果と共にダンプファイルを生成します。|
|-遅延 \<秒 >|指定された時間 *(秒単位)* でデータの収集を遅らせます。|
|-out \<FilePath >|収集したデータを保存するパスとファイル名を指定します。 これは、最後のパラメーターである必要があります。|
|-?|使用可能なコマンドパラメーターを表示し、それらを使用するためのヘルプを提供します。|