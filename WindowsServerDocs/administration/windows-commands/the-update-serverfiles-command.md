---
title: 更新-ServerFiles
description: 更新プログラム ServerFiles のリファレンストピック。サーバーの%Windir%\System32\RemInst フォルダーに格納されている最新のファイルを使用して、REMINST 共有フォルダー内のファイルを更新します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 23aa79df-38c6-401e-91bd-cd23811b30b4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0005d8e198300c4aad9fdfc772957b460d6fee74
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82721380"
---
# <a name="update-serverfiles"></a>更新-ServerFiles

サーバーの %Windir%\System32\RemInst フォルダーに格納されている最新のファイルを使用して、REMINST 共有フォルダー内のファイルを更新します。 Windows 展開サービス インストールの有効性を確実には、Windows 展開サービスのファイルに、各サーバーのアップグレード、サービス パックのインストールまたは更新後に 1 回このコマンドを実行する必要があります。

## <a name="syntax"></a>構文

```
WDSUTIL [Options] /Update-ServerFiles [/Server:<Server name>]
```

### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|[/Server:\<サーバー名>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|

## <a name="examples"></a>例

ファイルを更新するには、次のいずれかを入力します。
```
WDSUTIL /Update-ServerFiles
WDSUTIL /Verbose /Progress /Update-ServerFiles /Server:MyWDSServer
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)