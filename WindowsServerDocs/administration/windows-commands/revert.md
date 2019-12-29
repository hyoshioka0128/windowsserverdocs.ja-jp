---
title: 反転
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 75ad40e4-502a-401e-b11e-8b31e00424b5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3243f13a4997824d9fff7c874ce26d56325fefa4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371451"
---
# <a name="revert"></a>反転



指定したシャドウ コピーにボリュームを元に戻します。 これは CLIENTACCESSIBLE コンテキストでのシャドウ コピーに対してのみサポートされます。 これらのシャドウ コピーは、永続的なシステム プロバイダーによってのみ実行できます。 パラメーターを指定せずに使用する場合 **を元に戻す** コマンド プロンプトでヘルプを表示します。

## <a name="syntax"></a>構文

```
revert <ShadowCopyID>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<ShadowCopyID >|ボリュームを元に戻すシャドウ コピー ID を指定します。|

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)