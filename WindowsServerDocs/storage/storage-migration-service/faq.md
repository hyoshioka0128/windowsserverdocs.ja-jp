---
title: 記憶域移行サービスに関してよく寄せられる質問 (FAQ)
description: 記憶域の移行サービスに関してよく寄せられる質問 (あるサーバーから別のサーバーへの移行時に転送から除外されるファイルなど)。
author: nedpyle
ms.author: nedpyle
manager: siroy
ms.date: 08/19/2019
ms.topic: article
ms.prod: windows-server
ms.technology: storage
ms.openlocfilehash: a776920caa85c3ee133070d52b020c8ad3c799e1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402992"
---
# <a name="storage-migration-service-frequently-asked-questions-faq"></a>記憶域移行サービスに関してよく寄せられる質問 (FAQ)

このトピックでは、 [Storage Migration Service](overview.md)を使用したサーバーの移行に関してよく寄せられる質問 (faq) に対する回答を示します。

## <a name="what-files-and-folders-are-excluded-from-transfers"></a>転送から除外されるファイルとフォルダー

Storage Migration Service は、Windows の操作に干渉する可能性があるファイルまたはフォルダーを転送しません。 具体的には、転送されたり、宛先の PreExistingData フォルダーに移動したりすることはありません。

- Windows、program Files、Program Files (x86)、Program Data、Users
- $Recycle.bin、recycler、Recycled、システム ボリューム情報、$UpgDrv$、$SysReset、$Windows ~ $Windows。 bt によって ~ %.ls、Windows.old、ブート、回復、Documents and Settings。
- pagefile.sys、hiberfil.sys、bootsect.exe、winpepge.sys、config、config.sys、bootmgr、bootnxt のうちのすべてのファイルを
- 移行先の除外されたフォルダーと競合する、移行元サーバー上のすべてのファイルまたはフォルダー。 <br>たとえば、ソースに N:\Windows フォルダーがあり、それが C:\ にマップされているとします。コピー先のボリュームは、格納されている内容に関係なく転送されません。これは、変換先の C:\Windows システムフォルダーが影響を受ける可能性があるためです。

## <a name="are-domain-migrations-supported"></a>ドメインの移行はサポートされていますか?

記憶域移行サービスでは、Active Directory ドメイン間での移行は許可されていません。 サーバー間の移行は、常に移行先サーバーを同じドメインに参加させます。 Active Directory フォレスト内の異なるドメインからの移行資格情報を使用できます。 記憶域移行サービスは、ワークグループ間の移行をサポートしています。  

## <a name="are-clusters-supported-as-sources-or-destinations"></a>クラスターは変換元または変換先としてサポートされていますか。

記憶域移行サービスは、Windows Server 2019 のクラスター間で現在移行されていません。 将来のリリースの Storage Migration Service でクラスターサポートを追加する予定です。

## <a name="do-local-groups-and-local-users-migrate"></a>ローカルグループとローカルユーザーを移行しますか?

現在、Storage Migration Service では、ローカルユーザーまたはローカルグループを Windows Server 2019 で移行することはできません。 Storage Migration Service の将来のリリースでは、ローカルユーザーとローカルグループの移行サポートを追加する予定です。

## <a name="is-domain-controller-migration-supported"></a>ドメインコントローラーの移行はサポートされていますか?

Storage Migration Service は、Windows Server 2019 のドメインコントローラを現在移行していません。 回避策として、Active Directory ドメインに複数のドメインコントローラーがある場合は、移行する前にドメインコントローラーを降格し、カットオーバーが完了した後で移行先を昇格させます。 将来のリリースの Storage Migration Service では、ドメインコントローラーの移行サポートを追加する予定です。

## <a name="what-attributes-are-migrated-by-the-storage-migration-service"></a>Storage Migration Service によってどのような属性が移行されますか?

記憶域移行サービスは、すべてのフラグ、設定、および SMB 共有のセキュリティを移行します。 記憶域移行サービスによって移行されるフラグの一覧を次に示します。

    - 状態の共有
    - 可用性の種類
    - 共有の種類
    - フォルダー列挙モード *(アクセスベースの列挙型または ABE とも*呼ばれます)
    - キャッシュモード
    - リースモード
    - Smb インスタンス
    - CA タイムアウト
    - 同時ユーザー数の制限
    - 継続的に利用可能
    - 説明           
    - データの暗号化
    - Id リモート処理
    - インフラストラクチャ
    - 名前
    - パス
    - 役割
    - スコープ名
    - セキュリティ記述子
    - シャドウコピー
    - 既定
    - Temporary

