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
ms.openlocfilehash: 65804f99095d0c0a56537b1d155ac26e768f61a7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827663"
---
# <a name="ntcmdprompt"></a>ntcmdprompt

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

コマンド インタープリターが実行**Cmd.exe**、なく**Command.com**Terminate と TSR) を実行した後、または、MS-DOS アプリケーション内からコマンド プロンプトを起動した後。
## <a name="syntax"></a>構文
```
ntcmdprompt
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/?|コマンド プロンプトにヘルプを表示します。|
## <a name="remarks"></a>注釈
-   ときに**Command.com**実行している、一部の機能の**Cmd.exe**など、 **doskey**コマンド履歴の表示、利用できません。 実行する場合、 **Cmd.exe** MS-DOS に基づいてアプリケーション内からコマンド プロンプトを開始または終了と TSR) を開始した後は、コマンド インタープリターを使用できます、 **ntcmdprompt**コマンド。 ただし、留意する TSR できない可能性があります使用可能な実行しているときに**Cmd.exe**します。 含めることができます、 **ntcmdprompt**コマンド、 **Config.nt**ファイルまたはアプリケーションのプログラム情報ファイル (Pif) で同等のカスタム スタートアップ ファイルです。
## <a name="examples"></a>例
含める**ntcmdprompt**で、 **Config.nt**ファイル、または Pif、型で指定された構成のスタートアップ ファイル: **ntcmdprompt**
## <a name="additional-references"></a>その他の参照
-   [コマンドライン構文キー](command-line-syntax-key.md)

