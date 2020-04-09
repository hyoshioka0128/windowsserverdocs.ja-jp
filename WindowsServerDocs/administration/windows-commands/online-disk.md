---
title: オンラインディスク
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bc44a783-eaa4-40ca-be01-5703b5bf4eb3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c61d852ba71329c3d7345d74fd352a6c19436cec
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80837895"
---
# <a name="online-disk"></a>オンラインディスク



現在のオンライン状態にオフラインになっているディスクが表示されます。

> [!IMPORTANT]
> このコマンドは、Windows Vista のどのエディションでも使用できません。

> [!IMPORTANT]
> 読み取り専用ディスクで使用されている場合、このコマンドは失敗します。

このコマンドの使用方法については、「[不足またはオフラインのダイナミックディスクを再アクティブ化](https://go.microsoft.com/fwlink/?LinkId=207046)する」 (https://go.microsoft.com/fwlink/?LinkId=207046)を参照してください。

## <a name="syntax"></a>構文

```
online disk [noerr]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|noerr|スクリプト専用です。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|

## <a name="remarks"></a>コメント

-   Windows Vista でパラメーターを指定せずに使用した場合、このコマンドはディスクグループ上で動作します。 ベーシック ディスクのグループごとの 1 つ以上のディスクです。 ダイナミックディスクの場合、このグループには、非外部ダイナミックディスクがすべて含まれます。
-   ベーシック ディスクには、このコマンドをオンラインにする、選択したディスクとすべてのボリュームをそのディスクを試みます。
-   ダイナミック ディスクの場合はこのコマンドは、ローカル コンピューター上の外部とマークされていないすべてのディスクをオンラインに試みます。 または、一連のダイナミック ディスク上のすべてのボリュームをオンラインに試みます。
-   ディスク グループのダイナミック ディスクがオンラインになり、グループ内の唯一のディスクは場合、は、元のグループが再作成し、ディスクはそのグループに移動します。 グループの他のディスクがオンラインである場合は、し、ディスクは単に戻るグループに追加します。
-   選択したディスクのグループにミラーボリュームまたは RAID-5 ボリュームが含まれている場合は、このコマンドによってこれらのボリュームも再同期されます。
-   このコマンドを成功させるには、ディスクを選択してください。 使用して、 **select ディスク** コマンド ディスクを選択し、それにフォーカスをします。

## <a name="examples"></a><a name=BKMK_examples></a>例

ディスクをオンラインに戻すと、次のように入力します。
```
online disk
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

