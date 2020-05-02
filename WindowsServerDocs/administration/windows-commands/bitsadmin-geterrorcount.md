---
title: bitsadmin geterrorcount
description: Bitsadmin geterrorcount コマンドのリファレンストピックでは、指定されたジョブが一時的なエラーを生成した回数のカウントを取得します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8840ae78-52b0-4c7e-b592-0547359a237e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 516bd02ed296a2eba75e174c6f084926bde63e90
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718006"
---
# <a name="bitsadmin-geterrorcount"></a>bitsadmin geterrorcount

指定したジョブが一時的なエラーを生成した回数のカウントを取得します。

## <a name="syntax"></a>構文

```
bitsadmin /geterrorcount <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブのエラー数情報を取得するには、次のようにします。

```
bitsadmin /geterrorcount myDownloadJob
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
