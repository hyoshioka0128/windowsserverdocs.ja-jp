---
title: サブコマンド セット デバイス
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 401567f8-eaeb-4a2d-b811-140bb007028d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 80bb9144936cf493784603bcbdb8a0d1e5c870bd
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848063"
---
# <a name="subcommand-set-device"></a>サブコマンド: セット デバイス

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

事前設定されたコンピューターの属性を変更します。 事前設定されたコンピューターは、active directory ドメイン サービス (AD DS) 内のコンピューター アカウント オブジェクトにリンクされているコンピューターです。 事前登録されたクライアントは、既知のコンピューターとも呼ばれます。 クライアントのインストールを管理するコンピューター アカウントのプロパティを構成できます。 たとえば、ネットワーク ブート プログラムとクライアントが受信すると、無人セットアップ ファイルだけでなく、クライアントがネットワーク ブート プログラムをダウンロードする必要があります、サーバーを構成できます。
## <a name="syntax"></a>構文
```
wdsutil [Options] /Set-Device /Device:<Device name> [/ID:<UUID | MAC address>] [/ReferralServer:<Server name>] [/BootProgram:<Relative path>] 
[/WdsClientUnattend:<Relative path>] [/User:<Domain\User | User@Domain>] [/JoinRights:{JoinOnly | Full}] [/JoinDomain:{Yes | No}] [/BootImagepath:<Relative path>] [/Domain:<Domain>] [/resetAccount]
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/デバイス:<computer name>|コンピューター (SAM アカウント名) の名前を指定します。|
|[/Id: < UUID &#124 文字です。MAC アドレス >]|GUID/UUID またはコンピューターの MAC アドレスのいずれかを指定します。 この値は、次の 3 つの形式のいずれかである必要があります。<br /><br />-バイナリ文字列: **/ID:ACEFA3E81F20694E953EB2DAA1E8B1B6**<br />文字列の GUID/UUID:/id:**E8A3EFAC-201F-4E69-953E-B2DAA1E8B1B6**<br />MAC アドレス:**00B056882FDC** (ダッシュ) または**00-B0-56-88-2F-DC** (ダッシュ付き) を含む|
|[/ReferralServer:<Server name>]|簡易のファイル転送プロトコル (tftp) を使用してネットワーク ブート プログラムとブート イメージをダウンロードする接続先サーバーの名前を指定します。|
|[/BootProgram:<Relative path>]|RemoteInstall フォルダーから、指定されたコンピューターが受信するネットワーク ブート プログラムへの相対パスを指定します。 例: **boot\x86\pxeboot.com**|
|[/WdsClientUnattend:<Relative path>]|Windows 展開サービス クライアントのインストール画面を自動化する無人セットアップ ファイルを remoteInstall フォルダーからの相対パスを指定します。|
|[/User:<Domain\User &#124; User@Domain>]|指定したユーザー、コンピューターをドメインに参加させるために必要な権限を与えるコンピューター アカウント オブジェクトのアクセス許可を設定します。|
|[/JoinRights: {JoinOnly &#124 文字です。完全}]|ユーザーに割り当てられる権限の種類を指定します。<br /><br />-   **JoinOnly**ユーザーでコンピューターをドメインに参加する前に、コンピューター アカウントをリセットするには、管理者が必要です。<br />-   **完全な**コンピューターをドメインに参加する権限を含め、ユーザーへのフル アクセスを提供します。|
|[/JoinDomain: {[はい] (& a) #124 文字です。No}]|ドメインに、Windows 展開サービスのインストール中のこのコンピューター アカウントとコンピューターを参加する必要があるかどうかを指定します。 既定の設定は **はい**します。|
|[/BootImagepath:<Relative path>]|コンピューターが使用するブート イメージには、remoteInstall フォルダーからの相対パスを指定します。|
|[/ドメイン:<Domain>]|事前登録されたコンピューターを検索するドメインを指定します。 既定値は、ローカル ドメインです。|
|[/resetAccount]|指定したコンピューター上のアクセス許可がリセットされるので、適切なアクセス許可を持っているユーザー アカウントを使用してドメインに参加できます。|
## <a name="BKMK_examples"></a>例
コンピューターのネットワーク ブート プログラムと参照サーバーを設定するには、次のように入力します。
```
wdsutil /Set-Device /Device:computer1 /ReferralServer:MyWDSServer
/BootProgram:boot\x86\pxeboot.n12
```
コンピューターのさまざまな設定を指定するには、次のように入力します。
```
wdsutil /verbose /Set-Device /Device:computer2 /ID:00-B0-56-88-2F-DC /WdsClientUnattend:WDSClientUnattend\unattend.xml 
/User:Domain\user /JoinRights:JoinOnly /JoinDomain:No /BootImagepath:boot\x86\images\boot.wim /Domain:NorthAmerica /resetAccount
```
#### <a name="additional-references"></a>その他の参照
[コマンドライン構文のポイント](command-line-syntax-key.md)
[デバイスの追加のコマンドを使用して](using-the-add-device-command.md)
[取得しているコマンドを使用して](using-the-get-alldevices-command.md)
[get デバイス コマンドを使用します。](using-the-get-device-command.md)
