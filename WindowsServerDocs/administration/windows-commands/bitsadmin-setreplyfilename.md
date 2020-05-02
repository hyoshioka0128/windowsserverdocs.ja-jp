---
title: bitsadmin setreplyfilename
description: Bitsadmin setreplyfilename コマンドのリファレンストピック。サーバーのアップロード-応答を含むファイルのパスを指定します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c26d3342-0533-40b1-a13e-e09678232b25
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2f0bd184db274dc915817ff3e26ae2c686190c27
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720479"
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

| パラメーター | [説明] |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |
| file_path | サーバーのアップロード-応答を配置する場所。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブのアップロード応答ファイル名ファイルパスを設定するには、次のようにします。

```
bitsadmin /setreplyfilename myDownloadJob c:\upload-reply
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
