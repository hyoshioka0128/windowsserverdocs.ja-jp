---
title: bitsadmin replaceremoteprefix
description: Bitsadmin replaceremoteprefix コマンドのリファレンストピック。必要に応じて、ジョブ内のすべてのファイルのリモート URL を*oldprefix*から*newprefix*に変更します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d0e0abb1-bdb4-4c74-abbc-16c809f5fd81
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 745d026513413db799e86df3422d5ee19c89274f
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717035"
---
# <a name="bitsadmin-replaceremoteprefix"></a>bitsadmin replaceremoteprefix

必要に応じて、ジョブ内のすべてのファイルのリモート URL を*oldprefix*から*newprefix*に変更します。

## <a name="syntax"></a>構文

```
bitsadmin /replaceremoteprefix <job> <oldprefix> <newprefix>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |
| oldprefix | 既存の URL プレフィックス。 |
| newprefix | 新しい URL プレフィックス。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブ内のすべてのファイルのリモート URL *http://stageserver*を*http://prodserver*に変更するには、をからに変更します。

```
bitsadmin /replaceremoteprefix myDownloadJob http://stageserver http://prodserver
```

## <a name="additional-information"></a>追加情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
