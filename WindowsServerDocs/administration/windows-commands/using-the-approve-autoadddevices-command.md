---
title: 承認-AutoaddDevices
description: '[承認-AutoaddDevices] の参照記事。管理者の承認が保留中のコンピューターを承認します。'
ms.topic: article
ms.assetid: 8d76e8d3-ab35-429c-be7b-904f95d0782d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 79cc6d2aa9c91433cecb08e9a380b99a8c12332e
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87896582"
---
# <a name="approve-autoadddevices"></a>承認-AutoaddDevices

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

管理者の承認が保留中のコンピューターを承認します。 自動追加ポリシーを有効にすると、不明なコンピューター (事前登録されていないコンピューター) がイメージをインストールする前に、管理者の承認が必要になります。 このポリシーを有効にするには、[サーバーのプロパティ] ページの [ **PXE 応答**] タブを使用します。

## <a name="syntax"></a>構文
```
wdsutil [Options] /Approve-AutoaddDevices [/Server:<Server name>] /RequestId:{<Request ID>| ALL} [/MachineName:<Device name>] [/OU:<DN of OU>]
[/User:<Domain\User | User@Domain>] [/JoinRights:{JoinOnly | Full}] [/JoinDomain:{Yes | No}] [/ReferralServer:<Server name>] [/BootProgram:<Relative path>] [/WdsClientUnattend:<Relative path>] [/BootImagepath:<Relative path>]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|[/Server:<Server name>]|サーバーの名前を指定します。 NetBIOS 名または完全修飾ドメイン名 (FQDN) のいずれかを指定できます。 サーバー名が指定されていない場合は、ローカルのサーバーが使用されます。|
|/RequestId: {要求 ID と #124 文字です。すべて}|保留中のコンピューターに割り当てられた要求 ID を指定します。 指定 **すべて** 保留中のすべてのコンピューターを承認します。|
|[/MachineName:<Device name>]|追加するコンピューターの名前を指定します。 すべてのコンピューターを承認する場合は、このオプションを使用することはできません。|
|[/OU:<DN of OU>]|コンピューター アカウント オブジェクトを作成する必要が組織単位 (OU) の識別名を指定します。 例: **OU = MyOU, CN テスト, DC = Domain, DC = com を =** です。 既定の場所は、既定のコンピュータのコンテナーです。|
|[/User: <Domain\User &#124; User@Domain>]|指定されたユーザーに必要なアクセス権を割り当てるコンピュータ アカウント オブジェクトのアクセス許可を設定します。|
|[/JoinRights: {JoinOnly & #124 文字です。完全}]|指定されたユーザーに割り当てられる権限の種類を指定します。<p>-   **Joinonly**では、ユーザーがコンピューターをドメインに参加させる前に、管理者がコンピューターアカウントをリセットする必要があります。<br />-   **Full**を指定すると、コンピューターをドメインに参加させる権限を含む、ユーザーにフルアクセスできます。|
|[/JoinDomain: {[はい] (& a) #124 文字です。No}]|ドメインに、オペレーティング システムのインストール中のこのコンピューター アカウントとコンピューターを参加する必要があるかどうかを指定します。 既定値は **[はい]** です。|
|[/ReferralServer:<Server name>]|簡易ファイル転送プロトコル (tftp) を使用して、ネットワークブートプログラムとブートイメージをダウンロードするために、接続するサーバーの名前を指定します。|
|[/BootProgram:<Relative path>]|RemoteInstall フォルダからこのコンピュータが受信するネットワークブートプログラムへの相対パスを指定します。 例: **boot\x86\pxeboot.com**します。|
|[/WdsClientUnattend:<Relative path>]|Windows 展開サービスクライアントを自動化する無人セットアップファイルへの remoteInstall フォルダーからの相対パスを指定します。|
|[/BootImagepath: <Relative path> ]|RemoteInstall フォルダからこのコンピュータが受信するブートイメージへの相対パスを指定します。|
## <a name="examples"></a>例
12 の要求 Id を使用してコンピューターを承認するには、次のように入力します。
```
wdsutil /Approve-AutoaddDevices /RequestId:12
```
指定した設定を使用してイメージを展開 20 の要求 Id を使用してコンピューターを承認して、次のように入力します。
```
wdsutil /Approve-AutoaddDevices /RequestId:20 /MachineName:computer1 /OU:OU=Test,CN=company,DC=Domain,DC=Com /User:Domain\User1
/JoinRights:Full /ReferralServer:MyWDSServer /BootProgram:boot\x86\pxeboot.n12 /WdsClientUnattend:WDSClientUnattend\Unattend.xml /BootImagepath:boot\x86\images\boot.wim
```
承認保留中のすべてのコンピューターに、次のように入力します。
```
wdsutil /verbose /Approve-AutoaddDevices /RequestId:ALL
```
## <a name="additional-references"></a>その他の参照情報
- [コマンドライン構文のキー](command-line-syntax-key.md) 
[Delete AutoaddDevices コマンド](using-the-delete-autoadddevices-command.md) 
 の使用[Get AutoaddDevices コマンド](using-the-get-autoadddevices-command.md) 
 の使用[拒否 AutoaddDevices コマンドの使用](using-the-reject-autoadddevices-command.md)
