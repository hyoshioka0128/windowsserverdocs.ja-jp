---
title: logman
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 574a5203-5b3b-4759-a678-f26d00dde447
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9aed5a83c503c03f52757abf525aa5d122f41466
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724272"
---
# <a name="logman"></a>logman

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

**logman**は、イベントトレースセッションとパフォーマンスログを作成して管理し、コマンドラインからのパフォーマンスモニターの多くの機能をサポートします。
## <a name="syntax"></a>構文
```
logman [create | query | start | stop | delete| update | import | export | /?] [options]
```
## <a name="actions"></a>Actions
|アクション|説明|
|-----|--------|
|[logman create](logman-create.md)|カウンター、トレース、構成データコレクター、または API を作成します。|
|[logman query](logman-query.md)|データコレクターのプロパティを照会します。|
|[logman start &#124; stop](logman-start-stop.md)|データコレクションを開始または停止します。|
|[logman delete](logman-delete.md)|既存のデータコレクターを削除します。|
|[logman update](logman-update.md)|既存のデータコレクターのプロパティを更新します。|
|[logman import &#124; export](logman-import-export.md)|XML ファイルからデータコレクターセットをインポートするか、データコレクターセットを XML ファイルにエクスポートします。|
