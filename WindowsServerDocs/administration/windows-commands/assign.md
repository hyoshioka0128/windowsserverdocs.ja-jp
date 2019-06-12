---
title: assign
description: Windows コマンド」のトピック**割り当てる**-フォーカスのあるボリュームにドライブ文字またはマウント ポイントを割り当てます。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 57912b73-622e-489b-b053-a369021ba8e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8e7f680fe93e846f5b916cf3210a7ca61f190674
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66435300"
---
# <a name="assign"></a>assign

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

フォーカスのあるボリュームにドライブ文字またはマウント ポイントを割り当てます。

## <a name="syntax"></a>構文
```
assign [{letter=<d> | mount=<path>}] [noerr]
```
## <a name="parameters"></a>パラメーター

|  パラメーター   |                                                                                                                                 説明                                                                                                                                 |
|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  文字 =<d>  |                                                                                                             ボリュームに割り当てるドライブ文字。                                                                                                              |
| mount=<path> | ボリュームに割り当てるマウント ポイントのパス。<br /><br />このコマンドを使用する方法に関する手順については、次を参照してください。[マウント ポイント フォルダー パスをドライブに割り当てる](https://go.microsoft.com/fwlink/?LinkId=207059)(<https://go.microsoft.com/fwlink/?LinkId=207059>)。 |
|    noerr     |                                    スクリプト専用です。 エラーが発生すると、DiskPart は、エラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。                                     |

## <a name="remarks"></a>注釈
- ドライブ文字またはマウント ポイントが指定されていない場合は、次の利用可能なドライブ文字が割り当てられます。 ドライブ文字またはマウント ポイントが既に使用されている場合、エラーが生成されます。
- Assign コマンドを使用すると、リムーバブル ドライブに関連付けられたドライブ文字を変更できます。
- システム ボリューム、ブート ボリューム、またはページング ファイルを含むボリュームにドライブ文字を割り当てることはできません。 さらに、Original Equipment Manufacturer (OEM) パーティションまたはベーシック データ パーティション以外の任意の GUID パーティション テーブル (gpt) パーティションにドライブ文字を割り当てることはできません。
- この操作を成功させるのには、ボリュームを選択してください。 使用して、 **ボリュームを選択して** コマンドのボリュームを選択し、それにフォーカスをします。
  ## <a name="BKMK_examples"></a>例
  フォーカスのあるボリュームに割り当てる文字 E には、次のように入力します。
  ```
  assign letter=e
  ```

