---
title: bitsadmin wrap
description: '**Bitsadmin wrap**の Windows コマンドトピックでは、コマンドウィンドウの右端から次の行まで拡張する出力テキストの行をラップしています。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 14e57522-539d-4621-ad15-09f7a44ccab7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e754a765d94661baf24190431b455584d29991ec
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/11/2020
ms.locfileid: "81122562"
---
# <a name="bitsadmin-wrap"></a>bitsadmin wrap

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

コマンドウィンドウの右端から次の行まで拡張する出力テキストの行をラップします。 このスイッチは、他のスイッチの前に指定する必要があります。

既定では、 [bitsadmin monitor](bitsadmin-monitor.md)スイッチを除くすべてのスイッチによって出力テキストがラップされます。

## <a name="syntax"></a>構文

```
bitsadmin /wrap <job>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ---------- |
| Job | ジョブの表示名または GUID。 |

## <a name="examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブの情報を取得し、出力をラップします。

```
C:\>bitsadmin /wrap /info myDownloadJob /verbose
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
