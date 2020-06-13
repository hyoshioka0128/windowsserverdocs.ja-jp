---
title: nslookup set class
description: Nslookup set class コマンドのリファレンストピック。クエリクラスを変更します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ed826400-40da-42b6-b7f0-95db73790723
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e939be13eedcab557dc6dcbe16f2e83f810c20d5
ms.sourcegitcommit: 99d548141428c964facf666c10b6709d80fbb215
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/12/2020
ms.locfileid: "84721565"
---
# <a name="nslookup-set-class"></a>nslookup set class

クエリクラスを変更します。 クラスは、情報のプロトコルグループを指定します。

## <a name="syntax"></a>構文

```
set class=<class>
```

### <a name="parameters"></a>パラメーター

| パラメーター | Description |
| --------- | ----------- |
| `<class>` | 有効な値は次のとおりです。<ul><li>**:** インターネットクラスを指定します。 これが既定値です。</li><li>**混乱:** 混乱クラスを指定します。</li><li>**HESIOD:** MIT アテナ Hesiod クラスを指定します。</li><li>**任意:** 以前に一覧表示された値のいずれかを使用するように指定します。</li></ul> |
| /? | コマンド プロンプトにヘルプを表示します。 |
| /help | コマンド プロンプトにヘルプを表示します。 |

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)
