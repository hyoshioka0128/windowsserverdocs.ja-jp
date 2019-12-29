---
title: 取得しているコマンドを使用してください。
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5824b3d2-2df1-4ed6-a289-e6c47c13fea2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5b7d2ce709c7e3fbaf7ab4f0e49be14c98ba1cd9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71401974"
---
# <a name="using-the-get-alldevices-command"></a>取得しているコマンドを使用してください。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

すべての事前設定されたコンピューターの Windows 展開サービス プロパティを表示します。 事前登録されたコンピューターとは、active directory ドメインサービスのコンピューターアカウントにリンクされている物理コンピューターのことです。
## <a name="syntax"></a>構文
```
wdsutil [Options] /Get-AllDevices [/forest:{Yes | No}] [/ReferralServer:<Server name>]
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|[/forest: {Yes &#124; No}]|Windows 展開サービスがフォレスト全体またはローカル ドメインでコンピューターを返すかどうかを指定します。 既定の設定は **いいえ**, 、ローカル ドメイン内のコンピューターのみが返されることを意味します。|
|[/ReferralServer:<Server name>]|指定されたサーバーの事前登録されているコンピューターのみを返します。|
## <a name="BKMK_examples"></a>例
すべてのコンピューターを表示するには、次のいずれかを入力します。
```
wdsutil /Get-AllDevices
wdsutil /verbose /Get-AllDevices /forest:Yes /ReferralServer:MyWDSServer
```
#### <a name="additional-references"></a>その他の参照情報
[コマンドライン構文のポイント](command-line-syntax-key.md)
[サブコマンド: セット デバイス](subcommand-set-device.md)
[デバイスの追加のコマンドを使用して](using-the-add-device-command.md)
[get デバイス コマンドを使用します。](using-the-get-device-command.md)
