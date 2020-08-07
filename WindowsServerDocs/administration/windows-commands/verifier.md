---
title: verifier
description: Driver verifier マネージャーを実行する検証ツールのリファレンス記事です。
ms.topic: article
ms.assetid: 782173d6-f196-4bc4-a547-76109829453c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1f19840d6a9dffe32a1febb8a313500b49f625e8
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87891868"
---
# <a name="verifier"></a>verifier

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ドライバー検証マネージャー。

## <a name="syntax"></a>構文
```
verifier /standard /driver <name> [<name> ...]
verifier /standard /all
verifier [/flags <flags>] [/faults [<probability> [<tags> [<applications> [<minutes>]]]] /driver <name> [<name>...]
verifier [/flags FLAGS] [/faults [<probability> [<tags> [<applications> [<minutes>]]]] /all
verifier /querysettings
verifier /volatile /flags <flags>
verifier /volatile /adddriver <name> [<name>...]
verifier /volatile /removedriver <name> [<name>...]
verifier /volatile /faults [<probability> [<tags> [<applications>]]
verifier /reset
verifier /query
verifier /log <LogFileName> [/interval <seconds>]
```
#### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|\<flags>|Bits の 10 進数または 16 進数、組み合わせて数値でなければなりません。<p>-   **値: 説明**<br />-   **ビット 0:** 特別なプールチェック<br />-   **ビット 1:** irql チェックを強制する<br />-   **ビット 2:** 低リソースのシミュレーション<br />-   **ビット 3:** プールの追跡<br />-   **ビット 4:** I/o の検証<br />-   **ビット 5:** デッドロックの検出<br />-   **ビット 6:** 未使用<br />-   **ビット 7:** DMA の検証<br />-   **ビット 8:** セキュリティチェック<br />-   **ビット 9:** 強制的に保留中の i/o 要求を実行する<br />-   **ビット 10:** IRP ログ<br />-   **ビット 11:** その他のチェック<p>たとえば、 **/flags 27**は **/flags 0x1B**と同等です。|
|/volatile|システムを再起動しなくても、検証の設定を動的に変更するために使用します。 システムを再起動するときに、新しい設定は失われます。|
|\<probability>|1 ~ 10,000 フォールト インジェクション確率を指定する値。 たとえば、100 を指定するには、1% (100/10,000) のフォールト インジェクション確率を意味します。<p>このパラメーターが指定されていない場合、既定の確率である6% が使用されます。|
|\<tags>|空白文字で区切られた、フォールトが挿入され、プール タグを指定します。 このパラメーターが指定されていない場合、エラー、プールの割り当てを挿入できます。|
|\<applications>|空白文字で区切られたエラーが挿入され、アプリケーションのイメージ ファイル名を指定します。 このパラメーターが指定されていない場合低リソース シミュレーションは任意のアプリケーション内の場所にかかることができます。|
|\<minutes>|正の数値を分単位での再起動後に期間の長さを指定する正の挿入が発生します。 このパラメーターが指定されていない場合は、8 分の既定の長さが使用されます。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="additional-references"></a>その他の参照情報
- [コマンド ライン構文の記号](command-line-syntax-key.md)