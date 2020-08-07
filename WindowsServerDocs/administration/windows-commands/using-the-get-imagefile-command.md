---
title: get-help-イメージ
description: Windows イメージ (.wim) ファイルに格納されているイメージに関する情報を取得する、ファイルイメージの参照記事。
ms.topic: article
ms.assetid: e1e296fb-20cf-4a60-9db4-4cbac7d4dab5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 10b86929366cc8734a5ff155200fb3078f0cd5d4
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87879378"
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