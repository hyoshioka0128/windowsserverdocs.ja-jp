---
title: recover
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8cc3a73d-9456-41a0-b375-2b4cc37c3992
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3a77e83f1a7143a82fd626390c7373dc87afdb17
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722610"
---
# <a name="recover"></a>recover



ディスクグループ内のすべてのディスクの状態を更新し、無効なディスクグループのディスクを回復します。また、古いデータを保持しているミラーボリュームと RAID-5 ボリュームを再同期します。

> [!IMPORTANT]
> この DiskPart コマンドは、Windows Vista のどのエディションでも使用できません。

## <a name="syntax"></a>構文

```
recover [noerr]
```

### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|noerr|スクリプト専用です。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|

## <a name="remarks"></a>Remarks

-   このコマンドは、ディスク グループ上で動作します。
-   このコマンドは、ダイナミック ディスクのグループにのみ適用されます。 ベーシック ディスクを使用してグループでは、このコマンドを使用する場合は、エラーは返されませんが、アクションは実行されません。
-   このコマンドは、失敗したディスクまたは失敗した場合に動作します。 また、または冗長の失敗の状態が失敗すると、失敗しているボリューム上でも機能します。
-   このコマンドは成功するには、ディスク グループの一部であるディスクを選択してください。 使用して、 **select ディスク** コマンド ディスクを選択し、それにフォーカスをします。

## <a name="examples"></a>例

フォーカスのあるディスクが含まれるディスク グループを回復するには、次のように入力します。
```
recover
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

