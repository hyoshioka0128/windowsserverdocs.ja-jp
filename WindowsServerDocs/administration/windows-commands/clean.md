---
title: clean
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 6e7d7613784f3e599005b25259f70466db60e626
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877433"
---
# <a name="clean"></a>clean

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Diskpart のクリーン コマンドは、すべてのパーティションまたはボリュームにフォーカスがあるディスクから書式設定を削除します。
## <a name="syntax"></a>構文
```
clean [all]
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|all|ディスク上のすべてのセクターが、ディスク上に含まれるすべてのデータを完全に削除する、0 に設定されているを指定します。|
## <a name="remarks"></a>注釈
-   マスター ブート レコード (MBR) ディスクでは、MBR パーティション情報と隠しセクター情報だけが上書きされます。
-   GUID パーティション テーブル (gpt) ディスクを gpt パーティション、プロテクティブ MBR を含む情報が上書きされます。 隠しセクター情報はありません。
-   この操作を成功させるのには、ディスクを選択してください。 使用して、 **select ディスク** コマンド ディスクを選択し、それにフォーカスをします。
## <a name="BKMK_examples"></a>例
選択したディスクからすべての書式設定を削除するには、次のように入力します。
```
clean
```

[Clear-disk](https://technet.microsoft.com/library/hh848661.aspx)
