---
title: bitsadmin listfiles
description: 指定されたジョブ内のファイルを一覧表示する bitsadmin listfiles コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ad0d1eaa-3bd8-45e5-8f72-4da7366f0d59
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6826c1ec2f624a06d11fedcb8ca9f14d86b7ec27
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717417"
---
# <a name="bitsadmin-listfiles"></a>bitsadmin listfiles

指定されたジョブ内のファイルを一覧表示します。

## <a name="syntax"></a>構文

```
bitsadmin /listfiles <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブのファイルの一覧を取得するには、次のようにします。

```
bitsadmin /listfiles myDownloadJob
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
