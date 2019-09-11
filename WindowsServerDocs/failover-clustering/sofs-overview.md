---
title: アプリケーション データ用のスケールアウト ファイル サーバーの概要
description: Windows Server 201 R2 および Windows Server 2012 のスケールアウトファイルサーバー機能の概要について説明します。
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 04/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: 80bf85caac6f84e0d6da0c6139e39f3823b3a961
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70868710"
---
# <a name="scale-out-file-server-for-application-data-overview"></a>アプリケーション データ用のスケールアウト ファイル サーバーの概要

>適用対象:Windows Server 2012 R2、Windows Server 2012

スケールアウト ファイル サーバーは、ファイル ベースのサーバー アプリケーション記憶域用に継続的に使用可能なスケールアウト ファイル共有を提供するように設計された機能です。 スケールアウト ファイル共有では、同じクラスターの複数のノードから同じフォルダーを共有できる機能が提供されます。 このシナリオでは、スケールアウト ファイル サーバーの計画および展開方法に焦点を当てます。

クラスター化されたファイル サーバーを展開および構成するには、次のいずれかの方法を使用します。

- **アプリケーションデータのスケールアウトファイルサーバー**このクラスター化されたファイルサーバー機能は、Windows Server 2012 で導入されました。 Hyper-v 仮想マシンファイルなどのサーバーアプリケーションデータをファイル共有に格納し、同様のレベルの信頼性、可用性、管理容易性、高を実現することができます。記憶域ネットワークに期待されるパフォーマンス。 すべてのファイル共有が、すべてのノードで同時にオンラインになります。 このタイプのクラスター化されたファイル サーバーに関連付けられたファイル共有はスケールアウト ファイル共有と呼ばれます。 これはアクティブ - アクティブと呼ばれることもあります。 Hyper-V over SMV (サーバー メッセージ ブロック) または Microsoft SQL Server over SMB を展開する場合は、このファイル サーバーの種類を使用することをお勧めします。
- **汎用ファイル サーバー** これはフェールオーバー クラスタリングの導入以来、Windows Server でサポートされているクラスター化されたファイル サーバーの後続です。 このタイプのクラスター化されたファイル サーバーと、そのクラスター化されたファイル サーバーに関連付けられたすべての共有は、一度に 1 つのノードでオンラインになります。 これはアクティブ - パッシブまたはデュアル アクティブと呼ばれることもあります。 このタイプのクラスター化されたファイル サーバーに関連付けられたファイル共有はクラスター化されたファイル共有と呼ばれます。 情報ワーカーのシナリオを展開する場合は、このファイル サーバーの種類を使用することをお勧めします。

## <a name="scenario-description"></a>シナリオの説明

スケールアウト ファイル共有では、クラスターの複数のノードから同じフォルダーを共有できます。 たとえば、サーバーメッセージブロック (SMB) スケールアウトを使用している4ノードのファイルサーバークラスターがある場合、Windows Server 2012 R2 または Windows Server 2012 を実行しているコンピューターは、4つのノードのいずれからでもファイル共有にアクセスできます。 これは、新しい Windows Server のフェールオーバー クラスタリング機能と Windows ファイル サーバー プロトコル SMB 3.0 の機能を使用することで実現されます。 ファイル サーバー管理者は、スケールアウト ファイル共有と継続的に使用可能なファイル サービスをサーバー アプリケーションに提供し、オンラインにするサーバーを増やすだけで要求の増大に迅速に対応することができます。 これらすべては運用環境で実行することができ、サーバー アプリケーションにとっては完全に透過的です。

スケールアウト ファイル サーバーにより提供される主な利点は次のとおりです。

