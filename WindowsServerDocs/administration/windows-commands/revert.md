---
title: 反転
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 75ad40e4-502a-401e-b11e-8b31e00424b5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d7dae609e4615868b03e4b5ea9a681f553aa0667
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80835755"
---
# <a name="revert"></a>反転



指定したシャドウ コピーにボリュームを元に戻します。 これは CLIENTACCESSIBLE コンテキストでのシャドウ コピーに対してのみサポートされます。 これらのシャドウ コピーは、永続的なシステム プロバイダーによってのみ実行できます。 パラメーターを指定せずに使用する場合 **を元に戻す** コマンド プロンプトでヘルプを表示します。

## <a name="syntax"></a>構文

```
revert <ShadowCopyID>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<ShadowCopyID >|ボリュームを元に戻すシャドウ コピー ID を指定します。|

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)