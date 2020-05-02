---
title: manage-bde resume
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ca3cd1ca-6f2c-4190-b68f-27816635facb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1ecd5900dba2cb4ed7f7a3d4e2a2924a3393e94b
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724101"
---
# <a name="manage-bde-resume"></a>manage-bde: resume



一時停止された後は、BitLocker 暗号化または復号化を再開します。

## <a name="syntax"></a>構文

```
manage-bde -resume [<Drive>] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

#### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|\<ドライブ>|コロンの後にドライブ文字を表します。|
|-computername|別のコンピューターに BitLocker による保護を変更する、bde.exe を使用することを指定します。 また、このコマンドの省略版として **-cn**を使用することもできます。|
|\<Name>|BitLocker による保護を変更するコンピューターの名前を表します。 指定できる値には、コンピューターの NetBIOS 名とコンピューターの IP アドレスが含まれます。|
|-? または /?|コマンドプロンプトで簡単なヘルプを表示します。|
|-help または-h|表示は、コマンド プロンプトでヘルプを完了します。|

## <a name="examples"></a>例

**-Resume**コマンドを使用してドライブ C で BitLocker 暗号化を再開する方法を示します。
```
manage-bde –resume C:
```

## <a name="additional-references"></a>その他のリファレンス

-   - [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)