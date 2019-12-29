---
title: 属性ディスク
description: '**Attributes ディスク**の Windows コマンドに関するトピック-ディスクの属性を表示、設定、またはクリアします。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: eed57071-c1c6-4394-9542-62b52a878c92
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 415125208b13d82adeed736107f59fda9489a953
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382569"
---
# <a name="attributes-disk"></a>属性ディスク



ディスクの属性を表示、設定、またはクリアします。

> [!IMPORTANT]
> このパラメーターは、Windows Vista のどのエディションでも使用できません。

## <a name="syntax"></a>構文

```
attributes disk [{set | clear}] [readonly] [noerr]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|セット (set)|フォーカスがあるディスクの指定された属性を設定します。|
|クリア|フォーカスがあるディスクの指定された属性をクリアします。|
|readonly|ディスクが読み取り専用であることを指定します。|
|noerr|スクリプトの場合のみ。 エラーが発生した場合、DiskPart はエラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|

## <a name="remarks"></a>コメント

-   **Attributes disk**を使用してディスクの現在の属性を表示すると、スタートアップディスク属性は、コンピューターを起動するために使用されるディスクを表します。 ダイナミックミラーの場合は、ブートボリュームのブートプレックスが格納されているディスクに対して表示されます。
-   **[ディスクの属性]** コマンドを正常に実行するには、ディスクを選択する必要があります。 使用して、 **select ディスク** コマンド ディスクを選択し、それにフォーカスをします。

## <a name="BKMK_examples"></a>例

選択したディスクの属性を表示するには、次のように入力します。
```
attributes disk
```
選択したディスクを読み取り専用に設定するには、次のように入力します。
```
attributes disk set readonly
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)

