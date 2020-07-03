---
title: rundll32
description: 参照記事 * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 46d9cd64-8186-4cd4-a500-44700340fe81
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c9a0dca06bb3077ec308ae3a9792deb1f72e023b
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85932799"
---
# <a name="rundll32"></a>rundll32



読み込みを 32 ビットのダイナミック リンク ライブラリ (Dll) を実行します。 Rundll32 を構成できる設定はありません。 使用して実行する特定の DLL のヘルプ情報を提供、 **rundll32** コマンドです。

実行する必要があります、 **rundll32** 管理者特権でコマンド プロンプトからコマンドです。 コマンド プロンプトを開くにはクリックして **開始**, を右クリックして **コマンド プロンプト**, 、] をクリックし、 **管理者として実行**します。

## <a name="syntax"></a>Syntax

```
Rundll32 <DLLname>
```

## <a name="commands"></a>コマンド

|パラメーター|説明|
|---------|-----------|
|[Rundll32 printui.dll,PrintUIEntry](rundll32-printui.md)|プリンターのユーザー インターフェイスが表示されます。|

## <a name="remarks"></a>注釈

Rundll32 は、明示的に記述された DLL からの関数のみを、Rundll32 によって呼び出されるように呼び出すことができます。

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
