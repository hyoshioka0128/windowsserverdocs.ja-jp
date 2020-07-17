---
title: bitsadmin wrap
description: Bitsadmin wrap コマンドの参照記事。コマンドウィンドウの右端から次の行まで拡張する出力テキストの行をラップします。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 14e57522-539d-4621-ad15-09f7a44ccab7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e47f5e38555eb2464d3febf5f958ce5a6af20452
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85927250"
---
# <a name="bitsadmin-wrap"></a>bitsadmin wrap

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

コマンドウィンドウの右端から次の行まで拡張する出力テキストの行をラップします。 このスイッチは、他のスイッチの前に指定する必要があります。

既定では、 [bitsadmin monitor](bitsadmin-monitor.md)スイッチを除くすべてのスイッチによって出力テキストがラップされます。

## <a name="syntax"></a>構文

```
bitsadmin /wrap <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ---------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブの情報を取得し、出力テキストをラップするには、次のように入力します。

```
bitsadmin /wrap /info myDownloadJob /verbose
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
