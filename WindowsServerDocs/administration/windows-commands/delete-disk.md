---
title: delete disk
description: ディスクの削除に関する Windows コマンドのトピック。ディスクの一覧から、不足しているダイナミックディスクを削除します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 44079900-e4ed-49d0-81e4-d652c38cd636
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1a767e0689d5fbabb193df37528a0909ab63a1ab
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80846655"
---
# <a name="delete-disk"></a>delete disk

ディスクの一覧から不足しているダイナミックディスクを削除します。

このコマンドの使用方法については、「不足している[ダイナミックディスクを削除する](https://go.microsoft.com/fwlink/?LinkId=207055)」 (https://go.microsoft.com/fwlink/?LinkId=207055)を参照してください。

## <a name="syntax"></a>構文

```
delete disk [noerr] [override]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|noerr|スクリプト専用です。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|
|override|DiskPart でディスク上のすべてのシンプル ボリュームを削除できるようにします。 ミラー ボリュームを構成する領域がディスクに格納されている場合、ディスク上のそのミラー領域は削除されます。 ディスクが RAID-5 ボリュームのメンバーの場合、delete disk override コマンドは失敗します。|

## <a name="examples"></a><a name=BKMK_examples></a>例

ディスクの一覧から不足しているダイナミックディスクを削除するには、次のように入力します。
```
delete disk
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

