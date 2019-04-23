---
title: ディスクを削除します。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 44079900-e4ed-49d0-81e4-d652c38cd636
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e401133854118e82a45fd5e01466288ae41f67da
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863913"
---
# <a name="delete-disk"></a>ディスクを削除します。



ディスクの一覧から不明なダイナミック ディスクを削除します。

このコマンドを使用する方法に関する手順については、次を参照してください。[不足しているダイナミック ディスクを削除する](https://go.microsoft.com/fwlink/?LinkId=207055)(https://go.microsoft.com/fwlink/?LinkId=207055)します。

## <a name="syntax"></a>構文

```
delete disk [noerr] [override]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|noerr|スクリプト専用です。 エラーが発生すると、DiskPart は、エラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|
|上書き|Diskpart でディスク上のすべてのシンプル ボリュームを削除します。 ディスクがミラー化されたボリュームの半分含まれる場合、ディスク上のミラーの半分は削除されます。 ディスクが raid-5 ボリュームのメンバーである場合、delete disk override のコマンドが失敗します。|

## <a name="BKMK_examples"></a>例

不明なダイナミック ディスクをディスクの一覧から削除するには、次のように入力します。
```
delete disk
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)

