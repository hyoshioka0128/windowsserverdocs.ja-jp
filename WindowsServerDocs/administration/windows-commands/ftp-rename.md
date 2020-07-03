---
title: ftp rename
description: リモートファイルの名前を変更する ftp rename コマンドの参照記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 977b7c95-6428-4980-80ec-79c3ae7e8c4d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f46caa4394be9edc80da018d88809a0dd6e91862
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85925736"
---
# <a name="ftp-rename"></a>ftp rename

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモートファイルの名前を変更します。

## <a name="syntax"></a>構文

```
rename <filename> <newfilename>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<filename>` | 名前を変更するファイルを指定します。 |
| `<newfilename>` | 新しいファイル名を指定します。 |

### <a name="examples"></a>例

リモートファイル*example.txt*の名前を*example1.txt*に変更するには、次のように入力します。

```
rename example.txt example1.txt
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [追加の FTP ガイダンス](https://docs.microsoft.com/previous-versions/orphan-topics/ws.10/cc756013(v=ws.10))