- **アクティブ/アクティブファイル共有**。 すべてのクラスターノードは、SMB クライアント要求を受け入れてサービスを提供できます。 ファイル共有コンテンツをすべてのクラスター ノードから同時にアクセス可能にすることにより、SMB 3.0 クラスターおよびクライアントは連携して、計画的なメンテナンスやサービスの中断を伴う予期しない障害の間に、代わりのクラスター ノードへの透過フェールオーバーを提供します。
- **帯域幅の増加**。 最大共有帯域幅は、すべてのファイルサーバークラスターノードの合計帯域幅です。 以前のバージョンの Windows Server とは異なり、合計の帯域幅は、1 つのクラスター ノードの帯域幅には制限されなくなりました。制約は、補助記憶域システムの機能によって定義されます。 ノードを追加することで合計の帯域幅を増大することができます。
- **ダウンタイムなしの CHKDSK**。 Windows Server 2012 の CHKDSK は、ファイルシステムが修復のためにオフラインになる時間を大幅に短縮するために大幅に拡張されています。 クラスター化共有ボリュー ム (CSV) はオフライン フェーズを排除することで、これをさらに一歩進めます。 CSV ファイル システム (CSVFS) は、ファイル システムでハンドルを開いたまま、アプリケーションに影響を与えることなく、CHKDSK を使用できます。
- **クラスター化共有ボリュームキャッシュ**。 Windows Server 2012 の Csv では、読み取りキャッシュのサポートが導入されており、仮想デスクトップインフラストラクチャ (VDI) などの特定のシナリオでパフォーマンスを大幅に向上させることができます。
- **管理が簡単**になります。 スケールアウトファイルサーバーでは、スケールアウトファイルサーバーを作成し、必要な Csv およびファイル共有を追加します。 個別のクラスター ディスクを持つ複数のクラスター化されたファイル サーバーを作成し、それぞれのクラスター ノードでのアクティビティを保証する配置ポリシーを開発する必要がなくなりました。
- **スケールアウトファイルサーバークライアントの自動**再分配。 Windows Server 2012 R2 では、自動再調整によって、スケールアウトファイルサーバーのスケーラビリティと管理容易性が向上します。 SMB クライアント接続は (サーバーごとではなく) ファイル共有ごとに追跡され、クライアントは、ファイル共有で使用されるボリュームへのアクセスに優れたクラスター ノードにリダイレクトされます。 これにより、ファイル サーバー ノード間のリダイレクト トラフィックが減少し、効率性が向上します。 クライアントがリダイレクトされるのは、初期接続の後、クラスター記憶域が再構成された場合です。

## <a name="in-this-scenario"></a>このシナリオの内容

スケールアウト ファイル サーバーの展開に役立つ次のトピックを紹介します。

- [スケールアウトファイルサーバーの計画](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134258(v%3dws.11)>)

  - [ステップ 1: スケールアウトファイルサーバーでの記憶域の計画](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134181%28v%3dws.11%29>)
  - [手順 2:スケールアウトファイルサーバーでのネットワークの計画](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134253%28v%3dws.11%29>)

- [スケールアウトファイルサーバーのデプロイ](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831359%28v%3dws.11%29>)

  - [ステップ 1: スケールアウトファイルサーバーの必須コンポーネントをインストールする](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831478%28v%3dws.11%29>)
  - [手順 2:スケールアウトファイルサーバーの構成](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831718%28v%3dws.11%29>)
  - [手順 3:スケールアウトファイルサーバーを使用するように Hyper-v を構成する](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831463%28v%3dws.11%29>)
  - [手順 4:スケールアウトファイルサーバーを使用するように Microsoft SQL Server を構成する](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831815%28v%3dws.11%29>)

## <a name="when-to-use-scale-out-file-server"></a>スケールアウト ファイル サーバーを使用する場合

ファイルを開く、ファイルを閉じる、新しいファイルを作成する、既存のファイル名を変更するなどのメタデータ操作がワークロードにより大量に生成される場合には、スケールアウト ファイル サーバーを使用しないでください。 一般的なインフォメーション ワーカーでは大量のメタデータ操作が生成されます。 スケールアウト ファイル サーバーが提供するスケーラビリティや簡潔さに注目している場合、およびスケールアウト ファイル サーバーでサポートされるテクノロジを必要としている場合にのみ、スケールアウト ファイル サーバーを使用してください。

