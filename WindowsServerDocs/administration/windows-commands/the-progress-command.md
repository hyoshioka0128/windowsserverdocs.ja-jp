---
title: progress
description: 進行状況に関する参照記事。コマンドの実行中に進行状況を表示します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8ce5e77b-e13f-4ac3-948d-31770a6c7e25
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9e9650a980d74f15bc0ec5c88d8df2dc93a3d8b0
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85934588"
---
# <a name="progress"></a>progress

コマンドの実行中に進行状況を表示します。 使用することができます **]、[進行状況の** を実行するその他の WDSUTIL コマンドを使用します。 指定する必要があります **/verbose** と **]、[進行状況の** 直後後 **WDSUTIL**します。

## <a name="syntax"></a>構文

```
WDSUTIL /progress <commands>
```

## <a name="examples"></a>例

サーバーを初期化して進行状況を表示、次のように入力します。
```
WDSUTIL /Verbose /Progress /Initialize-Server /Server:MyWDSServer /RemInst:C:\RemoteInstall
```