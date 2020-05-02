---
title: bitsadmin getsecurityflags
description: Bitsadmin getsecurityflags コマンドのリファレンストピック。転送中にサーバー証明書に対して実行される URL リダイレクトとチェックの HTTP セキュリティフラグを報告します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c2e73519-34f4-487b-af11-97d5d08ef9bb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 41b710f9897f24eb4161d9379dc3b1f89b141472
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717550"
---
# <a name="bitsadmin-getsecurityflags"></a>bitsadmin getsecurityflags

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

転送中にサーバー証明書に対して実行された URL リダイレクトおよび確認の HTTP セキュリティフラグを報告します。

## <a name="syntax"></a>構文

```
bitsadmin /getsecurityflags <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブからセキュリティフラグを取得するには、次のようにします。

```
bitsadmin /getsecurityflags myDownloadJob
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
