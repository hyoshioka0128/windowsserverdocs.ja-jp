---
title: スケール アウト ファイル サーバー アプリケーションのデータの概要
description: Windows Server 201 R2、Windows Server 2012、および Windows Server 2016 のスケール アウト ファイル サーバー機能の概要です。
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage-failover-clustering
ms.date: 04/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: 04e25e9c69062611d9d14c220614f148ac5de770
ms.sourcegitcommit: e0479b0114eac7f232e8b1e45eeede96ccd72b26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2018
ms.locfileid: "2082382"
---
# <a name="scale-out-file-server-for-application-data-overview"></a>スケール アウト ファイル サーバー アプリケーションのデータの概要

>対象: Windows Server 2012 R2、Windows Server 2012、Windows Server 2016

スケール アウト ファイル サーバーは、ファイル サーバー アプリケーション記憶域を継続的に対応したスケール アウト ファイルの共有を提供するように設計された機能です。 スケール アウトしたファイルの共有では、同じクラスターの複数のノードのと同じフォルダーを共有する機能を提供します。 このシナリオでは、計画し、スケール アウト ファイル サーバーを展開する方法について説明します。

展開して、次のいずれかを使用して集合ファイル サーバーを構成することができます。

- **アプリケーションのデータのスケール アウト ファイル サーバー**Windows Server 2012 では、この集合ファイル サーバー機能が導入され、ファイルの共有] で、HYPER-V 仮想マシン ファイルなど、サーバー アプリケーションのデータを保存して、信頼性、空き時間情報、管理、および高のと同じレベルを取得することができます。記憶域ネットワーク期待されるパフォーマンスします。 すべてのファイルの共有は、すべてのノードで同時にオンラインです。 集合ファイル サーバーの種類に関連付けられているファイルの共有は、スケール アウト ファイル共有と呼ばれます。 これとも呼ばアクティブにします。 これは、一般法でサーバー メッセージ ブロック (一般法) または Microsoft SQL Server 上のいずれかの HYPER-V を配置する場合に推奨されるファイル サーバーの種類です。
- **ファイルのサーバー**これは、導入しないでの Windows Server でサポートされている集合ファイル サーバーの継続時です。 一度に 1 つのノードのオンラインではこの種類の集合ファイル サーバー、および集合ファイル サーバーに関連付けられているすべての共有のため。 これがアクティブ パッシブまたはデュアル アクティブとして呼ばれます。 集合ファイル サーバーの種類に関連付けられているファイルの共有は、クラスター ファイル共有と呼ばれます。 これは、情報の作業者のシナリオを展開する際に推奨されるファイル サーバーの種類です。

## <a name="scenario-description"></a>シナリオの説明

拡大/縮小されたファイルの共有では、クラスターの複数のノードのと同じフォルダーを共有できます。 たとえば、4 ノード ファイル サーバー クラスター スケール アウト サーバー メッセージ ブロック (一般法) を使用している場合は、Windows Server 2012 R2 または Windows Server 2012 の実行中のコンピューターがファイルの共有を 4 つのノードのいずれかからにアクセスすることができます。 これは、Windows Server しないでの新機能と、Windows ファイルのサーバー プロトコルの機能を活用して一般法 3.0 します。 ファイル サーバー管理者は、スケール アウト ファイル共有とサーバー アプリケーションの継続的に使用できるファイルのサービスを提供し、単にその他のサーバーをオンラインにすることによりすばやく向上要求に応答します。 このすべての運用環境で実行できる、サーバー アプリケーションに完全に透明なします。

スケール アウト ファイル サーバーによって提供されるキーの主な利点は次のとおりです。

