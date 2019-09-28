---
title: ntcmdprompt
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 5fef1641bf1b48bd1fe4aaf284ed309ab4d4d5f1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372669"
---
# <a name="ntcmdprompt"></a>ntcmdprompt

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Terminate (TSR) を実行した後、または MS-DOS アプリケーション内からコマンドプロンプトを起動した後、 **Command.com**ではなく、コマンドインタープリター **cmd.exe**を実行します。
## <a name="syntax"></a>構文
```
ntcmdprompt
```
### <a name="parameters"></a>パラメーター

| パラメーター |             説明              |
|-----------|--------------------------------------|
|    /?     | コマンド プロンプトにヘルプを表示します。 |

## <a name="remarks"></a>コメント
- **Command.com**が実行されている場合、コマンド履歴の**doskey**表示など、 **cmd.exe**の一部の機能は使用できません。 終了と常駐 (TSR) を開始した後、または MS-DOS に基づくアプリケーション内からコマンドプロンプトを起動した後に**cmd.exe**コマンドインタープリターを実行する場合は、 **ntcmdprompt**コマンドを使用できます。 ただし、 **cmd.exe**を実行している場合は、TSR を使用できない可能性があることに注意してください。 **Ntcmdprompt**コマンドは、アプリケーションのプログラム情報ファイル (Pif) にある**config.xml**ファイルまたはそれと同等のカスタムスタートアップファイルに含めることができます。
  ## <a name="examples"></a>使用例
  **Ntcmdprompt**を**config.xml**ファイルに含めるか、または Pif で指定された構成スタートアップファイルに含めるには、「 **ntcmdprompt** 」と入力します。
  ## <a name="additional-references"></a>その他の参照情報
- [コマンド ライン構文の記号](command-line-syntax-key.md)

