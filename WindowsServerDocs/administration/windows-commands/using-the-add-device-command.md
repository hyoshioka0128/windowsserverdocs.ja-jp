---
title: デバイスの追加のコマンドを使用してください。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1e599cc4-464a-421b-b6bb-c101af154131
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 85e9ef4445b4dabbe85c2397d62b06756e17879d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59878543"
---
# <a name="using-the-add-device-command"></a>デバイスの追加のコマンドを使用してください。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Active directory Domain Services 内のコンピューターを事前にします。 プレステージしたコンピューターは、既知のコンピューターとも呼ばれます。 これにより、クライアントのインストールを制御するプロパティを構成できます。 たとえば、ネットワーク ブート プログラムとクライアントが受信すると、無人セットアップ ファイルだけでなく、クライアントがネットワーク ブート プログラムをダウンロードする必要があります、サーバーを構成できます。
このコマンドを使用する方法の例については、次を参照してください。[例](#BKMK_examples)します。
## <a name="syntax"></a>構文
```
wdsutil /add-Device /Device:<Device name> /ID:<UUID | MAC address> [/ReferralServer:<Server name>] [/BootProgram:<Relative path>] [/WdsClientUnattend:<Relative path>] 
[/User:<Domain\User | User@Domain>] [/JoinRights:{JoinOnly | Full}] [/JoinDomain:{Yes | No}] [/BootImagepath:<Relative path>] [/OU:<DN of OU>] [/Domain:<Domain>]
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/デバイス:<computer name>|追加するコンピューターの名前を指定します。|
|/ID: < UUID &#124; MAC アドレス >|GUID/UUID またはコンピューターの MAC アドレスのいずれかを指定します。 GUID または UUID は、2 つの形式のバイナリ文字列または GUID の文字列のいずれかである必要があります。 例:<br /><br />バイナリ文字列: **/ID:ACEFA3E81F20694E953EB2DAA1E8B1B6**<br /><br />GUID 文字列: **/ID:E8A3EFAC-201F-4E69-953E-B2DAA1E8B1B6**<br /><br />MAC アドレスは、次の形式である必要があります。**00B056882FDC** (ダッシュ) または**00-B0-56-88-2F-DC** (ダッシュ付き) を含む|
|[/ReferralServer:<Server name>]|簡易のファイル転送プロトコル (tftp) を使用してネットワーク ブート プログラムとブート イメージをダウンロードする接続先サーバーの名前を指定します。|
|[/BootProgram:<Relative path>]|RemoteInstall フォルダーからこのコンピューターが受け取る必要のあるネットワーク ブート プログラムへの相対パスを指定します。 例:"boot\x86\pxeboot.com"|
|[/WdsClientUnattend:<Relative path>]|Windows 展開サービス クライアントのインストール画面を自動化する無人インストール ファイルを remoteInstall フォルダーからの相対パスを指定します。|
|[/User:<Domain\User &#124; User@Domain>]|指定したユーザー、コンピューターをドメインに参加させるために必要な権限を与えるコンピューター アカウント オブジェクトのアクセス許可を設定します。|
|[/JoinRights: {JoinOnly & #124 文字です。完全}]|ユーザーに割り当てられる権限の種類を指定します。<br /><br />-   **JoinOnly**ユーザーでコンピューターをドメインに参加する前に、コンピューター アカウントをリセットするには、管理者が必要です。<br />-   **完全な**へのフル アクセスは、ユーザー、コンピューターをドメインに参加する権限が含まれます。|
|[/JoinDomain: {[はい] (& a) #124 文字です。No}]|ドメインに、オペレーティング システムのインストール中のこのコンピューター アカウントとコンピューターを参加する必要があるかどうかを指定します。 既定値は **はい**します。|
|[/BootImagepath:<Relative path>]|このコンピューターが使用するブート イメージには、remoteInstall フォルダーからの相対パスを指定します。|
|[/OU:<DN of OU>]|コンピューター アカウント オブジェクトを作成する必要が組織単位の識別名。 次に、例を示します。**OU = MyOU, CN テスト, DC = Domain, DC = com を =** します。 既定の場所は、既定のコンピュータのコンテナーです。|
|[/ドメイン:<Domain>]|コンピューター アカウント オブジェクトを作成するドメイン。 既定の場所は、ローカル ドメインです。|
## <a name="BKMK_examples"></a>例
コンピューターを追加するには、MAC アドレスを使用して、次のように入力します。
```
wdsutil /add-Device /Device:computer1 /ID:00-B0-56-88-2F-DC
```
コンピューターを追加するには、GUID 文字列を使用して、次のように入力します。
```
wdsutil /add-Device /Device:computer1 /ID:{E8A3EFAC-201F-4E69-953F-B2DAA1E8B1B6} /ReferralServer:WDSServer1 /BootProgram:boot\x86\pxeboot.com 
/WDSClientUnattend:WDSClientUnattend\unattend.xml /User:Domain\MyUser/JoinRights:Full /BootImagepath:boot\x86\images\boot.wim /OU:"OU=MyOU,CN=Test,DC=Domain,DC=com"
```
#### <a name="additional-references"></a>その他の参照
[コマンドライン構文のポイント](command-line-syntax-key.md)
[取得しているコマンドを使用して](using-the-get-alldevices-command.md)
[get デバイス コマンドを使用して](using-the-get-device-command.md)
[サブコマンド: セット デバイス](subcommand-set-device.md)
[新規 WdsClient](https://technet.microsoft.com/library/dn283430.aspx)
