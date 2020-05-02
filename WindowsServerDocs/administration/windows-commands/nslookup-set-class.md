---
title: nslookup set class
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ed826400-40da-42b6-b7f0-95db73790723
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b1ae3a5336815a5273aafa976b1dcad8b60fac9b
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723658"
---
# <a name="nslookup-set-class"></a>nslookup set class



クエリクラスを変更します。 クラスは、情報のプロトコルグループを指定します。

## <a name="syntax"></a>構文

```
set class=<Class>
```

### <a name="parameters"></a>パラメーター

| パラメーター |                                                                                                                                    [説明]                                                                                                                                    |
|-----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| \<Class>  | 既定のクラスは、にあります。 このコマンドの有効な値を次に示します。</br>-IN: インターネットクラスを指定します。</br>-混乱: 混乱クラスを指定します。</br>-HESIOD: MIT アテナ Hesiod クラスを指定します。</br>-ANY: 前に示したワイルドカードのいずれかを指定します。 |
|   {ヘルプ   |                                                                                                                                        ?}                                                                                                                                         |

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)