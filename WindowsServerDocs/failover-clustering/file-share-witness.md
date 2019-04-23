---
title: Windows Server 2019 でファイル共有監視をデプロイします。
ms.prod: windows-server-threshold
ms.manager: eldenc
ms.technology: failover-clustering
ms.topic: article
author: johnmarlin-msft
ms.date: 01/24/2019
description: ファイル共有監視サーバーを使用すると、ファイル共有を使用してクラスター クォーラムの投票できます。 このトピックでは、ファイル共有監視サーバーとファイル共有監視として、ルーターに接続されている USB ドライブの使用など、新しい機能について説明します。
ms.localizationpriority: medium
ms.openlocfilehash: 1888142f96208800a0417c9caeea89e8a0472e88
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59831753"
---
# <a name="deploy-a-file-share-witness"></a>ファイル共有監視をデプロイします。

> 適用先:Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ファイル共有監視は、クラスター クォーラムの投票としてフェールオーバー クラスターを使用する SMB 共有です。 このトピックでは、テクノロジと Windows Server 2019、ファイル共有監視として、ルーターに接続されている USB ドライブの使用などの新機能の概要を示します。

ファイル共有監視サーバーは、次の状況で便利です。  

- クラスター内のすべてのサーバーが信頼性の高いインターネット接続があるために、クラウド監視を使用できません。
- ディスクのミラーリング監視サーバーを使用できる共有ドライブがないために、ディスクのミラーリング監視サーバーを使用できません。 これは、記憶域スペース ダイレクト クラスター、SQL Server 常に 可用性グループ (AG)、Exchange データベース可用性グループ (DAG) など。これらの種類のクラスターの なし は、共有ディスクを使用します。

## <a name="file-share-witness-requirements"></a>ファイル共有のミラーリング監視サーバーの要件

ドメインに参加している Windows サーバー上のファイル共有監視をホストする、または場合、クラスターを実行している Windows Server 2019、任意のデバイス ホスト、SMB 2 またはそれ以降のファイルを共有できます。

|ファイル サーバーの種類                 | サポートされているクラスター |
|---------------------------------|--------------------|
|デバイス、w/2 の SMB ファイル共有 | Windows Server 2019|
|ドメインに参加している Windows Server     | Windows Server 2008 以降|

クラスターで Windows Server 2019 が実行されている場合、要件を示します。

- SMB ファイル共有*SMB 2 またはそれ以降のプロトコルを使用する任意のデバイスで*など。
    - ネットワーク接続ストレージ (NAS) デバイス
    - Windows コンピューターがワークグループに参加しています。
    - ローカルに接続されている USB 記憶域を持つ
- クラスターを認証するため、デバイス上のローカル アカウント
- ファイル共有を使用したクラスターの認証に Active Directory を使う代わりに場合、は、クラスター名オブジェクト (CNO) が、共有に対する書き込みアクセス許可を必要し、サーバーがクラスターと同じ Active Directory フォレストである必要があります。
- ファイル共有が 5 MB の空き領域の最小値

2016 以前、クラスターが Windows Server を実行している場合、要件を示します。

- SMB ファイル共有*クラスターと同じ Active Directory フォレストに参加している Windows サーバー*
- クラスター名オブジェクト (CNO) では、共有に対する書き込みアクセス許可が必要
- ファイル共有が 5 MB の空き領域の最小値

その他の注意事項:
- Windows ドメインに参加しているサーバー以外のデバイスでホストされているファイル共有監視を使用する必要があります使用している、 **Set-clusterquorum-資格情報**PowerShell コマンドレットをこのトピックの後半で説明したように、ミラーリング監視サーバーを設定します。
- 高可用性のため、個別のフェールオーバー クラスターでファイル共有監視を使用することができます。
- 複数のクラスターで使用できるファイル共有
- フェールオーバー クラスタ リングの任意のバージョンでは、分散ファイル システム (DFS) 共有またはレプリケートされた記憶域の使用はサポートされていません。  これらには、クラスター化されたサーバーが互いを実行しているし、データの損失が発生する可能性がありますスプリット ブレイン状況可能性があります。

## <a name="creating-a-file-share-witness-on-a-router-with-a-usb-device"></a>ルーターで USB デバイスとファイル共有監視を作成します。

[Microsoft Ignite 2018](https://azure.microsoft.com/ignite/)、[データ ストレージ](http://www.dataonstorage.com/)キオスク分野の記憶域スペース ダイレクト クラスターを必要があります。  このクラスターが接続されていた、 [NetGear](https://www.netgear.com) Nighthawk X4S WiFi ルーターが USB ポートを使用して、ファイルとしては、次のようにミラーリング監視サーバーを共有します。

![NetGear ミラーリング監視サーバー](media\File-Share-Witness\FSW1.png)

この特定のルーター上の USB デバイスを使用してファイル共有監視を作成する手順は、以下に示します。  その他のルーターと NAS アプライアンス上の手順はさまざまで、仕入先を使用して実行することことに注意してくださいでは、方向を指定します。


1. ルーター接続されている USB デバイスにログインします。

   ![NetGear インターフェイス](media\File-Share-Witness\FSW2.png)

2. オプションの一覧で、共有を作成できるは ReadySHARE を選択します。

   ![NetGear ReadySHARE](media\File-Share-Witness\FSW3.png)

3. ファイル共有監視の基本的な共有とは、必要なことです。  編集 ボタンを選択すると、USB デバイス上の共有を作成できます ダイアログ表示されます。

   ![NetGear 共有インターフェイス](media\File-Share-Witness\FSW4.png)

4. [適用] ボタンを選択すると、共有が作成され、一覧で確認できます。

   ![NetGear 共有](media\File-Share-Witness\FSW5.png)

5. 共有が作成されたら、PowerShell を使用したはクラスターのファイル共有監視の作成が行われます。

   ```PowerShell
   Set-ClusterQuorum -FileShareWitness \\readyshare\Witness -Credential (Get-Credential)
   ```

   これには、デバイスのローカル アカウントを入力するダイアログ ボックスが表示されます。

USB 機能、NAS デバイス、またはその他の Windows デバイスで他のルーターにも同じような手順を実行できます。
