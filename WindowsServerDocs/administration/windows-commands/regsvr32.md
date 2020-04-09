---
title: regsvr32
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3345e964-7d3e-42b8-abeb-42ed6edfe2b2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d3b775b0c49e4191a9fee6dc9e2e91f968142085
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80836215"
---
# <a name="regsvr32"></a>regsvr32



レジストリ内のコマンド コンポーネントとして .dll ファイルを登録します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
regsvr32 [/u] [/s] [/n] [/i[:cmdline]] <DllName>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/u|サーバーの登録を解除します。|
|/s|実行 **Regsvr32** せず、メッセージを表示します。|
|/n|実行 **Regsvr32** 呼び出さずに **DllRegisterServer**します。 (必要、 **/i** パラメーターです)。|
|/i:\<cmdline >|省略可能なコマンドライン文字列を渡します (*cmdline*) に **DllInstall**します。 組み合わせてこのパラメーターを使用する場合、 **/u** 呼び出しパラメーター、 **DllUninstall**します。|
|\<DllName >|登録される .dll ファイルの名前。|
|/?|コマンド プロンプトでヘルプを表示します。|

## <a name="examples"></a><a name=BKMK_examples></a>例

Active Directory スキーマの .dll ファイルを登録するには、次のように入力します。
```
regsvr32 schmmgmt.dll
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)