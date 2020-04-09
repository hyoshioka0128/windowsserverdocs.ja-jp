---
title: 属性ディスク
description: ディスクの属性の表示、設定、またはクリアを行う Windows コマンド**に関するトピックを参照**してください。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: eed57071-c1c6-4394-9542-62b52a878c92
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f3c29a009a1efdfb7fed3d04d194cc8cfd2ea4eb
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851245"
---
# <a name="attributes-disk"></a>属性ディスク

ディスクの属性を表示、設定、またはクリアします。

## <a name="syntax"></a>構文

```
attributes disk [{set | clear}] [readonly] [noerr]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| set | フォーカスがあるディスクの指定された属性を設定します。 |
| クリア | フォーカスがあるディスクの指定された属性をクリアします。 |
| readonly | ディスクが読み取り専用であることを指定します。 |
| noerr | スクリプト専用です。 エラーが発生しても、エラーが発生しなかったかのように DiskPart はコマンドの処理を続けます。 このパラメーターは、エラー発生すると、DiskPart はエラー コードを生成して終了します。 |

## <a name="remarks"></a>コメント

-   **Attributes disk**を使用してディスクの現在の属性を表示すると、スタートアップディスク属性は、コンピューターを起動するために使用されるディスクを表します。 ダイナミックミラーの場合は、ブートボリュームのブートプレックスが格納されているディスクに対して表示されます。

-   **[ディスクの属性]** コマンドを正常に実行するには、ディスクを選択する必要があります。 使用して、 **select ディスク** コマンド ディスクを選択し、それにフォーカスをします。

## <a name="examples"></a><a name=BKMK_examples></a>例

選択したディスクの属性を表示するには、次のように入力します。

```
attributes disk
```

選択したディスクを読み取り専用に設定するには、次のように入力します。

```
attributes disk set readonly
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)