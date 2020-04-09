---
title: manage-bde forcerecovery
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: eecae37c-c9a3-46c5-b615-a0ace1f1d778
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fc22e4eddca19344340af0f36b2f8b200c1950ff
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80840115"
---
# <a name="manage-bde-forcerecovery"></a>manage-bde: forcerecovery



再起動時に復旧モードに BitLocker で保護されたドライブを強制します。 このコマンドは、すべてのトラステッドプラットフォームモジュール (TPM) 関連のキー保護機能をドライブから削除します。 コンピューターが再起動したら、回復パスワードまたは回復キーは、ドライブのロック解除に使用できます。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
manage-bde –forcerecovery <Drive> [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

#### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<ドライブ >|コロンの後にドライブ文字を表します。|
|-computername|別のコンピューターに BitLocker による保護を変更する、bde.exe を使用することを指定します。 また、このコマンドの省略版として **-cn**を使用することもできます。|
|\<名 >|BitLocker による保護を変更するコンピューターの名前を表します。 指定できる値には、コンピューターの NetBIOS 名とコンピューターの IP アドレスが含まれます。|
|-? または /?|コマンドプロンプトで簡単なヘルプを表示します。|
|-help または-h|表示は、コマンド プロンプトでヘルプを完了します。|

## <a name="examples"></a><a name=BKMK_Examples></a>例

次の例では、 **-forcerecovery**コマンドを使用して、ドライブ C の回復モードで BitLocker を開始する方法を示します。
```
manage-bde –forcerecovery C:
```

## <a name="additional-references"></a>その他の参照情報

-   - [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)