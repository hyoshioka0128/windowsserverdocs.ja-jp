---
title: 記憶域スペース ダイレクトのハードウェア要件
ms.prod: windows-server-threshold
description: 記憶域スペース ダイレクトをテストするための最小ハードウェア要件です。
ms.author: eldenc
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: eldenchristensen
ms.date: 04/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 84d10ab3e25500720dd13e2ba057dc3c5bf05a6f
ms.sourcegitcommit: 515b4fd5c40fcbae0e12a2c30090384533972353
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/29/2018
ms.locfileid: "8232531"
---
# 記憶域スペース ダイレクトのハードウェア要件

> 適用対象: Windows Server 2016、Windows Server Insider Preview

このトピックでは、記憶域スペース ダイレクトを使用するための最小ハードウェア要件について説明します。

Microsoft、運用環境には、展開ツールと手順が含まれるパートナーからこれらの[Windows Server ソフトウェア定義](https://microsoft.com/wssd)のハードウェア/ソフトウェア製品ことをお勧めします。 オブジェクトは設計、アセンブル、および互換性と取得するための信頼性とすばやく実行していることを確認するには、当社の参照をアーキテクチャに対して検証します。 詳しくは、[https://microsoft.com/wssd](https://microsoft.com/wssd) をご覧ください。

![Windows Server ソフトウェア定義のパートナーのロゴ](media/hardware-requirements/wssd-partners.png)

   > [!TIP]
   > 記憶域スペース ダイレクトを評価したいが、ハードウェアがないかどうか。 [使用して記憶域スペース ダイレクトでは、ゲスト仮想マシン クラスター](storage-spaces-direct-in-vm.md)で説明したようには、HYPER-V または Azure の仮想マシンを使用します。

## 基本の要件

システム、コンポーネント、デバイス、およびドライバーは、 **Windows Server 2016 の認定**を[Windows Server Catalog](https://www.windowsservercatalog.com)ごとである必要があります。 さらに、お勧めしますが、サーバー、ドライブ、ホスト バス アダプター、およびネットワーク アダプターある、 **Software-Defined データ センター (SDDC) の標準**や**Software-Defined データ センター (SDDC) Premium**の追加の条件 (AQs) になっている場合は以下に。 SDDC AQs の 1,000 人を超えるコンポーネントがあります。

![SDDC AQs を示す Windows Server catalog のスクリーン ショット](media/hardware-requirements/sddc-aqs.png)

完全に構成されたクラスター (サーバー、ネットワーク、および記憶域) は、フェールオーバー クラスター マネージャーでまたはウィザードごとにすべての[クラスター検証テスト](https://technet.microsoft.com/library/cc732035(v=ws.10).aspx)に渡す必要があります、 `Test-Cluster` PowerShell の[コマンドレット](https://docs.microsoft.com/powershell/module/failoverclusters/test-cluster?view=win10-ps)です。

さらに、次の要件が適用されます。

## サーバー

- 最低 2 台のサーバー、最大 16 台のサーバー
- すべてのサーバーを同じ製造元とモデルをお勧めします

## CPU

- Intel Nehalem または以降の互換プロセッサ。または
- AMD EPYC または以降の互換プロセッサ

## メモリ

- Windows Server、Vm では、およびその他のアプリやワークロード; メモリプラス
- 4 GB の RAM ごとの記憶域スペース ダイレクト メタデータの各サーバーで、キャッシュ ドライブ容量テラバイト (TB)

## Boot

- [SATADOM が追加されました](https://cloudblogs.microsoft.com/windowsserver/2017/08/30/announcing-support-for-satadom-boot-drives-in-windows-server-2016/)が、Windows Server でサポートされている任意のブート デバイス
- RAID 1 ミラーは必須では**ありません**が、ブートがサポートされています。
- 200 GB の最小サイズをお勧めします。

## ネットワーク

(小規模な 2 ~ 3 ノード) 用の最小値
- 10 Gbps のネットワーク インターフェイス
- 2 ノードに直接接続 (スイッチレス) がサポートされています。

(スケール、または 4 つ以上のノードの展開での高パフォーマンス) をお勧めします。
- (推奨) iWARP または RoCE のリモート ダイレクト メモリ アクセス (RDMA) 対応である Nic
- 冗長性とパフォーマンスのための 2 つ以上の Nic
- 25 Gbps のネットワーク インターフェイス以上

## ドライブ

記憶域スペース ダイレクトの直接接続の SATA、SAS、または NVMe ドライブ 1 台のサーバーに物理的に接続されていると連携します。 ドライブ選択の他のヒントについては、「[ドライブの選択](choosing-drives.md)」をご覧ください。

- これは、SATA、SAS、NVMe (M.2、U.2、およびカードでの登録) すべてサポートされているドライブ
- 512n、512 e、および 4 K ネイティブのドライブのすべてをサポートします。
- ソリッドステート ドライブが[電源障害の保護](https://blogs.technet.microsoft.com/filecab/2016/11/18/dont-do-it-consumer-ssd/)を提供する必要があります。
- 同じ数と種類のすべてのサーバーでドライブは、[ドライブの対称性に関する考慮事項](drive-symmetry-considerations.md)を参照してください。
- NVMe ドライバーは、Microsoft のボックスは、または NVMe ドライバーを更新します。
- 推奨: データ格納用ドライブの数は、キャッシュ ドライブの数の倍数
- 推奨: キャッシュ ドライブする必要がありますが高い書き込み耐久性: 3 以上ドライブの書き込み-1 日あたり (DWPD) または日当たりの tbw () – 1 日あたり 4 つ以上のテラバイト[drive writes per day DWPD ()、書き込みテラバイト数 (TBW) の推奨最小を記憶域を参照してくださいスペース ダイレクト](https://blogs.technet.microsoft.com/filecab/2017/08/11/understanding-dwpd-tbw/)

記憶域スペース ダイレクトのドライブを接続する方法を次に示します。

1. SATA ドライブの直接接続
2. 直接接続された最新の NVMe ドライブ
3. SAS ドライブと SAS ホスト バス アダプター (HBA)
4. SATA ドライブと SAS ホスト バス アダプター (HBA)
5. **サポートされていません:** RAID コント ローラー カードまたは SAN (ファイバー チャネル、iSCSI、FCoE) 記憶域。 ホスト バス アダプター (HBA) カードには、単純なパススルー モードを実装する必要があります。

![サポートされているドライブの図が相互接続します。](media/hardware-requirements/drive-interconnect-support-1.png)

ドライブは、サーバーに内部または外部の筐体の 1 つだけに接続されているサーバーです。 SCSI エンクロージャ サービス (SES) は、スロット マッピングと識別必要があります。 各外部の筐体には、一意の識別子 (一意の ID) を表示する必要があります。

1. 内部サーバーのドライブ
2. 1 台のサーバーに接続されている外部エンクロージャ ("JBOD") でドライブします。
3. **サポートされていません:** 共有 SAS エンクロージャを複数のサーバーまたは任意の形式のマルチパス IO (MPIO) ドライブに複数のパスを使用してアクセスできる場所に接続されます。

![サポートされているドライブの図が相互接続します。](media/hardware-requirements/drive-interconnect-support-2.png)

### ドライブの最小数 (ブート ドライブを除く)

- キャッシュとして使用するドライブがある場合、サーバーあたり 2 つ以上のドライブが必要です。
- サーバーあたり 4 つ以上のデータ格納用 (非キャッシュ) ドライブが必要です。

| 存在するドライブの種類   | 必要な最小数 |
|-----------------------|-------------------------|
| すべて NVMe (同じモデル) | 4 つの NVMe                  |
| すべて SSD (同じモデル)  | 4 つの SSD                   |
| NVMe + SSD            | 2 つの NVMe + 4 つの SSD          |
| NVMe + HDD            | 2 つの NVMe + 4 つの HDD          |
| SSD + HDD             | 2 つの SSD + 4 つの HDD           |
| NVMe + SSD + HDD      | 2 つの NVMe + 4 つのそれ以外のドライブ       |

   >[!NOTE]
   > 次の表は、ハードウェア展開では、最小値を提供します。 仮想マシンを展開して、記憶域をなど、Microsoft azure では、仮想化する場合[を使用して記憶域スペース ダイレクトでは、ゲスト仮想マシンのクラスター](storage-spaces-direct-in-vm.md)を参照してください。

### 最大容量

- サーバーあたり最大 100 テラバイト (TB) 生の記憶域容量をお勧めします。
- 最大 1 ペタバイト (1,000 TB) 生の容量、記憶域プール