次の表は、SMB 3.0 の機能、共通 Windows ファイル システム、ファイル サーバー データ管理テクノロジ、および一般的なワークロードを示しています。 テクノロジがスケールアウト ファイル サーバーでサポートされているかどうか、また、従来のクラスター化されたファイル サーバー (汎用のファイル サーバーとも呼ばれます) が必要かどうかも確認できます。

<table>
<thead>
<tr class="header">
<th>テクノロジの分野</th>
<th>機能</th>
<th>汎用のファイル サーバー クラスター</th>
<th>スケールアウト ファイル サーバー</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>SMB</td>
<td>継続的な SMB 可用性</td>
<td>はい</td>
<td>はい</td>
</tr>
<tr class="even">
<td>SMB</td>
<td>SMB マルチチャネル</td>
<td>はい</td>
<td>はい</td>
</tr>
<tr class="odd">
<td>SMB</td>
<td>SMB ダイレクト</td>
<td>はい</td>
<td>はい</td>
</tr>
<tr class="even">
<td>SMB</td>
<td>SMB 暗号化</td>
<td>はい</td>
<td>はい</td>
</tr>
<tr class="odd">
<td>SMB</td>
<td>SMB 透過フェールオーバー</td>
<td>はい (継続的な可用性が有効な場合)</td>
<td>はい</td>
</tr>
<tr class="even">
<td>[ファイル システム]</td>
<td>NTFS</td>
<td>はい</td>
<td>NA</td>
</tr>
<tr class="odd">
<td>[ファイル システム]</td>
<td>弾性ファイルシステム (<a href="https://docs.microsoft.com/windows-server/storage/refs/refs-overview">ReFS</a>)</td>
<td>記憶域スペースダイレクトで推奨</td>
<td>記憶域スペースダイレクトで推奨</td>
</tr>
<tr class="even">
<td>[ファイル システム]</td>
<td>クラスターの共有ボリューム ファイル システム (CSV)</td>
<td>NA</td>
<td>はい</td>
</tr>
<tr class="odd">
<td>ファイル管理</td>
<td>BranchCache</td>
<td>はい</td>
<td>いいえ</td>
</tr>
<tr class="even">
<td>ファイル管理</td>
<td>データ重複除去 (Windows Server 2012)</td>
<td>はい</td>
<td>いいえ</td>
</tr>
<tr class="odd">
<td>ファイル管理</td>
<td>データ重複除去 (Windows Server 2012 R2)</td>
<td>はい</td>
<td>はい (VDI のみ)</td>
</tr>
<tr class="even">
<td>ファイル管理</td>
<td>DFS 名前空間 (DFSN) ルート サーバーのルート</td>
<td>はい</td>
<td>いいえ</td>
</tr>
<tr class="odd">
<td>ファイル管理</td>
<td>DFS 名前空間 (DFSN) フォルダー ターゲット サーバー</td>
<td>はい</td>
<td>はい</td>
</tr>
<tr class="even">
<td>ファイル管理</td>
<td>DFS レプリケーション (DFSR)</td>
<td>はい</td>
<td>いいえ</td>
</tr>
<tr class="odd">
<td>ファイル管理</td>
<td>ファイル サーバー リソース マネージャー (画面とクォータ)</td>
<td>はい</td>
<td>いいえ</td>
</tr>
<tr class="even">
<td>ファイル管理</td>
<td>ファイル分類インフラストラクチャ</td>
<td>はい</td>
<td>いいえ</td>
</tr>
<tr class="odd">
<td>ファイル管理</td>
<td>ダイナミック アクセス制御 (要求ベースのアクセス、CAP)</td>
<td>はい</td>
<td>いいえ</td>
</tr>
<tr class="even">
<td>ファイル管理</td>
<td>フォルダー リダイレクト</td>
<td>はい</td>
<td>推奨されません<em></td>
</tr>
<tr class="odd">
<td>ファイル管理</td>
<td>オフライン ファイル (クライアント側キャッシュ)</td>
<td>はい</td>
<td>非推奨</em></td>
</tr>
<tr class="even">
<td>ファイル管理</td>
<td>移動ユーザー プロファイル</td>
<td>はい</td>
<td>推奨されません<em></td>
</tr>
<tr class="odd">
<td>ファイル管理</td>
<td>ホーム ディレクトリ</td>
<td>はい</td>
<td>非推奨</em></td>
</tr>
<tr class="even">
<td>ファイル管理</td>
<td>ワーク フォルダー</td>
<td>はい</td>
<td>いいえ</td>
</tr>
<tr class="odd">
<td>NFS</td>
<td>NFS サーバー</td>
<td>はい</td>
<td>いいえ</td>
</tr>
<tr class="even">
<td>[アプリケーション]</td>
<td>Hyper-V</td>
<td>非推奨</td>
<td>はい</td>
</tr>
<tr class="odd">
<td>[アプリケーション]</td>
<td>Microsoft SQL Server</td>
<td>非推奨</td>
<td>はい</td>
</tr>
</tbody>
</table>

