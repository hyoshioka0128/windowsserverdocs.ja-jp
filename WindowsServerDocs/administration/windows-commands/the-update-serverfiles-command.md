---
title: 更新プログラム ServerFiles コマンド
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 23aa79df-38c6-401e-91bd-cd23811b30b4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 93eeb0deaa527921db35f4ab955d2ccc46b57d7a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385846"
---
# <a name="the-update-serverfiles-command"></a>更新プログラム ServerFiles コマンド



サーバーの %Windir%\System32\RemInst フォルダーに格納されている最新のファイルを使用して、REMINST 共有フォルダー内のファイルを更新します。 Windows 展開サービス インストールの有効性を確実には、Windows 展開サービスのファイルに、各サーバーのアップグレード、サービス パックのインストールまたは更新後に 1 回このコマンドを実行する必要があります。

## <a name="syntax"></a>構文

```
WDSUTIL [Options] /Update-ServerFiles [/Server:<Server name>]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|[/Server: \<Server name >]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|

## <a name="BKMK_examples"></a>例

ファイルを更新するには、次のいずれかを入力します。
```
WDSUTIL /Update-ServerFiles
WDSUTIL /Verbose /Progress /Update-ServerFiles /Server:MyWDSServer
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)