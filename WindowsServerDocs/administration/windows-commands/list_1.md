---
title: リスト
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 69b105a1-9710-4a06-8102-38cc9e475ca5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b36600ff4de16bf35b1c2067efac9b13957cefaa
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841035"
---
# <a name="list"></a>リスト



ディスクのパーティション、ディスク内のボリューム、またはバーチャルハードディスク (Vhd) のディスクの一覧を表示します。

## <a name="syntax"></a>構文

```
list { disk | partition | volume | vdisk }
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|ディスク|ディスクの一覧とディスクに関する情報を表示します。ディスクに関する情報には、ディスクのサイズ、使用可能な空き領域の量、ディスクがベーシック ディスクであるかダイナミック ディスクであるか、ディスクが使用しているパーティション スタイルがマスター ブート レコード (MBR) であるか GUID パーティション テーブル (GPT) であるかなどがあります。|
|partition|現在のディスクのパーティション テーブルに記録されているパーティションを一覧表示します。|
|ボリューム●ぼりゅーむ○|すべてのディスク上のベーシック ボリュームとダイナミック ボリュームの一覧を表示します。|
|vdisk|アタッチされている、または選択されている Vhd の一覧を表示します。 このコマンドは、デタッチされている Vhd を一覧表示します (現在選択されている場合)。ただし、VHD が接続されるまで、ディスクの種類は [不明] に設定されます。 アスタリスク (*) でマークされた VHD にフォーカスがあります。</br>注: このコマンドは、Windows 7 および Windows Server 2008 R2 でのみ使用できます。|

## <a name="remarks"></a>コメント

-   ダイナミックディスク上のパーティションを一覧表示する場合、パーティションはディスク上のダイナミックボリュームに対応していない可能性があります。 この不一致が発生するのは、ダイナミック ディスクにシステム ボリュームまたはブート ボリュームが存在する場合、それらのエントリがパーティション テーブル内に格納されるためです。 また、ダイナミックボリュームで使用する領域を確保するために、ディスクの残りの部分を占有するパーティションも含まれています。
-   アスタリスク (*) でマークされたオブジェクトにフォーカスがあります。
-   ディスクを一覧表示するとき、ディスクが見つからない場合は、そのディスク番号の先頭に M が付きます。たとえば、最初の見つからないディスクには M0 という番号が付けられます。

## <a name="examples"></a><a name=BKMK_examples></a>例

```
list disk
list partition
list volume
list vdisk
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

