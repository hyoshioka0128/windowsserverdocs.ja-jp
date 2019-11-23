---
title: manage-bde をオフにします
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0a27c119-d385-45e5-89fe-e311d4429876
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a3da40146441a057db73dd76442189e3357415de
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374020"
---
# <a name="manage-bde-off"></a>manage-bde: off



ドライブの暗号化を解除し、BitLocker をオフにします。 復号化が完了すると、すべてのキー プロテクターが削除されます。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
manage-bde -off [<Volume>] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<ボリューム >|ドライブ文字の後にコロン、ボリューム GUID パス、またはマウントされたボリュームが続きます。|
|-computername|別のコンピューターに BitLocker による保護を変更する、bde.exe を使用することを指定します。 また、このコマンドの省略版として **-cn**を使用することもできます。|
|\<名 >|BitLocker による保護を変更するコンピューターの名前を表します。 指定できる値には、コンピューターの NetBIOS 名とコンピューターの IP アドレスが含まれます。|
|-? または /?|コマンドプロンプトで簡単なヘルプを表示します。|
|-help または-h|表示は、コマンド プロンプトでヘルプを完了します。|

## <a name="BKMK_Examples"></a>例

次の例では、 **-off**コマンドを使用して、C ドライブで BitLocker を無効にしています。
```
manage-bde –off C:
```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)