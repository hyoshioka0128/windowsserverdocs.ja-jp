---
title: シフト
description: バッチファイル内のバッチパラメーターの位置を変更する shift の Windows コマンドトピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b56574e8-570a-4cc9-bbac-1b94fbf6a47a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9c242fe90a8bf32eda5a3db511910e3d7aa4610f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80834265"
---
# <a name="shift"></a>シフト

バッチ ファイル内のバッチのパラメーターの位置を変更します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
shift [/n <N>]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/n \<N >|移行を開始することを指定、 *N*番目の引数、 *N* は 8 ~ 0 の値。 既定で有効になっているコマンド拡張機能が必要です。|
|/?|コマンド プロンプトでヘルプを表示します。|

## <a name="remarks"></a>コメント

- **Shift キーを押し** コマンド バッチのパラメーターの値を変更する **%0** を通じて **%9** 前に各パラメーターをコピーして: の値 **%1** にコピー **%0**, の値 **%2** にコピー **%1**, 、という具合です。 これは、パラメーターの数にかかわらず、同じ操作を実行するバッチ ファイルを作成するため便利です。
- コマンド拡張機能が有効になっている場合、 **shift** コマンドをサポートする、 **/n** コマンド ライン オプションです。 **/N** n 番目の引数で移行を開始するオプションが指定場所 **N** は 8 ~ 0 の値。 など **SHIFT/2** 移動することに **%3** に **%2**, 、 **%4** に **%3**, のままにし、 **%0** と **%1** 影響はありません。 既定では、コマンド拡張機能が有効にします。
- 使用することができます、 **shift** 10 個を超えるバッチ パラメーターを受け取りが可能なバッチ ファイルを作成するコマンドです。 コマンドラインで複数の 10 個のパラメーターを指定する場合、表示される、10 分後に ( **%9**) には、一度に 1 つのシフトをする **%9**します。
- **Shift**コマンドを実行しても、 **%\\** * batch パラメーターには影響しません。
- いいえ旧バージョンとは **shift** コマンドです。 実装した後、 **shift キーを押し** コマンド、バッチのパラメーターを回復することはできません ( **%0**)、shift キーを押し前に存在します。

## <a name="examples"></a><a name=BKMK_examples></a>例

Mycopy.bat をというサンプル バッチ ファイルの次の行を使用する方法をデモンストレーションする **shift** バッチ パラメーターの任意の数にします。 この例では、Mycopy.bat は、特定のディレクトリにファイルの一覧をコピーします。 バッチ パラメーターは、ディレクトリとファイル名の引数によって表されます。
```
@echo off 
rem MYCOPY.BAT copies any number of files
rem to a directory.
rem The command uses the following syntax:
rem mycopy dir file1 file2 ... 
set todir=%1
:getfile
shift
if %1== goto end
copy %1 %todir%
goto getfile
:end
set todir=
echo All done
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)