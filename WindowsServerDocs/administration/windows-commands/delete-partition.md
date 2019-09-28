---
title: パーティションの削除
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 65752312-cb16-46f6-870f-1b95c507b101
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 46a214f26e7c21f6ae08eb16d95fd898bd949b0f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378658"
---
# <a name="delete-partition"></a>パーティションの削除



フォーカスがあるパーティションを削除します。

## <a name="syntax"></a>構文

```
delete partition [noerr] [override]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|上書き|型に関係なく、DiskPart でパーティションを削除できるようにします。 通常、DiskPart では既知のデータパーティションのみを削除できます。|
|noerr|スクリプトの場合のみ。 エラーが発生した場合、DiskPart はエラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|

## <a name="remarks"></a>コメント

> [!CAUTION]
> ダイナミックディスク上のパーティションを削除すると、ディスク上のすべてのダイナミックボリュームが削除されるため、データが破棄され、ディスクが破損状態のままになります。 ダイナミックボリュームを削除するには、代わりに **[ボリュームの削除]** コマンドを常に使用します。 パーティションはダイナミックディスクから削除できますが、作成することはできません。 たとえば、ダイナミック GPT ディスク上の認識されていない GUID パーティションテーブル (GPT) パーティションを削除することができます。 このようなパーティションを削除しても、結果として得られる空き領域が使用できなくなることはありません。 このコマンドは、DiskPart の**clean**コマンドを使用できない緊急の状況で、破損したオフラインダイナミックディスク上の領域を再利用できるようにするためのものです。
> -   システムパーティション、ブートパーティション、またはアクティブなページングファイルやクラッシュダンプ情報が含まれているパーティションを削除することはできません。
> -   この操作を成功させるには、パーティションを選択する必要があります。 **[パーティションの選択**] コマンドを使用してパーティションを選択し、それにフォーカスを移動します。

## <a name="BKMK_examples"></a>例

フォーカスのあるパーティションを削除するには、次のように入力します。
```
delete partition
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)

