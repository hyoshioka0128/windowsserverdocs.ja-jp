---
title: nslookup set class
description: Nslookup set class コマンドの参照記事。クエリクラスを変更します。
ms.topic: article
ms.assetid: ed826400-40da-42b6-b7f0-95db73790723
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dbbcfa3dbdce653dc1318b69a33ba0bacbc2e359
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87885710"
---
# <a name="nslookup-set-class"></a>nslookup set class

クエリクラスを変更します。 クラスは、情報のプロトコルグループを指定します。

## <a name="syntax"></a>構文

```
set class=<class>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<class>` | 有効な値は次のとおりです。<ul><li>**:** インターネットクラスを指定します。 これが既定値です。</li><li>**混乱:** 混乱クラスを指定します。</li><li>**HESIOD:** MIT アテナ Hesiod クラスを指定します。</li><li>**任意:** 以前に一覧表示された値のいずれかを使用するように指定します。</li></ul> |
| /? | コマンド プロンプトにヘルプを表示します。 |
| /help | コマンド プロンプトにヘルプを表示します。 |

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
