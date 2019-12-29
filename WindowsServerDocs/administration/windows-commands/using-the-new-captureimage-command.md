---
title: 新しいキャプチャ イメージのコマンドを使用してください。
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2dfd08f0-be59-4715-96e6-c498305873f4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fb48cb76ef99eac51b862a5e1a3d1999a1cfc89d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363049"
---
# <a name="using-the-new-captureimage-command"></a>新しいキャプチャ イメージのコマンドを使用してください。



既存のブート イメージから新しいキャプチャ イメージを作成します。 キャプチャ イメージとは、Windows 展開サービスを起動するブート イメージは、セットアップを開始する代わりにユーティリティをキャプチャします。 (Sysprep で準備された) を参照コンピューターをキャプチャ イメージを起動すると、ウィザードは、参照コンピュータのインストール イメージを作成し、Windows イメージ (.wim) ファイルとして保存します。 イメージをメディア (CD、DVD、または USB ドライブなど) を追加することもでき、そのメディアからコンピューターを起動することができます。 インストール イメージを作成した後は、PXE ブート展開サーバーにイメージを追加できます。 詳細については、「イメージの作成 ([https://go.microsoft.com/fwlink/?LinkId=115311](https://go.microsoft.com/fwlink/?LinkId=115311))」を参照してください。

## <a name="syntax"></a>構文

```
WDSUTIL [Options] /New-CaptureImage [/Server:<Server name>]
     /Image:<Image name>
     /Architecture:{x86 | ia64 | x64}
     [/Filename:<File name>]
     /DestinationImage
        /FilePath:<File path and name>
        [/Name:<Name>]
        [/Description:<Description>]
        [/Overwrite:{Yes | No | Append}]
        [/UnattendFilePath:<File path>]
```

## <a name="parameters"></a>パラメーター

|        パラメーター         |                                                                                                                                                                                                                         説明                                                                                                                                                                                                                          |
|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [/Server: \<Server name >] |                                                                                                                                       サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。                                                                                                                                        |
|   /Image: \<Image 名 >   |                                                                                                                                                                                                         ソース ブート イメージの名前を指定します。                                                                                                                                                                                                         |
|   /アーキテクチャ: {x86    |                                                                                                                                                                                                                             ia64                                                                                                                                                                                                                             |
| /ファイル名\<Filename >] |                                                                                                                                                                            イメージは、名前によって一意に識別できない場合、は、ファイル名を指定するこのオプションを使用する必要があります。                                                                                                                                                                            |
|    /DestinationImage     | コピー先の画像の設定を指定します。 次のオプションを使用して設定を指定します。</br>/FilePath\<File パスと name > 新しいキャプチャイメージの完全なファイルパスを設定します。</br>-[/Name:\<Name >]-イメージの表示名を設定します。 表示名が指定されていない場合は、ソース イメージの表示名が使用されます。</br>-[/Description:\<Description >]-イメージの説明を設定します。</br>-[/Overwrite: {はい |

## <a name="BKMK_examples"></a>例

キャプチャ イメージを作成し、WinPECapture.wim という名前を入力します。
```
WDSUTIL /New-CaptureImage /Image:"WinPE boot image" /Architecture:x86 /DestinationImage /FilePath:"C:\Temp\WinPECapture.wim"
```
キャプチャ イメージを作成し、指定した設定を適用するには、次のように入力します。
```
WDSUTIL /Verbose /Progress /New-CaptureImage /Server:MyWDSServer /Image:"WinPE boot image" /Architecture:x64 /Filename:boot.wim 
/DestinationImage /FilePath:"\\Server\Share\WinPECapture.wim" /Name:"New WinPE image" /Description:"WinPE image with capture utility" /Overwrite:No /UnattendFilePath:"\\Server\Share\WDSCapture.inf"
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)