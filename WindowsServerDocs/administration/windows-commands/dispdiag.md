---
title: dispdiag
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5079e1dd-b57c-44ed-970f-e6b409369e03
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9b640883a207648d2ef6c9a7d6e5366cd0bb384c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377756"
---
# <a name="dispdiag"></a>dispdiag



ログには、ファイルの情報が表示されます。

## <a name="syntax"></a>構文

```
dispdiag [-testacpi] [-d] [-delay <Seconds>] [-out <FilePath>]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|-testacpi|ホットキー診断テストを実行します。 テスト中に押されたキーのキー名、コード、およびスキャンコードを表示します。|
|-d|テスト結果と共にダンプファイルを生成します。|
|-delay \<Seconds >|指定された時間 *(秒単位)* でデータの収集を遅らせます。|
|-out \<FilePath >|収集したデータを保存するパスとファイル名を指定します。 これは、最後のパラメーターである必要があります。|
|-?|使用可能なコマンドパラメーターを表示し、それらを使用するためのヘルプを提供します。|