---
title: rundll32
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 46d9cd64-8186-4cd4-a500-44700340fe81
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 29a87f9f07c25a0c671e47550e0a054d8308f747
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384420"
---
# <a name="rundll32"></a>rundll32



読み込みを 32 ビットのダイナミック リンク ライブラリ (Dll) を実行します。 Rundll32 を構成できる設定はありません。 使用して実行する特定の DLL のヘルプ情報を提供、 **rundll32** コマンドです。

実行する必要があります、 **rundll32** 管理者特権でコマンド プロンプトからコマンドです。 コマンド プロンプトを開くにはクリックして **開始**, を右クリックして **コマンド プロンプト**, 、 をクリックし、 **管理者として実行**します。

## <a name="syntax"></a>構文

```
Rundll32 <DLLname>
```

## <a name="commands"></a>コマンド

|パラメーター|説明|
|---------|-----------|
|[Rundll32 printui.dll、PrintUIEntry](rundll32-printui.md)|プリンターのユーザー インターフェイスが表示されます。|

## <a name="remarks"></a>コメント

Rundll32 は、Rundll32 によって呼び出される明示的に記述されている DLL から関数を呼び出すのみできます。 Rundll32 の要件の詳細については、Microsoft サポート技術情報の[記事 164787](https://go.microsoft.com/fwlink/?LinkID=165773) (https://go.microsoft.com/fwlink/?LinkID=165773) を参照してください。

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)