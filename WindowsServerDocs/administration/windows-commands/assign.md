---
title: assign
description: '**Assign**の Windows コマンドに関するトピック。フォーカスのあるボリュームにドライブ文字またはマウントポイントを割り当てます。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 57912b73-622e-489b-b053-a369021ba8e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c4745b0472e2c8ee7a4034d9a06d395d6089db6f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851305"
---
# <a name="assign"></a>assign

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

フォーカスがあるボリュームに、ドライブ文字またはマウント ポイントを割り当てます。

## <a name="syntax"></a>構文

```
assign [{letter=<d> | mount=<path>}] [noerr]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `letter=<d>` | ボリュームに割り当てるドライブ文字です。 |
| `mount=<path>` | ボリュームに割り当てるマウントポイントのパス。 このコマンドの使用方法については、「[ドライブにマウントポイントフォルダーパスを割り当てる](https://go.microsoft.com/fwlink/?LinkId=207059)」を参照してください。 |
| noerr | スクリプト専用です。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。 |

## <a name="remarks"></a>コメント

- ドライブ文字またはマウント ポイントを指定しない場合は、次に利用できるドライブ文字が割り当てられます。 ドライブ文字またはマウント ポイントが既に使用されている場合は、エラーが発生します。

- Assign コマンドを使用して、リムーバブルドライブに関連付けられているドライブ文字を変更できます。

- システム ボリューム、ブート ボリューム、またはページング ファイルを持つボリュームにドライブ文字を割り当てることはできません。 さらに、ベーシックデータパーティション以外の OEM (相手先ブランド供給) パーティションまたは GUID パーティションテーブル (gpt) パーティションにドライブ文字を割り当てることはできません。

- この操作を正常に実行するには、ボリュームを選択する必要があります。 使用して、 **ボリュームを選択して** コマンドのボリュームを選択し、それにフォーカスをします。

## <a name="examples"></a><a name=BKMK_examples></a>例
フォーカスがあるボリュームに E という文字を割り当てるには、次のように入力します。
```
assign letter=e
```

## <a name="additional-references"></a>その他の参照情報

- [コマンドライン構文のキー](command-line-syntax-key.md

