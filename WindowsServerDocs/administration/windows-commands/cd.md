---
title: cd
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 932d9cc1-3dff-40da-835c-1cb0894874f1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 53340612d26eaa7c4ae6fd977a0eac573f91881d
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66434603"
---
# <a name="cd"></a>cd



名前を表示します。 または、現在のディレクトリを変更します。 ドライブ文字のみで使用されている場合 (たとえば、 `cd C:`)、 **cd**指定したドライブの現在のディレクトリの名前を表示します。 パラメーターを指定せずに使用されている場合**cd**現在のドライブとディレクトリが表示されます。

> [!NOTE]
> このコマンドと同じ、 **chdir**コマンド。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
cd [/d] [<Drive>:][<Path>]
cd [..]
chdir [/d] [<Drive>:][<Path>]
chdir [..]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/d|現在のドライブと、ドライブの現在のディレクトリを変更します。|
|\<ドライブ >:|表示または変更 (現在のドライブとは異なる) 場合、ドライブを指定します。|
|\<パス >|表示または変更するディレクトリへのパスを指定します。|
|[..]|親フォルダーに変更することを指定します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

次の条件が適用コマンド拡張機能が有効な場合、 **cd**コマンド。
- 現在のディレクトリの文字列は、ディスク上での名前として同じ大文字と小文字を使用する変換されます。 たとえば、`cd C:\TEMP`はディスクの場合、C:\Temp に現在のディレクトリを設定します。
- スペースはそのため、区切り記号として扱われません*パス*引用符に囲まれていない空白を含めることができます。 例:  
  ```
  cd username\programs\start menu
  ```  
  同じです。  
  ```
  cd "username\programs\start menu"
  ```  
  引用符が必要ですただし、拡張機能が無効になっています。

コマンド拡張機能を無効にするには、次のように入力します。
```
cmd /e:off
```

## <a name="BKMK_examples"></a>例

ルート ディレクトリとは、ドライブのディレクトリ階層の最上位です。 ルート ディレクトリに戻り、次のように入力します。
```
cd\
```
使用しているものとは異なるドライブに既定のディレクトリを変更するには、次のように入力します。
```
cd [<Drive>:\[<Directory>]]
```
ディレクトリに変更を確認するには、次のように入力します。
```
cd [<Drive>:]
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)