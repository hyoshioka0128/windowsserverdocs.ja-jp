---
title: 追加
description: Windows コマンド」のトピック**add_1** - ボリュームをシャドウ コピー、ボリュームのセットに追加します。 またはエイリアスの環境にエイリアスを追加します。
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 549c8560774f004a60926ce568c850fd1b71c7f9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889953"
---
# <a name="add"></a>追加


シャドウ コピー、ボリュームのセットにボリュームを追加するか、別名環境にエイリアスを追加します。 サブコマンドを指定せずに使用する場合**追加**現在のボリュームおよびエイリアスを一覧表示されます。

> [!NOTE]
> エイリアスは、シャドウ コピーが作成されるまで、エイリアスの環境に追加されません。 使用してすぐに必要なエイリアスを追加する必要があります**エイリアスの追加**します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
add 
add volume <Volume> [provider <ProviderID>] 
add alias <AliasName> <AliasValue>
```

## <a name="add-subcommands"></a>サブコマンドを追加します。

|サブコマンド|説明|
|----------|-----------|
|ボリューム|シャドウ コピーを設定するにはシャドウ コピー ボリュームのセットであるボリュームを追加します。 参照してください[ボリュームの追加](add-volume.md)構文およびパラメーターについてです。|
|別名 (alias)|エイリアスの環境には、指定した名前と値を追加します。 参照してください[追加エイリアス](add-alias.md)構文およびパラメーターについてです。|
|/?|コマンド ライン ヘルプを表示します。|

## <a name="BKMK_examples"></a>例

追加されたボリュームとを環境は、現在のエイリアスを表示するには、次のように入力します。
```
add
```
次の出力は、ドライブ C がシャドウ コピー セットに追加されたことを示しています。
```
Volume c: alias System1    GUID \\?\Volume{XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX}\
1 volume in Shadow Copy Set.
No Diskshadow aliases in the environment.
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)