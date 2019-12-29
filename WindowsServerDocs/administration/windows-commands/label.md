---
title: label
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bbae8bdd-97d4-4566-9118-7c95aa07645f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e66a2d9a7d28462b287084e3f8b129ffc03800bd
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374792"
---
# <a name="label"></a>label



ディスクのボリュームラベル (名前) を作成、変更、または削除します。 パラメーターを指定せずに使用した場合、 **label**コマンドは、現在のボリュームラベルを変更するか、既存のラベルを削除します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
label [/mp] [<Volume>] [<Label>]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/mp|ボリュームをマウントポイントまたはボリューム名として扱うことを指定します。|
|\<ボリューム >|ドライブ文字 (後ろにコロンを付ける)、マウントポイント、またはボリューム名を指定します。 ボリューム名が指定されている場合、 **/mp**パラメーターは必要ありません。|
|\<ラベル >|ボリュームのラベルを指定します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

- Windows では、ディレクトリの一覧の一部としてボリュームラベルとシリアル番号 (ある場合) が表示されます。
- NTFS ボリュームラベルには、スペースを含め、最大32文字の長さを指定できます。 NTFS ボリュームラベルは、ラベルが作成されたときに使用されたケースを保持し、表示します。
- **Label**パラメーターの値を指定しない場合、 **label**コマンドは次の形式で出力を表示します。  
  ```
  Volume in drive C: xxxxxxxxxxx 
  Volume Serial Number is xxxx-xxxx 
  Volume label (32 characters, ENTER for none)?
  ```  
  新しいボリュームラベルを入力するか、enter キーを押して現在のラベルを維持することができます。 ENTER キーを押すと、現在ボリュームにラベルがある場合、 **label**コマンドによって次のメッセージが表示されます。  
  ```
  Delete current volume label (Y/N)?
  ```  
  Y キーを押してラベルを削除するか、N キーを押してラベルを保持します。

## <a name="BKMK_examples"></a>例

7月の売上情報が含まれているドライブ A のディスクにラベルを付けるには、次のように入力します。
```
label a:sales-july
```
C ドライブの現在のラベルを削除するには、次の手順を実行します。
1. コマンド プロンプトで、次のように入力します。  
   ```
   Label
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
3. Y キーを押して現在のラベルを削除します。

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)