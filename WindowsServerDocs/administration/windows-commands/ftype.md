---
title: ftype
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6fb53cee-9bed-44dd-af5d-bc7cec1dd114
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c29ca0aa027d11fa8f981134e5367021227d3096
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881683"
---
# <a name="ftype"></a>ftype



表示またはファイル名拡張子の関連付けで使用されているファイルの種類を変更します。 代入演算子を使用せずに使用する場合 (**=**)、 **ftype** 指定したファイルの種類に対して現在開いているコマンド文字列を表示します。 パラメーターを指定せずに使用する場合 **ftype** 開いているコマンド文字列が定義されているファイルの種類が表示されます。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
ftype [<FileType>[=[<OpenCommandString>]]]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<FileType>|表示または変更するファイルの種類を指定します。|
|\<OpenCommandString >|指定したファイルの種類のファイルを開くときに使用する開いているコマンド文字列を指定します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

次の表方法 **ftype** [開く] コマンド文字列内の変数に置換します。

|変数|置換値|
|--------|-----------------|
|%0 または %1|アソシエーションを起動して、ファイル名と置き換えを取得します。|
|%*|すべてのパラメーターを取得します。|
|%2, %3, ...|最初のパラメーター (%2)、2 番目のパラメーター (%3) およびなどを取得します。|
|%~\<N>|以降で、残りのパラメーターのすべてを取得、 *N*番目のパラメーター位置 *N* 2 ~ 9 の任意の数値を指定できます。|

## <a name="BKMK_examples"></a>例

開いているコマンド文字列が定義されている現在のファイルの種類を表示するには、次のように入力します。
```
ftype
```
現在開いているコマンド文字列を表示する、 *txtfile* ファイルの種類、種類。
```
ftype txtfile
```
このコマンドには、次のような出力が生成されます。
```
txtfile=%SystemRoot%\system32\NOTEPAD.EXE %1
```
呼ばれるファイルの種類の開いているコマンド文字列を削除する *例*, 、種類。
```
ftype example=
```
.Pl ファイル名拡張子を PerlScript ファイルの種類に関連付け、PERL を実行する PerlScript ファイルの種類を有効にします。実行可能ファイルで、次のコマンドを入力します。
```
assoc .pl=PerlScript 
ftype PerlScript=perl.exe %1 %*
```
Perl スクリプトを呼び出すときに、.pl のファイル名拡張子を入力する必要をなくすためには、次のように入力します。
```
set PATHEXT=.pl;%PATHEXT%
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)