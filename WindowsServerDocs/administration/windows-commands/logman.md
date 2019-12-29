---
title: logman
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 574a5203-5b3b-4759-a678-f26d00dde447
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 420c591a8a6c15d563a344d0450be5eb7da46191
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374258"
---
# <a name="logman"></a>logman

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

**logman**は、イベントトレースセッションとパフォーマンスログを作成して管理し、コマンドラインからのパフォーマンスモニターの多くの機能をサポートします。
## <a name="syntax"></a>構文
```
logman [create | query | start | stop | delete| update | import | export | /?] [options]
```
## <a name="actions"></a>Actions
|操作|説明|
|-----|--------|
|[logman create](logman-create.md)|カウンター、トレース、構成データコレクター、または API を作成します。|
|[logman query](logman-query.md)|データコレクターのプロパティを照会します。|
|[logman start &#124; stop](logman-start-stop.md)|データコレクションを開始または停止します。|
|[logman delete](logman-delete.md)|既存のデータコレクターを削除します。|
|[logman update](logman-update.md)|既存のデータコレクターのプロパティを更新します。|
|[logman import &#124; export](logman-import-export.md)|XML ファイルからデータコレクターセットをインポートするか、データコレクターセットを XML ファイルにエクスポートします。|
