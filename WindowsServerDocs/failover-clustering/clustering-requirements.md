---
title: フェールオーバー クラスタ リングのハードウェア要件と記憶域オプション
description: ハードウェア要件とフェールオーバー クラスターを作成するためのストレージ オプション。
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 04/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: e6eb6f2acd420ae657a5c1b698e9733751378552
ms.sourcegitcommit: ed27ddbe316d543b7865bc10590b238290a2a1ad
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/09/2019
ms.locfileid: "65476085"
---
# <a name="failover-clustering-hardware-requirements-and-storage-options"></a>フェールオーバー クラスタ リングのハードウェア要件と記憶域オプション

適用対象:Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

フェールオーバー クラスターを作成するには、次のハードウェアが必要です。 Microsoft でサポートされるために、すべてのハードウェアが実行している Windows Server のバージョン用に認定されている必要があり、フェールオーバー クラスター ソリューション全体が構成の検証ウィザードのすべてのテストに合格する必要があります。 フェールオーバー クラスターの検証の詳細については、「 [Validate Hardware for a Failover Cluster](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134244(v%3dws.11)>)」を参照してください。

- **サーバー**:同一または類似したコンポーネントで構成された一連のコンピューターを使用することをお勧めします。
- **ネットワーク アダプターおよびケーブル (ネットワーク通信用)** :iSCSI を使用する場合は、各ネットワーク アダプターを、ネットワーク通信と iSCSI の両方ではなく、いずれか専用にする必要があります。

    クラスター ノードを接続するネットワーク インフラストラクチャでは、単一障害点を回避する必要があります。 たとえば、複数の個別のネットワークを使用してクラスター ノードを接続する方法があります。 または、チーム化されたネットワーク アダプター、冗長なスイッチ、冗長なルーター、または単一障害点を除去するハードウェアで作成されますが、1 つのネットワークとクラスター ノードを接続できます。

    >[!NOTE]
    >単一のネットワークにクラスター ノードを接続すると、このネットワークは構成の検証ウィザードの冗長性要件に適合します。 ただし、このウィザードのレポートには、ネットワークに単一障害点が含まれないようにする必要があることを示す警告が含まれます。

- **記憶域用のデバイス コントローラーまたは適切なアダプター**:

  - **Serial Attached SCSI またはファイバー チャネル**:Serial Attached SCSI またはファイバー チャネルを使用する場合、クラスター化されたすべてのサーバーで、記憶域スタックにすべて同一の要素を使用する必要があります。 必要なは、マルチパス I/O (MPIO) ソフトウェアが同一であることと、デバイス固有モジュール (DSM) ソフトウェアが同一であること。 お勧めする大容量記憶装置コント ローラー-ホスト バス アダプター (HBA)、HBA ドライバー、および HBA ファームウェア-に接続されているクラスター記憶域が同一で。 異なる HBA を使用する場合は、サポートされる構成または推奨される構成に従っていることを記憶域の製造元に確認する必要があります。
  - **iSCSI**:iSCSI を使用する場合は、クラスター化されたサーバーごとに、クラスター記憶域専用のネットワーク アダプターまたは HBA が 1 つまたは複数必要です。 iSCSI に使用するネットワークは、ネットワーク通信には使用できません。 クラスター化されたすべてのサーバーで、iSCSI 記憶域ターゲットへの接続に同一のネットワーク アダプターを使用する必要があります。ギガビット イーサネット以上の通信規格を使用することをお勧めします。
- **記憶域**:使用する必要があります[記憶域スペース ダイレクト](../storage/storage-spaces/storage-spaces-direct-overview.md)または Windows Server 2012 R2 または Windows Server 2012 と互換性がある記憶域を共有します。 接続されている共有記憶域を使用して、HYPER-V を実行しているフェールオーバー クラスターで構成されているサーバーの共有記憶域として SMB 3.0 ファイル共有を使用することもできます。 詳細については、「[Hyper-V over SMB の展開](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134187(v%3dws.11)>)」を参照してください。

    通常、アタッチされる記憶域には、ハードウェア レベルで構成されている複数の個別のディスク (論理ユニット番号 (LUN)) が含まれている必要があります。 一部のクラスターでは、これらのディスクの 1 つがディスク監視として機能します (ディスク監視については、このサブセクションの最後で説明します)。 他のディスクには、クラスター役割 (以前のクラスター化されたサービスまたはアプリケーション) に必要なファイルが含まれます。 記憶域の要件を次に示します。

  - フェールオーバー クラスタリングに含まれるネイティブのディスク サポートを利用するには、ダイナミック ディスクではなくベーシック ディスクを使用してください。
  - NTFS でパーティションをフォーマットすることをお勧めします。 クラスターの共有ボリューム (CSV) を使用する場合は、それらのすべてのパーティションが NTFS である必要があります。

    >[!NOTE]
    >クォーラム構成用にディスク監視を使用する場合は、ディスクを NTFS または Resilient File System (ReFS) のいずれかでフォーマットできます。

  - ディスクのパーティション スタイルとして、マスター ブート レコード (MBR) と GUID パーティション テーブル (GPT) のいずれかを使用できます。

    ディスクのミラーリング監視サーバーは、クラスター構成データベースのコピーを保持するように指定されたクラスター記憶域ディスクです。 フェールオーバー クラスターには、クォーラム構成の一部として指定されている場合にのみディスク監視が与えられます。 詳細については、次を参照してください。[記憶域スペース ダイレクトでのクォーラムの理解](../storage/storage-spaces/understand-quorum.md)します。

