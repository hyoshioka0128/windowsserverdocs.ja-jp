---
title: オフラインディスク
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8fb9b3c3-0b2c-4192-a2e7-f706292653e3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3a00b7f51bc950c3737ba6350fe15a7a4c6cc45e
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723445"
---
# <a name="offline-disk"></a>オフラインディスク



オフラインの状態にフォーカスがあるオンライン ディスクを移動します。

> [!IMPORTANT]
> この DiskPart コマンドは、Windows Vista のどのエディションでも使用できません。

## <a name="syntax"></a>構文

```
offline disk [noerr]
```

### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|noerr|スクリプト専用です。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|

## <a name="remarks"></a>Remarks

-   このコマンドは、SAN のオンライン モードであるディスクに動作します。 オフラインに SAN モードを変更します。
-   ディスクの状態を変更する場合は、ダイナミック ディスクにディスク グループがオフラインのままにするに **見つからない** され、グループがオフラインになっているディスクを表示します。 不足しているディスクは、無効なグループに移動されます。 かどうかは、ダイナミック ディスクとは、グループ内の最後のディスク、ディスクの状態が変わります **オフライン**, 、空のグループが削除されます。
-   ディスクを選択する必要があります、 **オフライン ディスク** コマンドを正しく実行されます。 使用して、 **select ディスク** コマンド ディスクを選択し、それにフォーカスをします。

## <a name="examples"></a>例

フォーカスがあるディスクをオフラインにするため次のように入力します。
```
offline disk
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

