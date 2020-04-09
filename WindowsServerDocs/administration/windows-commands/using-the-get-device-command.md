---
title: get-デバイス
description: デバイスの Windows コマンドに関するトピック。事前登録されたコンピューター (つまり、active directory ドメインサービスのコンピューターアカウントに適用された物理コンピューター) に関する Windows 展開サービス情報を取得します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1da79286-7e1d-45f2-aea2-d446e16a6911
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4b9554ed6236d02be0be3502f42552bafbbfe1cb
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80831115"
---
# <a name="get-device"></a>get-デバイス

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

事前設定されたコンピューター (つまり、active directory ドメインサービスのコンピューターアカウントに関連する物理コンピューター) に関する Windows 展開サービス情報を取得します。

## <a name="syntax"></a>構文
```
wdsutil /Get-Device {/Device:<Device name> | /ID:<MAC or UUID>} [/Domain:<Domain>] [/forest:{Yes | No}]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/デバイス:<Device name>|コンピューター (SAMAccountName) の名前を指定します。|
|/ID:<MAC or UUID>|次の例に示すように、MAC アドレスまたはコンピューターの UUID (GUID) のいずれかを指定します。 有効な GUID は、バイナリ文字列または GUID 文字列の2つの形式のいずれかにする必要があります。<p>-   **バイナリ文字列**:/ID: ACEFA3E81F20694E953EB2DAA1E8B1B6<br />-   **MAC アドレス**: 00B056882FDC (ダッシュなし)、または 00-B0-56-88-2F-DC (ダッシュ付き)<br />-   **GUID 文字列**:/ID: E8A3EFAC-4E69-953-B2DAA1E8B1B6|
|[/ドメイン:<Domain>]|事前登録されたコンピューターを検索するドメインを指定します。 このパラメーターの既定値は、ローカル ドメインです。|
|[/forest: {Yes &#124; No}]|Windows 展開サービスがフォレスト全体またはローカル ドメインを検索する必要があるかどうかを指定します。 既定値は **いいえ**, 、ローカルのドメインのみを検索することを意味します。|
## <a name="examples"></a><a name=BKMK_examples></a>例
情報を取得するコンピューター名を使用して、次のように入力します。
```
wdsutil /Get-Device /Device:computer1
```
情報を取得する MAC アドレスを使用して、次のように入力します。
```
wdsutil /verbose /Get-Device /ID:00-B0-56-88-2F-DC /Domain:MyDomain
```
情報を取得する GUID 文字列を使用して、次のように入力します。
```
wdsutil /verbose /Get-Device /ID:E8A3EFAC-201F-4E69-953-B2DAA1E8B1B6 /forest:Yes
```
## <a name="additional-references"></a>その他の参照情報
- [コマンドライン構文のポイント](command-line-syntax-key.md)
[サブコマンド: セット デバイス](subcommand-set-device.md)
[デバイスの追加のコマンドを使用して](using-the-add-device-command.md)
[取得しているコマンドを使用して](using-the-get-alldevices-command.md)
