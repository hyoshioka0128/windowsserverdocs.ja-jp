---
title: Convert RiprepImage コマンドを使用してください。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 88c2b96f-5947-4b64-9dcf-1946b3c013cf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9b41b6dcc52c3e6700d1d18c61eceea8b990ecdf
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66440580"
---
# <a name="using-the-convert-riprepimage-command"></a>Convert RiprepImage コマンドを使用してください。



既存のリモート インストールの準備 (RIPrep) イメージを Windows イメージ (.wim) 形式に変換します。

## <a name="syntax"></a>構文

```
WDSUTIL [Options] /Convert-RIPrepImage /FilePath:<File path and name>
     /DestinationImage
         /FilePath:<File path and name>
         [/Name:<Name>]
         [/Description:<Description>]
         [/InPlace]
         [/Overwrite:{Yes | No | Append}]
```

## <a name="parameters"></a>パラメーター

|            パラメーター            |                                                                                                                                                                                                                                                                                                               説明                                                                                                                                                                                                                                                                                                                |
|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /FilePath:\<ファイルのパスと名前 > |                                                                                                                                                                                                       RIPrep イメージに対応する .sif ファイルの完全パスとファイル名を指定します。 このファイルは、Riprep.sif と通常呼ばれるは、RIPrep イメージを含むフォルダーの \Templates サブフォルダーにあります。                                                                                                                                                                                                       |
|        /DestinationImage        | 次のオプションを使用してコピー先の画像の設定を指定します。</br>-/FilePath:\<ファイルのパスと名前 >-新しいファイルのファイルの完全パスを設定します。 例:**C:\Temp\convert.wim**</br>-[/Name:\<名 >]-イメージの表示名を設定します。 表示名が指定されていない場合は、ソース イメージの表示名が使用されます。</br>-[/説明。\<説明 >]-イメージの説明を設定します。</br>-[/InPlace] には、変換を実行して、既定の動作は、元のイメージのコピーではなくを元の RIPrep イメージを指定します。</br>-[/Overwrite: {[はい] |

## <a name="BKMK_examples"></a>例

指定した RIPrep.sif イメージを RIPREP.wim に変換するには、次のように入力します。
```
WDSUTIL /Convert-RiPrepImage /FilePath:"R:\RemoteInstall\Setup\English
\Images\Win2k3.SP1\i386\Templates\riprep.sif" /DestinationImage
/FilePath:"C:\Temp\RIPREP.wim"
```
RIPREP.wim を指定した名前と説明した、指定された RIPrep.sif イメージに変換をファイルが既に存在する場合、新しいファイルで上書きは、次のように入力します。
```
WDSUTIL /Verbose /Progress /Convert-RiPrepImage /FilePath:"\\Server
\RemInst\Setup\English\Images\WinXP.SP2\i386\Templates\riprep.sif"
/DestinationImage /FilePath:"\\Server\Share\RIPREP.wim"
/Name:"WindowsXP image" /Description:"Converted RIPREP image of WindowsXP"
/Overwrite:Append
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)