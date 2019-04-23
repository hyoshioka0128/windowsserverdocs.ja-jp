---
title: 元に戻す
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 5bc77b17317f602d642c7a9e025b67be10ad7256
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59875113"
---
# <a name="revert"></a>元に戻す



指定したシャドウ コピーにボリュームを元に戻します。 これは CLIENTACCESSIBLE コンテキストでのシャドウ コピーに対してのみサポートされます。 これらのシャドウ コピーは、永続的なシステム プロバイダーによってのみ実行できます。 パラメーターを指定せずに使用する場合 **を元に戻す** コマンド プロンプトでヘルプを表示します。

## <a name="syntax"></a>構文

```
revert <ShadowCopyID>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<ShadowCopyID>|ボリュームを元に戻すシャドウ コピー ID を指定します。|

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)