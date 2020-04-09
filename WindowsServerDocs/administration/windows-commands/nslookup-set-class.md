---
title: nslookup set class
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ed826400-40da-42b6-b7f0-95db73790723
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bc3bb4e36582f01584c0b89a12d43874322c3190
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80838585"
---
# <a name="nslookup-set-class"></a>nslookup set class



クエリクラスを変更します。 クラスは、情報のプロトコルグループを指定します。

## <a name="syntax"></a>構文

```
set class=<Class>
```

### <a name="parameters"></a>パラメーター

| パラメーター |                                                                                                                                    説明                                                                                                                                    |
|-----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| \<クラス >  | 既定のクラスは、にあります。 このコマンドの有効な値を次に示します。</br>-IN: インターネットクラスを指定します。</br>-混乱: 混乱クラスを指定します。</br>-HESIOD: MIT アテナ Hesiod クラスを指定します。</br>-ANY: 前に示したワイルドカードのいずれかを指定します。 |
|   {ヘルプ   |                                                                                                                                        ?}                                                                                                                                         |

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)