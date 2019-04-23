---
title: オフラインのディスク
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8fb9b3c3-0b2c-4192-a2e7-f706292653e3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 617371583a3f0cb3d0cb739845208e4216573d9c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59834623"
---
# <a name="offline-disk"></a>オフラインのディスク



オフラインの状態にフォーカスがあるオンライン ディスクを移動します。

> [!IMPORTANT]
> この DiskPart コマンドは、Windows Vista のエディションでご利用いただけません。

## <a name="syntax"></a>構文

```
offline disk [noerr]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|noerr|スクリプト専用です。 エラーが発生すると、DiskPart は、エラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|

## <a name="remarks"></a>注釈

-   このコマンドは、SAN のオンライン モードであるディスクに動作します。 オフラインに SAN モードを変更します。
-   ディスクの状態を変更する場合は、ダイナミック ディスクにディスク グループがオフラインのままにするに **見つからない** され、グループがオフラインになっているディスクを表示します。 不足しているディスクは、無効なグループに移動されます。 かどうかは、ダイナミック ディスクとは、グループ内の最後のディスク、ディスクの状態が変わります **オフライン**, 、空のグループが削除されます。
-   ディスクを選択する必要があります、 **オフライン ディスク** コマンドを正しく実行されます。 使用して、 **select ディスク** コマンド ディスクを選択し、それにフォーカスをします。

## <a name="BKMK_examples"></a>例

フォーカスがあるディスクをオフラインにするため次のように入力します。
```
offline disk
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)

