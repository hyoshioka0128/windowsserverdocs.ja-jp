---
title: 影の一覧表示
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: fe568423-00ae-4ede-a1e7-07977cb50ad1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e22b0006709e1cf6636ad6c2bcc18432f59b4d1a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841165"
---
# <a name="list-shadows"></a>影の一覧表示



システム上の永続的なシャドウコピーと永続的でないシャドウコピーを一覧表示します。

## <a name="syntax"></a>構文

```
list shadows {all | set <SetID> | id <ShadowID>}
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|all|すべてのシャドウコピーを一覧表示します。|
|\<SetID > を設定します|指定されたシャドウコピーセット ID に属するシャドウコピーを一覧表示します。|
|id \<ShadowID >|指定されたシャドウコピー ID を持つシャドウコピーを一覧表示します。|

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)