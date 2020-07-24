---
title: assign
description: Assign コマンドの参照記事。フォーカスのあるボリュームにドライブ文字またはマウントポイントを割り当てます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 57912b73-622e-489b-b053-a369021ba8e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 41c6194b68414be65fcf6b93b662e25ae80e0309
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86955504"
---
# <a name="assign"></a>assign

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

フォーカスがあるボリュームに、ドライブ文字またはマウント ポイントを割り当てます。 また、このコマンドを使用して、リムーバブルドライブに関連付けられているドライブ文字を変更することもできます。 ドライブ文字またはマウント ポイントを指定しない場合は、次に利用できるドライブ文字が割り当てられます。 ドライブ文字またはマウント ポイントが既に使用されている場合は、エラーが発生します。

この操作を成功させるのには、ボリュームを選択してください。 使用して、 **ボリュームを選択して** コマンドのボリュームを選択し、それにフォーカスをします。

> [!IMPORTANT]
> システムボリューム、ブートボリューム、またはページングファイルを含むボリュームにドライブ文字を割り当てることはできません。 さらに、ベーシックデータパーティション以外の OEM (相手先ブランド供給) パーティションまたは GUID パーティションテーブル (gpt) パーティションにドライブ文字を割り当てることはできません。

## <a name="syntax"></a>構文

```
assign [{letter=<d> | mount=<path>}] [noerr]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `letter=<d>` | ボリュームに割り当てるドライブ文字です。 |
| `mount=<path>` | ボリュームに割り当てるマウントポイントのパス。 このコマンドの使用方法については、「[ドライブにマウントポイントフォルダーパスを割り当てる](../../storage/disk-management/assign-a-mount-point-folder-path-to-a-drive.md)」を参照してください。 |
| noerr | スクリプト専用です。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。 |

## <a name="examples"></a>例

フォーカスがあるボリュームに E という文字を割り当てるには、次のように入力します。

```
assign letter=e
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [ボリュームの選択コマンド](select-volume.md)
