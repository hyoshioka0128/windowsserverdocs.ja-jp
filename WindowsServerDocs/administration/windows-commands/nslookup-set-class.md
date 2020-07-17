---
title: nslookup set class
description: Nslookup set class コマンドの参照記事。クエリクラスを変更します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ed826400-40da-42b6-b7f0-95db73790723
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 073f27f6f10721b11e6d0889d1cb8c16f15db283
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85934424"
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
