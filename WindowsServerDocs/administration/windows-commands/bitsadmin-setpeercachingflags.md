---
title: bitsadmin setpeercachingflags
description: '**Bitsadmin setpeercachingflags**の Windows コマンドトピック-ジョブのファイルをキャッシュしてピアに配信できるかどうか、およびジョブがピアからコンテンツをダウンロードできるかどうかを決定するフラグを設定します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3f54a127-fb68-49a5-b843-664ec833df67
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 147f28268f1b4dd6dfb40cff85f073feabbc35a0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380464"
---
# <a name="bitsadmin-setpeercachingflags"></a>bitsadmin setpeercachingflags



ジョブのファイルをキャッシュしてピアに提供できるかどうか、およびジョブがピアからコンテンツをダウンロードできるかどうかを決定するフラグを設定します。

## <a name="syntax"></a>構文

```
bitsadmin /SetPeerCachingFlags <Job> <value> 
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|値|値は符号なし整数で、バイナリ表現のビットに対して次のように解釈されます。</br>1-ジョブは、ピアからコンテンツをダウンロードできます。</br>2-ジョブのファイルをキャッシュしてピアに配信できます。|

## <a name="BKMK_examples"></a>例

次の例では、 *myjob*という名前のジョブのフラグを設定して、ピアからコンテンツをダウンロードできるようにします。
```
C:\>bitsadmin / SetPeerCachingFlags myJob 1 
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)