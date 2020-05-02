---
title: clean
description: Diskpart の clean コマンドのリファレンストピック。フォーカスがあるディスクからすべてのパーティションまたはボリュームのフォーマットを削除します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9bbe6fd3-e07e-487b-9035-910957a1d326
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 45a23919dc07c8c1525808859471fdcb9f9e9403
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82712876"
---
# <a name="clean"></a>clean

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

フォーカスがあるディスクからすべてのパーティションまたはボリュームのフォーマットを削除します。

>[!NOTE]
> このコマンドの PowerShell バージョンについては、「 [clear-disk コマンド](https://docs.microsoft.com/powershell/module/storage/clear-disk)」を参照してください。

## <a name="syntax"></a>構文

```
clean [all]
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| --------- | ----------- |
| すべて | ディスク上のすべてのセクターをゼロに設定し、ディスクに含まれるすべてのデータを完全に削除することを指定します。 |

#### <a name="remarks"></a>Remarks

- マスターブートレコード (MBR) ディスクでは、MBR パーティション情報と隠しセクター情報のみが上書きされます。

- GUID パーティションテーブル (gpt) ディスクでは、gpt パーティション情報 (保護 MBR を含む) が上書きされます。 隠しセクター情報はありません。

- この操作を成功させるには、ディスクを選択する必要があります。 使用して、 **select ディスク** コマンド ディスクを選択し、それにフォーカスをします。

## <a name="examples"></a>例

選択したディスクからすべてのフォーマットを削除するには、次のように入力します。

```
clean
```

## <a name="additional-references"></a>その他のリファレンス

- [ディスクの消去コマンド](https://docs.microsoft.com/powershell/module/storage/clear-disk)

- [コマンド ライン構文の記号](command-line-syntax-key.md)
