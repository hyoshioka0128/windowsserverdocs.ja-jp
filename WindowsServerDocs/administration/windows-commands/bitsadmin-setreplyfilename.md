---
title: bitsadmin setreplyfilename
description: '**Bitsadmin setreplyfilename**の Windows コマンドに関するトピックでは、サーバーのアップロードと応答を含むファイルのパスを指定しています。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c26d3342-0533-40b1-a13e-e09678232b25
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6c476073cb22ff66bcefc75a45fcd0526cdf3d25
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/11/2020
ms.locfileid: "81122734"
---
# <a name="bitsadmin-setreplyfilename"></a>bitsadmin setreplyfilename

サーバーのアップロード-応答を含むファイルのパスを指定します。

> [!NOTE]
> このコマンドは、BITS 1.2 以前ではサポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /setreplyfilename <job> <file_path>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| 送信 | ジョブの表示名または GUID。 |
| file_path | サーバーのアップロード-応答を配置する場所。 |

## <a name="examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブのアップロード応答ファイル名ファイルパスを設定します。

```
C:\>bitsadmin /setreplyfilename myDownloadJob c:\upload-reply
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)