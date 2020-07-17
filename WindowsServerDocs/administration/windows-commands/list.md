---
title: list
description: List コマンドの参照記事。ディスクの一覧、ディスク内のパーティション、ディスク内のボリューム、またはバーチャルハードディスク (Vhd) の一覧が表示されます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 69b105a1-9710-4a06-8102-38cc9e475ca5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fda60b0520da00659d0ac8fc9cab483c62e2a6a7
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85931708"
---
# <a name="list"></a>list

ディスクのパーティション、ディスク内のボリューム、またはバーチャルハードディスク (Vhd) のディスクの一覧を表示します。

## <a name="syntax"></a>構文

```
list { disk | partition | volume | vdisk }
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| disk | ディスクの一覧とディスクに関する情報を表示します。ディスクに関する情報には、ディスクのサイズ、使用可能な空き領域の量、ディスクがベーシック ディスクであるかダイナミック ディスクであるか、ディスクが使用しているパーティション スタイルがマスター ブート レコード (MBR) であるか GUID パーティション テーブル (GPT) であるかなどがあります。 |
| partition | 現在のディスクのパーティション テーブルに記録されているパーティションを一覧表示します。 |
| ボリューム | すべてのディスク上のベーシック ボリュームとダイナミック ボリュームの一覧を表示します。 |
| vdisk | アタッチされている、または選択されている Vhd の一覧を表示します。 このコマンドは、デタッチされている Vhd を一覧表示します (現在選択されている場合)。ただし、VHD が接続されるまで、ディスクの種類は [不明] に設定されます。 アスタリスク (*) でマークされた VHD にフォーカスがあります。 |

#### <a name="remarks"></a>注釈

- ダイナミックディスク上のパーティションを一覧表示する場合、パーティションはディスク上のダイナミックボリュームに対応していない可能性があります。 この不一致が発生するのは、ダイナミック ディスクにシステム ボリュームまたはブート ボリュームが存在する場合、それらのエントリがパーティション テーブル内に格納されるためです。 また、ダイナミックボリュームで使用する領域を確保するために、ディスクの残りの部分を占有するパーティションも含まれています。

- アスタリスク (*) でマークされたオブジェクトにフォーカスがあります。

- ディスクを一覧表示するとき、ディスクが見つからない場合は、そのディスク番号の先頭に M が付きます。たとえば、最初の見つからないディスクには*M0*という番号が付けられます。

### <a name="examples"></a>例

```
list disk
list partition
list volume
list vdisk
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
