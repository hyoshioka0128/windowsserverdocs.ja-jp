---
title: オンラインディスク
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bc44a783-eaa4-40ca-be01-5703b5bf4eb3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3d798bf34ec2f9d2f01b5470c4ec52f936674135
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372512"
---
# <a name="online-disk"></a>オンラインディスク



現在のオンライン状態にオフラインになっているディスクが表示されます。

> [!IMPORTANT]
> このコマンドは、Windows Vista のどのエディションでも使用できません。

> [!IMPORTANT]
> 読み取り専用ディスクで使用されている場合、このコマンドは失敗します。

このコマンドの使用方法については、「[不足またはオフラインのダイナミックディスクを再アクティブ化](https://go.microsoft.com/fwlink/?LinkId=207046)する」 (https://go.microsoft.com/fwlink/?LinkId=207046) を参照してください。

## <a name="syntax"></a>構文

```
online disk [noerr]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|noerr|スクリプトの場合のみ。 エラーが発生した場合、DiskPart はエラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|

## <a name="remarks"></a>コメント

-   Windows Vista でパラメーターを指定せずに使用した場合、このコマンドはディスクグループ上で動作します。 ベーシック ディスクのグループごとの 1 つ以上のディスクです。 ダイナミックディスクの場合、このグループには、非外部ダイナミックディスクがすべて含まれます。
-   ベーシック ディスクには、このコマンドをオンラインにする、選択したディスクとすべてのボリュームをそのディスクを試みます。
-   ダイナミック ディスクの場合はこのコマンドは、ローカル コンピューター上の外部とマークされていないすべてのディスクをオンラインに試みます。 または、一連のダイナミック ディスク上のすべてのボリュームをオンラインに試みます。
-   ディスク グループのダイナミック ディスクがオンラインになり、グループ内の唯一のディスクは場合、は、元のグループが再作成し、ディスクはそのグループに移動します。 グループの他のディスクがオンラインである場合は、し、ディスクは単に戻るグループに追加します。
-   選択したディスクのグループにミラーボリュームまたは RAID-5 ボリュームが含まれている場合は、このコマンドによってこれらのボリュームも再同期されます。
-   このコマンドを成功させるには、ディスクを選択してください。 使用して、 **select ディスク** コマンド ディスクを選択し、それにフォーカスをします。

## <a name="BKMK_examples"></a>例

ディスクをオンラインに戻すと、次のように入力します。
```
online disk
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)

