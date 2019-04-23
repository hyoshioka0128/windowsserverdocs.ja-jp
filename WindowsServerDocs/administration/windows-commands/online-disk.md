---
title: オンラインのディスク
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 4c30d0853ff0ae065f02c0ee198c8cdcb90c950b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858063"
---
# <a name="online-disk"></a>オンラインのディスク



現在のオンライン状態にオフラインになっているディスクが表示されます。

> [!IMPORTANT]
> このコマンドでは、Windows Vista のエディションでは使用できません。

> [!IMPORTANT]
> 読み取り専用のディスクで使用されている場合、このコマンドは失敗します。

このコマンドを使用する方法に関する手順については、次を参照してください。[不足] または [オフラインのダイナミック ディスクを再アクティブ化](https://go.microsoft.com/fwlink/?LinkId=207046)(https://go.microsoft.com/fwlink/?LinkId=207046)します。

## <a name="syntax"></a>構文

```
online disk [noerr]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|noerr|スクリプト専用です。 エラーが発生すると、DiskPart は、エラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|

## <a name="remarks"></a>注釈

-   Windows Vista でパラメーターを使用する場合、このコマンドは、ディスク グループ上で動作します。 ベーシック ディスクのグループごとの 1 つ以上のディスクです。 ダイナミック ディスクの場合は、グループには、すべての非外部ダイナミック ディスクが含まれます。
-   ベーシック ディスクには、このコマンドをオンラインにする、選択したディスクとすべてのボリュームをそのディスクを試みます。
-   ダイナミック ディスクの場合はこのコマンドは、ローカル コンピューター上の外部とマークされていないすべてのディスクをオンラインに試みます。 または、一連のダイナミック ディスク上のすべてのボリュームをオンラインに試みます。
-   ディスク グループのダイナミック ディスクがオンラインになり、グループ内の唯一のディスクは場合、は、元のグループが再作成し、ディスクはそのグループに移動します。 グループの他のディスクがオンラインである場合は、し、ディスクは単に戻るグループに追加します。
-   選択したディスクのグループのミラー ボリュームまたは raid-5 ボリュームの場合は、このコマンドにはこれらのボリュームも再同期化します。
-   このコマンドを成功させるには、ディスクを選択してください。 使用して、 **select ディスク** コマンド ディスクを選択し、それにフォーカスをします。

## <a name="BKMK_examples"></a>例

ディスクをオンラインに戻すと、次のように入力します。
```
online disk
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)

