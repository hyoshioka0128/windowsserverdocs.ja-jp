---
title: ボリュームの追加
description: '**[ボリュームの追加]** の Windows コマンドのトピック-シャドウコピーセットにボリュームを追加します。これはシャドウコピーするボリュームのセットです。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b7d4d35d-8bda-46d2-8df5-eb598cecaaba
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c534bcc5a264fbb51d12cfd2a6fc93b4e6fbd857
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382788"
---
# <a name="add-volume"></a>ボリュームの追加



シャドウコピーするボリュームのセットであるボリュームをシャドウコピーセットに追加します。 このコマンドは、シャドウコピーを作成するために必要です。 パラメーターを指定せずに使用する場合は、 **[ボリュームの追加]** コマンドプロンプトでヘルプを表示します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
add volume <Volume> [provider <ProviderID>]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<ボリューム >|シャドウコピーセットに追加するボリュームを指定します。 シャドウコピーの作成には、少なくとも1つのボリュームが必要です。|
|[プロバイダー \<ProviderID >]|シャドウコピーの作成に使用する登録済みプロバイダーのプロバイダー ID を指定します。 **プロバイダー**が指定されていない場合は、既定のプロバイダーが使用されます。|

## <a name="remarks"></a>注釈

-   ボリュームは一度に1つずつ追加されます。
-   ボリュームが追加されるたびに、VSS がそのボリュームのシャドウコピーの作成をサポートしているかどうかがチェックされます。 ただし、このプライマリチェックは、後で**set コンテキスト**コマンドを使用することによって無効にされる場合があります。
-   シャドウコピーが作成されると、環境変数によってエイリアスがシャドウ ID にリンクされるため、エイリアスをスクリプト作成に使用できます。

## <a name="BKMK_examples"></a>例

登録されているプロバイダーの現在の一覧を表示するには、`DISKSHADOW>` プロンプトで次のように入力します。
```
list providers
```
次の出力には、既定で使用される単一のプロバイダーが表示されます。
```
* ProviderID: {b5946137-7b9f-4925-af80-51abd60b20d5}
        Type: [1] VSS_PROV_SYSTEM
        Name: Microsoft Software Shadow Copy provider 1.0
        Version: 1.0.0.7
        CLSID: {65ee1dba-8ff4-4a58-ac1c-3470ee2f376a}
1 provider registered.
```
シャドウコピーセットにドライブ C を追加し、System1 という名前のエイリアスを割り当てるには、次のように入力します。
```
add volume c: alias System1
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)