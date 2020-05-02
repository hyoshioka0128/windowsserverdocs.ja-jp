---
title: manage-bde ステータス
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1444a360-fabf-4dd3-b67f-188e6ea3fa5b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d1bf42da356d8326f459066fc168bbd38b7765b0
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724088"
---
# <a name="manage-bde-status"></a>manage-bde: 状態



コンピューター上のすべてのドライブに関する次の情報を提供します。BitLocker で保護されたをされているかどうか。
-   サイズ
-   BitLocker のバージョン
-   変換の状態
-   暗号化された割合
-   暗号化方法
-   保護の状態
-   ロックの状態
-   識別フィールド
-   キープロテクター



## <a name="syntax"></a>構文

```
manage-bde -status [<Drive>] [-protectionaserrorlevel] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

#### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|\<ドライブ>|コロンの後にドライブ文字を表します。|
|-protectionaserrorlevel|ボリュームは保護されている; がない場合に、ボリュームが保護されている場合に 0 のリターン コードと 1 を送信する、manage-bde コマンド ライン ツールと、します。ドライブが BitLocker で保護されているかを判断バッチ スクリプトでよく使用されます。 使用することも **-p** としてこのコマンドの簡易版です。|
|-computername|別のコンピューターに BitLocker による保護を変更する、bde.exe を使用することを指定します。 また、このコマンドの省略版として **-cn**を使用することもできます。|
|\<Name>|BitLocker による保護を変更するコンピューターの名前を表します。 指定できる値には、コンピューターの NetBIOS 名とコンピューターの IP アドレスが含まれます。|
|-? または /?|コマンドプロンプトで簡単なヘルプを表示します。|
|-help または-h|表示は、コマンド プロンプトでヘルプを完了します。|

## <a name="examples"></a>例

**-Status**コマンドを使用して C ドライブの状態を表示する方法を示します。
```
manage-bde –status C:
```

## <a name="additional-references"></a>その他のリファレンス

-   - [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)