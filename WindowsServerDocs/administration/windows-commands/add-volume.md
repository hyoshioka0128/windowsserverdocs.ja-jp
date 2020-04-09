---
title: ボリュームの追加
description: '**[ボリュームの追加]** の Windows コマンドトピック。シャドウコピーセットにボリュームを追加します。これはシャドウコピーするボリュームのセットです。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b7d4d35d-8bda-46d2-8df5-eb598cecaaba
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 806ab273dbb63eb7341520f56a07691fe3fac214
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851355"
---
# <a name="add-volume"></a>ボリュームの追加

シャドウコピーするボリュームのセットであるボリュームをシャドウコピーセットに追加します。 このコマンドは、シャドウコピーを作成するために必要です。 パラメーターを指定せずに使用する場合は、 **[ボリュームの追加]** コマンドプロンプトでヘルプを表示します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
add volume <Volume> [provider <ProviderID>]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
| `<Volume>` | シャドウコピーセットに追加するボリュームを指定します。 シャドウコピーの作成には、少なくとも1つのボリュームが必要です。|
| `[provider \<ProviderID>]` | シャドウコピーの作成に使用する登録済みプロバイダーのプロバイダー ID を指定します。 **プロバイダー**が指定されていない場合は、既定のプロバイダーが使用されます。|

## <a name="remarks"></a>コメント

-   ボリュームは一度に1つずつ追加されます。

-   ボリュームが追加されるたびに、VSS がそのボリュームのシャドウコピーの作成をサポートしているかどうかがチェックされます。 ただし、このプライマリチェックは、後で**set コンテキスト**コマンドを使用することによって無効にされる場合があります。

-   シャドウコピーが作成されると、環境変数によってエイリアスがシャドウ ID にリンクされるため、エイリアスをスクリプト作成に使用できます。

## <a name="examples"></a><a name=BKMK_examples></a>例

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

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)