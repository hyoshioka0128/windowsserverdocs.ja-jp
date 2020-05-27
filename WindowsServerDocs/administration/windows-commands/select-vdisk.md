---
title: vdisk の選択
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 8808872a-3523-4205-a6c6-83fa738ee37a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 23741d9211ebdf98ac198af2ae1c562724a1955b
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2020
ms.locfileid: "83821082"
---
# <a name="select-vdisk"></a>vdisk の選択

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定された仮想ハードディスク VHD を選択 \( \) し、それにフォーカスを移動します。

> [!NOTE]
> このコマンドは、Windows 7 と Windows Server 2008 R2 に該当するだけです。

## <a name="syntax"></a>構文

```
select vdisk file=<full path> [noerr]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------|--------|
|拡張子\=<full path>|既存の VHD ファイルの完全パスとファイル名を指定します。|
|noerr|スクリプト作成にのみ使用されます。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。|

## <a name="examples"></a>例
フォーカスを Test.vhd という名前の VHD に、次のように入力します。

```
select vdisk file=c:\test\test.vhd
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

-   [vdisk のアタッチ](attach-vdisk.md)

-   [compact vdisk](compact-vdisk.md)



-   [Vdisk のデタッチ](detach-vdisk.md)

-   [詳細 vdisk](detail-vdisk.md)

-   [vdisk を展開する](expand-vdisk.md)

-   [Vdisk をマージします。](merge-vdisk.md)

-   [list_1](list_1.md)


