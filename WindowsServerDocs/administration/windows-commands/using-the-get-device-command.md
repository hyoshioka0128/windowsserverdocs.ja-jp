---
title: Get-デバイスの場合、コマンドを使用します。
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1da79286-7e1d-45f2-aea2-d446e16a6911
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6451e0a55a72fc88867a3f3be0e1317d881391aa
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363198"
---
# <a name="using-the-get-device-command"></a>Get-デバイスの場合、コマンドを使用します。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

事前設定されたコンピューター (つまり、active directory ドメインサービスのコンピューターアカウントに関連する物理コンピューター) に関する Windows 展開サービス情報を取得します。
## <a name="syntax"></a>構文
```
wdsutil /Get-Device {/Device:<Device name> | /ID:<MAC or UUID>} [/Domain:<Domain>] [/forest:{Yes | No}]
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/デバイス: <Device name>|コンピューター (SAMAccountName) の名前を指定します。|
|/ID: <MAC or UUID>|次の例に示すように、MAC アドレスまたはコンピューターの UUID (GUID) のいずれかを指定します。 有効な GUID は、バイナリ文字列または GUID 文字列の2つの形式のいずれかにする必要があります。<br /><br />-   **バイナリ文字列**:/ID: ACEFA3E81F20694E953EB2DAA1E8B1B6<br />-    の**MAC アドレス**:00B056882FDC (ダッシュなし) または 00-B0-56-88-2F-DC (ダッシュ付き)<br />-   **GUID 文字列**:/ID: E8A3EFAC-4E69-953-B2DAA1E8B1B6|
|[/ドメイン:<Domain>]|事前登録されたコンピューターを検索するドメインを指定します。 このパラメーターの既定値は、ローカル ドメインです。|
|[/forest: {Yes &#124; No}]|Windows 展開サービスがフォレスト全体またはローカル ドメインを検索する必要があるかどうかを指定します。 既定値は **いいえ**, 、ローカルのドメインのみを検索することを意味します。|
## <a name="BKMK_examples"></a>例
情報を取得するコンピューター名を使用して、次のように入力します。
```
wdsutil /Get-Device /Device:computer1
```
情報を取得する MAC アドレスを使用して、次のように入力します。
```
wdsutil /verbose /Get-Device /ID:"00-B0-56-88-2F-DC" /Domain:MyDomain
```
情報を取得する GUID 文字列を使用して、次のように入力します。
```
wdsutil /verbose /Get-Device /ID:E8A3EFAC-201F-4E69-953-B2DAA1E8B1B6 /forest:Yes
```
#### <a name="additional-references"></a>その他の参照情報
[コマンドライン構文のポイント](command-line-syntax-key.md)
[サブコマンド: セット デバイス](subcommand-set-device.md)
[デバイスの追加のコマンドを使用して](using-the-add-device-command.md)
[取得しているコマンドを使用して](using-the-get-alldevices-command.md)
