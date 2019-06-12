---
title: label
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: d0c68fbbf3ea776bbf6cd49fc4fa446d5dd46542
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437911"
---
# <a name="label"></a>label



作成、変更、またはディスクのボリューム ラベル (名) を削除します。 パラメーターを指定せずに使用されている場合、**ラベル**コマンドが現在のボリューム ラベルを変更または既存のラベルを削除します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
label [/mp] [<Volume>] [<Label>]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/mp|ボリュームをマウント ポイントまたはボリューム名として扱うことを指定します。|
|\<ボリューム >|(コロンの後に)、ドライブ文字を指定します。 マウント ポイント、またはボリュームの名前。 ボリューム名が指定されている場合、 **/mp**パラメーターは必要ありません。|
|\<ラベル >|ボリュームのラベルを指定します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

- Windows が表示されます、ボリューム ラベルとシリアル番号 (ある) 場合、ディレクトリの一覧の一部として。
- NTFS のボリューム ラベルは最大 32 文字で、スペースを含むできます。 NTFS ボリューム ラベルを保持し、ラベルが作成されたときに使用されたケースを表示します。
- 値を指定しない場合、**ラベル**パラメーター、**ラベル**コマンドでは、次の形式で出力が表示されます。  
  ```
  Volume in drive C: xxxxxxxxxxx 
  Volume Serial Number is xxxx-xxxx 
  Volume label (32 characters, ENTER for none)?
  ```  
  新しいボリューム ラベルを入力したり、現在のラベルを保持するには ENTER キーを押します。 ENTER キーを押すし、現在、ボリュームには、ラベルが付いている場合、**ラベル**コマンドは、次のメッセージを要求します。  
  ```
  Delete current volume label (Y/N)?
  ```  
  ラベルを削除するには、キーを押して Y または N キーを押して、ラベルを保持します。

## <a name="BKMK_examples"></a>例

7 月の売上情報を含むドライブ A でのディスクをラベルには、次のように入力します。
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
3. 現在のラベルを削除するには Y キーを押します。

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)