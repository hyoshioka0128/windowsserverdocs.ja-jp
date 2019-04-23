---
title: import
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7bd78d76-0560-4d47-944c-fe960be2c10b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ddef3958bc431519e3cb89b658a58d1f4dba6938
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835263"
---
# <a name="import"></a>import



システムに読み込まれたメタデータ ファイルからの移植可能なシャドウ コピーをインポートします。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
import
```

## <a name="remarks"></a>注釈

-   移動可能なシャドウ コピーはすぐに、システムでは保存されません。 その詳細は、DiskShadow は自動的に要求し、作業ディレクトリで .cab メタデータ ファイルに保存のバックアップ コンポーネント ドキュメントの XML ファイルに格納されます。 使用してこのファイルの名前とパスを変更することができます、**メタデータ設定**コマンド。
-   使用する前に**インポート**、DiskShadow メタデータ ファイルを使用して、読み込む必要があります、**メタデータの読み込み**コマンド。

## <a name="BKMK_examples"></a>例

使用方法を示すサンプル DiskShadow スクリプトを次に、**インポート**コマンド。
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

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)