## <a name="can-i-consolidate-multiple-servers-into-one-server"></a>複数のサーバーを1台のサーバーに統合することはできますか。

Windows Server 2019 に出荷された Storage Migration Service のバージョンでは、複数のサーバーを1台のサーバーに統合することはできません。 統合の例としては、3つの異なるソースサーバーを移行する場合があります。これには、同じ共有名とローカルファイルパスが存在することがあります。これにより、これらのパスと共有を仮想化して重複や衝突を防ぐことができます。以前のサーバー名と IP アドレス。 この機能は、今後のバージョンの Storage Migration Service で追加される予定です。 

## <a name="can-i-migrate-from-sources-other-than-windows-server"></a>Windows Server 以外のソースから移行できますか?

Windows Server 2019 に同梱されている Storage Migration Service のバージョンは、Windows Server 2003 以降のオペレーティングシステムからの移行をサポートしています。 また、Samba を使用する Linux サーバーまたはデバイスから記憶域を移行することもできます。これを行うには、Windows Server バージョン1903以降を実行しているサーバーで Storage Migration Service を実行します。

## <a name="can-i-migrate-previous-file-versions"></a>以前のバージョンのファイルを移行できますか?

Windows Server 2019 に出荷された記憶域移行サービスのバージョンでは、ファイルの以前のバージョン (ボリュームシャドウコピーサービスを使用した) の移行はサポートされていません。 現在のバージョンのみが移行されます。 

## <a name="optimizing-inventory-and-transfer-performance"></a>インベントリと転送のパフォーマンスの最適化

Storage Migration Service には、Storage Migration Service プロキシサービスと呼ばれるマルチスレッドの読み取りおよびコピーエンジンが含まれています。これは、多くのファイルコピーツールではなく、データの忠実性を完全に再現することを目的として設計されています。 既定の構成は多くのお客様に最適ですが、インベントリおよび転送中に SMS のパフォーマンスを向上させる方法があります。

- **対象のオペレーティングシステムに Windows Server 2019 を使用します。** Windows Server 2019 には、Storage Migration Service プロキシサービスが含まれています。 この機能をインストールして Windows Server 2019 の変換先に移行すると、すべての転送は、ソースと宛先の間で直接表示されるように動作します。 対象のコンピューターが Windows Server 2012 R2 または Windows Server 2016 の場合、このサービスは、転送中に orchestrator 上で実行されます。これは、転送がダブルホップで、処理速度が大幅に低下することを意味します。 Windows Server 2012 R2 または Windows Server 2016 の変換先で複数のジョブが実行されている場合、orchestrator はボトルネックになります。 

- **既定の転送スレッドを変更します。** 記憶域移行サービスのプロキシサービスは、指定されたジョブで8個のファイルを同時にコピーします。 Storage Migration Service プロキシを実行しているすべてのノードで、次のレジストリの REG_DWORD 値の名前を10進数で調整することにより、同時コピースレッド数を増やすことができます。

    HKEY_Local_Machine\Software\Microsoft\SMSProxy
    
    FileTransferThreadCount

   Windows Server 2019 では、有効な範囲は 1 ~ 128 です。 変更後は、移行に参加しているすべてのコンピューターで、Storage Migration Service プロキシサービスを再起動する必要があります。 この設定には注意してください。この値を高く設定すると、追加のコア、記憶域のパフォーマンス、およびネットワーク帯域幅が必要になる場合があります。 設定値が高すぎると、既定の設定と比較してパフォーマンスが低下する可能性があります。

- **コアとメモリを追加します。**  ソース、orchestrator、および対象のコンピューターには少なくとも2つのプロセッサコアまたは2つの vCPUs があることを強くお勧めします。これにより、特に FileTransferThreadCount (上記の) と組み合わせた場合に、インベントリと転送のパフォーマンスを大幅に向上させることができます。 通常の Office 形式 (ギガバイト以上) を超えるファイルを転送する場合は、既定の2GB よりも多くのメモリを利用した方がパフォーマンスが向上します。

