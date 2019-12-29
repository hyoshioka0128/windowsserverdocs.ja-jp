---
title: assign
description: '**Assign**の Windows コマンドに関するトピックでは、フォーカスのあるボリュームにドライブ文字またはマウントポイントを割り当てます。'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 3e07edcd4ac4ddf5eca1e57da17df441043d15f6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382678"
---
# <a name="assign"></a>assign

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

フォーカスがあるボリュームにドライブ文字またはマウントポイントを割り当てます。

## <a name="syntax"></a>構文
```
assign [{letter=<d> | mount=<path>}] [noerr]
```
## <a name="parameters"></a>パラメーター

|  パラメーター   |                                                                                                                                 説明                                                                                                                                 |
|--------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  文字 = <d>  |                                                                                                             ボリュームに割り当てるドライブ文字です。                                                                                                              |
| mount = <path> | ボリュームに割り当てるマウントポイントのパス。<br /><br />このコマンドの使用方法については、「[ドライブにマウントポイントフォルダーパスを割り当てる](https://go.microsoft.com/fwlink/?LinkId=207059)(<https://go.microsoft.com/fwlink/?LinkId=207059>)」を参照してください。 |
|    noerr     |                                    スクリプトの場合のみ。 エラーが発生した場合、DiskPart はエラーが発生しなかったかのようにコマンドを処理し続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。                                     |

## <a name="remarks"></a>コメント
- ドライブ文字またはマウントポイントが指定されていない場合は、次に利用可能なドライブ文字が割り当てられます。 ドライブ文字またはマウントポイントが既に使用されている場合は、エラーが生成されます。
- Assign コマンドを使用して、リムーバブルドライブに関連付けられているドライブ文字を変更できます。
- システムボリューム、ブートボリューム、またはページングファイルを含むボリュームにドライブ文字を割り当てることはできません。 さらに、ベーシックデータパーティション以外の OEM (相手先ブランド供給) パーティションまたは GUID パーティションテーブル (gpt) パーティションにドライブ文字を割り当てることはできません。
- この操作を成功させるのには、ボリュームを選択してください。 使用して、 **ボリュームを選択して** コマンドのボリュームを選択し、それにフォーカスをします。
  ## <a name="BKMK_examples"></a>例
  フォーカスがあるボリュームに E という文字を割り当てるには、次のように入力します。
  ```
  assign letter=e
  ```

