---
title: 新しい検出イメージのコマンドを使用してください。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ede9fbbb-0bba-4309-8c21-3cc13e1dc3cd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1212571fc07b912ab9fa3344b973ce5a25085d86
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835773"
---
# <a name="using-the-new-discoverimage-command"></a>新しい検出イメージのコマンドを使用してください。



既存のブート イメージから新しい検出イメージを作成します。 イメージは Windows 展開サービス モードで起動し、Windows 展開サービス サーバーを検出するには、Setup.exe プログラムを強制するブート イメージを検出します。 通常これらのイメージは、pxe ブートに対応していないコンピューターにイメージの展開に使用されます。 詳細については、イメージの作成を参照してください ([https://go.microsoft.com/fwlink/?LinkId=115311](https://go.microsoft.com/fwlink/?LinkId=115311))。

## <a name="syntax"></a>構文

```
WDSUTIL [Options] /New-DiscoverImage [/Server:<Server name>]
     /Image:<Image name>
     /Architecture:{x86 | ia64 | x64}
     [/Filename:<File name>]
     /DestinationImage
         /FilePath:<File path and name>
         [/Name:<Name>]
         [/Description:<Description>]
         [/WDSServer:<Server name>]
         [/Overwrite:{Yes | No | Append}]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|[/Server:\<サーバー名 >]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
|/Image:\<イメージ名 >|ソース ブート イメージの名前を指定します。|
|/アーキテクチャ: {x86 | ia64 | x64}|返されるイメージのアーキテクチャを指定します。 さまざまなアーキテクチャのさまざまなブート イメージで同じイメージの名前を持つことなのでアーキテクチャの値を指定するにより、WDSUTIL が適切なイメージを返します。|
|[/ファイル名:\<ファイル名 >]|イメージは、名前によって一意に識別できない場合、は、ファイル名を指定するこのオプションを使用する必要があります。|
|/DestinationImage|コピー先の画像の設定を指定します。 次のオプションを使用して設定を指定できます。</br>-/FilePath: < ファイル パスと名前 > に新しいイメージのファイルの完全パスを設定します。</br>-[/Name:\<名 >]-イメージの表示名を設定します。 表示名が指定されていない場合は、ソース イメージの表示名が使用されます。</br>-[/説明。\<説明 >]-イメージの説明を設定します。</br>-[/WDSServer:\<サーバー名 >]-インストール イメージをダウンロードする、指定されたイメージから起動したすべてのクライアントが通信するサーバーの名前を指定します。 既定では、このイメージを起動したすべてのクライアントは有効な Windows 展開サービス サーバーを検出します。 このオプションを使用して、探索機能をバイパスし、強制的に起動されるクライアント指定のサーバーに接続します。</br>-[/Overwrite: {[はい] | いいえ | 追加}] - で、ファイルが指定されているかどうか判断 **/DestinationImage** /FilePath でその名前を持つ別のファイルが既に存在する場合に上書きする必要があります。 **[はい]** 既存のファイルを上書きします。 **いいえ** (既定値) と同じ名前の別のファイルが既に存在する場合に発生するエラーが発生します。 **追加** 既存の .wim ファイル内に新しいイメージとして生成されたイメージをアタッチします。|

## <a name="BKMK_examples"></a>例

ブート イメージから検出イメージを作成し、WinPEDiscover.wim という名前を付けて、次のように入力します。
```
WDSUTIL /New-DiscoverImage /Image:"WinPE boot image" /Architecture:x86 /DestinationImage /FilePath:"C:\Temp\WinPEDiscover.wim"
```
ブート イメージから検出イメージを作成し、指定した設定で WinPEDiscover.wim と名前、次のように入力します。
```
WDSUTIL /Verbose /Progress /New-DiscoverImage /Server:MyWDSServer
/Image:"WinPE boot image" /Architecture:x64 /Filename:boot.wim /DestinationImage /FilePath:"\\Server\Share\WinPEDiscover.wim" 
/Name:"New WinPE image" /Description:"WinPE image for WDS Client discovery" /Overwrite:No
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)