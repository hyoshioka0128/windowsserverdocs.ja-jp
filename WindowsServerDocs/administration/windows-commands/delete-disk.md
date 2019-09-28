---
title: ディスクの削除
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 886e84edf80227d42ad77e36aed388b9e853ca62
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378671"
---
# <a name="delete-disk"></a>ディスクの削除



ディスクの一覧から不足しているダイナミックディスクを削除します。

このコマンドの使用方法については、「不足している[ダイナミックディスクの削除](https://go.microsoft.com/fwlink/?LinkId=207055)(https://go.microsoft.com/fwlink/?LinkId=207055) 」を参照してください。

## <a name="syntax"></a>構文

```
delete disk [noerr] [override]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|noerr|スクリプトの場合のみ。 エラーが発生した場合、DiskPart はエラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|
|上書き|DiskPart でディスク上のすべてのシンプルボリュームを削除できるようにします。 ミラーボリュームの半分がディスクに含まれている場合、ディスク上のミラーの半分が削除されます。 ディスクが RAID-5 ボリュームのメンバーである場合、delete disk override コマンドは失敗します。|

## <a name="BKMK_examples"></a>例

ディスクの一覧から不足しているダイナミックディスクを削除するには、次のように入力します。
```
delete disk
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)

