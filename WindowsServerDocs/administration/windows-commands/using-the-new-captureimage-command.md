---
title: 新しいキャプチャ イメージのコマンドを使用してください。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 7d9f402acb9904624bdb4193a4306d57b104eda8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888613"
---
# <a name="using-the-new-captureimage-command"></a>新しいキャプチャ イメージのコマンドを使用してください。



既存のブート イメージから新しいキャプチャ イメージを作成します。 キャプチャ イメージとは、Windows 展開サービスを起動するブート イメージは、セットアップを開始する代わりにユーティリティをキャプチャします。 (Sysprep で準備された) を参照コンピューターをキャプチャ イメージを起動すると、ウィザードは、参照コンピュータのインストール イメージを作成し、Windows イメージ (.wim) ファイルとして保存します。 イメージをメディア (CD、DVD、または USB ドライブなど) を追加することもでき、そのメディアからコンピューターを起動することができます。 インストール イメージを作成した後は、PXE ブート展開サーバーにイメージを追加できます。 詳細については、イメージの作成を参照してください ([https://go.microsoft.com/fwlink/?LinkId=115311](https://go.microsoft.com/fwlink/?LinkId=115311))。

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

|パラメーター|説明|
|---------|-----------|
|[/Server:\<サーバー名 >]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
|/Image:\<イメージ名 >|ソース ブート イメージの名前を指定します。|
|/Architecture: {x86 | ia64 | x64}|使用するイメージのアーキテクチャを指定します。 別のブート イメージで同じイメージの名前を持つさまざまなアーキテクチャで、これにより、適切なイメージを指定することが使用されます。|
|[/ファイル名。\<ファイル名 >]|イメージは、名前によって一意に識別できない場合、は、ファイル名を指定するこのオプションを使用する必要があります。|
|/DestinationImage|コピー先の画像の設定を指定します。 次のオプションを使用して設定を指定します。</br>-   /FilePath:\<ファイルのパスと名前 > 新しいキャプチャ イメージのファイルの完全パスを設定します。</br>-[/Name:\<名 >]-イメージの表示名を設定します。 表示名が指定されていない場合は、ソース イメージの表示名が使用されます。</br>-[/説明。\<説明 >]-イメージの説明を設定します。</br>-   [/Overwrite: {Yes | X | 追加}] - で、ファイルが指定されているかどうか判断 **/DestinationImage** /FilePath でその名前を持つ別のファイルが既に存在する場合に上書きする必要があります。 **[はい]** 既存のファイルを上書きします。 **いいえ** (既定値) と同じ名前の別のファイルが既に存在する場合に発生するエラーが発生します。 **追加** 既存の .wim ファイル内に新しいイメージとして生成されたイメージをアタッチします。</br>-   [/UnattendFilePath:\<ファイルのパス >]-無人のイメージのキャプチャ ファイルの名前と完全なパスを設定します。|

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

[コマンドライン構文キー](command-line-syntax-key.md)