---
title: Windows Admin Center でのハイパー コンバージド インフラストラクチャを管理します。
description: Windows Admin Center (プロジェクト ホノルル) でのハイパー コンバージド インフラストラクチャを管理します。
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 03/01/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: fe00072932d9c7f283ebd887a5292ac9a9d0e37f
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446031"
---
# <a name="manage-hyper-converged-infrastructure-with-windows-admin-center"></a>Windows Admin Center でのハイパー コンバージド インフラストラクチャを管理します。

>適用先:Windows Admin Center、Windows Admin Center プレビュー

## <a name="what-is-hyper-converged-infrastructure"></a>Hyper-Converged インフラストラクチャします。

ハイパー コンバージド インフラストラクチャでは、ソフトウェアによるコンピューティング、ストレージ、および高パフォーマンス、コスト効率に優れたを提供する 1 つのクラスターに簡単に拡張できる仮想化ネットワークを統合します。 この機能は、Windows Server 2016 で導入された[記憶域スペース ダイレクト](https://docs.microsoft.com/windows-server/storage/storage-spaces/storage-spaces-direct-overview)、[ソフトウェアによるネットワーク制御](https://docs.microsoft.com/en-us/windows-server/networking/sdn/software-defined-networking)と[HYPER-V](https://docs.microsoft.com/windows-server/virtualization/hyper-v/hyper-v-on-windows-server)します。

> [!Tip]
> Hyper-Converged インフラストラクチャを取得しようとしていますか。 マイクロソフトでは、これらをお勧め[Windows Server ソフトウェア定義](https://microsoft.com/wssd)パートナーからソリューションです。 設計は、アセンブリ、互換性および取得するための信頼性と簡単に実行されているように、参照アーキテクチャの検証にあり。

> [!IMPORTANT]
> この記事で説明されている機能の一部は、Windows Admin Center プレビューでのみです。 [このバージョンを取得する方法はありますか](http://aka.ms/windowsadmincenter)

## <a name="what-is-windows-admin-center"></a>Windows Admin Center とは

[Windows Admin Center](../understand/windows-admin-center.md)次世代の管理ツールを Windows Server、Server Manager などの従来の「ボックス」ツールの後継です。 無料とインストールされているし、インターネット接続なしで使用できます。 Windows Admin Center を使用して、管理および Windows Server 2016 または Windows Server 2019 実行 Hyper-Converged インフラストラクチャを監視することができます。

![ハイパー コンバージド クラスター ダッシュ ボード](../media/manage-hyper-converged/hci-dashboard-v1809.png)

## <a name="key-features"></a>主な機能

Hyper-Converged インフラストラクチャ用の Windows Admin Center の主な特徴は次のとおりです。

- **統一された単一ウィンドウ-の-ガラスのコンピューティング、ストレージ、およびネットワークのすぐにします。** 仮想マシン、ホスト サーバー、ボリューム、ドライブ、および 1 つの専用に作成された、一貫性のある、相互接続されたエクスペリエンス内で詳細を表示します。
- **作成し、記憶域スペースと HYPER-V の仮想マシンを管理します。** 極めて簡単なワークフローを作成するには、開く、サイズ、および、; のボリュームを削除作成、起動への接続、および仮想マシンを移動その他さまざまな。
- **強力なクラスター全体を監視します。** メモリと CPU 使用率、記憶域容量、IOPS、スループット、および待機時間がグラフで、ダッシュ ボード、問題が生じているときにアラートをクリアして、クラスター内の各サーバーではリアルタイムです。
- **ソフトウェア定義ネットワーク (SDN) のサポート。** 管理し、仮想ネットワークの監視、サブネット、仮想ネットワーク、および SDN インフラストラクチャの監視に仮想マシンを接続します。

Hyper-Converged インフラストラクチャ用の Windows Admin Center Microsoft が積極的に開発中です。 既存の機能を向上させ、新しい機能の追加を頻繁に更新プログラムを受け取ります。

## <a name="before-you-start"></a>開始前の作業

Windows Admin Center で Hyper-Converged インフラストラクチャとして、クラスターを管理する Windows Server 2016 または Windows Server 2019、実行されている必要があり、Hyper-v ホストと記憶域スペース ダイレクトを有効にします。 必要に応じて、有効になっており、Windows Admin Center を使用して管理、ソフトウェアによるネットワーク制御も、かまいません。

> [!Tip]
> Windows Admin Center では、汎用的な管理は、Windows Server 2012 以降使用可能なすべてのワークロードをサポートしている任意のクラスターのエクスペリエンスも提供します。 Windows Admin Center をクラスターを追加するより適したのように聞こえるこの場合は、選択[**フェイル オーバー クラスター** ](manage-failover-clusters.md)の代わりに**Hyper-Converged クラスター**します。

### <a name="prepare-your-windows-server-2016-cluster-for-windows-admin-center"></a>Windows Admin Center の Windows Server 2016 クラスターを準備します。

Hyper-Converged インフラストラクチャ用の Windows Admin Center は、Windows Server 2016 がリリースされた後に Api が追加の管理に依存します。 Windows Server 2016 を Windows Admin Center を使用したクラスターを管理するには、これら 2 つの手順を実行する必要があります。

1. クラスター内のすべてのサーバーがインストールされていることを確認、 [2018-05 の累積更新プログラムを Windows Server 2016 (KB4103723)](https://support.microsoft.com/help/4103723/windows-10-update-kb4103723)またはそれ以降。 をダウンロードしてこの更新プログラムをインストールするには**設定** > **更新とセキュリティ** > **Windows 更新**選択**Microsoft Update から更新プログラムをオンラインで確認**します。
2. クラスターの管理者として次の PowerShell コマンドレットを実行します。

```powershell
    Add-ClusterResourceType -Name "SDDC Management" -dll "$env:SystemRoot\Cluster\sddcres.dll" -DisplayName "SDDC Management"
```

> [!Tip]
> のみ、任意のサーバー クラスターに 1 回、コマンドレットを実行する必要があります。 Windows PowerShell でローカルで実行または Credential Security Service Provider (CredSSP) を使用して、リモートで実行することができます。 構成によっては、Windows Admin Center 内からこのコマンドレットを実行することはできません。

### <a name="prepare-your-windows-server-2019-cluster-for-windows-admin-center"></a>Windows Admin Center の Windows Server 2019 クラスターを準備します。

クラスターは、Windows Server 2019 を実行する場合は上記の手順は必要ありません。 次のセクションで説明した Windows Admin Center をクラスターに追加し、移動する準備が整いました。

### <a name="configure-software-defined-networking-optional"></a>ソフトウェア定義ネットワーク (省略可能) を構成します。 ###

次の手順でソフトウェア定義ネットワーク (SDN) を使用するには、Windows Server 2016 または 2019 を実行している、Hyper-Converged インフラストラクチャを構成できます。

1. これは、同じ OS のハイパー コンバージド インフラストラクチャのホストにインストールされている OS の VHD を準備します。 この VHD は、すべての NC/SLB/GW Vm に対して使用されます。
2. すべての SDN の Express から下にあるファイルとフォルダーをダウンロード[ https://github.com/Microsoft/SDN/tree/master/SDNExpress](https://github.com/Microsoft/SDN/tree/master/SDNExpress)します。
3. 展開コンソールを使用して別の VM を準備します。 この VM は、SDN のホストにアクセスできる必要があります。 また、VM には、インストールされている RSAT HYPER-V ツールが必要です。
4. VM の展開コンソールに SDN Express をダウンロードしたすべてのものをコピーします。 これを共有および**SDNExpress**フォルダー。 すべてのホストがアクセスできるように、 **SDNExpress** 8 構成ファイルの行で定義されているフォルダーを共有します。
   ```
    \\$env:Computername\SDNExpress
   ```
5. OS の VHD をコピーして、**イメージ**の下のフォルダー、 **SDNExpress**展開コンソール VM 上のフォルダー。
6. 環境のセットアップで、SDN Express の構成を変更します。 環境の情報に基づいて、SDN Express の構成を変更した後は、次の 2 つの手順を完了します。
7. SDN を展開する管理者特権で PowerShell を実行します。

```powershell
    .\SDNExpress.ps1 -ConfigurationDataFile .\your_fabricconfig.PSD1 -verbose 
```

展開は、約 30 ~ 45 分かかります。

## <a name="get-started"></a>作業開始

Hyper-Converged インフラストラクチャをデプロイすると、Windows Admin Center を使用して管理できます。

### <a name="install-windows-admin-center"></a>Windows Admin Center のインストール

既に、していない場合はダウンロードして、Windows Admin Center をインストールします。 起動方法を最も迅速かつ実行中を Windows 10 コンピューターにインストールし、サーバーをリモートで管理です。 これは、5 分未満です。 [今すぐダウンロード](https://aka.ms/windowsadmincenter)または[の詳細については、他のインストール オプションは](../deploy/install.md)します。

### <a name="add-hyper-converged-cluster"></a>ハイパー コンバージド クラスターを追加します。

クラスターを Windows Admin Center に追加します。

1. クリックして **+ 追加**すべての接続。
2. 追加することも、 **Hyper-Converged クラスター接続**します。
3. クラスターの名前を入力し、使用する資格情報を求められた場合。
4. クリックして**追加**を完了します。

クラスターは、接続の一覧に追加されます。 クリックしてダッシュ ボードを起動します。

![ハイパー コンバージド クラスター接続を追加します。](../media/manage-hyper-converged/add-hyper-converged-cluster-connection.gif)

### <a name="add-sdn-enabled-hyper-converged-cluster-windows-admin-center-preview"></a>ハイパー コンバージド クラスターの SDN 有効になっている (Windows Admin Center プレビュー) の追加します。

最新の Windows Admin Center プレビューでは、Hyper-Converged インフラストラクチャ ソフトウェアによるネットワーク制御の管理をサポートします。 ネットワーク コント ローラーの REST URI を追加すると、ハイパー コンバージド クラスターの接続に、SDN リソースを管理し、SDN インフラストラクチャを監視するハイパー コンバージド クラスター マネージャーを使用できます。

1. クリックして **+ 追加**すべての接続。
2. 追加することも、 **Hyper-Converged クラスター接続**します。
3. クラスターの名前を入力し、使用する資格情報を求められた場合。
4. 確認**ネットワーク コント ローラーを構成する**を続行します。
5. 入力、**ネットワーク コント ローラーの URI**クリック**検証**。
6. クリックして**追加**を完了します。

クラスターは、接続の一覧に追加されます。 クリックしてダッシュ ボードを起動します。

![ハイパー コンバージド クラスターの SDN が有効な接続を追加します。](../media/manage-hyper-converged/add-snd-enabled-hci-connection.png)

> [!Important]
> Northbound 通信用の Kerberos 認証を使用した SDN の環境は現在サポートされていません。

## <a name="frequently-asked-questions"></a>よく寄せられる質問

### <a name="are-there-differences-between-managing-windows-server-2016-and-windows-server-2019"></a>Windows Server 2016 および Windows Server 2019 の管理の違いはありますか。

[はい]。 Hyper-Converged インフラストラクチャ用の Windows Admin Center では、Windows Server 2016 と Windows Server 2019 の両方のエクスペリエンスを向上させる、頻繁に更新プログラムを受信します。 ただし、一部の新機能では、Windows Server 2019 – たとえば、トグル スイッチを重複除去と圧縮の使用のみです。

### <a name="can-i-use-windows-admin-center-to-manage-storage-spaces-direct-for-other-use-cases-not-hyper-converged-such-as-converged-scale-out-file-server-sofs-or-microsoft-sql-server"></a>他のユース ケース (いないハイパー コンバージドの両方)、集約型のスケール アウト ファイル サーバー (SoFS) または Microsoft SQL Server などの記憶域スペース ダイレクトを管理するのに Windows Admin Center を使用できますか。

Hyper-Converged インフラストラクチャ用の Windows Admin Center では、管理や記憶域スペース ダイレクトの他のユース ケースの具体的には監視オプションは提供されません – たとえば、ファイル共有を作成できません。 ただし、ボリュームの作成や、ドライブの交換などのダッシュ ボードとコア機能は、任意の記憶域スペース ダイレクト クラスターの動作します。

### <a name="whats-the-difference-between-a-failover-cluster-and-a-hyper-converged-cluster"></a>フェールオーバー クラスターと Hyper-Converged クラスターの違いは何ですか。

一般に、「ハイパー コンバージド」とは、同じ Hyper-v ホストと記憶域スペース ダイレクトを実行するには、コンピューティングおよびストレージ リソースを仮想化サーバーがクラスター化します。 クリックすると、Windows Admin Center のコンテキストで **+ 追加**の追加の接続の一覧から選択できます、**フェイル オーバー クラスター接続**または**Hyper-Converged クラスター接続**:

- **フェイル オーバー クラスター接続**フェールオーバー クラスター マネージャーのデスクトップ アプリの後継です。 Microsoft SQL Server を含む、すべてのワークロードをサポートしている任意のクラスターの使い慣れた、汎用的な管理エクスペリエンスを提供します。 以降を Windows Server 2012 の利用可能になります。

- **Hyper-Converged クラスター接続**記憶域スペース ダイレクトと HYPER-V 向け、まったく新しいエクスペリエンスに調整されます。 ダッシュ ボードを備えており、監視のためのグラフとアラートが強調されます。 Windows Server 2016 および Windows Server 2019 の使用可能になります。

### <a name="why-do-i-need-the-latest-cumulative-update-for-windows-server-2016"></a>Windows Server 2016 の最新の累積的な更新プログラムが必要する理由

Hyper-Converged インフラストラクチャ用の Windows Admin Center は、Windows Server 2016 がリリースされてから、Api が開発された管理に依存します。 これらの Api を追加、[累積更新プログラムを Windows Server 2016 (KB4103723) を 2018-05](https://support.microsoft.com/help/4103723/windows-10-update-kb4103723)2018 年 5 月 8 日の時点で利用可能です。

### <a name="how-much-does-it-cost-to-use-windows-admin-center"></a>Windows Admin Center を使用するにはいくらかかりますか。

Windows Admin Center には、Windows 以外の追加コストはありません。

追加コストなしで Windows Server または Windows 10 の有効なライセンスを持つ Windows Admin Center (個別のダウンロードとして入手可能) を使用することができます - Windows の追加契約書の下でライセンスを取得します。

### <a name="does-windows-admin-center-require-system-center"></a>Windows Admin Center に System Center は必要ですか。

No.

### <a name="does-it-require-an-internet-connection"></a>インターネット接続が必要ですか。

No.

Windows Admin Center、強力で、Microsoft Azure クラウドでは、中心的な管理および Hyper-Converged インフラストラクチャの監視のエクスペリエンスとの便利な統合は、完全にオンプレミスにします。 インストールして、インターネット接続なしで使用できます。

## <a name="things-to-try"></a>対処方法

いる作業を開始した場合、Hyper-Converged インフラストラクチャ用の Windows Admin Center の構成し、機能の学習に役立ついくつかのクイック チュートリアルを示します。 適切な判断を実行しての運用環境に注意してください。 これらのビデオは、Windows Admin Center バージョン 1804 および Windows Server 2019、Insider Preview ビルドで記録されています。

### <a name="manage-storage-spaces-direct-volumes"></a>記憶域スペース ダイレクトのボリュームを管理します。

<ul>
               <li>(0:37) <a href="https://youtu.be/o66etKq70N8">3 方向ミラー ボリュームを作成する方法</a></li>
               <li>(1:17)<a href="https://youtu.be/R72QHudqWpE">ミラー アクセラレータを使用したパリティ ボリュームを作成する方法</a></li>
               <li>(1:02)<a href="https://youtu.be/j59z7ulohs4">ボリュームを開き、ファイルを追加する方法</a></li>
               <li>(0:51)<a href="https://youtu.be/PRibTacyKko">重複除去と圧縮を有効にする方法</a></li>
               <li>(0:47)<a href="https://youtu.be/hqyBzipBoTI">ボリュームを拡張する方法</a></li>
               <li>(0:26)<a href="https://youtu.be/DbjF8r2F6Jo">ボリュームを削除する方法</a></li>
</ul>

<table>
    <tr style="border: 0;">
        <td style="padding: 5px; border: 0;">
            <strong>3 方向ミラー ボリュームを作成します。</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/o66etKq70N8" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
        <td style="padding: 5px; border: 0;">
            <strong>ボリューム、ミラー アクセラレータを使用したパリティを作成します。</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/R72QHudqWpE" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 5px; border: 0;">
            <strong>ボリュームを開き、ファイルの追加</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/j59z7ulohs4" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
        <td style="padding: 5px; border: 0;">
            <strong>重複除去と圧縮を有効にします。</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/PRibTacyKko" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 5px; border: 0;">
            <strong>ボリュームを拡張します。</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/hqyBzipBoTI" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
        <td style="padding: 5px; border: 0;">
            <strong>ボリュームを削除します。</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/DbjF8r2F6Jo" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
    </tr>
</table>

### <a name="create-a-new-virtual-machine"></a>新しい仮想マシンを作成する

1. をクリックして、**仮想マシン**、左側のナビゲーション ウィンドウからのツール。
2. 仮想マシンのツールの上部にある次のように選択します。、**インベントリ** タブの 、 をクリックし、**新規**新しい仮想マシンを作成します。
3. 仮想マシンの名前を入力し、世代 1 および 2 世代仮想マシンを選択します。
4. やすいは、最初に、仮想マシンを作成または推奨されるホストを使用するホストを選択できます。
5. 仮想マシン ファイルのパスを選択します。 ドロップダウン リストからボリュームを選択するかクリックして**参照**フォルダー ピッカーを使用してフォルダーを選択します。 仮想マシン構成ファイルとバーチャル ハード ディスク ファイルは、1 つのフォルダーの下に保存されます、`\Hyper-V\[virtual machine name]`パスの選択したボリュームのパス。
6. 入れ子になった仮想化が有効にする、メモリの設定、ネットワーク アダプタ、バーチャル ハード_ディスクを構成し、.iso イメージ ファイルから、またはネットワークからオペレーティング システムをインストールするかどうかを選択するかどうか、仮想プロセッサの数を選択します。
7. **[作成]** をクリックして、バーチャル マシンを作成します。
8. 仮想マシンを作成し、仮想マシンの一覧に表示される、仮想マシンを開始できます。
9. 仮想マシンが開始されると、オペレーティング システムをインストールする VMConnect を使用して、仮想マシンのコンソールに接続できます。 一覧から仮想マシンを選択し、 をクリックして**詳細** > **Connect** .rdp ファイルをダウンロードします。 Remote Desktop Connection アプリでは、.rdp ファイルを開きます。 これは、仮想マシンのコンソールに接続する、ため、HYPER-V ホストの管理者の資格情報を入力する必要があります。

[詳細については、Windows Admin Center での仮想マシンの管理は](manage-virtual-machines.md)します。

### <a name="pause-and-safely-restart-a-server"></a>一時停止し、安全に、サーバーを再起動

1. **ダッシュ ボード**を選択します**サーバー** 、ナビゲーションの左側にあるかをクリックしてから、**サーバーの表示 >** ダッシュ ボードの右下隅のタイル上のリンク.
2. 上部から切り替える**概要**を**インベントリ**タブ。
3. 開くには、その名前をクリックして、サーバーの選択、 **Server**詳細ページ。
4. クリックして**保守のため一時停止サーバー**します。 続行しても安全である場合は、仮想マシンをクラスター内の他のサーバーに移動がこれです。 サーバーでは、この処理中も状態のドレイン必要があります。 する場合は、上の移動、仮想マシンを見ることができます、**仮想マシン > インベントリ** ページで、そのホスト サーバーが明らかに、グリッド内に表示される場所。 すべての仮想マシンを移動して、サーバーの状態がなります**Paused**します。
5. クリックして**管理サーバー** Windows Admin Center でのすべてのサーバー管理ツールにアクセスします。
6. クリックして**再起動**、し**はい**します。 接続の一覧のバックアップを開始します。
7. 戻り、**ダッシュ ボード**、停止中に、サーバーは赤です。
8. バックアップが、もう一度移動、**サーバー**ページし、クリックして**メンテナンスからサーバーを再開**を単に、サーバーの状態を設定します。 仮想マシンへ移動: ユーザー操作は必要ありません。

### <a name="replace-a-failed-drive"></a>失敗したドライブを交換します。

1. ドライブに失敗すると、左上に表示されたアラート**アラート**の領域、**ダッシュ ボード**します。
2. 選択することもできます**ドライブ**のナビゲーションで、左側にあるまたはをクリックしてから、**ビュー ドライブ >** ドライブを参照し、自分でその状態を表示する右下隅のタイルにリンクします。 **インベントリ**並べ替え、グループ化とキーワード検索 タブで、グリッドをサポートします。
3. **ダッシュ ボード**アラートをクリックして、ドライブの物理的な場所などの詳細を参照してください。
4. 詳細については、クリックして、**ドライブに移動して**へのショートカット、**ドライブ**詳細ページ。
5. ご使用のハードウェアがサポートする場合は、クリックして**ライトのオン/オフを有効にする**ドライブのライトを制御します。
6. 記憶域スペース ダイレクト自動的にインベントリから削除され失敗したドライブを退避させます。 ドライブの状態を終了すると、これが発生した場合、その記憶域容量のバーが空です。
7. 失敗したドライブを削除し、交換品を挿入します。
8. **ドライブ > インベントリ**、新しいドライブが表示されます。 時間では、アラートがクリアされますボリュームは、[ok] の状態に戻す修復し記憶域が新しいドライブに再調整: ユーザー操作は必要ありません。

### <a name="manage-virtual-networks-sdn-enabled-hci-clusters-using-windows-admin-center-preview"></a>仮想ネットワーク (SDN が有効な HCI クラスターが Windows Admin Center プレビューを使用して) の管理します。

1. 選択**仮想ネットワーク**左側のナビゲーションから。
2. をクリックして**新規**を新しい仮想ネットワークとサブネットを作成または既存の仮想ネットワークを選択し、をクリックして**設定**構成を変更します。
3. 仮想ネットワーク サブネットに VM の接続を表示およびアクセス制御リストが仮想ネットワークのサブネットに適用する既存の仮想ネットワークをクリックします。

![仮想ネットワークを管理します。](../media/manage-hyper-converged/manage-virtual-networks.png)

### <a name="connect-a-virtual-machine-to-a-virtual-network-sdn-enabled-hci-clusters-using-windows-admin-center-preview"></a>仮想マシンを仮想ネットワーク (SDN が有効な HCI クラスターが Windows Admin Center プレビューを使用して) に接続します。

1. 選択**仮想マシン**左側のナビゲーションから。
2. 既存の仮想マシンを選択 > をクリックして**設定**> オープン、**ネットワーク** タブの **設定**します。
3. 構成、**仮想ネットワーク**と**仮想サブネット**フィールドを仮想マシンを仮想ネットワークに接続します。

仮想マシンを作成するときに、仮想ネットワークを構成することもできます。

![仮想マシンを仮想ネットワークに接続します。](../media/manage-hyper-converged/connect-vm-to-virtual-network.png)

### <a name="monitor-software-defined-networking-infrastructure-sdn-enabled-hci-clusters-using-windows-admin-center-preview"></a>ソフトウェアによるネットワーク制御インフラストラクチャの監視 (HCI の SDN が有効なクラスターが Windows Admin Center プレビューを使用して)

1. 選択**SDN 監視**左側のナビゲーションから。
2. ネットワーク コント ローラー、ソフトウェア ロード バランサー、仮想ゲートウェイの正常性に関する詳細情報を表示し、仮想ゲートウェイ プール、パブリックおよびプライベート IP プールの使用状況と SDN のホストの状態を監視します。

![SDN インフラストラクチャの監視](../media/manage-hyper-converged/sdn-monitoring.png)

## <a name="feedback"></a>Feedback

お客様のフィードバックに関するあらゆるです。 頻繁に更新プログラムの最も重要な利点は、機能するいると改善が必要なものです。 何を考えているお知らせをいくつかの点を次に示します。

- [送信して、UserVoice での機能の要望に投票](https://windowsserver.uservoice.com/forums/295071/category/319162?query=%5Bhci%5D)
- [Microsoft Tech Community で Windows Admin Center フォーラムに参加します。](https://techcommunity.microsoft.com/t5/Windows-Server-Management/bd-p/WindowsServerManagement)
- ツイートするには `@servermgmt`

### <a name="see-also"></a>関連項目

- [Windows Admin Center](../understand/windows-admin-center.md)
- [記憶域スペース ダイレクト](https://docs.microsoft.com/windows-server/storage/storage-spaces/storage-spaces-direct-overview)
- [Hyper-V](https://docs.microsoft.com/windows-server/virtualization/hyper-v/hyper-v-on-windows-server)
- [ソフトウェア定義ネットワーク](https://docs.microsoft.com/windows-server/networking/sdn/software-defined-networking)
