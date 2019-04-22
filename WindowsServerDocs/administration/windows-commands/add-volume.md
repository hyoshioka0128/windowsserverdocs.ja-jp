---
title: ボリュームを追加します。
description: Windows コマンド」のトピック**ボリュームの追加**-シャドウ コピー セットは一連のボリューム シャドウ コピーにボリュームを追加します。
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 8960ffafdf49d4512e1df2dfcc046bdfbe56e224
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819473"
---
# <a name="add-volume"></a>ボリュームを追加します。



シャドウ コピーを設定するにはシャドウ コピー ボリュームのセットであるボリュームを追加します。 このコマンドは、シャドウ コピーを作成する必要があります。 パラメーターを指定せずに使用されている場合**ボリュームの追加**コマンド プロンプトでヘルプを表示します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
add volume <Volume> [provider <ProviderID>]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<ボリューム >|シャドウ コピー セットに追加するボリュームを指定します。 少なくとも 1 つのボリュームは、シャドウ コピーの作成に必要です。|
|[プロバイダー \<ProviderID >]|シャドウ コピーの作成に使用する登録済みプロバイダーのプロバイダー ID を指定します。 場合**プロバイダー**が指定されていない、既定のプロバイダーを使用します。|

## <a name="remarks"></a>注釈

-   ボリュームは一度に 1 つずつに追加されます。
-   ボリュームが追加されるたびに、そのボリュームのシャドウ コピーの作成をサポートする VSS チェックされます。 このプライマリの確認がによって無効にする、ただしの後で使用、**セット コンテキスト**コマンド。
-   シャドウ コピーが作成されると、環境変数はスクリプトを実行して、エイリアスを使用しできるようにシャドウ ID に、エイリアスをリンクします。

## <a name="BKMK_examples"></a>例

登録済みのプロバイダーの現在の一覧を表示する、`DISKSHADOW>`プロンプトで入力します。
```
list providers
```
次の出力には、既定で使用される 1 つのプロバイダーが表示されます。
```
* ProviderID: {b5946137-7b9f-4925-af80-51abd60b20d5}
        Type: [1] VSS_PROV_SYSTEM
        Name: Microsoft Software Shadow Copy provider 1.0
        Version: 1.0.0.7
        CLSID: {65ee1dba-8ff4-4a58-ac1c-3470ee2f376a}
1 provider registered.
```
シャドウ コピー セットにドライブ C を追加し、という名前のエイリアスの System1 を割り当てると、次のように入力します。
```
add volume c: alias System1
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)