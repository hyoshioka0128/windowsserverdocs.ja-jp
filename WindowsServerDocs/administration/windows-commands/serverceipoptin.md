---
title: serverceipoptin
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3d7d7fa7-0689-4797-b802-36fe260d21a0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f400a8f66f15e5a138cf355ad54d276cfa7f3ce3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371006"
---
# <a name="serverceipoptin"></a>serverceipoptin

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

カスタマー エクスペリエンス向上プログラム (CEIP) に参加できます。
## <a name="syntax"></a>構文
```
serverceipoptin [/query] [/enable] [/disable]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/query|現在の設定を検証します。|
|/enable|参加を有効にします。|
|/disable|参加を無効にします。|
|/?|コマンド プロンプトにヘルプを表示します。|
## <a name="BKMK_Examples"></a>例
現在の設定を確認するには、次のように入力します。
```
serverceipoptin /query
```
参加を有効にするには、次のように入力します。
```
serverceipoptin /enable
```
参加を無効にするには、次のように入力します。
```
serverceipoptin /disable
```
## <a name="additional-references"></a>その他の参照情報
-   [コマンド ライン構文の記号](command-line-syntax-key.md)

