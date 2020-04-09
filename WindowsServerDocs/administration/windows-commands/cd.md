---
title: cd
description: Windows コマンドに関するトピック (cd の場合)。現在のディレクトリの名前を表示したり、変更したりします。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 932d9cc1-3dff-40da-835c-1cb0894874f1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2d62f529ab6c45957f0fdea24358a2f13151adb6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80848225"
---
# <a name="cd"></a>cd

現在のディレクトリの名前を表示または変更します。 ドライブ文字 (`cd C:`など) でのみ使用する場合、 **cd**には、指定されたドライブの現在のディレクトリの名前が表示されます。 パラメーターを指定せずに使用した場合、 **cd**には現在のドライブとディレクトリが表示されます。

> [!NOTE]
> このコマンドは、 **chdir**コマンドと同じです。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
cd [/d] [<Drive>:][<Path>]
cd [..]
chdir [/d] [<Drive>:][<Path>]
chdir [..]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/d|現在のドライブおよびドライブの現在のディレクトリを変更します。|
|\<ドライブ >:|表示または変更するドライブを指定します (現在のドライブと異なる場合)。|
|\<パス >|表示または変更するディレクトリへのパスを指定します。|
|[..]|親フォルダーに変更することを指定します。|
|/?|コマンド プロンプトでヘルプを表示します。|

## <a name="remarks"></a>コメント

コマンド拡張機能が有効になっている場合、 **cd**コマンドには次の条件が適用されます。
- 現在のディレクトリ文字列は、ディスク上の名前と同じケースを使用するように変換されます。 たとえば、ディスク上の場合は、現在のディレクトリを C:\Temp に設定 `cd C:\TEMP` ます。
- スペースは区切り記号として扱われないため、引用符を囲まずに*パス*にスペースを含めることができます。 例 :  
  ```
  cd username\programs\start menu
  ```  
  は次のようになります。  
  ```
  cd username\programs\start menu
  ```  
  ただし、拡張機能が無効になっている場合は、引用符が必要です。

コマンド拡張機能を無効にするには、次のように入力します。
```
cmd /e:off
```

## <a name="examples"></a><a name=BKMK_examples></a>例

ルートディレクトリは、ドライブのディレクトリ階層の最上位にあります。 ルートディレクトリに戻るには、次のように入力します。
```
cd\
```
使用しているドライブとは異なるドライブ上の既定のディレクトリを変更するには、次のように入力します。
```
cd [<Drive>:\[<Directory>]]
```
ディレクトリへの変更を確認するには、次のように入力します。
```
cd [<Drive>:]
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)