## <a name="hardware-requirements-for-hyper-v"></a>Hyper-V のハードウェア要件

クラスター化された仮想マシンが含まれるフェールオーバー クラスターを作成する場合、クラスター サーバーは Hyper-V の役割のハードウェア要件を満たしている必要があります。 Hyper-V には、次のものを含む 64 ビット プロセッサが必要です。

- ハードウェア補助による仮想化。 これは、仮想化オプションが組み込まれたプロセッサ、特に、Intel バーチャライゼーション テクノロジ (Intel VT) または AMD Virtualization (AMD-V) テクノロジを備えたプロセッサで使用できます。
- ハードウェアによるデータ実行防止 (DEP) が利用でき、有効にされていることが必要です。 具体的には、Intel XD ビット (execute disable bit) または AMD NX ビット (no execute bit) を有効にする必要があります。

Hyper-V の役割の詳細については、「 [Hyper-V の概要](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831531(v%3dws.11)>)」を参照してください。

## <a name="deploying-storage-area-networks-with-failover-clusters"></a>フェールオーバー クラスターを備えた記憶域ネットワークの展開

フェールオーバー クラスターを備えた記憶域ネットワーク (SAN) を展開するときは、次のガイドラインに従ってください。

- **記憶域の互換性を確認する**:記憶域 (記憶域に使用するドライバー、ファームウェア、およびソフトウェアを含む) に、実行している Windows Server のバージョンのフェールオーバー クラスターとの互換性があるかどうかを製造元に確認してください。
- **1 つのクラスターで 1 つの記憶装置を使用する**:異なるクラスターのサーバーが同一の記憶装置にアクセスしないようにしてください。 ほとんどの場合、LUN マスキングまたはゾーニングにより、1 つのクラスター サーバー セットに使用される LUN を、その他のすべてのサーバーから分離する必要があります。
- **マルチパス I/O ソフトウェアまたはチーム化されたネットワーク アダプターの使用を検討する**:可用性の高い記憶域ファブリックでは、マルチパス I/O ソフトウェアまたはネットワーク アダプターのチーム化 (負荷分散とフェールオーバー (LBFO) とも呼ばれます) を使用して、複数のホスト バス アダプターを備えたフェールオーバー クラスターを展開できます。 これによって、冗長性と可用性を最大限に引き出すことができます。 Windows Server 2012 R2 または Windows Server 2012 では、マルチパス ソリューションを Microsoft マルチパス I/O (MPIO) に基づく必要があります。 通常は、ハードウェアに対応した MPIO デバイス固有モジュール (DSM) がハードウェアの製造元から提供されますが、Windows Server にはオペレーティング システムの一部として 1 つ以上の DSM が組み込まれています。

    LBFO については、次を参照してください。 [NIC チーミングの概要](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nic-teaming)、Windows Server テクニカル ライブラリにします。

    >[!IMPORTANT]
    >ホスト バス アダプターとマルチパス I/O ソフトウェアは、バージョンの違いが原因で正しく機能しない場合があります。 クラスターにマルチパス ソリューションを実装する場合は、ハードウェアの製造元に相談して、実行している Windows Server のバージョンに対応した正しいアダプター、ファームウェア、およびソフトウェアを選択してください。

- **記憶域スペースの使用を検討する**:Serial attached SCSI (SAS) クラスター化された記憶域、記憶域スペースを使用して構成をデプロイする予定の場合を参照してください[Deploy Clustered Storage Spaces](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj822937(v%3dws.11)>)要件。

## <a name="more-information"></a>詳細情報

- [フェールオーバー クラスタリング](failover-clustering.md)
- [記憶域スペース](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831739(v%3dws.11)>)
- [ゲスト クラスタ リングの高可用性を使用します。](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn440540(v%3dws.11)>)