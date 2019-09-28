---
title: セットのメタデータ
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 67e6f60a-b42a-451a-95cf-b22ace7d50c2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ac73a4131d3f4065cd1aeae873734b079ad664e2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71370954"
---
# <a name="set-metadata"></a>セットのメタデータ



シャドウ コピーを別の 1 台のコンピューターに転送するために使用したシャドウの作成のメタデータ ファイルの場所と名前を設定します。 パラメーターを指定せずに使用する場合 **メタデータ設定** コマンド プロンプトでヘルプを表示します。

## <a name="syntax"></a>構文

```
set metadata [<Drive>:][<Path>]<MetaData.cab>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|[\<Drive >:][<Path>]|メタデータ ファイルを作成する場所を指定します。|
|@no__t のメタデータ .cab >|シャドウの作成のメタデータを格納する cab ファイルの名前を指定します。|

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)