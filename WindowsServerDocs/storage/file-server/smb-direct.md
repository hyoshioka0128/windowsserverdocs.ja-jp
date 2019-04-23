---
title: SMB ダイレクトとファイル サーバーのパフォーマンスを向上させる
description: Windows Server 2012 R2、Windows Server 2012、および Windows Server 2016 で SMB ダイレクトの機能について説明します。
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 04/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: ed8fd5b4114fc9fd9c7dc278a98cea8cc67a8749
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826443"
---
# <a name="smb-direct"></a>SMB ダイレクト

>適用対象:Windows Server 2012 R2、Windows Server 2012、Windows Server 2016

Windows Server 2012 R2、Windows Server 2012、および Windows Server 2016 には、リモート ダイレクト メモリ アクセス (RDMA) 機能を搭載するネットワーク アダプターの使用をサポートする SMB ダイレクトと呼ばれる機能が含まれます。 RDMA を搭載するネットワーク アダプターは、遅延がきわめて小さく、CPU をほとんど使用せずに、最高速度で動作できます。 Hyper-V や Microsoft SQL Server などのワークロードについては、この機能によってリモート ファイル サーバーをローカル ストレージのように利用することができます。 SMB ダイレクトの特徴を以下に示します。

- スループットの向上:ネットワーク アダプターが回線速度で大量のデータの転送を調整する高速ネットワークの完全スループットを活用します。
- 低い待機時間:ネットワーク要求に対する応答が非常に高速であるため、リモート ファイル記憶域を、直接接続されたブロック記憶域のような感覚で使用できます。
- 低い CPU 使用率:データをネットワークで転送するときに使用される CPU サイクルを節約して、サーバー アプリケーションで使用できる処理能力を増やすことができます。

SMB ダイレクトは、Windows Server 2012 R2 と Windows Server 2012 では構成に自動的に。

## <a name="smb-multichannel-and-smb-direct"></a>SMB マルチチャネルと SMB ダイレクト

SMB マルチチャネルとは、ネットワーク アダプターの RDMA 機能を検出して SMB ダイレクトを有効にする機能です。 SMB マルチチャネルを使用しない場合は、RDMA 対応ネットワーク アダプターで通常の TCP/IP が使用されます (すべてのネットワーク アダプターで、新しい RDMA スタックと共に TCP/IP スタックが提供されます)。

SMB マルチチャネルを使用する場合は、ネットワーク アダプターに RDMA 機能が搭載されているかどうかが検出され、その 1 つのセッションに対して複数の RDMA 接続 (インターフェイスごとに 2 つ) が作成されます。 これにより、RDMA 対応ネットワーク アダプターによって提供される高スループット、低待機時間、低 CPU 使用率の利点を SMB で活用できるようになります。 複数の RDMA インターフェイスを使用している場合は、フォールト トレランスも提供されます。

>[!NOTE]
>RDMA 機能を使用する場合は、RDMA 対応ネットワーク アダプターをチーム化しないでください。 チーム化すると、ネットワーク アダプターで RDMA がサポートされなくなります。
>1 つ以上の RDMA ネットワーク接続が作成されると、最初のプロトコル ネゴシエーションに使用された TCP/IP 接続は使用されなくなります。 ただし、RDMA ネットワーク接続に障害が発生した場合は、TCP/IP 接続が維持されます。

## <a name="requirements"></a>要件

SMB ダイレクトの要件は次のとおりです。

- Windows Server 2012 R2 または Windows Server 2012 を実行している少なくとも 2 つのコンピューター
- RDMA 機能を搭載しているネットワーク アダプター 1 つ以上。

### <a name="considerations-when-using-smb-direct"></a>SMB ダイレクトを使用する場合の考慮事項

- SMB ダイレクトはフェールオーバー クラスターで使用できますが、クライアント アクセスに使用するクラスター ネットワークが SMB ダイレクトに適していることを確認する必要があります。 フェールオーバー クラスタリングでは、クライアント アクセスに複数のネットワークを使用することも、RSS (Receive Side Scaling) 対応および RDMA 対応のネットワーク アダプターを使用することもサポートされています。
- Hyper-V 管理オペレーティング システムで SMB ダイレクトを使用して、Hyper-V over SMB を使用できるようにしたり、Hyper-V 記憶域スタックを使用する仮想マシンに記憶域を提供したりできます。 ただし、RDMA 対応ネットワーク アダプターは Hyper-V クライアントに直接公開されません。 RDMA 対応ネットワーク アダプターを仮想スイッチに接続すると、そのスイッチからの仮想ネットワーク アダプターは RDMA 対応ではなくなります。
- SMB マルチチャネルを無効にすると、SMB ダイレクトも無効になります。 SMB マルチチャネルによって、ネットワーク アダプターの機能が検出され、ネットワーク アダプターが RDMA 対応かどうかが確認されるため、SMB マルチチャネルが無効になっていると、クライアントが SMB ダイレクトを使用できません。
- SMB ダイレクトではサポートされません Windows RT. SMB ダイレクト サポートを必要と rdma 対応ネットワーク アダプターでは、これは Windows Server 2012 R2 および Windows Server 2012 でのみ使用できます。
- SMB ダイレクトは、ダウンレベル バージョンの Windows Server ではサポートされていません。 これは、Windows Server 2012 R2 および Windows Server 2012 でのみサポートされます。

