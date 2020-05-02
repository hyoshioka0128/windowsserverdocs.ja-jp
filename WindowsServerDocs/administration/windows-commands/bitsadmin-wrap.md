---
title: bitsadmin wrap
description: Bitsadmin wrap コマンドのリファレンストピック。コマンドウィンドウの右端から次の行まで拡張する出力テキストの行をラップします。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 14e57522-539d-4621-ad15-09f7a44ccab7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8c1c2c78fd3cc78674ef497526ba236ad058fe83
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82707571"
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

| パラメーター | [説明] |
| --------- | ---------- |
| ジョブ (job) | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブの情報を取得し、出力テキストをラップするには、次のように入力します。

```
bitsadmin /wrap /info myDownloadJob /verbose
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
