---
title: 記憶域スペース ダイレクトのハードウェア要件
ms.prod: windows-server
description: 記憶域スペース ダイレクトをテストするための最小ハードウェア要件です。
ms.author: eldenc
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: eldenchristensen
ms.date: 08/05/2019
ms.localizationpriority: medium
ms.openlocfilehash: 42022b6e2e3564d1440e2ba1d45f9f98430242c0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861055"
---
# <a name="storage-spaces-direct-hardware-requirements"></a>記憶域スペース ダイレクトのハードウェア要件

> 適用対象: Windows Server 2019、Windows Server 2016

このトピックでは、記憶域スペース ダイレクトを使用するための最小ハードウェア要件について説明します。

運用環境では、Microsoft のパートナーから検証済みのハードウェア/ソフトウェアソリューションを購入することをお勧めします。これには、展開ツールと手順が含まれます。 これらのソリューションは、互換性と信頼性を確保するために、参照アーキテクチャに対して設計、組み立て、検証を行い、迅速に稼働させることができます。 Windows Server 2019 ソリューションについては、 [AZURE STACK HCI solutions の web サイト](https://azure.microsoft.com/overview/azure-stack/hci)を参照してください。 Windows Server 2016 ソリューションの詳細については、「 [Windows Server Software Defined](https://microsoft.com/wssd)」を参照してください。

   > [!TIP]
   > 記憶域スペースダイレクト評価するが、ハードウェアがない場合は、 「[ゲスト仮想マシンクラスターでの記憶域スペースダイレクトの使用](storage-spaces-direct-in-vm.md)」の説明に従って、hyper-v または Azure の仮想マシンを使用します。

## <a name="base-requirements"></a>基本要件

システム、コンポーネント、デバイス、およびドライバーは、windows [Server カタログ](https://www.windowsservercatalog.com)に従って**Windows server 2016 認定**を受ける必要があります。 さらに、以下に示すように、サーバー、ドライブ、ホストバスアダプター、およびネットワークアダプターには、**ソフトウェア定義データセンター (sddc) 標準**または**ソフトウェア定義データセンター (sddc) Premium**追加の要件 (aqs) があることをお勧めします。 これには、1000以上のコンポーネントが含まれています。

![SDDC が表示されている Windows Server カタログのスクリーンショット](media/hardware-requirements/sddc-aqs.png)

完全に構成されたクラスター (サーバー、ネットワーク、および記憶域) は、フェールオーバークラスターマネージャーのウィザードに従って、または PowerShell の `Test-Cluster`[コマンドレット](https://docs.microsoft.com/powershell/module/failoverclusters/test-cluster?view=win10-ps)を使用して、すべての[クラスター検証テスト](https://technet.microsoft.com/library/cc732035(v=ws.10).aspx)に合格する必要があります。

また、次の要件が適用されます。

## <a name="servers"></a>[サーバー]

- 2 台～ 16 台
- すべてのサーバーを同じ製造元およびモデルにすることをお勧めします。

## <a name="cpu"></a>CPU

- Intel Nehalem 以降の互換性のあるプロセッサ。もしくは
- AMD EPYC 以降の互換性のあるプロセッサ

## <a name="memory"></a>メモリ

- Windows Server、Vm、およびその他のアプリやワークロード用のメモリ足
- 各サーバーのキャッシュドライブ容量が 1 tb あたり 4 GB の RAM (記憶域スペースダイレクトメタデータ用)

## <a name="boot"></a>Boot

- Windows Server でサポートされているすべてのブートデバイスで、 [SATADOM が含まれるようになりました](https://cloudblogs.microsoft.com/windowsserver/2017/08/30/announcing-support-for-satadom-boot-drives-in-windows-server-2016/)。
- RAID 1 ミラーは必要**ありません**が、ブートではサポートされています。
- 推奨: 200 GB の最小サイズ

## <a name="networking"></a>ネットワーク

記憶域スペースダイレクトには、信頼性の高い高帯域幅、低待機時間の各ノード間のネットワーク接続が必要です。  

Small scale 2-3 ノードの最小相互接続
- 10 Gbps ネットワークインターフェイスカード (NIC)、またはより高速
- 冗長性とパフォーマンスのために推奨される各ノードからの2つ以上のネットワーク接続

4 + の高パフォーマンス、大規模、またはデプロイのために推奨される相互接続 
- リモートダイレクトメモリアクセス (RDMA) 対応の Nic、iWARP (推奨) または RoCE
- 冗長性とパフォーマンスのために推奨される各ノードからの2つ以上のネットワーク接続
- 25 Gbps NIC 以上

スイッチまたは switchless ノードの相互接続
- スイッチ: ネットワークスイッチが帯域幅とネットワークの種類を処理するように適切に構成されている必要があります。  RoCE プロトコルを実装する RDMA を使用している場合は、ネットワークデバイスとスイッチの構成がさらに重要になります。 
- Switchless: ノードは、直接接続を使用して相互接続できます。スイッチの使用は避けてください。  すべてのノードがクラスターの他のすべてのノードと直接接続している必要があります。


## <a name="drives"></a>ドライブ

記憶域スペースダイレクトは、1台のサーバーに物理的に接続されている直接接続 SATA、SAS、または NVMe ドライブに対応しています。 ドライブ選択の他のヒントについては、「[ドライブの選択](choosing-drives.md)」をご覧ください。

- SATA、SAS、NVMe (M. 2、米国2、およびカードの追加) ドライブがすべてサポートされます。
- 512n、512n、および4K のネイティブドライブがすべてサポートされています。
- ソリッドステートドライブは[、電源損失保護を](https://blogs.technet.microsoft.com/filecab/2016/11/18/dont-do-it-consumer-ssd/)提供する必要があります。
- すべてのサーバーで同じ数と種類のドライブ–[ドライブの対称に関する考慮事項](drive-symmetry-considerations.md)を参照してください。
- キャッシュデバイスは 32 GB 以上である必要があります
- 永続メモリデバイスをキャッシュデバイスとして使用する場合は、NVMe または SSD 容量デバイスを使用する必要があります (Hdd は使用できません)。
- NVMe ドライバーは、Windows に付属している Microsoft 提供のドライバーです。 (stornvme .sys)
- 推奨: 容量ドライブの数は、キャッシュドライブの数の倍数になります。
- 推奨: キャッシュドライブには、1日あたり少なくとも3つのドライブ書き込み (DWPD)、または少なくとも4テラバイトの書き込み (tbw) が必要です。1日[あたり記憶域スペースダイレクトのドライブの書き込み量 (dwpd)、テラバイトの書き込み (TBW)、および推奨される最小値](https://blogs.technet.microsoft.com/filecab/2017/08/11/understanding-dwpd-tbw/)について確認してください。

ドライブを記憶域スペースダイレクトに接続する方法を次に示します。

- 直接接続 SATA ドライブ
- 直接接続されている NVMe ドライブ
- Sas ドライブを使用する SAS ホストバスアダプター (HBA)
- SATA ドライブを搭載した SAS ホストバスアダプター (HBA)
- **サポートされていない:** RAID コントローラーカードまたは SAN (ファイバーチャネル、iSCSI、FCoE) ストレージ。 ホストバスアダプター (HBA) カードは、単純なパススルーモードを実装する必要があります。

![サポートされているドライブの相互接続の図](media/hardware-requirements/drive-interconnect-support-1.png)

ドライブは、サーバーの内部、または1台のサーバーに接続されている外部エンクロージャに存在することができます。 スロットのマッピングと識別には SCSI エンクロージャサービス (SES) が必要です。 各外部エンクロージャは、一意の識別子 (一意の ID) を提示する必要があります。

- サーバー内部のドライブ
- 1つのサーバーに接続されている外部エンクロージャ ("JBOD") 内のドライブ
- **サポートされていない:** 複数のサーバーに接続されている共有 SAS エンクロージャ、または複数のパスからドライブにアクセスできる任意の形式のマルチパス IO (MPIO)。

![サポートされているドライブの相互接続の図](media/hardware-requirements/drive-interconnect-support-2.png)

### <a name="minimum-number-of-drives-excludes-boot-drive"></a>ドライブの最小数 (ブートドライブを除く)

- キャッシュとして使用するドライブがある場合、サーバーあたり 2 つ以上のドライブが必要です。
- サーバーあたり 4 つ以上のデータ格納用 (非キャッシュ) ドライブが必要です。

| 存在するドライブの種類   | 必要な最小数 |
|-----------------------|-------------------------|
| すべての永続メモリ (同じモデル) | 4永続メモリ |
| すべて NVMe (同じモデル) | 4 つの NVMe                  |
| すべて SSD (同じモデル)  | 4 つの SSD                   |
| 永続メモリ + NVMe または SSD | 2永続メモリ + 4 NVMe または SSD |
| NVMe + SSD            | 2 つの NVMe + 4 つの SSD          |
| NVMe + HDD            | 2 つの NVMe + 4 つの HDD          |
| SSD + HDD             | 2 つの SSD + 4 つの HDD           |
| NVMe + SSD + HDD      | 2 つの NVMe + 4 つのそれ以外のドライブ       |

   >[!NOTE]
   > 次の表は、ハードウェア展開の最小値を示しています。 Microsoft Azure など、仮想マシンおよび仮想化された記憶域を使用してデプロイする場合は、「[ゲスト仮想マシンクラスターでの記憶域スペースダイレクトの使用](storage-spaces-direct-in-vm.md)」を参照してください。

### <a name="maximum-capacity"></a>最大容量

| 最大                | Windows Server 2019  | Windows Server 2016  |
| ---                     | ---------            | ---------            |
| サーバーあたりの生の容量 | 400 TB               | 100 TB               |
| プールの容量           | 4 PB (4000 TB)      | 1 PB                 |
