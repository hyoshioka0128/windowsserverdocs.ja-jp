---
title: 記憶域スペース ダイレクトのハードウェア要件
ms.prod: windows-server-threshold
description: 記憶域スペース ダイレクトをテストするための最小ハードウェア要件です。
ms.author: eldenc
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: eldenchristensen
ms.date: 06/04/2019
ms.localizationpriority: medium
ms.openlocfilehash: f2031afada302c0f73621a75f572c8547620db16
ms.sourcegitcommit: cd12ace92e7251daaa4e9fabf1d8418632879d38
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2019
ms.locfileid: "66501659"
---
# <a name="storage-spaces-direct-hardware-requirements"></a>記憶域スペース ダイレクトのハードウェア要件

> 適用対象:Windows Server 2019、Windows Server 2016

このトピックでは、記憶域スペース ダイレクトを使用するための最小ハードウェア要件について説明します。

運用環境で検証済みハードウェア/ソフトウェア ソリューションをパートナーから購入をお勧めは、展開ツールと手順がこれが含まれます。 これらのソリューションの設計、アセンブル、および互換性と取得するための信頼性と簡単に実行されているように、参照アーキテクチャの検証にしていること。 Windows Server 2019 ソリューションでは、次を参照してください。、 [solutions の web サイトを Azure Stack HCI](https://azure.microsoft.com/overview/azure-stack/hci)します。 Windows Server 2016 のソリューションの詳細については、について説明します。 [Windows Server ソフトウェア定義](https://microsoft.com/wssd)します。

![Windows Server ソフトウェア定義のパートナーのロゴ](media/hardware-requirements/wssd-partners.png)

   > [!TIP]
   > 記憶域スペース ダイレクトを評価するたいが、ハードウェアを持っていないでしょうか。 」の説明に従って、HYPER-V または Azure の仮想マシンを使用して[を使用して記憶域スペース ダイレクトでは、仮想マシンのゲスト クラスター](storage-spaces-direct-in-vm.md)します。

## <a name="base-requirements"></a>基本的な要件

システム、コンポーネント、デバイス、およびドライバーである必要があります**Windows Server 2016 認定**ごと、 [Windows Server Catalog](https://www.windowsservercatalog.com)します。 さらに、サーバー、ドライブ、ホスト バス アダプター、およびネットワーク アダプターが推奨、 **Software-Defined データ センター (SDDC) 標準**や**Software-Defined データ センター (SDDC) Premium**追加の制限 (AQs)、下図とがあります。 SDDC AQs と 1,000 を超えるコンポーネントがあります。

![SDDC AQs を示す Windows Server カタログのスクリーン ショット](media/hardware-requirements/sddc-aqs.png)

(サーバー、ネットワーク、および記憶域) は、完全に構成されたクラスターは、すべてを渡す必要があります[クラスター検証テストの](https://technet.microsoft.com/library/cc732035(v=ws.10).aspx)ウィザードでは、フェールオーバー クラスター マネージャーまたはにあたり、 `Test-Cluster` [コマンドレット](https://docs.microsoft.com/powershell/module/failoverclusters/test-cluster?view=win10-ps)powershell。

さらに、次の要件が適用されます。

## <a name="servers"></a>サーバー

- 2 台～ 16 台
- すべてのサーバーが、同じ製造元とモデルにすることをお勧めします

## <a name="cpu"></a>CPU

- Intel Nehalem または後で互換性のあるプロセッサ。または
- AMD EPYC または互換プロセッサを後で

## <a name="memory"></a>メモリ

- Windows Server、Vm、およびその他のアプリまたはワークロード; 用のメモリプラス
- 4 GB の記憶域スペース ダイレクトのメタデータの各サーバーで、キャッシュ ドライブ容量のテラバイト (TB) あたりの RAM

## <a name="boot"></a>Boot

- Windows Server でサポートされているすべてのブート デバイスを[SATADOM が含まれています](https://cloudblogs.microsoft.com/windowsserver/2017/08/30/announcing-support-for-satadom-boot-drives-in-windows-server-2016/)
- RAID 1 ミラーが**いない**ブートすることは必須ですが
- 推奨:200 GB の最小サイズ

## <a name="networking"></a>ネットワーク

最小値 (小規模な 2 ~ 3 ノード)
- 10 Gbps ネットワーク インターフェイス
- 2 ノードの直接接続 (スイッチレス ・) がサポートされています

(高パフォーマンス、スケール、または 4 + ノードのデプロイ) をお勧めします。
- (推奨) iWARP または RoCE はリモート ダイレクト メモリ アクセス (RDMA) 対応 Nic
- 冗長性とパフォーマンスのための 2 つまたは複数の Nic
- 25 Gbps ネットワーク インターフェイスまたはそれ以降

## <a name="drives"></a>ドライブ

直接接続された SATA、SAS、nvme ドライブと 1 台のサーバーに物理的に接続されている記憶域スペース ダイレクトは機能します。 ドライブ選択の他のヒントについては、「[ドライブの選択](choosing-drives.md)」をご覧ください。

- SATA、SAS、NVMe (M.2、U.2、およびカードでの登録) のドライブはすべてサポートされます。
- 512n、512 e、および 4 K ネイティブ ドライブのすべてをサポートします。
- ソリッド ステート ドライブを指定する必要があります[電力喪失の保護](https://blogs.technet.microsoft.com/filecab/2016/11/18/dont-do-it-consumer-ssd/)
- 同じ数と種類のすべてのサーバーでドライブを参照してください[ドライブ対称性に関する考慮事項。](drive-symmetry-considerations.md)
- キャッシュ デバイスは 32 GB である必要がありますまたはそれ以上
- キャッシュ デバイスとして永続的なメモリ デバイスを使用する場合は、NVMe または SSD の容量デバイス (Hdd を使用することはできません) を使用する必要があります。
- NVMe ドライバーでは、Microsoft のボックスは、または、NVMe ドライバーを更新します。
- 推奨:容量のドライブの数は、キャッシュ ドライブの数の倍数
- 推奨:キャッシュ ドライブの書き込み頻度の高い耐久性がある必要があります: には少なくとも 3 ドライブ書き込み-1 日 (DWPD) または 1 日あたりの (TBW) の記述で少なくとも 4 つのテラバイトを参照してください。[理解ドライブ書き込みます (DWPD) 1 日あたりテラバイトに書き込まれます (TBW) との最小値ストレージをお勧めします。スペース ダイレクト](https://blogs.technet.microsoft.com/filecab/2017/08/11/understanding-dwpd-tbw/)

記憶域スペース ダイレクトのドライブを接続する方法を次に示します。

- SATA ドライブの直接接続
- NVMe ドライブの直接接続
- SAS ドライブで SAS ホスト バス アダプター (HBA)
- SATA ドライブを使用した SAS ホスト バス アダプター (HBA)
- **サポートされていません。** RAID コント ローラー カードまたは SAN (ファイバ チャネル、iSCSI、FCoE) ストレージ。 ホスト バス アダプター (HBA) カードでは、単純なパススルー モードを実装する必要があります。

![サポートされているドライブのダイアグラムの相互接続します。](media/hardware-requirements/drive-interconnect-support-1.png)

ドライブ、サーバーの内部または外部のエンクロージャでは 1 つだけに接続されているサーバー。 SCSI エンクロージャ サービス (SES) は、スロットのマッピングと識別に必要です。 各外部エンクロージャでは、一意の識別子 (一意の ID) を示す必要があります。

- サーバーの内部ドライブ
- 1 つのサーバーに接続されている外部エンクロージャ ("JBOD") に存在するドライブします。
- **サポートされていません。** 共有の SAS エンクロージャは、複数のサーバーまたは任意の形式のマルチパス IO (MPIO) ドライブが複数のパスによってアクセス可能な場所に接続します。

![サポートされているドライブのダイアグラムの相互接続します。](media/hardware-requirements/drive-interconnect-support-2.png)

### <a name="minimum-number-of-drives-excludes-boot-drive"></a>ドライブの最小数 (ブート ドライブを除く)

- キャッシュとして使用するドライブがある場合、サーバーあたり 2 つ以上のドライブが必要です。
- サーバーあたり 4 つ以上のデータ格納用 (非キャッシュ) ドライブが必要です。

| 存在するドライブの種類   | 必要な最小数 |
|-----------------------|-------------------------|
| すべての永続的なメモリ (同じモデル) | 4 つの永続的なメモリ |
| すべて NVMe (同じモデル) | 4 つの NVMe                  |
| すべて SSD (同じモデル)  | 4 つの SSD                   |
| または、永続的なメモリ + NVMe SSD | 2 つの永続的なメモリ + 4 NVMe または SSD |
| NVMe + SSD            | 2 つの NVMe + 4 つの SSD          |
| NVMe + HDD            | 2 つの NVMe + 4 つの HDD          |
| SSD + HDD             | 2 つの SSD + 4 つの HDD           |
| NVMe + SSD + HDD      | 2 つの NVMe + 4 つのそれ以外のドライブ       |

   >[!NOTE]
   > この表では、ハードウェアのデプロイの最小値を示します。 仮想化と仮想マシンを展開する場合など、Microsoft Azure storage を参照してください[を使用して記憶域スペース ダイレクトでは、仮想マシンのゲスト クラスター](storage-spaces-direct-in-vm.md)します。

### <a name="maximum-capacity"></a>最大容量

| 最大値                | Windows Server 2019  | Windows Server 2016  |
| ---                     | ---------            | ---------            |
| サーバーごとの生の容量 | 100 TB               | 100 TB               |
| プールの容量           | 4 PB (4,000 TB)      | 1 PB                 |