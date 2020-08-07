---
title: bitsadmin getreplyfilename
description: Bitsadmin getreplyfilename コマンドの参照記事。このコマンドは、ジョブのサーバーアップロード応答を含むファイルのパスを取得します。
ms.topic: article
ms.assetid: 85447184-1732-4816-a365-2e3599551bf8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 213df5c5dcef57db8f1cdc2b26c90dbdc124007c
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893886"
---
# <a name="bitsadmin-getreplyfilename"></a>bitsadmin getreplyfilename

ジョブのサーバーアップロード-応答を含むファイルのパスを取得します。

> [!NOTE]
> このコマンドは、BITS 1.2 以前ではサポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /getreplyfilename <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブのアップロード応答ファイル名を取得するには、次のようにします。

```
bitsadmin /getreplyfilename myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
