---
title: mask
description: Mask コマンドのリファレンストピック。インポートコマンドを使用してインポートされたハードウェアシャドウコピーを削除します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bf301474-d74a-44e7-9fad-c8a11e7ca3bd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ee01bb74b1fef1bb31a266c01a9e9bde7743691d
ms.sourcegitcommit: 5e313a004663adb54c90962cfdad9ae889246151
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2020
ms.locfileid: "84354642"
---
# <a name="mask"></a>mask

**インポート**コマンドを使用してインポートされたハードウェアシャドウコピーを削除します。

## <a name="syntax"></a>構文

```
mask <shadowsetID>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| shadowsetID | 指定されたシャドウコピーセット ID に属するシャドウコピーを削除します。 |

#### <a name="remarks"></a>解説

- *ShadowSetID*の代わりに、既存のエイリアスまたは環境変数を使用できます。 既存のエイリアスを表示するには、パラメーターを指定せずに**add**を使用します。

### <a name="examples"></a>例

インポートされたシャドウコピー *% Import_1%* を削除するには、次のように入力します。

```
mask %Import_1%
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)