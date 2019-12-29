---
title: clean
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9bbe6fd3-e07e-487b-9035-910957a1d326
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f871ad1d13e06bf0cbb886ba64a52e7a55a9a797
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379324"
---
# <a name="clean"></a>clean

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Diskpart の clean コマンドは、フォーカスがあるディスクからすべてのパーティションまたはボリュームのフォーマットを削除します。
## <a name="syntax"></a>構文
```
clean [all]
```
## <a name="parameters"></a>パラメーター

| パラメーター |                                                        説明                                                        |
|-----------|---------------------------------------------------------------------------------------------------------------------------|
|    all    | ディスク上のすべてのセクターをゼロに設定し、ディスクに含まれるすべてのデータを完全に削除することを指定します。 |

## <a name="remarks"></a>コメント
- マスターブートレコード (MBR) ディスクでは、MBR パーティション情報と隠しセクター情報のみが上書きされます。
- GUID パーティションテーブル (gpt) ディスクでは、gpt パーティション情報 (保護 MBR を含む) が上書きされます。 隠しセクター情報はありません。
- この操作を成功させるには、ディスクを選択する必要があります。 使用して、 **select ディスク** コマンド ディスクを選択し、それにフォーカスをします。
  ## <a name="BKMK_examples"></a>例
  選択したディスクからすべてのフォーマットを削除するには、次のように入力します。
  ```
  clean
  ```

[ディスクの消去](https://technet.microsoft.com/library/hh848661.aspx)