## <a name="enabling-and-disabling-smb-direct"></a>SMB ダイレクトを有効および無効にする

SMB ダイレクトを有効に既定で Windows Server 2012 R2 または Windows Server 2012 がインストールされている場合。 SMB クライアントは、適切な構成が見つかると、自動的に複数のネットワーク接続を検出して使用します。

### <a name="disable-smb-direct"></a>直接 SMB を無効にします。

通常は、SMB ダイレクトを無効にする必要はありませんが、無効にする場合は、次のいずれかの Windows PowerShell スクリプトを実行します。

特定のインターフェイスで RDMA を無効にするには、次のように入力します。

```PowerShell
Disable-NetAdapterRdma <name>
```

すべてのインターフェイスで RDMA を無効にするには、次のように入力します。

```PowerShell
Set-NetOffloadGlobalSetting -NetworkDirect Disabled
```

クライアントかサーバーのいずれかで RDMA を無効にすると、RDMA を使用できなくなります。 *Network Direct* RDMA インターフェイスの基本的なネットワーク サポートを Windows Server 2012 R2 および Windows Server 2012 の内部名です。

### <a name="re-enable-smb-direct"></a>再度直接 SMB を有効にします。

RDMA を無効にした後、再び有効にするには、次のいずれかの Windows PowerShell スクリプトを実行します。

特定のインターフェイスで RDMA を再び有効にするには、次のように入力します。

```PowerShell
Enable-NetAdapterRDMA <name>
```

すべてのインターフェイスで RDMA を再び有効にするには、次のように入力します。

```PowerShell
Set-NetOffloadGlobalSetting -NetworkDirect Enabled
```

RDMA の使用を再開するには、クライアントとサーバーの両方で RDMA を有効にする必要があります。

## <a name="test-performance-of-smb-direct"></a>SMB ダイレクトのパフォーマンスをテストする

パフォーマンスをテストするには、次のいずれかの手順に従います。

### <a name="compare-a-file-copy-with-and-without-using-smb-direct"></a>SMB ダイレクトを使用する場合と使用しない場合のファイル コピーのパフォーマンスを比較する

SMB ダイレクトのスループットを測定する方法を次に示します。

1. SMB ダイレクトを構成します。
2. SMB ダイレクトを使用して大きなファイル コピーを実行して、所要時間を測定します。
3. ネットワーク アダプターで RDMA を無効にします (「[SMB ダイレクトを有効および無効にする](#enabling-and-disabling-smb-direct)」を参照)。
4. SMB ダイレクトを使用せずに大きなファイル コピーを実行して、所要時間を測定します。
5. ネットワーク アダプターで再び RDMA を有効にし、2 つの結果を比較します。
6. キャッシュが結果に影響しないようにするために、次の操作を行う必要があります。
    1. 大量 (メモリで処理できる量を上回る量) のデータをコピーします。
    2. データを 2 回コピーします。1 回目は練習として、2 回目に時間を測定します。
    3. テストの前に毎回サーバーとクライアントの両方を再起動して、同様の条件でテストできるようにします。

### <a name="fail-one-of-multiple-network-adapters-during-a-file-copy-with-smb-direct"></a>SMB ダイレクトを使用してファイルをコピーしているときにいずれかのネットワーク アダプターに障害が発生した状況をシミュレートする

SMB ダイレクトのフェールオーバー機能を確認する方法を次に示します。

1. SMB ダイレクトが複数のネットワーク アダプターの構成で機能していることを確認します。
2. 大きなファイル コピーを実行します。 コピーの実行中にいずれかのケーブルを外して (または、いずれかのネットワーク アダプターを無効にして)、いずれかのネットワーク パスで障害が発生した状況をシミュレートします。
3. 残ったネットワーク アダプターのいずれかを使用してファイルのコピーが続行され、ファイル コピー エラーが発生しないことを確認します。

>[!NOTE]
>SMB ダイレクトを使用しないワークロードが失敗しないようにするには、切断されたネットワーク パスを使用しているワークロードがほかにないことを確認します。

## <a name="more-information"></a>詳細情報

- [サーバー メッセージ ブロックの概要](file-server-smb-overview.md)
- [サーバー、ストレージ、およびネットワークの可用性の向上。シナリオの概要](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831437(v%3dws.11)>)
- [SMB 経由での Hyper V を展開します。](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134187(v%3dws.11)>)
