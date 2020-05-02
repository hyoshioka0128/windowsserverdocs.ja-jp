---
title: manage-bde をオフにします
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0a27c119-d385-45e5-89fe-e311d4429876
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 588ce453cfca72a029d907be894b142567a43ab5
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724140"
---
# <a name="manage-bde-off"></a>manage-bde: off



ドライブの暗号化を解除し、BitLocker をオフにします。 復号化が完了すると、すべてのキー プロテクターが削除されます。

## <a name="syntax"></a>構文

```
manage-bde -off [<Volume>] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

#### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|\<ボリューム>|ドライブ文字の後にコロン、ボリューム GUID パス、またはマウントされたボリュームが続きます。|
|-computername|別のコンピューターに BitLocker による保護を変更する、bde.exe を使用することを指定します。 また、このコマンドの省略版として **-cn**を使用することもできます。|
|\<Name>|BitLocker による保護を変更するコンピューターの名前を表します。 指定できる値には、コンピューターの NetBIOS 名とコンピューターの IP アドレスが含まれます。|
|-? または /?|コマンドプロンプトで簡単なヘルプを表示します。|
|-help または-h|表示は、コマンド プロンプトでヘルプを完了します。|

## <a name="examples"></a>例

**-Off**コマンドを使用してドライブ C で BitLocker をオフにする方法を示します。
```
manage-bde –off C:
```

## <a name="additional-references"></a>その他のリファレンス

-   - [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)