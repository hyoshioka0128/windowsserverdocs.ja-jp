---
title: revert
description: 参照記事 * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 75ad40e4-502a-401e-b11e-8b31e00424b5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8d2d8bfbfa10df9776e849b1450c2fce47c097b7
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85933038"
---
# <a name="revert"></a>revert



指定したシャドウ コピーにボリュームを元に戻します。 これは CLIENTACCESSIBLE コンテキストでのシャドウ コピーに対してのみサポートされます。 これらのシャドウ コピーは、永続的なシステム プロバイダーによってのみ実行できます。 パラメーターを指定せずに使用する場合 **を元に戻す** コマンド プロンプトでヘルプを表示します。

## <a name="syntax"></a>構文

```
revert <ShadowCopyID>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<ShadowCopyID>|ボリュームを元に戻すシャドウ コピー ID を指定します。|

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)