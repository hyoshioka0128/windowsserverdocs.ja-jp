---
title: msinfo32
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a38f31d7-1766-4103-becc-9d0b87c2826d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f8ad4cf5480492042cdd1e372abae652aff71b90
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437193"
---
# <a name="msinfo32"></a>msinfo32

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ローカル コンピューターのハードウェア、システム コンポーネント、およびソフトウェア環境の包括的なビューを表示するシステム情報ツールを開きます。 
## <a name="syntax"></a>構文
```
msinfo32 [/pch] [/nfo <path>] [/report <path>] [/computer <computerName>] [/showcategories] [/category <CategoryID>] [/categories {+<CategoryID>(+<CategoryID>)|+all(-<CategoryID>)}]
```
### <a name="parameters"></a>パラメーター

|    パラメーター    |                                                                                                                                 説明                                                                                                                                  |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     <path>      | ファイル形式で開くことを指定して*C:\Folder1\File1.XXX*ここで、 *C*は、ドライブ文字を*Folder1*フォルダー *File1*ファイルの名前と*XXX*はファイル名の拡張子です。<br /><br />このファイルを指定できます、 **.nfo**、 **.xml**、 **.txt**、または **.cab**ファイル。 |
| <computerName>  |                                                                             ローカル コンピューターまたは複数のターゲットの名前を指定します。 UNC 名、IP アドレス、またはフル コンピューター名を指定できます。                                                                              |
|  <CategoryID>   |                                                                                     カテゴリの項目の ID を指定します。 カテゴリ ID を取得するを使用して **/showcategories**します。                                                                                      |
|      /pch       |                                                                                                       システム情報ツールで、システムの履歴ビューを表示します。                                                                                                       |
|      /nfo       |                                     エクスポート ファイルを保存、 **.nfo**ファイル。 場合は、ファイル名がで指定された*パス*で終わらない、 **.nfo**拡張機能、 **.nfo**拡張機能が自動的にファイル名に付加されます。                                      |
|     /report     |                                               ファイルを保存します*パス*テキスト ファイルとして。 表示されているとおり、ファイル名が保存された*パス*します。 パスに指定されている場合を除き、.txt 拡張子がファイルに追加されません。                                                |
|    /computer    |                                                                指定したリモート コンピューターのシステム情報ツールを起動します。 リモート コンピューターにアクセスする適切なアクセス許可が必要です。                                                                |
| /showcategories |                         わかりやすいまたはローカライズされた名前を表示するのではなく、Id が表示されたら、使用可能なすべてのカテゴリとシステム情報ツールを起動します。 として環境のソフトウェア カテゴリを表示するなど、 **SWEnv**カテゴリ。                         |
|    /category    |                                                                     選択されている指定したカテゴリには、システム情報を開始します。 使用 **/showcategories**利用可能なカテゴリ Id の一覧を表示します。                                                                     |
|   /categories   |                          システム情報を指定したカテゴリまたはカテゴリの表示のみに始まります。 選択したカテゴリまたはカテゴリへの出力も制限されます。 使用 **/showcategories**利用可能なカテゴリ Id の一覧を表示します。                          |
|       /?        |                                                                                                                     コマンド プロンプトにヘルプを表示します。                                                                                                                     |

## <a name="remarks"></a>注釈
一部のシステム情報カテゴリには、大量データにはが含まれます。 使用することができます、 **start/wait**これらのカテゴリのレポートの作成のパフォーマンスを最適化するためにコマンド。 詳細については、次を参照してください。[システム情報](https://technet.microsoft.com/library/cc783305(v=ws.10).aspx)します。
## <a name="BKMK_Examples"></a>例
利用可能なカテゴリ Id を一覧表示するには、次のように入力します。
```
msinfo32 /showcategories
```
起動してシステム情報ツールを利用可能なすべての情報表示、読み込まれたモジュール、型を除く。
```
msinfo32 /categories +all -loadedmodules
```
システムの概要情報のみをシステムの概要 で情報を含む syssum.nfo と呼ばれる .nfo ファイルを作成するには、次のように入力します。
```
msinfo32 /nfo syssum.nfo /categories +systemsummary
```
リソースの競合情報をリソースの競合に関する情報を含む conflicts.nfo と呼ばれる .nfo ファイルを作成するには、次のように入力します。
```
msinfo32 /nfo conflicts.nfo /categories    +componentsproblemdevices+resourcesconflicts+resourcesforcedhardware
```
## <a name="additional-references"></a>その他の参照
-   [コマンド ライン構文の記号](command-line-syntax-key.md)

