---
title: 一意の id
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 64235a4a-b91c-46da-b9b0-68ee90571c2a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d237f4d6d3562e3787efe28ca98f9dc553d74898
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440753"
---
# <a name="uniqueid"></a>一意の id



表示または GUID パーティション テーブル (GPT) の識別子またはマスター ブート レコード (MBR) の署名、フォーカスがあるディスクを設定します。

> [!IMPORTANT]
> この DiskPart コマンドは、Windows Vista のエディションでご利用いただけません。

## <a name="syntax"></a>構文

```
uniqueid disk [id={<dword> | <GUID>}] [noerr]
```

## <a name="parameters"></a>パラメーター

|  パラメーター   |                                                                                             説明                                                                                              |
|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| id={\<dword> |                                                                                               <GUID>}                                                                                                |
|    noerr     | スクリプト専用です。 エラーが発生すると、DiskPart は、エラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。 |

## <a name="remarks"></a>注釈

-   このコマンドは、ベーシック ディスクとダイナミック ディスクで機能します。
-   このコマンドを成功させるには、ディスクを選択してください。 使用して、 **select ディスク** コマンド ディスクを選択し、それにフォーカスをします。

## <a name="BKMK_examples"></a>例

MBR ディスクでは、フォーカスのシグネチャを表示するには、次のように入力します。
```
uniqueid disk
```
MBR ディスクでは、フォーカスのシグネチャを 5f1b2c36 を設定するには、次のように入力します。
```
uniqueid disk id=5f1b2c36
```
Baf784e7-6bbd-4cfb-aaac-e86c96e166ee にフォーカスを持つ GPT ディスクの識別子を設定するには、次のように入力します。
```
uniqueid disk id=baf784e7-6bbd-4cfb-aaac-e86c96e166ee
```

#### <a name="additional-references"></a>その他の参照情報

