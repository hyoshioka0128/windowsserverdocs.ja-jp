---
title: manage-bde 変更キーを管理します。
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 69463db9-7e03-47ff-b233-a95d5055725f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6b5f152e4e98387adb7e7780f8458edd409b1a9d
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724200"
---
# <a name="manage-bde-changekey"></a>manage-bde: 変更キー



オペレーティング システム ドライブのスタートアップ キーを変更します。

## <a name="syntax"></a>構文

```
manage-bde -changekey [<Drive>] [<PathToExternalKeyDirectory>] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

#### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|\<ドライブ>|コロンの後にドライブ文字を表します。|
|\<PathToExternalKeyDirectory>|ドライブのロックを解除するために使用する外部のスタートアップ キー ファイルを保存するディレクトリの場所を表します。|
|-computername|別のコンピューターに BitLocker による保護を変更する、bde.exe を使用することを指定します。 また、このコマンドの省略版として **-cn**を使用することもできます。|
|\<Name>|BitLocker による保護を変更するコンピューターの名前を表します。 指定できる値には、コンピューターの NetBIOS 名とコンピューターの IP アドレスが含まれます。|
|-? または /?|コマンドプロンプトで簡単なヘルプを表示します。|
|-help または-h|表示は、コマンド プロンプトでヘルプを完了します。|

## <a name="examples"></a>例

**-Changekey**コマンドを使用して、ドライブ C で BitLocker 暗号化と共に使用する新しいスタートアップキーをドライブ E に作成する方法を示します。
```
manage-bde -changekey C: E:\
```

## <a name="additional-references"></a>その他のリファレンス

-   - [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)
