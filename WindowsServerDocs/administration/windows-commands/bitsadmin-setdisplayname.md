---
title: bitsadmin setdisplayname
description: Bitsadmin setdisplayname コマンドのリファレンストピックでは、指定されたジョブの表示名を設定します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 13706c53-fb5f-4879-b5ca-82531361d6e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 382cb2f20f0374c2d2787c4c3d88670b4f7260cd
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719387"
---
# <a name="bitsadmin-setdisplayname"></a>bitsadmin setdisplayname

指定されたジョブの表示名を設定します。

## <a name="syntax"></a>構文

```
bitsadmin /setdisplayname <job> <display_name>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| --------- | ----------- |
| ジョブ (job) | ジョブの表示名または GUID。 |
| display_name | 特定のジョブの表示名として使用されるテキスト。 |

## <a name="examples"></a>例

ジョブの表示名を*Mydownloadjob*に設定するには、次のようにします。

```
bitsadmin /setdisplayname myDownloadJob
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
