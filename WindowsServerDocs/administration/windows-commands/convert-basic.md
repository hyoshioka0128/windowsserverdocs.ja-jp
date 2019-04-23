---
title: convert basic
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 61329896-3b56-4959-8d58-45cbe18ba860
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5a5aef930689e809b9b697e5f428177610ff723b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862403"
---
# <a name="convert-basic"></a>convert basic



空のダイナミック ディスクをベーシック ディスクに変換します。

このコマンドを使用する方法に関する手順については、次を参照してください。[ベーシック ディスクに変更なダイナミック ディスク バックアップを](https://go.microsoft.com/fwlink/?LinkId=207048)(https://go.microsoft.com/fwlink/?LinkId=207048)します。

## <a name="syntax"></a>構文

```
convert basic [noerr]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|noerr|スクリプト専用です。 エラーが発生すると、DiskPart は、エラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|

## <a name="remarks"></a>注釈

> [!IMPORTANT]
> ディスクをベーシック ディスクに変換する空にする必要があります。 データのバックアップし、ディスクを変換する前にすべてのパーティションまたはボリュームを削除します。
-   この操作を成功させるのには、ダイナミック ディスクを選択してください。 使用して、 **select ディスク**コマンドをダイナミック ディスクを選択し、それにフォーカスをします。

## <a name="BKMK_examples"></a>例

選択されたダイナミック ディスクを basic に変換するには、次のように入力します。
```
convert basic
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)

