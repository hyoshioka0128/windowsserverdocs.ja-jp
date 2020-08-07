---
title: diskshadow のインポート
description: Import コマンドの参照記事。読み込まれたメタデータファイルからシステムに転送可能なシャドウコピーをインポートします。
ms.topic: article
ms.assetid: 7bd78d76-0560-4d47-944c-fe960be2c10b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4d0d76c9565904d6e24c41f4c728bf43061f5040
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87888363"
---
# <a name="import-diskshadow"></a>インポート (diskshadow)

読み込まれたメタデータファイルからシステムに転送可能なシャドウコピーをインポートします。

> :このコマンドを使用する前に、[[メタデータの読み込み] コマンド](load-metadata.md)を使用して、DiskShadow メタデータファイルを読み込む必要があります。

## <a name="syntax"></a>構文

```
import
```

#### <a name="remarks"></a>Remarks

- 転送可能シャドウコピーは、システムにすぐには保存されません。 これらの詳細は、バックアップコンポーネントドキュメント XML ファイルに格納されます。この XML ファイルは、自動的に要求され、.cab メタデータファイルを作業ディレクトリに保存します。 この XML ファイルのパスと名前を変更するには、[[メタデータの設定] コマンド](set-metadata.md)を使用します。

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

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [diskshadow コマンド](diskshadow.md)