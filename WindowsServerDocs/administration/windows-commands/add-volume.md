---
title: add volume
description: '[ボリュームの追加] コマンドの参照記事。シャドウコピーセットにボリュームを追加します。これはシャドウコピーするボリュームのセットです。'
ms.topic: article
ms.assetid: b7d4d35d-8bda-46d2-8df5-eb598cecaaba
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 374fec353397916fa76952401571dee92073dd59
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87895594"
---
# <a name="add-volume"></a>add volume

シャドウコピーするボリュームのセットであるボリュームをシャドウコピーセットに追加します。 シャドウコピーが作成されると、環境変数によってエイリアスがシャドウ ID にリンクされるため、エイリアスをスクリプト作成に使用できます。

ボリュームは一度に1つずつ追加されます。 ボリュームを追加するたびに、そのボリュームのシャドウコピーの作成を VSS がサポートしているかどうかがチェックされます。 このチェックは、後で**set コンテキスト**コマンドを使用することによって無効にすることができます。

このコマンドは、シャドウコピーを作成するために必要です。 パラメーターを指定せずに使用する場合は、[**ボリュームの追加**] コマンドプロンプトでヘルプを表示します。

## <a name="syntax"></a>構文

```
add volume <volume> [provider <providerid>]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<volume>` | シャドウコピーセットに追加するボリュームを指定します。 シャドウコピーの作成には、少なくとも1つのボリュームが必要です。 |
| `[provider \<providerid>]` | シャドウコピーの作成に使用する登録済みプロバイダーのプロバイダー ID を指定します。 **プロバイダー**が指定されていない場合は、既定のプロバイダーが使用されます。 |

## <a name="examples"></a>例

登録されているプロバイダーの現在の一覧を表示するには、 `diskshadow>` プロンプトで次のように入力します。

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

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [コンテキストコマンドの設定](set-context.md)
