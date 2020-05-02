---
title: ボリュームの追加
description: '[ボリュームの追加] コマンドのリファレンストピック。シャドウコピーセットにボリュームを追加します。これはシャドウコピーするボリュームのセットです。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b7d4d35d-8bda-46d2-8df5-eb598cecaaba
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a8cfd3d8f7d9f008e3136d8f694dc00370b8b0f2
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719207"
---
# <a name="add-volume"></a>ボリュームの追加

シャドウコピーするボリュームのセットであるボリュームをシャドウコピーセットに追加します。 シャドウコピーが作成されると、環境変数によってエイリアスがシャドウ ID にリンクされるため、エイリアスをスクリプト作成に使用できます。

ボリュームは一度に1つずつ追加されます。 ボリュームを追加するたびに、そのボリュームのシャドウコピーの作成を VSS がサポートしているかどうかがチェックされます。 このチェックは、後で**set コンテキスト**コマンドを使用することによって無効にすることができます。

このコマンドは、シャドウコピーを作成するために必要です。 パラメーターを指定せずに使用する場合は、[**ボリュームの追加**] コマンドプロンプトでヘルプを表示します。

## <a name="syntax"></a>構文

```
add volume <volume> [provider <providerid>]
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| --------- | ----------- |
| `<volume>` | シャドウコピーセットに追加するボリュームを指定します。 シャドウコピーの作成には、少なくとも1つのボリュームが必要です。 |
| `[provider \<providerid>]` | シャドウコピーの作成に使用する登録済みプロバイダーのプロバイダー ID を指定します。 **プロバイダー**が指定されていない場合は、既定のプロバイダーが使用されます。 |

## <a name="examples"></a>例

登録されているプロバイダーの現在の一覧を`diskshadow>`表示するには、プロンプトで次のように入力します。

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

ドライブ C: をシャドウコピーセットに追加し、 *System1*という名前のエイリアスを割り当てるには、次のように入力します。

```
add volume c: alias System1
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [コンテキストコマンドの設定](set-context.md)
