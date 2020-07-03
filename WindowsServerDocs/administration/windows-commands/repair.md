---
title: 修復
description: 参照記事 * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9f84f661-f3cd-48c8-bf08-87819cf626fe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3e9afb6c418558078496871b71bfaff706753b0a
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85936763"
---
# <a name="repair"></a>修復

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

\-障害が発生したディスク領域を指定されたダイナミックディスクに交換することで、フォーカスのある RAID 5 ボリュームを修復します。



## <a name="syntax"></a>構文

```
repair disk=<n> [align=<n>] [noerr]
```

### <a name="parameters"></a>パラメーター

| パラメーター  |                                                                                             説明                                                                                              |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ディスク\=<n>  |                                                                 障害が発生したディスク領域を置き換えるダイナミックディスクを指定します。                                                                 |
| 位置\=<n> |          すべてのボリュームまたはパーティションエクステントを最も近いアラインメント境界に配置します。 *n*は、 \( \) ディスクの先頭から最も近いアラインメント境界までのキロバイト kb 数です。           |
|   noerr    | スクリプトの場合のみ。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。 |

## <a name="remarks"></a>注釈

-   指定されたダイナミックディスクには、RAID 5 ボリューム内の障害が発生したディスク領域の合計サイズ以上の空き領域が必要 \- です。

-   この操作を成功させるには、RAID 5 アレイのボリュームを \- 選択する必要があります。 使用して、 **ボリュームを選択して** コマンドのボリュームを選択し、それにフォーカスをします。

## <a name="examples"></a>例
ダイナミックディスク4に置き換えることによって、フォーカスのあるボリュームを置き換えるには、次のように入力します。

```
repair disk=4
```

## <a name="additional-references"></a>その他の参照情報
- [コマンド ライン構文の記号](command-line-syntax-key.md)




