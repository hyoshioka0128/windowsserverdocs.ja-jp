---
title: get-help-イメージ
description: Windows イメージ (.wim) ファイルに格納されているイメージに関する情報を取得する、ファイルイメージの参照記事。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e1e296fb-20cf-4a60-9db4-4cbac7d4dab5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 127b5282b74020f002c7ccc55663fc2571584582
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85932222"
---
# <a name="get-imagefile"></a>get-help-イメージ

Windows イメージ (.wim) ファイルに含まれるイメージに関する情報を取得します。

## <a name="syntax"></a>構文

```
WDSUTIL [Options] /Get-ImageFile /ImageFile:<wim file path> [/Detailed]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|イメージ\<WIM file path>|.Wim ファイルの完全パスとファイル名を指定します。|
|[/詳細]|各イメージからすべてのイメージのメタデータを返します。 このオプションを使用しない場合、既定の動作は、イメージの名前、説明、およびファイル名のみを返すには。|

## <a name="examples"></a>例

イメージに関する情報を表示するには、次のように入力します。
```
WDSUTIL /Get-ImageFile /ImageFile:C:\temp\install.wim
```
詳細な情報を表示するには、次のように入力します。
```
WDSUTIL /Verbose /Get-ImageFile /ImageFile:\\Server\Share\My Folder \install.wim /Detailed
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)