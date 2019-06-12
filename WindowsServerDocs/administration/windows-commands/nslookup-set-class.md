---
title: nslookup set class
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ed826400-40da-42b6-b7f0-95db73790723
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7953f450c17afdee849515f8d8945631a30f4b98
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66436845"
---
# <a name="nslookup-set-class"></a>nslookup set class



クエリ クラスを変更します。 クラスには、情報のプロトコルのグループを指定します。

## <a name="syntax"></a>構文

```
set class=<Class>
```

## <a name="parameters"></a>パラメーター

| パラメーター |                                                                                                                                    説明                                                                                                                                    |
|-----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| \<Class>  | 既定のクラスは、in です。 このコマンドの有効な値を次に示します。</br>インします。インターネット クラスを指定します。</br>-混乱します。Chaos クラスを指定します。</br>-HESIOD:MIT アテナ Hesiod クラスを指定します。</br>-すべて。上記のワイルドカードのいずれかを指定します。 |
|   {0} のヘルプ   |                                                                                                                                        ?}                                                                                                                                         |

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)