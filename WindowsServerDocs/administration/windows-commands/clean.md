---
title: clean
description: Diskpart の clean コマンドに関する Windows コマンドのトピック。フォーカスがあるディスクからすべてのパーティションまたはボリュームのフォーマットを削除します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9bbe6fd3-e07e-487b-9035-910957a1d326
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d573a0480c24a2a622618197dea7dccaeddac271
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80847755"
---
# <a name="clean"></a>clean

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Diskpart の clean コマンドは、フォーカスがあるディスクからすべてのパーティションまたはボリュームのフォーマットを削除します。

## <a name="syntax"></a>構文
```
clean [all]
```
### <a name="parameters"></a>パラメーター

| パラメーター |                                                        説明                                                        |
|-----------|---------------------------------------------------------------------------------------------------------------------------|
|    all    | ディスク上のすべてのセクターをゼロに設定し、ディスクに含まれるすべてのデータを完全に削除することを指定します。 |

## <a name="remarks"></a>コメント
- マスター ブート レコード (MBR) ディスクでは、MBR パーティション情報と隠しセクター情報のみが上書きされます。
- GUID パーティションテーブル (gpt) ディスクでは、gpt パーティション情報 (保護 MBR を含む) が上書きされます。 隠しセクター情報はありません。
- この操作を成功させるには、ディスクを選択する必要があります。 使用して、 **select ディスク** コマンド ディスクを選択し、それにフォーカスをします。

## <a name="examples"></a><a name=BKMK_examples></a>例
  選択したディスクからすべてのフォーマットを削除するには、次のように入力します。
  ```
  clean
  ```

## <a name="additional-references"></a>その他の参照情報
[ディスクの消去](https://technet.microsoft.com/library/hh848661.aspx)