- **複数のジョブを作成します。** 複数のサーバーソースを持つジョブを作成する場合、各サーバーは、インベントリ、転送、およびカットオーバーのために、直列に接続されます。 つまり、各サーバーは、別のサーバーが起動する前にフェーズを完了する必要があります。 複数のサーバーを並行して実行するには、各ジョブに1つのサーバーのみを含む複数のジョブを作成するだけです。 SMS では、同時に最大で100のジョブを実行できます。つまり、1つの orchestrator が多数の Windows Server 2019 対象コンピューターを並列化できます。 対象のコンピューターが Windows Server 2016 または Windows Server 2012 R2 の場合、移行先で SMS プロキシサービスが実行されていない場合は、複数の並列ジョブを実行しないことをお勧めします。 orchestrator は、すべての転送を実行する必要があり、次のようになります。なる. サーバーを1つのジョブ内で並列に実行する機能は、新しいバージョンの SMS で追加する予定です。

- **RDMA ネットワークで SMB 3 を使用します。** Windows Server 2012 以降のソースコンピューターから転送する場合、smb 3.x は SMB Direct モードと RDMA ネットワークをサポートします。 RDMA は、マザーボードの Cpu からの転送にかかる CPU コストを最も多く移動し、待機時間とサーバーの CPU 使用率を削減します。 さらに、ROCE や iWARP のような RDMA ネットワークは、通常の TCP/イーサネットよりもはるかに高い帯域幅を備えています。これには、インターフェイスあたり25、50、100 Gb の速度が含まれます。 通常、SMB ダイレクトを使用すると、ネットワークから記憶域自体に転送速度の制限が移動します。   

- **SMB 3 マルチチャネルを使用します。** Windows Server 2012 以降のソースコンピューターから転送する場合、SMB 2.x では、ファイルコピーのパフォーマンスを大幅に向上させることができるマルチチャネルコピーがサポートされます。 この機能は、移行元と移行先の両方が次のことを行う限り、自動的に機能します。

   - 複数のネットワーク アダプター
   - Receive Side Scaling (RSS) をサポートする1つまたは複数のネットワークアダプター
   - NIC チーミングを使用して構成されているその他のネットワークアダプターの1つ
   - RDMA をサポートしているネットワーク アダプター 1 つ以上

- **ドライバーを更新します。** 必要に応じて、最新のベンダーの記憶域とエンクロージャのファームウェアとドライバー、最新のベンダー HBA ドライバー、最新のベンダーの BIOS/UEFI ファームウェア、最新のベンダーネットワークドライバー、最新のマザーボードのチップセットドライバーをソース、ターゲット、および orchestrator にインストールします。サーバー. 必要に応じてノードを再起動します。 共有記憶域およびネットワーク ハードウェアの構成については、ハードウェア ベンダーのドキュメントを参照してください。

- **高パフォーマンスの処理を有効にします。** サーバーの BIOS および UEFI の設定が、C 状態の無効化、QPI 速度の設定、NUMA の有効化、最大メモリ動作周波数の設定など、高パフォーマンスを有効にする設定であることを確認します。 Windows Server の電源管理が高パフォーマンスに設定されていることを確認します。 必要に応じて再起動します。 移行が完了したら、必ずこれらの状態を適切な状態に戻してください。 

