---
title: Windows Server 2019 でファイル共有監視を展開します。
ms.prod: windows-server-threshold
ms.manager: eldenc
ms.technology: failover-clustering
ms.topic: article
author: johnmarlin-msft
ms.date: 01/24/2019
description: ファイル共有証人を使用すると、ファイル共有を使用してクラスター クォーラムで投票できます。 このトピックでは、ファイル共有証人となどのファイル共有監視としてルーターに接続されている USB ドライブを使用して、新機能について説明します。
ms.localizationpriority: medium
ms.openlocfilehash: 1888142f96208800a0417c9caeea89e8a0472e88
ms.sourcegitcommit: d622f7af181ed0063d716b30278d41887a57db19
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2019
ms.locfileid: "9150892"
---
# ファイル共有監視を展開する

> 適用対象: Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ファイル共有監視は、クラスター クォーラムで投票としてフェールオーバー クラスターを使用する SMB 共有です。 このトピックでは、テクノロジとなどのファイル共有監視としてルーターに接続されている USB ドライブを使用して、Windows Server 2019 の新機能の概要を示します。

ファイル共有証人は、次の場合に便利です。  

- クラスター内のすべてのサーバーの信頼性の高いインターネット接続があるために、クラウド監視を使用できません。
- ディスクの監視に使用する共有のすべてのドライブがないために、ディスクの監視を使用できません。 これは、記憶域スペース ダイレクト クラスターでは、SQL Server 常の可用性グループ (AG)、Exchange データベース可用性グループ (DAG) などです。 これらの種類のクラスターは、共有ディスクを使用します。

## ファイル共有監視の要件

ドメインに参加している Windows server を使用して、ファイル共有監視をホストするまたは場合、クラスターが実行されている Windows Server 2019、任意のデバイスをホストする SMB 2 またはそれ以降のファイルを共有できます。

|ファイル サーバーの種類                 | サポートされているクラスター |
|---------------------------------|--------------------|
|どのデバイス w/、SMB 2 ファイル共有 | Windows Server 2019|
|ドメインに参加している Windows Server     | Windows Server 2008 以降|

クラスターが Windows Server 2019 を実行している場合は、要件を以下に示します。

- SMB ファイル共有*SMB 2 またはそれ以降のプロトコルを使用する任意のデバイス*など。
    - ネットワーク接続ストレージ (NAS) デバイス
    - Windows コンピューターがワークグループに参加しています。
    - ローカルに接続されている USB 記憶域を持つルーター
- クラスターを認証するため、デバイス上のローカル アカウント
- ファイル共有を持つクラスターを認証する代わりに Active Directory を使用している場合は、クラスター名オブジェクト (CNO) では、共有では、書き込みのアクセス許可が必要し、サーバーがクラスターと同じ Active Directory フォレストである必要があります。
- ファイル共有に、5 MB の空き領域の最小値

クラスターには、Windows Server 2016 が実行されている場合は、前の手順の要件を次に示します。

- *クラスターと同じ Active Directory フォレストに参加している Windows server で*の SMB ファイル共有します。
- クラスター名オブジェクト (CNO) では、共有では、書き込みのアクセス許可が必要
- ファイル共有に、5 MB の空き領域の最小値

その他の注意事項:
- 使用するには、ドメインに参加している Windows server 以外のデバイスによってホストされているファイル共有監視する現在使う必要があります、 **Set-clusterquorum-Credential** PowerShell コマンドレットは、このトピックの後半で説明したように、監視を設定します。
- 高可用性の個別のフェールオーバー クラスターでファイル共有監視を使用することができます。
- 複数のクラスターで使用できるファイル共有
- フェールオーバー クラスタ リングの任意のバージョンでは、分散ファイル システム (DFS) 共有またはレプリケートされた記憶域の使用はサポートされていません。  これらには、クラスター化されたサーバーが相互に独立して実行しているし、データの損失が発生する可能性がありますスプリット ブレイン状況可能性があります。

## USB デバイスとルーターのファイル共有監視の作成

[Microsoft Ignite 2018](https://azure.microsoft.com/ignite/)年に[DataOn 記憶域](http://www.dataonstorage.com/)キオスク領域で、記憶域スペース ダイレクト クラスター必要があります。  このクラスターは、次のようなファイル共有監視として USB ポートを使用して[NetGear](https://www.netgear.com) Nighthawk X4S WiFi ルーターに接続されました。

![NetGear の監視](media\File-Share-Witness\FSW1.png)

この特定のルーターの USB デバイスを使用してファイル共有監視を作成する手順は次のとおりです。  その他のルーターや NAS アプライアンスの手順では異なります、ベンダーを使用して実行する必要がありますでは、ルート案内を提供します。


1. USB デバイスが接続されていると、ルーターにログインします。

   ![NetGear インターフェイス](media\File-Share-Witness\FSW2.png)

2. オプションの一覧で、共有を作成できるは ReadySHARE を選択します。

   ![NetGear ReadySHARE](media\File-Share-Witness\FSW3.png)

3. ファイル共有監視では、基本的な共有のために必要なすべてします。  USB デバイスの共有を作成する場所] ダイアログが表示されます Edit] ボタンを選択します。

   ![NetGear 共有インターフェイス](media\File-Share-Witness\FSW4.png)

4. [適用] ボタンを選択すると、共有が作成され、一覧で確認できます。

   ![NetGear 共有](media\File-Share-Witness\FSW5.png)

5. 共有が作成されたら、PowerShell ではクラスターのファイル共有監視の作成が行われます。

   ```PowerShell
   Set-ClusterQuorum -FileShareWitness \\readyshare\Witness -Credential (Get-Credential)
   ```

   これには、デバイスで、ローカル アカウントを入力します] ダイアログ ボックスが表示されます。

他のルーター USB 機能、NAS デバイス、またはその他の Windows デバイスでは、これらと同じような手順を実行できます。
