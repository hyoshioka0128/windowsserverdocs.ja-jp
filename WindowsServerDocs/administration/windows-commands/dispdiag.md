---
title: dispdiag
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 9c96c70aac1b3329e050fa8b02743e61fed44d15
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59831463"
---
# <a name="dispdiag"></a>dispdiag



ログは、ファイルに情報を表示します。

## <a name="syntax"></a>構文

```
dispdiag [-testacpi] [-d] [-delay <Seconds>] [-out <FilePath>]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|-testacpi|ホットキー診断テストを実行します。 テスト中にコードとスキャンのコードを任意のキーが押されたキーの名前を表示します。|
|-d|テスト結果のダンプ ファイルを生成します。|
|-遅延\<(秒) >|指定した時間のデータのコレクションを遅らせます*秒*します。|
|-アウト\<FilePath >|パスと収集されたデータを保存するファイル名を指定します。 これには、最後のパラメーターがあります。|
|-?|使用可能なコマンドのパラメーターを表示し、それらの使用に関するヘルプを提供します。|