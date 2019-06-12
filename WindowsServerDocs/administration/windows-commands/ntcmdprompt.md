---
title: ntcmdprompt
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0063bdbb-dc2b-41c4-99ee-b011603aaa86
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 583f56c294e66542a75efca09e97d57ae54a8cea
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66436427"
---
# <a name="ntcmdprompt"></a>ntcmdprompt

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

コマンド インタープリターが実行**Cmd.exe**、なく**Command.com**Terminate と TSR) を実行した後、または、MS-DOS アプリケーション内からコマンド プロンプトを起動した後。
## <a name="syntax"></a>構文
```
ntcmdprompt
```
### <a name="parameters"></a>パラメーター

| パラメーター |             説明              |
|-----------|--------------------------------------|
|    /?     | コマンド プロンプトにヘルプを表示します。 |

## <a name="remarks"></a>注釈
- ときに**Command.com**実行している、一部の機能の**Cmd.exe**など、 **doskey**コマンド履歴の表示、利用できません。 実行する場合、 **Cmd.exe** MS-DOS に基づいてアプリケーション内からコマンド プロンプトを開始または終了と TSR) を開始した後は、コマンド インタープリターを使用できます、 **ntcmdprompt**コマンド。 ただし、留意する TSR できない可能性があります使用可能な実行しているときに**Cmd.exe**します。 含めることができます、 **ntcmdprompt**コマンド、 **Config.nt**ファイルまたはアプリケーションのプログラム情報ファイル (Pif) で同等のカスタム スタートアップ ファイルです。
  ## <a name="examples"></a>例
  含める**ntcmdprompt**で、 **Config.nt**ファイル、または Pif、型で指定された構成のスタートアップ ファイル: **ntcmdprompt**
  ## <a name="additional-references"></a>その他の参照
- [コマンド ライン構文の記号](command-line-syntax-key.md)

