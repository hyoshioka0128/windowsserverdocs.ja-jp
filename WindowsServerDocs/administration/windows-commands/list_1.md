---
title: list
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 69b105a1-9710-4a06-8102-38cc9e475ca5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a9ac8b19ecae30c339138f61a13c21147d4bcf1b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374648"
---
# <a name="list"></a>list



ディスクのパーティション、ディスク内のボリューム、またはバーチャルハードディスク (Vhd) のディスクの一覧を表示します。

## <a name="syntax"></a>構文

```
list { disk | partition | volume | vdisk }
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|ディスク|ディスクの一覧と、ディスクのサイズ、使用可能な空き領域の容量、ディスクがベーシックディスクまたはダイナミックディスクかどうか、ディスクがマスターブートレコード (MBR) または GUID パーティションテーブル (GPT) パーティションスタイルを使用しているかどうかなどの情報を表示します。|
|パーティション|現在のディスクのパーティションテーブルに一覧表示されているパーティションを表示します。|
|ボリューム|すべてのディスク上のベーシック ボリュームとダイナミック ボリュームの一覧を表示します。|
|vdisk|アタッチされている、または選択されている Vhd の一覧を表示します。 このコマンドは、デタッチされている Vhd を一覧表示します (現在選択されている場合)。ただし、VHD が接続されるまで、ディスクの種類は [不明] に設定されます。 アスタリスク (*) でマークされた VHD にフォーカスがあります。</br>メモ:このコマンドでは、Windows 7 および Windows Server 2008 R2 の使用のみです。|

## <a name="remarks"></a>コメント

-   ダイナミックディスク上のパーティションを一覧表示する場合、パーティションはディスク上のダイナミックボリュームに対応していない可能性があります。 このような不一致が発生するのは、ダイナミックディスクにシステムボリュームまたはブートボリューム (ディスク上に存在する場合) のパーティションテーブルのエントリが含まれているためです。 また、ダイナミックボリュームで使用する領域を確保するために、ディスクの残りの部分を占有するパーティションも含まれています。
-   アスタリスク (*) でマークされたオブジェクトにフォーカスがあります。
-   ディスクを一覧表示するとき、ディスクが見つからない場合は、そのディスク番号の先頭に M が付きます。たとえば、最初の見つからないディスクには M0 という番号が付けられます。

## <a name="BKMK_examples"></a>例

```
list disk
list partition
list volume
list vdisk
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)

