---
title: clean
description: Diskpart の clean コマンドの参照記事。フォーカスがあるディスクからすべてのパーティションまたはボリュームのフォーマットを削除します。
ms.topic: article
ms.assetid: 9bbe6fd3-e07e-487b-9035-910957a1d326
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9a8ab6d0b245862fbb935945b76f380b7163d2a3
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87880213"
---
# <a name="clean"></a>clean

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

フォーカスがあるディスクからすべてのパーティションまたはボリュームのフォーマットを削除します。

>[!NOTE]
> このコマンドの PowerShell バージョンについては、「 [clear-disk コマンド](/powershell/module/storage/clear-disk)」を参照してください。

## <a name="syntax"></a>構文

```
clean [all]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| all | ディスク上のすべてのセクターをゼロに設定し、ディスクに含まれるすべてのデータを完全に削除することを指定します。 |

#### <a name="remarks"></a>Remarks

- マスターブートレコード (MBR) ディスクでは、MBR パーティション情報と隠しセクター情報のみが上書きされます。

- GUID パーティションテーブル (gpt) ディスクでは、gpt パーティション情報 (保護 MBR を含む) が上書きされます。 隠しセクター情報はありません。

- この操作を成功させるには、ディスクを選択する必要があります。 使用して、 **select ディスク** コマンド ディスクを選択し、それにフォーカスをします。

## <a name="examples"></a>例

選択したディスクからすべてのフォーマットを削除するには、次のように入力します。

```
clean
```

## <a name="additional-references"></a>その他の参照情報

- [ディスクの消去コマンド](/powershell/module/storage/clear-disk)

- [コマンド ライン構文の記号](command-line-syntax-key.md)
