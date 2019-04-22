---
title: bcdboot
description: Windows コマンド」のトピック**bcdboot** - すぐに、システム パーティションを設定またはシステム パーティション上にあるブート環境を修復します。
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 78838dd6567ad886948df8ac21425a8f9b596d5f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825883"
---
# <a name="bcdboot"></a>bcdboot



で、システム パーティションをすばやくセットアップするか、システム パーティション上にあるブート環境を修復できます。 システム パーティションがブート構成データ (BCD) ファイルの単純なセットを既存の空のパーティションにコピーすることによってセットアップされます。

BCDboot、BCDboot、このコマンドを使用する方法の例の検索場所に関する情報などの詳細については、次を参照してください。、 [BCDboot のコマンドライン オプション](https://technet.microsoft.com/library/hh824874.aspx)トピック。

## <a name="syntax"></a>構文

```
bcdboot <source> [/l] [/s]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|source|ブート環境ファイルをコピーするために、ソースとして使用する Windows ディレクトリの場所を指定します。|
|/l|ロケールを指定します。 既定のロケールが英語 (米国) です。|
|/s|システム パーティションのボリューム文字を指定します。 既定では、ファームウェアによって識別されるシステム パーティションです。|

## <a name="BKMK_examples"></a>例

このコマンドを使用する方法の例については、次を参照してください。、 [BCDboot のコマンドライン オプション](https://technet.microsoft.com/library/hh824874.aspx)トピック。

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)