- **アクティブ - ファイル共有**します。 すべてのクラスター ノードでは、承諾でき、一般法クライアント要求を処理することができます。 一般法 3.0 クラスターとクライアントでさせて透明な代替ノード計画済みメンテナンスおよび予期しないエラーの中にサービスを共同で同時にすべてのクラスター ノードからアクセスできるコンテンツを共有するファイルを作成するには、継続します。
- **帯域幅の向上**します。 最大共有帯域幅は、すべてのファイル サーバー クラスター ノードの帯域幅の合計です。 以前のバージョンの Windows Server では、帯域幅の合計は不要になったを 1 つのクラスター ノードの帯域幅に制限します。バックアップの記憶域システムの機能が代わりに、制約を定義します。 帯域幅の合計を大きくノードを追加することができます。
- **ダウンタイム CHKDSK**します。 Windows Server 2012 CHKDSK がファイル システムは、オフライン修復に時間を大幅に短縮する大幅に向上します。 集合共有ボリューム (Csv) は、オフライン フェーズを排除することでさらにこの 1 つの手順を実行します。 CSV ファイル システム (CSVFS) のハンドルを開いて、[ファイル システムのアプリケーションに影響を与えずに CHKDSK を使用できます。
- **共有ボリュームの集合キャッシュ**します。 Windows Server 2012 Csv は大幅にパフォーマンスが向上特定のシナリオでなど、仮想デスクトップ インフラストラクチャ (VDI) で、読み取りのキャッシュのサポートについて説明します。
- **シンプルな管理**します。 スケール アウト ファイル サーバーでは、スケール アウト ファイル サーバーを作成し、必要な Csv とファイルの共有を追加します。 場合によっては、それぞれ別のクラスター ディスクに複数の集合ファイル サーバーを作成し、各クラスター ノードのアクティビティを確実に配置ポリシーを作成します必要はありません。
- **自動スケール アウト ファイル サーバーのクライアントの再調整**します。 Windows Server 2012 R2] で、自動再配分、スケーラビリティおよびスケール アウト ファイル サーバーの管理機能が向上します。 ファイル共有あたり一般法クライアント接続が管理されている (の代わりにサーバーあたり)、クライアントはクラスター ノードにファイルの共有が使用するボリュームに最適なアクセス権を持つリダイレクトします。 これにより、ファイル サーバー ノード間のトラフィックをリダイレクトして効率が向上します。 クライアントは、次の最初の接続とクラスター記憶域を再構成するときにリダイレクトされます。

## <a name="in-this-scenario"></a>このシナリオで

次のトピックでは、スケール アウト ファイル サーバーの展開をサポートを利用できます。

- [スケール アウト ファイル サーバーを計画します。](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134258(v%3dws.11)>)

  - [手順 1: スケール アウト ファイル サーバーでの記憶域を計画します。](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134181%28v%3dws.11%29>)
  - [手順 2: スケール アウト ファイル サーバーでネットワーク接続を計画します。](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134253%28v%3dws.11%29>)

- [スケール アウト ファイル サーバーを展開します。](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831359%28v%3dws.11%29>)

  - [手順 1: スケール アウト ファイル サーバーの前提条件をインストールします。](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831478%28v%3dws.11%29>)
  - [手順 2: スケール アウト ファイル サーバーを構成します。](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831718%28v%3dws.11%29>)
  - [手順 3: 構成 HYPER-V スケール アウト ファイル サーバーを使用するには](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831463%28v%3dws.11%29>)
  - [手順 4: スケール アウト ファイル サーバーを使用する Microsoft SQL Server を構成します。](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831815%28v%3dws.11%29>)

## <a name="when-to-use-scale-out-file-server"></a>スケール アウト ファイル サーバーを使用する場合

使用しないでくださいスケール アウト ファイル サーバーのワークロード多数のファイルを開くなどのメタデータの操作を生成する場合は、ファイルを閉じ、新しいファイルを作成する、または既存のファイルの名前を変更します。 多くのメタデータ操作の一般的な情報作業者が生成されます。 スケーラビリティと、シンプルで関心がある場合、およびのみテクノロジ スケール アウト ファイル サーバーでサポートされている必要がある場合は、スケール アウト ファイル サーバーを使用する必要があります。

