---
title: import
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7bd78d76-0560-4d47-944c-fe960be2c10b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 72cbd6195de64a6a0a7f2c258e19b2d5eb1378b1
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724855"
---
# <a name="import"></a>import



読み込まれたメタデータファイルからシステムに転送可能なシャドウコピーをインポートします。



## <a name="syntax"></a>構文

```
import
```

## <a name="remarks"></a>Remarks

-   転送可能なシャドウコピーは、システムにすぐには保存されません。 これらの詳細は、バックアップコンポーネントドキュメント XML ファイルに格納されます。この XML ファイルは、自動的に要求され、.cab メタデータファイルを作業ディレクトリに保存します。 このファイルのパスと名前は、[**メタデータの設定**] コマンドを使用して変更できます。
-   **Import**を使用するには、[**メタデータの読み込み**] コマンドを使用して、DiskShadow メタデータファイルを読み込む必要があります。

## <a name="examples"></a>例

**Import**コマンドの使用方法を示す DiskShadow スクリプトの例を次に示します。
```
#Sample DiskShadow script demonstrating IMPORT
SET CONTEXT PERSISTENT
SET CONTEXT TRANSPORTABLE
SET METADATA transHWshadow_p.cab
#P: is the volume supported by the Hardware Shadow Copy provider
ADD VOLUME P:
CREATE
END BACKUP
#The (transportable) shadow copy is not in the system yet.
#You can reset or exit now if you wish.

LOAD METADATA transHWshadow_p.cab
IMPORT
#The shadow copy will now be loaded into the system.
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)