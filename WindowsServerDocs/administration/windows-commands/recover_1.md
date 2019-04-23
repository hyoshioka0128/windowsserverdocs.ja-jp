---
title: 復元 (recover)
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 261bfd79d74323ad324246e21b84a5eb798ebcdf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867183"
---
# <a name="recover"></a>復元 (recover)



ディスク グループのすべてのディスクの状態を更新、グループでは無効なディスク、ディスクの復旧を試みるおよびミラー ボリュームや raid-5 ボリューム データは古いデータを再同期化します。

> [!IMPORTANT]
> この DiskPart コマンドは、Windows Vista のエディションでご利用いただけません。

## <a name="syntax"></a>構文

```
recover [noerr]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|noerr|スクリプト専用です。 エラーが発生すると、DiskPart は、エラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|

## <a name="remarks"></a>注釈

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

[コマンドライン構文キー](command-line-syntax-key.md)

