---
title: dispdiag
description: 表示情報をファイルに記録する dispdiag のリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5079e1dd-b57c-44ed-970f-e6b409369e03
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f9f44e261b9c46157fb3e6bb7f9105af2480a60b
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719411"
---
# <a name="dispdiag"></a>dispdiag

ログには、ファイルの情報が表示されます。

## <a name="syntax"></a>構文

```
dispdiag [-testacpi] [-d] [-delay <Seconds>] [-out <FilePath>]
```

#### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|-testacpi|ホットキー診断テストを実行します。 テスト中に押されたキーのキー名、コード、およびスキャンコードを表示します。|
|-d|テスト結果と共にダンプファイルを生成します。|
|-遅延\<時間 (秒)>|指定された時間 *(秒単位)* でデータの収集を遅らせます。|
|-out \<FilePath>|収集したデータを保存するパスとファイル名を指定します。 これは、最後のパラメーターである必要があります。|
|-?|使用可能なコマンドパラメーターを表示し、それらを使用するためのヘルプを提供します。|