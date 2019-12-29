---
title: manage-bde ステータス
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1444a360-fabf-4dd3-b67f-188e6ea3fa5b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 235db54ef2361c0e95c66b15a15be7f188fb74d9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71373856"
---
# <a name="manage-bde-status"></a>manage-bde: 状態



コンピューター上のすべてのドライブに関する次の情報を提供します。BitLocker で保護されたをされているかどうか。
-   サイズ
-   BitLocker のバージョン
-   変換の状態
-   暗号化された割合
-   暗号化の方法
-   保護の状態
-   ロックの状態
-   識別フィールド
-   キープロテクター

このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
manage-bde -status [<Drive>] [-protectionaserrorlevel] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<Drive >|コロンの後にドライブ文字を表します。|
|-protectionaserrorlevel|ボリュームは保護されている; がない場合に、ボリュームが保護されている場合に 0 のリターン コードと 1 を送信する、manage-bde コマンド ライン ツールと、します。ドライブが BitLocker で保護されているかを判断バッチ スクリプトでよく使用されます。 使用することも **-p** としてこのコマンドの簡易版です。|
|-computername|別のコンピューターに BitLocker による保護を変更する、bde.exe を使用することを指定します。 また、このコマンドの省略版として **-cn**を使用することもできます。|
|\<名前 >|BitLocker による保護を変更するコンピューターの名前を表します。 指定できる値には、コンピューターの NetBIOS 名とコンピューターの IP アドレスが含まれます。|
|-? または /?|コマンドプロンプトで簡単なヘルプを表示します。|
|-help または-h|表示は、コマンド プロンプトでヘルプを完了します。|

## <a name="BKMK_Examples"></a>例

次の例を使用して、 **-ステータス** C: ドライブの状態を表示するコマンド
```
manage-bde –status C:
```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)