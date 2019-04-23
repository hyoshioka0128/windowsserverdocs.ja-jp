---
title: list
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: ef9262a04f469f54e43cf3a83efe30fac7ad8580
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59854673"
---
# <a name="list"></a>list



ディスクのディスクのパーティションのディスク、ボリュームのや仮想ハード_ディスク (Vhd) の一覧を表示します。

## <a name="syntax"></a>構文

```
list { disk | partition | volume | vdisk }
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|ディスク|ディスクと、サイズ、使用可能な空き領域、かどうか、ディスクは、ベーシック ディスクまたはダイナミック ディスク、および、ディスクは、マスター ブート レコード (MBR) または GUID パーティション テーブル (GPT) パーティション スタイルを使用するかどうかの量などに関する情報を一覧表示します。|
|パーティション|パーティションの現在のディスクのパーティション テーブルの一覧が表示されます。|
|ボリューム|すべてのディスク上のベーシック ボリュームとダイナミック ボリュームの一覧を表示します。|
|vdisk|Vhd は、接続されているまたは選択を一覧表示します。 このコマンドは現在選択されている場合にデタッチされた Vhd を一覧表示します。ただし、VHD がアタッチされるまで、ディスクの種類が"不明"に設定されます。 アスタリスク (*) でマークされた VHD では、フォーカスがあります。</br>注:このコマンドでは、Windows 7 および Windows Server 2008 R2 の使用のみです。|

## <a name="remarks"></a>注釈

-   ダイナミック ディスク上のパーティションを一覧表示するとき、パーティションがディスク上のダイナミック ボリュームに対応していません。 この不一致は、ダイナミック ディスクにシステム ボリュームまたはブート ボリューム (ディスクに存在する) 場合のパーティション テーブル内のエントリが含まれているために発生します。 ダイナミック ボリュームで使用する領域を確保するために、ディスクの残りの部分を占有するパーティションも含まれます。
-   アスタリスク (*) でマークされたオブジェクトには、フォーカスがあります。
-   ディスクが見つからない場合は、ディスクを一覧表示、M でのディスク番号が付けられます。最初の不足しているディスクの番号はたとえば、M0 します。

## <a name="BKMK_examples"></a>例

```
list disk
list partition
list volume
list vdisk
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)

