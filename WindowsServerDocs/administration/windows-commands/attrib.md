---
title: attrib
description: Windows コマンド」のトピック**attrib** -ファイルまたはディレクトリに割り当てられている表示、設定、または属性を削除します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5e763ca5-21a2-45d2-b26d-a9c44c99091a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0f640af2c7957e43dd3f31dfa732bfc887112651
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841093"
---
# <a name="attrib"></a>attrib



表示、設定、またはファイルまたはディレクトリに割り当てられている属性を削除します。 パラメーターを指定せずに使用されている場合**attrib**現在のディレクトリ内のすべてのファイルの属性を表示します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
attrib [{+|-}r] [{+|-}a] [{+|-}s] [{+|-}h] [{+|-}i] [<Drive>:][<Path>][<FileName>] [/s [/d] [/l]]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|{+\|-}r|セット (**+**) またはオフにします (**-**) 読み取り専用ファイル属性。|
|{+\|-}a|セット (**+**) またはオフにします (**-**) アーカイブ ファイル属性。|
|{+\|-}s|セット (**+**) またはオフにします (**-**)、システム ファイル属性。|
|{+\|-}h|セット (**+**) またはオフにします (**-**) 隠しファイル属性。|
|{+\|-}i|セット (**+**) またはオフにします (**-**) ファイルのコンテンツのインデックス作成されなかった属性。|
|[\<ドライブ >:] [<Path>] [<FileName>]|ディレクトリ、ファイル、または表示属性を変更したりファイルのグループの名前と場所を指定します。 使用することができます、**でしょうか。** **&#42;** ワイルドカード文字、 *FileName*パラメーターを表示またはファイルのグループの属性を変更します。|
|/s|適用対象**attrib**と現在のディレクトリに一致するファイルに、コマンド ライン オプションとそのすべてのサブディレクトリ。|
|/d|適用対象**attrib**とディレクトリに、コマンド ライン オプション。|
|/l|適用対象**attrib**とシンボリック リンクのターゲットではなく、シンボリック リンクに、コマンド ライン オプション。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

-   ワイルドカード文字を使用することができます (**でしょうか。** **&#42;**) で、 *FileName*パラメーターを表示またはファイルのグループの属性を変更します。
-   ファイルに、システムがある場合 (**s**) または 非表示 (**h**) 属性を設定、そのファイルの他の属性を変更する前に属性をクリアする必要があります。
-   [アーカイブ] 属性 (**、**) 前回バックアップされた後に変更されたファイルをマークします。 なお、 **xcopy**コマンドを使用してアーカイブ属性。

## <a name="BKMK_examples"></a>例

現在のディレクトリにある News86 という名前のファイルの属性を表示するには、次のように入力します。
```
attrib news86 
```
読み取り専用属性を Report.txt という名前のファイルに割り当てるに次のように入力します。
```
attrib +r report.txt 
```
ドライブ B 内のディスク上のパブリック ディレクトリとそのサブディレクトリ内のファイルから読み取り専用属性を削除するに次のように入力します。
```
attrib -r b:\public\*.* /s 
```
A、ドライブのすべてのファイルにアーカイブ属性を設定し、拡張子が .bak のファイルにアーカイブ属性をオフにし、次のように入力します。
```
attrib +a a:*.* & attrib -a a:*.bak 
```