- **ハードウェアの調整**Windows server 2019 と Windows Server 2016 を実行する orchestrator および対象コンピューターのチューニングについては、「 [Windows server 2016 のパフォーマンスチューニングガイドライン](https://docs.microsoft.com/windows-server/administration/performance-tuning/)」を参照してください。 [ネットワークサブシステムのパフォーマンスチューニング](https://docs.microsoft.com/windows-server/networking/technologies/network-subsystem/net-sub-performance-tuning-nics)に関するセクションには、特に重要な情報が含まれています。

- **より高速なストレージを使用します。** ソースコンピューターのストレージ速度をアップグレードするのは困難な場合がありますが、転送時に不要なボトルネックが発生しないようにするために、ソースが読み取り IO パフォーマンスであるため、宛先ストレージの書き込み IO パフォーマンスが少なくとも高速であることを確認する必要があります。 移行先が VM の場合は、少なくとも移行の目的で、少なくとも移行のために、フラッシュ層、ミラー化されたすべてのフラッシュまたはハイブリッドスペースを使用する記憶域スペースダイレクト HCI クラスターなどのハイパーバイザーホストの最速のストレージ層で実行されることを確認します。 SMS の移行が完了したら、低速の層またはホストに VM をライブマイグレーションできます。

- **ウイルス対策ソフトウェアを更新します。** パフォーマンスのオーバーヘッドを最小限に抑えるために、移行元と移行先がウイルス対策ソフトウェアの最新のパッチバージョンを実行していることを必ず確認してください。 テストとして、移行元サーバーと移行先サーバーでインベントリまたは移行しているフォルダーのスキャンを*一時的*に除外することができます。 転送のパフォーマンスが向上した場合は、ウイルス対策ソフトウェアベンダーに問い合わせて、ウイルス対策ソフトウェアの更新版、または予想されるパフォーマンス低下について説明してください。

## <a name="can-i-migrate-from-ntfs-to-refs"></a>NTFS から REFS に移行できますか?

Windows Server 2019 に出荷された記憶域移行サービスのバージョンでは、NTFS から REFS ファイルシステムへの移行はサポートされていません。 NTFS から NTFS および REFS から ReFS に移行できます。 これは仕様によるものです。これは、機能、メタデータ、および参照が NTFS と重複しないという点に多くの違いがあるためです。 ReFS は、一般的なファイルシステムではなく、アプリケーションワークロードファイルシステムとして使用することを目的としています。 詳細については、「[弾力性ファイルシステム (ReFS) の概要](../refs/refs-overview.md)」を参照してください。 

## <a name="can-i-move-the-storage-migration-service-database"></a>Storage Migration Service データベースを移動できますか。

Storage Migration Service では、hidden c:\programdata\microsoft\storagemigrationservice フォルダーに既定でインストールされる拡張ストレージエンジン (ESE) データベースを使用します。 ジョブが追加され、転送が完了すると、このデータベースは拡張されます。ジョブを削除しない場合は、何百万ものファイルを移行した後で、大きなドライブ領域を消費する可能性があります。 データベースを移動する必要がある場合は、次の手順を実行します。

1. Orchestrator コンピューターの "Storage Migration Service" サービスを停止します。
2. フォルダーの所有権`%programdata%/Microsoft/StorageMigrationService`を取得する
3. ユーザーアカウントを追加して、その共有とそのすべてのファイルとサブフォルダーを完全に制御できるようにします。
4. フォルダーを orchestrator コンピューターの別のドライブに移動します。
5. 次のレジストリ REG_SZ 値を設定します。

    HKEY_Local_Machine\Software\Microsoft\SMS DatabasePath =*別のボリューム上の新しいデータベースフォルダーへのパス*。 
6. システムがそのフォルダーのすべてのファイルとサブフォルダーに対してフルコントロールを持っていることを確認する
7. 自分のアカウントのアクセス許可を削除します。
8. "Storage Migration Service" サービスを開始します。

## <a name="give-feedback"></a>フィードバックの提供、バグの報告、サポートを受けるためのオプションは何ですか?

ストレージ移行サービスに関するフィードバックを提供するには:

- Windows 10 に含まれているフィードバックハブツールを使用して、[機能の提案] をクリックし、[Windows Server] と [記憶域の移行] のカテゴリを指定します。
- [Windows Server UserVoice](https://windowsserver.uservoice.com)サイトを使用する
- 電子メールsmsfeed@microsoft.com

バグを報告するには:

- Windows 10 に含まれているフィードバックハブツールを使用し、[問題の報告] をクリックして、"Windows Server" と "Storage Migration" のカテゴリを指定します。
- [Microsoft サポート](https://support.microsoft.com)を使用してサポートケースを開く

サポートを受けるには:

 - [Windows Server Tech Community](https://techcommunity.microsoft.com/t5/Windows-Server/ct-p/Windows-Server)に質問を投稿する
 - [Windows Server 2019 Technet フォーラム](https://social.technet.microsoft.com/Forums/en-US/home?forum=ws2019&filter=alltypes&sort=lastpostdesc)の投稿 
 - [Microsoft サポート](https://support.microsoft.com)を使用してサポートケースを開く

## <a name="see-also"></a>関連項目

- [記憶域移行サービスの概要](overview.md)
