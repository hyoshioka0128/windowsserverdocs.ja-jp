---
title: Windows Server 2019 でファイル共有監視を展開する
description: ファイル共有監視サーバーを使用すると、ファイル共有を使用してクラスタークォーラムでの投票を行うことができます。 このトピックでは、ファイル共有の監視サーバーと新機能について説明します。これには、ファイル共有監視としてルーターに接続された USB ドライブの使用が含まれます。
manager: eldenc
ms.topic: article
author: johnmarlin-msft
ms.author: johnmar
ms.date: 01/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: ea9dd3f79576048a57c85e879daf86567d325046
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87945835"
---
# <a name="deploy-a-file-share-witness"></a>ファイル共有監視を展開する

> 適用先:Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ファイル共有監視は、フェールオーバークラスターがクラスタークォーラムの投票として使用する SMB 共有です。 このトピックでは、ファイル共有監視としてルーターに接続されている USB ドライブを使用するなど、Windows Server 2019 のテクノロジと新機能の概要について説明します。

ファイル共有監視サーバーは、次のような場合に便利です。

- クラスター内のすべてのサーバーに信頼性の高いインターネット接続があるわけではないため、クラウド監視を使用できません
- ディスク監視に使用する共有ドライブがないため、ディスク監視を使用できません。 これには、記憶域スペースダイレクトクラスター、SQL Server Always On 可用性グループ (AG)、Exchange データベース可用性グループ (DAG) などがあります。 これらの種類のクラスターでは共有ディスクを使用しません。

## <a name="file-share-witness-requirements"></a>ファイル共有監視の要件

ファイル共有監視は、ドメインに参加している Windows server 上でホストできます。また、クラスターで Windows Server 2019 が実行されている場合は、SMB 2 以降のファイル共有をホストできる任意のデバイスでホストできます。

|ファイルサーバーの種類                 | サポートされるクラスター |
|---------------------------------|--------------------|
|SMB 2 ファイル共有の任意のデバイス | Windows Server 2019|
|ドメインに参加している Windows Server     | Windows Server 2008 以降|

クラスターで Windows Server 2019 が実行されている場合は、次の要件があります。

- SMB 2 以降の*プロトコルを使用するデバイス上の*smb ファイル共有 (以下を含む)。
    - ネットワーク接続ストレージ (NAS) デバイス
    - ワークグループに参加している Windows コンピューター
    - ローカルに接続された USB 記憶域を持つルーター
- クラスターを認証するためのデバイス上のローカルアカウント
- ファイル共有でクラスターを認証するために Active Directory を使用する場合、クラスター名オブジェクト (CNO) には共有に対する書き込みアクセス許可が必要であり、サーバーはクラスターと同じ Active Directory フォレストにある必要があります。
- ファイル共有の空き領域が最低 5 MB

クラスターで Windows Server 2016 以前が実行されている場合は、次の要件があります。

- *クラスターと同じ Active Directory フォレストに参加している Windows server 上の*SMB ファイル共有
- クラスター名オブジェクト (CNO) には、共有に対する書き込みアクセス許可が必要です。
- ファイル共有の空き領域が最低 5 MB

その他の注意事項:
- ドメインに参加している Windows server 以外のデバイスでホストされているファイル共有監視を使用するには、現在、このトピックで後述するように、 **Set ClusterQuorum-Credential** PowerShell コマンドレットを使用してミラーリング監視サーバーを設定する必要があります。
- 高可用性を実現するために、別のフェールオーバークラスターでファイル共有監視を使用することができます。
- ファイル共有は複数のクラスターで使用できます。
- 分散ファイルシステム (DFS) 共有またはレプリケートされた記憶域の使用は、どのバージョンのフェールオーバークラスタリングでもサポートされていません。  このような場合、クラスターサーバーが互いに独立して実行され、データが失われる可能性があります。

## <a name="creating-a-file-share-witness-on-a-router-with-a-usb-device"></a>USB デバイスを使用したルーターへのファイル共有監視の作成

[Microsoft Ignite 2018](https://azure.microsoft.com/ignite/)では、 [dataon Storage に](http://www.dataonstorage.com/)は、キオスク領域に記憶域スペースダイレクトクラスターがありました。  このクラスターは、次のようなファイル共有監視として USB ポートを使用して、 [NetGear](https://www.netgear.com) Nighthawk X4S WiFi ルーターに接続されました。

![NetGear 監視](media/File-Share-Witness/FSW1.png)

この特定のルーターで USB デバイスを使用してファイル共有監視を作成する手順を次に示します。  他のルーターや NAS アプライアンスの手順は異なるため、ベンダーが提供する指示に従って実行する必要があります。


1. USB デバイスが接続されているルーターにログインします。

   ![NetGear インターフェイス](media/File-Share-Witness/FSW2.png)

2. オプションの一覧から [ReadySHARE] (共有を作成できる場所) を選択します。

   ![NetGear ReadySHARE](media/File-Share-Witness/FSW3.png)

3. ファイル共有監視の場合は、基本的な共有だけが必要です。  [編集] ボタンを選択すると、共有を USB デバイスで作成できるダイアログがポップアップ表示されます。

   ![NetGear 共有インターフェイス](media/File-Share-Witness/FSW4.png)

4. [適用] ボタンを選択すると、共有が作成され、一覧に表示されるようになります。

   ![NetGear 共有](media/File-Share-Witness/FSW5.png)

5. 共有が作成されたら、PowerShell を使用してクラスターのファイル共有監視を作成します。

   ```PowerShell
   Set-ClusterQuorum -FileShareWitness \\readyshare\Witness -Credential (Get-Credential)
   ```

   これにより、デバイス上のローカルアカウントを入力するためのダイアログボックスが表示されます。

これらの同様の手順は、USB 機能、NAS デバイス、またはその他の Windows デバイスを使用する他のルーターでも実行できます。
