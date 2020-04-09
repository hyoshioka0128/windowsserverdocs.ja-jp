---
title: 取得-AllDevices
description: すべての事前設定されたコンピューターの Windows 展開サービスのプロパティを表示する「get AllDevices」の Windows コマンドに関するトピック。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5824b3d2-2df1-4ed6-a289-e6c47c13fea2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 929a74b6cccaed6e85015648538c1ca875b62208
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80831415"
---
# <a name="get-alldevices"></a>取得-AllDevices

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

すべての事前設定されたコンピューターの Windows 展開サービス プロパティを表示します。 事前登録されたコンピューターとは、active directory ドメインサービスのコンピューターアカウントにリンクされている物理コンピューターのことです。

## <a name="syntax"></a>構文
```
wdsutil [Options] /Get-AllDevices [/forest:{Yes | No}] [/ReferralServer:<Server name>]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|[/forest: {Yes &#124; No}]|Windows 展開サービスがフォレスト全体またはローカル ドメインでコンピューターを返すかどうかを指定します。 既定の設定は **いいえ**, 、ローカル ドメイン内のコンピューターのみが返されることを意味します。|
|[/ReferralServer:<Server name>]|指定されたサーバーの事前登録されているコンピューターのみを返します。|
## <a name="examples"></a><a name=BKMK_examples></a>例
すべてのコンピューターを表示するには、次のいずれかを入力します。
```
wdsutil /Get-AllDevices
wdsutil /verbose /Get-AllDevices /forest:Yes /ReferralServer:MyWDSServer
```
## <a name="additional-references"></a>その他の参照情報
- [コマンドライン構文のポイント](command-line-syntax-key.md)
[サブコマンド: セット デバイス](subcommand-set-device.md)
[デバイスの追加のコマンドを使用して](using-the-add-device-command.md)
[get デバイス コマンドを使用します。](using-the-get-device-command.md)
