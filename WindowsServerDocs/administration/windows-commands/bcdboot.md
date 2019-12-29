---
title: bcdboot
description: '**Bcdboot**の Windows コマンドに関するトピック-システムパーティションを迅速にセットアップするか、システムパーティションにあるブート環境を修復します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e62a250e-08e9-47f6-89d1-e6002560ab57
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a1c0f505180a503617335cc9575fea3d346bbe02
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383440"
---
# <a name="bcdboot"></a>bcdboot



を使用すると、システムパーティションをすばやく設定したり、システムパーティションにあるブート環境を修復したりできます。 システムパーティションは、単純な一連のブート構成データ (BCD) ファイルを既存の空のパーティションにコピーすることによって設定されます。

Bcdboot の検索場所、およびこのコマンドの使用方法の例については、「bcdboot の[コマンドラインオプション](https://technet.microsoft.com/library/hh824874.aspx)」を参照してください。

## <a name="syntax"></a>構文

```
bcdboot <source> [/l] [/s]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|source|ブート環境ファイルをコピーするためのソースとして使用する Windows ディレクトリの場所を指定します。|
|/l|ロケールを指定します。 既定のロケールは英語 (米国) です。|
|/s|システムパーティションのボリューム文字を指定します。 既定値は、ファームウェアによって識別されるシステムパーティションです。|

## <a name="BKMK_examples"></a>例

このコマンドの使用方法のその他の例については、「 [BCDboot のコマンドラインオプション](https://technet.microsoft.com/library/hh824874.aspx)」を参照してください。

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)