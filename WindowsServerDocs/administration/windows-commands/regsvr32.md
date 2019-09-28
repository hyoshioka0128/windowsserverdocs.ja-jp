---
title: regsvr32
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3345e964-7d3e-42b8-abeb-42ed6edfe2b2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 444af0ccf7c9bbe21c013f32b396997b7cb2e00f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371628"
---
# <a name="regsvr32"></a>regsvr32



レジストリ内のコマンド コンポーネントとして .dll ファイルを登録します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
regsvr32 [/u] [/s] [/n] [/i[:cmdline]] <DllName>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/u|サーバーの登録を解除します。|
|/s|実行 **Regsvr32** せず、メッセージを表示します。|
|/n|実行 **Regsvr32** 呼び出さずに **DllRegisterServer**します。 (必要、 **/i** パラメーターです)。|
|/i: \<cmdline >|省略可能なコマンドライン文字列を渡します (*cmdline*) に **DllInstall**します。 組み合わせてこのパラメーターを使用する場合、 **/u** 呼び出しパラメーター、 **DllUninstall**します。|
|\<DllName >|登録される .dll ファイルの名前。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="BKMK_examples"></a>例

Active Directory スキーマの .dll ファイルを登録するには、次のように入力します。
```
regsvr32 schmmgmt.dll
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)