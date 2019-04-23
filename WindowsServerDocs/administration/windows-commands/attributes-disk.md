---
title: 属性のディスク
description: Windows コマンド」のトピック**属性ディスク**-表示、設定、またはディスクの属性をクリアします。
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 7cacc2fb6b47d095f5e452ca470c89f228949594
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890353"
---
# <a name="attributes-disk"></a>属性のディスク



表示、設定、またはディスクの属性をクリアします。

> [!IMPORTANT]
> このパラメーターは、Windows Vista のエディションでご利用いただけません。

## <a name="syntax"></a>構文

```
attributes disk [{set | clear}] [readonly] [noerr]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|セット (set)|フォーカスのあるディスクの指定した属性を設定します。|
|クリア|フォーカスのあるディスクの指定した属性をクリアします。|
|読み取り専用|ディスクが読み取り専用であることを指定します。|
|noerr|スクリプト専用です。 エラーが発生すると、DiskPart は、エラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|

## <a name="remarks"></a>注釈

-   ときに**属性ディスク**はスタートアップ ディスクの属性、ディスクの現在の属性を表示するために使用、コンピューターを起動するために使用するディスクを表します。 ダイナミック ミラーでは、ブート ボリュームのブート プレックスを含むディスクのことが表示されます。
-   ディスクを選択する必要があります、**属性ディスク**コマンドは成功します。 使用して、 **select ディスク** コマンド ディスクを選択し、それにフォーカスをします。

## <a name="BKMK_examples"></a>例

選択したディスクの属性を表示するには、次のように入力します。
```
attributes disk
```
読み取り専用で、選択したディスクを設定するには、次のように入力します。
```
attributes disk set readonly
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)

