---
title: bitsadmin getproxyusage
description: Bitsadmin getproxyusage コマンドの参照記事。指定されたジョブのプロキシ使用法の設定を取得します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f940a70e-3b02-497e-a47f-b37b905c299e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ad1ffe5786202d6fecc0d65a719c9d6be0f5609e
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926781"
---
# <a name="bitsadmin-getproxyusage"></a>bitsadmin getproxyusage

指定したジョブのプロキシ使用法の設定を取得します。

## <a name="syntax"></a>構文

```
bitsadmin /getproxyusage <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

#### <a name="output"></a>出力

返されるプロキシの使用値は、次のようになります。

- **Preconfig** -所有者の Internet Explorer の既定値を使用します。

- **No_Proxy** -プロキシサーバーを使用しないでください。

- **Override** -明示的なプロキシリストを使用します。

- **自動**検出-プロキシ設定を自動的に検出します。

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブのプロキシ使用法を取得するには、次のようにします。

```
bitsadmin /getproxyusage myDownloadJob
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
