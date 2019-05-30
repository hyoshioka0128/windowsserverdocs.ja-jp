---
title: 承認 AutoaddDevices コマンドを使用してください。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8d76e8d3-ab35-429c-be7b-904f95d0782d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9ce9824c45a00ccb9f1f9e357c7e3d36b2857f69
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886823"
---
# <a name="using-the-approve-autoadddevices-command"></a>承認 AutoaddDevices コマンドを使用してください。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

管理者の承認が保留中のコンピューターを承認します。 自動追加ポリシーが有効にすると (事前登録されていないもの) の不明なコンピューターにイメージをインストールする前に管理者の承認が必要です。 このポリシーを使用して有効にすることができます、 **PXE 応答**サーバー プロパティ ページのタブ。
## <a name="syntax"></a>構文
```
wdsutil [Options] /Approve-AutoaddDevices [/Server:<Server name>] /RequestId:{<Request ID>| ALL} [/MachineName:<Device name>] [/OU:<DN of OU>] 
[/User:<Domain\User | User@Domain>] [/JoinRights:{JoinOnly | Full}] [/JoinDomain:{Yes | No}] [/ReferralServer:<Server name>] [/BootProgram:<Relative path>] [/WdsClientUnattend:<Relative path>] [/BootImagepath:<Relative path>]
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
|/RequestId: {要求 ID と #124 文字です。すべて}|保留中のコンピューターに割り当てられた要求 ID を指定します。 指定 **すべて** 保留中のすべてのコンピューターを承認します。|
|[/MachineName:<Device name>]|追加するコンピューターの名前を指定します。 すべてのコンピューターを承認する場合は、このオプションを使用することはできません。|
|[/OU:<DN of OU>]|コンピューター アカウント オブジェクトを作成する必要が組織単位 (OU) の識別名を指定します。 次に、例を示します。**OU = MyOU, CN テスト, DC = Domain, DC = com を =** します。 既定の場所は、既定のコンピュータのコンテナーです。|
|[/User:<Domain\User &#124; User@Domain>]|指定されたユーザーに必要なアクセス権を割り当てるコンピュータ アカウント オブジェクトのアクセス許可を設定します。|
|[/JoinRights: {JoinOnly &#124;文字です。完全}]|指定されたユーザーに割り当てられる権限の種類を指定します。<br /><br />-   **JoinOnly**ユーザーでコンピューターをドメインに参加する前に、コンピューター アカウントをリセットするには、管理者が必要です。<br />-   **完全な**へのフル アクセスは、ユーザー、コンピューターをドメインに参加する権限が含まれます。|
|[/JoinDomain: {[はい] (& a) #124 文字です。No}]|ドメインに、オペレーティング システムのインストール中のこのコンピューター アカウントとコンピューターを参加する必要があるかどうかを指定します。 既定値は **はい**します。|
|[/ReferralServer:<Server name>]|簡易のファイル転送プロトコル (tftp) を使用して、ネットワーク ブート プログラムとブート イメージをダウンロードする接続先サーバーの名前を指定します。|
|[/BootProgram:<Relative path>]|RemoteInstall フォルダーからこのコンピューターが受け取る必要のあるネットワーク ブート プログラムへの相対パスを指定します。 例: **boot\x86\pxeboot.com**します。|
|[/WdsClientUnattend:<Relative path>]|Windows 展開サービス クライアントを自動化する無人セットアップ ファイルを remoteInstall フォルダーからの相対パスを指定します。|
|[/BootImagepath:<Relative path>]|このコンピューターが受け取る必要のあるブート イメージには、remoteInstall フォルダーからの相対パスを指定します。|
## <a name="BKMK_examples"></a>例
12 の要求 Id を使用してコンピューターを承認するには、次のように入力します。
```
wdsutil /Approve-AutoaddDevices /RequestId:12
```
指定した設定を使用してイメージを展開 20 の要求 Id を使用してコンピューターを承認して、次のように入力します。
```
wdsutil /Approve-AutoaddDevices /RequestId:20 /MachineName:computer1 /OU:"OU=Test,CN=company,DC=Domain,DC=Com" /User:Domain\User1 
/JoinRights:Full /ReferralServer:MyWDSServer /BootProgram:boot\x86\pxeboot.n12 /WdsClientUnattend:WDSClientUnattend\Unattend.xml /BootImagepath:boot\x86\images\boot.wim
```
承認保留中のすべてのコンピューターに、次のように入力します。
```
wdsutil /verbose /Approve-AutoaddDevices /RequestId:ALL
```
#### <a name="additional-references"></a>その他の参照
[コマンドライン構文のポイント](command-line-syntax-key.md)
[AutoaddDevices delete コマンドを使用して](using-the-delete-autoadddevices-command.md)
[get AutoaddDevices コマンドを使用して](using-the-get-autoadddevices-command.md)
 [却下 AutoaddDevices コマンドを使用して](using-the-reject-autoadddevices-command.md)
