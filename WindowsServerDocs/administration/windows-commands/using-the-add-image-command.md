---
title: イメージの追加
description: イメージの追加に関する Windows コマンドのトピックでは、Windows 展開サービスサーバーにイメージを追加します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d5b6f4da-90ba-4b0e-9423-66c8ef5172e2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6888027e3f5f7f44f2b37e958d0f779431e994a9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80831975"
---
# <a name="add-image"></a>イメージの追加

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Windows 展開サービス サーバーにイメージを追加します。 このコマンドを使用する方法の例については、次を参照してください。 [例](#BKMK_examples)します。

## <a name="syntax"></a>構文
ブートイメージの場合は、次の構文を使用します。
```
wdsutil /add-ImagmediaFile:<wim file path> [/Server:<Server name>mediatype:Boot [/Skipverify] [/Name:<Image name>] [/Description:<Image description>] 
[/Filename:<New wim file name>]
```
インストールイメージの場合は、次の構文を使用します。
```
wdsutil /add-ImagmediaFile:<wim file path>
     [/Server:<Server name>]
   mediatype:Install
     [/Skipverify]
    mediaGroup:<Image group name>]
     [/SingleImage:<Single image name>]
         [/Name:<Name>]
         [/Description:<Description>]
     [/Filename:<File name>]
     [/UnattendFile:<Unattend file path>]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
mediaFile: < .wim ファイルのパス >|追加するイメージを含む Windows イメージ (.wim) ファイルの完全パスとファイル名を指定します。|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
メディアの種類: {ブート&#124;インストール}|追加するイメージの種類を指定します。|
|[/Skipverify]|ある整合性の検証は実行されません、ソース イメージ ファイルのイメージを追加する前に指定します。|
|[/Name:<Name>]|イメージの表示名を設定します。|
|/Description<Description>]|イメージの説明を設定します。|
|[/ファイル名:<Filename>]|.Wim ファイルの新しいファイル名を指定します。 これにより、イメージを追加するときに、.wim ファイルのファイル名を変更することができます。 ファイル名が指定されていない場合、ソース イメージ ファイル名が使用されます。 常に、Windows 展開サービスをセットアップ先のコンピューターのブート イメージ ストアにファイル名が一意かどうかをチェックします。|
|\mediaGroup:<Image group name>]|イメージが追加されるイメージ グループの名前を指定します。 サーバーの 1 つ以上のイメージ グループが存在する場合は、イメージ グループを指定してください。 これが指定されていないイメージ グループが存在しない場合は、新しいイメージ グループが作成されます。 それ以外の場合、既存のイメージ グループが使用されます。|
|[/Singleimage:<Single image name>][/Name:<Name>]/Description<Description>]|.Wim ファイルから指定された 1 つのイメージをコピーし、イメージの表示名と説明を設定します。|
|[/UnattendFile:<Unattend file path>]|無人インストール ファイルが追加されているイメージと関連付けるへの完全パスを指定します。 場合 **/SingleImage** が指定されていない、同じ無人セットアップ ファイルはすべての .wim ファイル内のイメージに関連付けられます。|
## <a name="examples"></a><a name=BKMK_examples></a>例
ブート イメージを追加するには、次のように入力します。
```
wdsutil /add-ImagmediaFile:C:\MyFolder\Boot.wimmediatype:Boot
wdsutil /verbose /Progress /add-ImagmediaFile:\\MyServer\Share\Boot.wim /Server:MyWDSServemediatype:Boot /Name:My WinPE Image 
/Description:WinPE Image containing the WDS Client /Filename:WDSBoot.wim
```
インストール イメージを追加するには、次のいずれかを入力します。
```
wdsutil /add-ImagmediaFile:C:\MyFolder\Install.wimmediatype:Install
wdsutil /verbose /Progress /add-ImagmediaFile:\\MyServer\Share \Install.wim /Server:MyWDSServemediatype:InstalmediaGroup:ImageGroup1 
/SingleImage:Windows Pro /Name:My WDS Image
/Description:Windows Pro image with Microsoft Office /Filename:Win Pro.wim /UnattendFile:\\server\share\unattend.xml
```
## <a name="additional-references"></a>その他の参照情報
- [コマンドライン構文のポイント](command-line-syntax-key.md)
[コピー イメージのコマンドを使用して](using-the-copy-image-command.md)
[/export-image コマンドを使用して](using-the-export-image-command.md)
[get イメージのコマンドを使用して](using-the-get-image-command.md)
[削除イメージのコマンドを使用して](using-the-remove-image-command.md)
[置換イメージのコマンドを使用して](using-the-replace-image-command.md)
[サブコマンド: 画像の設定](subcommand-set-image.md)
