---
title: manage-bde 状態
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: d81808b57b1833ca30b95dc9d4b6aa0b0a4bdbaa
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59836563"
---
# <a name="manage-bde-status"></a>manage-bde: ステータス



コンピューター上のすべてのドライブに関する次の情報を提供します。BitLocker で保護されたをされているかどうか。
-   サイズ
-   BitLocker のバージョン
-   変換の状態
-   暗号化された割合
-   暗号化の方法
-   保護の状態
-   ロックの状態
-   識別フィールド
-   キーの保護機能

このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
manage-bde -status [<Drive>] [-protectionaserrorlevel] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<ドライブ >|コロンの後にドライブ文字を表します。|
|-protectionaserrorlevel|ボリュームは保護されている; がない場合に、ボリュームが保護されている場合に 0 のリターン コードと 1 を送信する、manage-bde コマンド ライン ツールと、します。ドライブが BitLocker で保護されているかを判断バッチ スクリプトでよく使用されます。 使用することも **-p** としてこのコマンドの簡易版です。|
|-computername|別のコンピューターに BitLocker による保護を変更する、bde.exe を使用することを指定します。 使用することも **- cn**としてこのコマンドの簡易版です。|
|\<名 >|BitLocker による保護を変更するコンピューターの名前を表します。 指定できる値には、コンピューターの NetBIOS 名とコンピューターの IP アドレスが含まれます。|
|-? または /?|ヘルプの簡単なコマンド プロンプトが表示されます。|
|--help または-h|表示は、コマンド プロンプトでヘルプを完了します。|

## <a name="BKMK_Examples"></a>例

次の例を使用して、 **-ステータス** C: ドライブの状態を表示するコマンド
```
manage-bde –status C:
```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンドライン構文キー](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)