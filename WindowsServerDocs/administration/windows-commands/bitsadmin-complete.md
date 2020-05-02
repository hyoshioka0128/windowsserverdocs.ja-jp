---
title: bitsadmin complete
description: ジョブを完了する bitsadmin complete コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a5e86677-8f7b-43b3-929e-97706c57e7f1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6b61f3475afdb0e29e5777940e6426a04fe33e78
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718227"
---
# <a name="bitsadmin-complete"></a>bitsadmin complete

ジョブを完了します。 ジョブが転送済み状態に移行した後に、このスイッチを使用します。 そうしないと、正常に転送されたファイルのみが使用可能になります。

## <a name="syntax"></a>構文

```
bitsadmin /complete <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| --------- | ----------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="example"></a>例

*Mydownloadjob*ジョブを完了するには、 `TRANSFERRED`次のようにします。

```
bitsadmin /complete myDownloadJob
```

複数のジョブが*Mydownloadjob*を名前として使用している場合は、ジョブの GUID を使用して、ジョブの完了を一意に識別する必要があります。

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
