---
title: 追加
description: '**Add_1**の Windows コマンドトピックでは、シャドウコピーするボリュームのセットにボリュームを追加したり、エイリアス環境に別名を追加したりします。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 47efce7a-86d2-4872-ae31-baa108757afd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d1aaa211938d14a0019d29e64867f4df2475a877
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382784"
---
# <a name="add"></a>追加


シャドウコピーするボリュームのセットにボリュームを追加するか、エイリアス環境に別名を追加します。 サブコマンドなしで使用する場合は、現在のボリュームとエイリアスの一覧を**追加**します。

> [!NOTE]
> エイリアスは、シャドウコピーが作成されるまでエイリアス環境に追加されません。 すぐに必要なエイリアスを追加するには、 **add alias**を使用します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
add 
add volume <Volume> [provider <ProviderID>] 
add alias <AliasName> <AliasValue>
```

## <a name="add-subcommands"></a>サブコマンドの追加

|サブコマンド|説明|
|----------|-----------|
|ボリューム|シャドウコピーするボリュームのセットであるボリュームをシャドウコピーセットに追加します。 「構文とパラメーターの[ボリュームの追加](add-volume.md)」を参照してください。|
|別名 (alias)|指定された名前と値をエイリアス環境に追加します。 「構文とパラメーターの[別名の追加](add-alias.md)」を参照してください。|
|/?|コマンドラインでヘルプを表示します。|

## <a name="BKMK_examples"></a>例

追加されたボリュームと現在の環境内にある別名を表示するには、次のように入力します。
```
add
```
次の出力は、ドライブ C がシャドウコピーセットに追加されたことを示しています。
```
Volume c: alias System1    GUID \\?\Volume{XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX}\
1 volume in Shadow Copy Set.
No Diskshadow aliases in the environment.
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)