---
title: 復元 (recover)
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8cc3a73d-9456-41a0-b375-2b4cc37c3992
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a83bb7502145cc09116241ea255e31b5f9981791
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384742"
---
# <a name="recover"></a>復元 (recover)



ディスクグループ内のすべてのディスクの状態を更新し、無効なディスクグループのディスクを回復します。また、古いデータを保持しているミラーボリュームと RAID-5 ボリュームを再同期します。

> [!IMPORTANT]
> この DiskPart コマンドは、Windows Vista のどのエディションでも使用できません。

## <a name="syntax"></a>構文

```
recover [noerr]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|noerr|スクリプトの場合のみ。 エラーが発生した場合、DiskPart はエラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|

## <a name="remarks"></a>コメント

-   このコマンドは、ディスク グループ上で動作します。
-   このコマンドは、ダイナミック ディスクのグループにのみ適用されます。 ベーシック ディスクを使用してグループでは、このコマンドを使用する場合は、エラーは返されませんが、アクションは実行されません。
-   このコマンドは、失敗したディスクまたは失敗した場合に動作します。 また、または冗長の失敗の状態が失敗すると、失敗しているボリューム上でも機能します。
-   このコマンドは成功するには、ディスク グループの一部であるディスクを選択してください。 使用して、 **select ディスク** コマンド ディスクを選択し、それにフォーカスをします。

## <a name="BKMK_examples"></a>例

フォーカスのあるディスクが含まれるディスク グループを回復するには、次のように入力します。
```
recover
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)

