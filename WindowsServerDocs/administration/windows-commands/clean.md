---
title: clean
description: Diskpart の clean コマンドの参照記事。フォーカスがあるディスクからすべてのパーティションまたはボリュームのフォーマットを削除します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9bbe6fd3-e07e-487b-9035-910957a1d326
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7a30e1f765959ed60efa662301f95defc21d6587
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85929906"
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

| パラメーター | 説明 |
| --------- | ----------- |
| all | ディスク上のすべてのセクターをゼロに設定し、ディスクに含まれるすべてのデータを完全に削除することを指定します。 |

#### <a name="remarks"></a>注釈

- マスターブートレコード (MBR) ディスクでは、MBR パーティション情報と隠しセクター情報のみが上書きされます。

- GUID パーティションテーブル (gpt) ディスクでは、gpt パーティション情報 (保護 MBR を含む) が上書きされます。 隠しセクター情報はありません。

- この操作を成功させるには、ディスクを選択する必要があります。 使用して、 **select ディスク** コマンド ディスクを選択し、それにフォーカスをします。

## <a name="examples"></a>例

選択したディスクからすべてのフォーマットを削除するには、次のように入力します。

```
clean
```

## <a name="additional-references"></a>その他の参照情報

- [ディスクの消去コマンド](https://docs.microsoft.com/powershell/module/storage/clear-disk)

- [コマンド ライン構文の記号](command-line-syntax-key.md)
