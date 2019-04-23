---
title: 影を削除します。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e29a84d2-04d1-4eb1-910a-5a47bddbc24d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4b0d5414cb5b60face5245d7ea22d66c8629bfcb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873733"
---
# <a name="delete-shadows"></a>影を削除します。



シャドウ コピーを削除します。

## <a name="syntax"></a>構文

```
delete shadows [all | volume <Volume> | oldest <Volume> | set <SetID> | id <ShadowID> | exposed {<Drive> | <MountPoint>}]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|all|すべてのシャドウ コピーを削除します。|
|ボリューム\<ボリューム >|特定のボリュームのシャドウ コピーをすべて削除します。|
|最も古い\<ボリューム >|特定のボリュームの最も古いシャドウ コピーを削除します。|
|設定\<SetID >|指定された ID のシャドウ コピー セットにシャドウ コピーを削除します 使用して別名を指定することができます、 **%** シンボルのエイリアスは、現在の環境に存在する場合。|
|id \<ShadowID>|指定された ID のシャドウ コピーを削除します。 使用して別名を指定することができます、 **%** シンボルのエイリアスは、現在の環境に存在する場合。|
|公開されている {\<ドライブ > | <MountPoint>}|指定したドライブ文字またはマウント ポイントで公開されているシャドウ コピーを削除します。 C:\mountPoint p: など、ドライブ文字またはマウント ポイントを指定します。|

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)