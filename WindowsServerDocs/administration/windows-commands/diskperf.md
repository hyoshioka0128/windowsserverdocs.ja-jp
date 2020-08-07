---
title: diskperf
description: Windows を実行しているコンピューターで物理ディスクまたは論理ディスクのパフォーマンスカウンターをリモートで有効または無効にするために使用できる、diskperf コマンドの参照記事。
ms.topic: article
ms.assetid: f06916e8-069b-4ec8-a6eb-59f1d9f77111
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 81cefe217abaa7b2d4ee843f3887076f66484422
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87890863"
---
# <a name="diskperf"></a>diskperf

**Diskperf**コマンドは、Windows を実行しているコンピューターの物理ディスクまたは論理ディスクのパフォーマンスカウンターをリモートで有効または無効にします。

## <a name="syntax"></a>構文

```
diskperf [-y[d|v] | -n[d|v]] [\\computername]
```

## <a name="options"></a>Options

| オプション | 説明 |
| ------ | ----------- |
| -y | コンピューターの再起動時に、すべてのディスクパフォーマンスカウンターを開始します。 |
| -yd | コンピューターの再起動時に、物理ドライブのディスクパフォーマンスカウンターを有効にします。 |
| -yv | コンピューターの再起動時に、論理ドライブまたは記憶域ボリュームのディスクパフォーマンスカウンターを有効にします。 |
| -n | コンピューターの再起動時に、すべてのディスクパフォーマンスカウンターを無効にします。 |
| -nd | コンピューターの再起動時に、物理ドライブのディスクパフォーマンスカウンターを無効にします。 |
| -nv | コンピューターの再起動時に、論理ドライブまたは記憶域ボリュームのディスクパフォーマンスカウンターを無効にします。 |
| `\\<computername>` | ディスクパフォーマンスカウンターを有効または無効にするコンピューターの名前を指定します。 |
| -? | 状況依存のヘルプを表示します。 |

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
