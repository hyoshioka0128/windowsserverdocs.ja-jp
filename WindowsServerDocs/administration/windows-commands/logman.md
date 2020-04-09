---
title: logman
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 574a5203-5b3b-4759-a678-f26d00dde447
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bb6654cce0e23ac08a2fa6334d6144b08c8b65f3
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80840405"
---
# <a name="logman"></a>logman

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

**logman**は、イベントトレースセッションとパフォーマンスログを作成して管理し、コマンドラインからのパフォーマンスモニターの多くの機能をサポートします。
## <a name="syntax"></a>構文
```
logman [create | query | start | stop | delete| update | import | export | /?] [options]
```
## <a name="actions"></a>操作
|操作|説明|
|-----|--------|
|[logman create](logman-create.md)|カウンター、トレース、構成データコレクター、または API を作成します。|
|[logman query](logman-query.md)|データコレクターのプロパティを照会します。|
|[logman start &#124; stop](logman-start-stop.md)|データコレクションを開始または停止します。|
|[logman delete](logman-delete.md)|既存のデータコレクターを削除します。|
|[logman update](logman-update.md)|既存のデータコレクターのプロパティを更新します。|
|[logman import &#124; export](logman-import-export.md)|XML ファイルからデータコレクターセットをインポートするか、データコレクターセットを XML ファイルにエクスポートします。|
