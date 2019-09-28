---
title: bitsadmin ピアキャッシュと setconfigurationflags
description: '**Bitsadmin ピアキャッシュと setconfigurationflags**の Windows コマンドのトピック-コンピューターがピアにコンテンツを提供し、ピアからコンテンツをダウンロードできるかどうかを決定する構成フラグを設定します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ff0a2b49-66e3-4d40-824c-6a3816055d2e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a65d54bcaa2bce26eb2b7c98250837ab09c7a423
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381108"
---
# <a name="bitsadmin-peercaching-and-setconfigurationflags"></a>bitsadmin ピアキャッシュと setconfigurationflags



コンピューターがピアにコンテンツを提供し、ピアからコンテンツをダウンロードできるかどうかを決定する構成フラグを設定します。

## <a name="syntax"></a>構文

```
bitsadmin /PeerCaching /SetConfigurationFlags <Job> <Value>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|値|値は、バイナリ表現のビットを次のように解釈する符号なし整数です。</br>-ジョブのデータをピアからダウンロードできるようにします。最下位ビットを設定する</br>-ジョブのデータをピアに提供できるようにします。右側の2番目のビットを設定します。|

## <a name="BKMK_examples"></a>例

次の例では、 *myjob*という名前のジョブについて、ピアからダウンロードされるジョブのデータを指定します。
```
C:\> Bitsadmin /PeerCaching /SetConfigurationFlags myJob 1
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)