\*フォルダーリダイレクト、オフラインファイル、移動ユーザープロファイル、またはホームディレクトリによって、継続的に使用可能なファイル共有を使用する場合に、ディスクにすぐに書き込む必要がある (バッファリングなしで) 大量の書き込みが生成されます。これに比べて、パフォーマンスが低下します。汎用ファイル共有。 また、継続的に使用可能なファイル共有にもファイル サーバー リソース マネージャー、および Windows XP を実行している PC との互換性がありません。 また、ユーザーが共有へのアクセスを失った後、オフラインファイルがオフライン3-6 モードに移行しないことがあります。これにより、オフラインファイルの Always Offline モードをまだ使用していないユーザーに不満が生じる可能性があります。

## <a name="practical-applications"></a>実際の適用例

スケールアウト ファイル サーバーは、サーバー アプリケーション記憶域に最適です。 スケールアウト ファイル共有にデータを格納できるサーバー アプリケーションの例をいくつか次に示します。

- インターネット インフォメーション サービス (IIS) Web サーバーは、Web サイトの構成とデータをスケールアウト ファイル共有に格納できます。 詳細については、 [共有構成](http://www.iis.net/learn/manage/managing-your-configuration-settings/shared-configuration_264)に関するページを参照してください。
- Hyper-V は、構成およびライブの仮想ディスクをスケールアウト ファイル共有に格納できます。 詳細については、「[Hyper-V over SMB の展開](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134187(v%3dws.11)>)」を参照してください。
- SQL Server は、ライブ データベース ファイルをスケールアウト ファイル共有に格納できます。 詳細については、「 [SQL Server をストレージ オプションとして SMB ファイル共有にインストールする](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server-with-smb-fileshare-as-a-storage-option)」を参照してください。
- Virtual Machine Manager (VMM) は、ライブラリ共有 (仮想マシン テンプレートと関連ファイルを含む) をスケールアウト ファイル共有に格納できます。 ただし、ライブラリサーバー自体をスケールアウトファイルサーバーにすることはできません。スタンドアロンサーバーまたはスケールアウトファイルサーバークラスターの役割を使用しないフェールオーバークラスター上にある必要があります。

スケールアウト ファイル共有をライブラリ共有として使用する場合は、スケールアウト ファイル サーバーと互換性があるテクノロジのみを使用できます。 たとえば、スケールアウトファイル共有でホストされているライブラリ共有をレプリケートするために DFS レプリケーションを使用することはできません。 また、スケールアウト ファイル サーバーに最新のソフトウェア更新プログラムがインストールされていることも重要です。

スケールアウト ファイル共有をライブラリ共有として使用するには、最初に、ローカル共有を備えた、または共有なしのライブラリ サーバー (おそらく仮想マシン) を追加します。 次に、ライブラリ共有を追加するときに、スケールアウトファイルサーバーでホストされているファイル共有を選択します。 この共有は、VMM で管理する必要があります。また、ライブラリ サーバー専用として作成されていなければなりません。 さらに、スケールアウト ファイル サーバーには必ず最新の更新プログラムをインストールします。 VMM ライブラリサーバーおよびライブラリ共有の追加の詳細については、「 [vmm ライブラリへのプロファイルの追加](https://docs.microsoft.com/system-center/vmm/library-profiles?view=sc-vmm-1801)」を参照してください。 ファイル サービスおよび記憶域サービスの現在使用可能な修正プログラムの一覧については、 [マイクロソフト サポート技術情報の記事 2899011](https://support.microsoft.com/help/2899011/list-of-currently-available-hotfixes-for-the-file-services-technologie)を参照してください。

>[!NOTE]
>インフォメーション ワーカーなど、一部のユーザーに対する負荷は、パフォーマンスにより大きな影響を与えます。 たとえば、ファイルを開く、閉じる、新しいファイルを作成する、既存のファイルの名前を変更するなどの操作を複数のユーザーが行うと、パフォーマンスに影響を及ぼします。 継続的な可用性によってファイル共有が有効になっている場合は、データの整合性が確保されますが、パフォーマンス全体にも影響します。 継続的な可用性では、スケールアウト ファイル サーバーのクラスター ノードでの障害発生時に整合性を確保するために、ディスクに対するデータの書き込みが必要です。 このため、ファイル サーバーに大きなファイルを複数コピーすると、継続的に使用可能なファイル共有のパフォーマンスが大幅に低下する場合があります。

## <a name="features-included-in-this-scenario"></a>このシナリオに含まれている機能

次の表で、このシナリオに含まれる機能を紹介すると共に、それをシナリオに活かす方法について説明します。

<table>
<thead>
<tr class="header">
<th>機能</th>
<th>このシナリオのサポート方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="failover-clustering.md">フェールオーバー クラスタリング</a></td>
<td>スケールアウトファイルサーバーをサポートするために、フェールオーバークラスターによって Windows Server 2012 に次の機能が追加されました。分散ネットワーク名、スケールアウトファイルサーバーリソースの種類、クラスターの共有ボリューム (CSV) 2、およびスケールアウトファイルサーバー高可用性ロール。 これらの機能の詳細については、「 <a href="https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265972(v%3dws.11)">Windows Server 2012 でのフェールオーバークラスタリングの新機能 [リダイレクト]&#39;</a>」を参照してください。</td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831795(v%3dws.11)">サーバーメッセージブロック</a></td>
<td>SMB 3.0 では、スケールアウトファイルサーバーをサポートするために、Windows Server 2012 に次の機能が追加されました。Smb 透過フェールオーバー、SMB マルチチャネル、および SMB ダイレクト。<br />
<br />
Windows Server 2012 R2 での SMB の新機能および変更された機能の詳細については、「 <a href="https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831474(v%3dws.11)">Windows server の smb の新&#39;</a>機能」を参照してください。</td>
</tr>
</tbody>
</table>

## <a name="more-information"></a>詳細情報

- [ソフトウェアで定義された記憶域の設計に関する考慮事項ガイド](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/mt243829(v%3dws.11)>)
- [サーバー、記憶域、およびネットワークの可用性の向上](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831437(v%3dws.11)>)
- [Hyper-v over SMB の展開](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134187(v%3dws.11)>)
- [サーバーアプリケーション用の高速で効率的なファイルサーバーの展開](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831723(v%3dws.11)>)
- [スケールアウトすべきか、スケールアウトせざるべきか、それが問題だ](https://blogs.technet.com/b/filecab/archive/2013/12/05/to-scale-out-or-not-to-scale-out-that-is-the-question.aspx) (ブログ記事)
- [フォルダーリダイレクト、オフラインファイル、移動ユーザープロファイル](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh848267(v%3dws.11)>)