---
title: label
description: ディスクのボリュームラベル (つまり名前) を作成、変更、または削除する、ラベルコマンドの参照記事です。
ms.topic: article
ms.assetid: bbae8bdd-97d4-4566-9118-7c95aa07645f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e7656078b87a74db789ed85c10be9f30cabfd971
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87887636"
---
# <a name="label"></a>label

ディスクのボリュームラベル (名前) を作成、変更、または削除します。 パラメーターを指定せずに使用した場合、 **label**コマンドは、現在のボリュームラベルを変更するか、既存のラベルを削除します。

## <a name="syntax"></a>構文

```
label [/mp] [<volume>] [<label>]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| /mp | ボリュームをマウントポイントまたはボリューム名として扱うことを指定します。 |
| `<volume>` | ドライブ文字 (後ろにコロンを付ける)、マウントポイント、またはボリューム名を指定します。 ボリューム名が指定されている場合、 **/mp**パラメーターは必要ありません。 |
| `<label>` | ボリュームのラベルを指定します。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

## <a name="remarks"></a>Remarks

- Windows では、ディレクトリの一覧の一部としてボリュームラベルとシリアル番号 (ある場合) が表示されます。

- NTFS ボリュームラベルには、スペースを含め、最大32文字の長さを指定できます。 NTFS ボリュームラベルは、ラベルが作成されたときに使用されたケースを保持し、表示します。

## <a name="examples"></a>例

7月の売上情報が含まれているドライブ A のディスクにラベルを付けるには、次のように入力します。

```
label a:sales-july
```

ドライブ C の現在のラベルを表示および削除するには、次の手順を実行します。

1. コマンド プロンプトに、次のコマンドを入力します。

   ```
   label
   ```

   次のような出力が表示されます。

   ```
   Volume in drive C: is Main Disk
   Volume Serial Number is 6789-ABCD
   Volume label (32 characters, ENTER for none)?
   ```

2. Enter キーを押します。 次のプロンプトが表示されます。

   ```
   Delete current volume label (Y/N)?
   ```

3. 現在のラベルを削除する場合は**Y**を、既存のラベルを保持する場合は**N**を押します。

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)