次の表は、一般法 3.0、一般的な Windows ファイル システム、ファイル サーバー データ管理の技術、および一般的なワークロード内での機能を一覧表示します。 従来の集合ファイル サーバー (一般的な用途ファイル サーバーとも呼ばれます) が必要になる場合または、技術スケール アウト ファイル サーバーでは、サポートされているかどうかを確認できます。

<table>
<thead>
<tr class="header">
<th>テクノロジの領域</th>
<th>機能</th>
<th>サーバー クラスターの一般的なファイルを使用します。</th>
<th>スケール アウト ファイル サーバー</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>SMB</td>
<td>一般法のビジネス継続性</td>
<td>はい</td>
<td>はい</td>
</tr>
<tr class="even">
<td>SMB</td>
<td>一般法マルチ チャンネル</td>
<td>はい</td>
<td>はい</td>
</tr>
<tr class="odd">
<td>SMB</td>
<td>一般法ダイレクト</td>
<td>はい</td>
<td>はい</td>
</tr>
<tr class="even">
<td>SMB</td>
<td>一般法暗号化</td>
<td>はい</td>
<td>はい</td>
</tr>
<tr class="odd">
<td>SMB</td>
<td>一般法透明なフェールオーバー</td>
<td>[はい (ビジネス継続性が有効な場合)</td>
<td>必須</td>
</tr>
<tr class="even">
<td>ファイル システム</td>
<td>NTFS</td>
<td>必須</td>
<td>該当なし</td>
</tr>
<tr class="odd">
<td>ファイル システム</td>
<td>回復ファイル システム (<a href="https://docs.microsoft.com/windows-server/storage/refs/refs-overview">参照</a>)</td>
<td>記憶域が推奨スペースを 1 レベルのみ</td>
<td>記憶域が推奨スペースを 1 レベルのみ</td>
</tr>
<tr class="even">
<td>ファイル システム</td>
<td>クラスターは、ボリューム ファイル システム (CSV) を共有します。</td>
<td>該当なし</td>
<td>必須</td>
</tr>
<tr class="odd">
<td>ファイルを管理します。</td>
<td>BranchCache</td>
<td>はい</td>
<td>×</td>
</tr>
<tr class="even">
<td>ファイルを管理します。</td>
<td>データの重複 (Windows Server 2012)</td>
<td>はい</td>
<td>×</td>
</tr>
<tr class="odd">
<td>ファイルを管理します。</td>
<td>データの重複 (Windows Server 2012 R2)</td>
<td>必須</td>
<td>[はい (VDI のみ)</td>
</tr>
<tr class="even">
<td>ファイルを管理します。</td>
<td>ルート サーバーのルート DFS Namespace (DFSN)</td>
<td>はい</td>
<td>×</td>
</tr>
<tr class="odd">
<td>ファイルを管理します。</td>
<td>DFS Namespace (DFSN) フォルダー ターゲット サーバー</td>
<td>はい</td>
<td>はい</td>
</tr>
<tr class="even">
<td>ファイルを管理します。</td>
<td>DFS レプリケーション (DFSR)</td>
<td>はい</td>
<td>×</td>
</tr>
<tr class="odd">
<td>ファイルを管理します。</td>
<td>(画面とクォータ)、ファイル サーバー リソース マネージャー</td>
<td>はい</td>
<td>×</td>
</tr>
<tr class="even">
<td>ファイルを管理します。</td>
<td>ファイル分類インフラストラクチャ</td>
<td>はい</td>
<td>×</td>
</tr>
<tr class="odd">
<td>ファイルを管理します。</td>
<td>動的なアクセス制御 (クレーム ベースのアクセス、キャップ)</td>
<td>はい</td>
<td>×</td>
</tr>
<tr class="even">
<td>ファイルを管理します。</td>
<td>フォルダーのリダイレクト</td>
<td>必須</td>
<td>お勧めしません *</td>
</tr>
<tr class="odd">
<td>ファイルを管理します。</td>
<td>オフラインのファイル (クライアント側のキャッシュ)</td>
<td>必須</td>
<td>お勧めしません *</td>
</tr>
<tr class="even">
<td>ファイルを管理します。</td>
<td>ユーザー プロファイルを移動します。</td>
<td>必須</td>
<td>お勧めしません *</td>
</tr>
<tr class="odd">
<td>ファイルを管理します。</td>
<td>ホーム ディレクトリ</td>
<td>必須</td>
<td>お勧めしません *</td>
</tr>
<tr class="even">
<td>ファイルを管理します。</td>
<td>ワーク フォルダー</td>
<td>はい</td>
<td>×</td>
</tr>
<tr class="odd">
<td>NFS</td>
<td>NFS サーバー</td>
<td>はい</td>
<td>×</td>
</tr>
<tr class="even">
<td>アプリケーション</td>
<td>Hyper-V</td>
<td>お勧めしません</td>
<td>必須</td>
</tr>
<tr class="odd">
<td>アプリケーション</td>
<td>Microsoft SQL Server</td>
<td>お勧めしません</td>
<td>必須</td>
</tr>
</tbody>
</table>

\ * フォルダー リダイレクト、オフライン ファイル、ユーザー プロファイルの移動、またはホーム ディレクトリの生成 (せずにバッファー処理) をディスクにすぐに記述する必要がある書き込みの数が多い継続的に使用できるファイルの共有を使用している場合と比べてのパフォーマンスが低下一般的な目的のファイル共有します。 継続的に使用できるファイルの共有もファイル サーバー リソース マネージャーおよび Windows XP を実行している Pc と互換性がします。 さらに、オフライン ファイルは、3 ~ 6 分後、ユーザーがまだオフライン ファイルを常にオフライン モードを使用していないユーザーが不満可能性があります共有へのアクセスを失いオフライン モードに移行できない場合があります。

## <a name="practical-applications"></a>実際の適用例

スケール アウト ファイル サーバーでは、サーバー アプリケーション記憶域に最適です。 スケール アウト ファイル共有データが保存されるサーバー アプリケーションのいくつかの例を以下に示します。

- インターネット インフォメーション サービス (IIS) Web サーバーに保存できます構成とデータの Web サイトのスケール アウト ファイル共有。 詳細については、[共有構成](http://www.iis.net/learn/manage/managing-your-configuration-settings/shared-configuration_264)を参照してください。
- HYPER-V は、スケール アウト ファイル共有の構成とライブ仮想ディスクに保存できます。 詳細については、[展開 HYPER-V 一般法上](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134187(v%3dws.11)>)を参照してください。
- SQL Server スケール アウト ファイル共有ライブ データベース ファイルを保存できます。 詳細については、 [SQL Server をインストールする一般法ファイル共有記憶域のオプションを](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server-with-smb-fileshare-as-a-storage-option)参照してください。
- 仮想マシン マネージャー (VMM) では、スケール アウト ファイル共有にライブラリの共有を含む仮想マシンのテンプレートと関連ファイル) を保存できます。 ただし、ライブラリ サーバー自体はスケール アウト ファイル サーバーをすることはできません: スタンドアロン サーバーなどのフェールオーバー クラスター スケール アウト ファイル サーバーの役割を使用しないことがあります。

ライブラリの共有とスケール アウト ファイル共有を使用する場合は、スケール アウト ファイル サーバーと互換性があるテクノロジのみを使用することができます。 たとえば、スケール アウト ファイル共有でホストされているライブラリの共有を複製する DFS レプリケーションを使うことはできません。 重要スケール アウト ファイル サーバーにインストールされている最新のソフトウェアの更新があることもできます。

スケール アウト ファイル共有を使用すると、ライブラリの共有を最初にライブラリ サーバー (仮想マシンの場合) が追加ローカル共有または共有なしまったくします。 [ライブラリの共有を追加するときに、スケール アウト ファイル サーバーでホストされているファイルの共有を選択します。 この共有 VMM が管理されていると、ライブラリのサーバーで作成した排他モードで使用する必要があります。 また、スケール アウト ファイル サーバー上で最新の更新プログラムをインストールすることを確認してください。 VMM ライブラリのサーバーとライブラリの共有を追加する方法の詳細については、 [VMM ライブラリに追加のプロファイル](https://docs.microsoft.com/system-center/vmm/library-profiles?view=sc-vmm-1801)を参照してください。 ファイルと記憶域サービスの現在利用可能な修正プログラムの一覧は、 [Microsoft サポート技術情報の記事 2899011](https://support.microsoft.com/help/2899011/list-of-currently-available-hotfixes-for-the-file-services-technologie)を参照してください。

>[!NOTE]
>インフォメーション ワーカーなど、一部のユーザーには、パフォーマンスに与える影響が大きい負荷が与えられています。 たとえば、操作を開くと、新しいファイルを作成するファイルを閉じると、パフォーマンスに影響を与える、複数のユーザーによって実行されるときに、既存のファイルの名前を変更します。 ビジネス継続性とファイルの共有を有効にする場合は、データの整合性を提供は、全体的なパフォーマンスにも影響します。 スケール アウト ファイル サーバーでクラスター ノードに失敗した場合の整合性を確保するためにディスクにデータが書き込まを通じてビジネス継続性が必要です。 このため、ファイル サーバーに、いくつかの大きなファイルをコピーするユーザーは、継続的に使用できるファイルの共有にパフォーマンスが大幅に低下を予想できます。

## <a name="features-included-in-this-scenario"></a>このシナリオに含まれる機能

次の表は、このシナリオの一部の機能の一覧が表示し、サポートされる方法について説明します。

<table>
<thead>
<tr class="header">
<th>機能</th>
<th>このシナリオをサポートする方法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="failover-clustering.md">フェールオーバー クラスタリング</a></td>
<td>フェールオーバー クラスター スケール アウト ファイル サーバーをサポートする Windows Server 2012 で、次の機能の追加: ネットワーク名の配布されるため、スケール アウト ファイル サーバー リソースの種類、クラスター共有ボリューム (CSV) 2、およびスケール アウト ファイル サーバーの可用性の役割は、します。 これらの機能の詳細については、 <a href="https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn265972(v%3dws.11)">[リダイレクト] Windows Server 2012 しないでの新機能</a>を参照してください。</td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831795(v%3dws.11)">サーバー メッセージ ブロック</a></td>
<td>一般法 3.0、次の機能をサポートする Windows Server 2012 のスケール アウト ファイル サーバーの追加: 一般法透明な/一般法マルチ チャンネル、/一般法直接します。<br />
<br />
In Windows Server 2012 R2 一般法の機能の追加、変更の詳細については、 <a href="https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831474(v%3dws.11)">Windows Server で一般法の新機能</a>を参照してください。</td>
</tr>
</tbody>
</table>

## <a name="more-information"></a>詳細

- [記憶域のソフトウェアで定義されるデザインの考慮事項ガイド](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/mt243829(v%3dws.11)>)
- [サーバー、ストレージ、およびネットワークの可用性の向上](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831437(v%3dws.11)>)
- [Hyper-V over SMB の展開](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj134187(v%3dws.11)>)
- [サーバー アプリケーションの迅速かつ効率的なファイル サーバーを展開します。](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831723(v%3dws.11)>)
- [または、拡大/縮小に調整するのには質問](https://blogs.technet.com/b/filecab/archive/2013/12/05/to-scale-out-or-not-to-scale-out-that-is-the-question.aspx)(ブログの投稿)
- [フォルダー リダイレクト、オフライン ファイル、移動ユーザー プロファイル](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh848267(v%3dws.11)>)