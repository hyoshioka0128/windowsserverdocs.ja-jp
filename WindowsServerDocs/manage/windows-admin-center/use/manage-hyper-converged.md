---
title: Windows 管理センターを使用したハイパー集約型インフラストラクチャの管理
description: Windows 管理センター (Project ホノルル) を使用したハイパー集約型インフラストラクチャの管理
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 03/01/2019
ms.localizationpriority: medium
ms.openlocfilehash: a2fd0e688d33265119c8dcb915d485e953507c80
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87990482"
---
# <a name="manage-hyper-converged-infrastructure-with-windows-admin-center"></a>Windows 管理センターを使用したハイパー集約型インフラストラクチャの管理

>適用先:Windows Admin Center、Windows Admin Center Preview

## <a name="what-is-hyper-converged-infrastructure"></a>ハイパー集約型インフラストラクチャとは

ハイパースレッディングインフラストラクチャでは、ソフトウェアで定義されたコンピューティング、記憶域、およびネットワークを1つのクラスターに統合して、パフォーマンス、コスト効率、および拡張性に優れた、拡張性の高い仮想化を実現します。 この機能は、Windows Server 2016 で[記憶域スペースダイレクト](../../../storage/storage-spaces/storage-spaces-direct-overview.md)、[ソフトウェアで定義さ](../../../networking/sdn/software-defined-networking.md)れたネットワーク、および[hyper-v](../../../virtualization/hyper-v/hyper-v-on-windows-server.md)を使用して導入されました。

> [!Tip]
> ハイパー集約型インフラストラクチャの取得を検討していますか? Microsoft では、これらの[Windows Server ソフトウェアで定義された](https://microsoft.com/wssd)ソリューションをパートナーから推奨しています。 これらは、互換性と信頼性を確保するために、参照アーキテクチャに対して設計、組み立て、検証を行い、迅速に稼働させることができます。

> [!IMPORTANT]
> この記事で説明されている機能の一部は、Windows 管理センタープレビューでのみ使用できます。 [このバージョンを取得操作方法には](https://aka.ms/windowsadmincenter)

## <a name="what-is-windows-admin-center"></a>Windows Admin Center とは

[Windows 管理センター](../overview.md)は、windows Server 用の次世代管理ツールであり、サーバーマネージャーなどの従来の "組み込み" ツールを後継としています。 これは無料で、インターネットに接続せずにインストールして使用することができます。 Windows 管理センターを使用して、Windows Server 2016 または Windows Server 2019 を実行しているハイパー集約型インフラストラクチャを管理および監視できます。

![ハイパー収束クラスターダッシュボード](../media/manage-hyper-converged/hci-dashboard-v1809.png)

## <a name="key-features"></a>主要な機能

ハイパー集約型インフラストラクチャの Windows 管理センターには、次のような特徴があります。

- **コンピューティング、ストレージ、およびまもなくネットワークのための統合された単一のウィンドウです。** 仮想マシン、ホストサーバー、ボリューム、ドライブなどを、1つの目的で、一貫性のある、相互接続されたエクスペリエンスで表示します。
- **記憶域スペースと Hyper-v 仮想マシンを作成および管理します。** ボリュームを作成、開く、サイズ変更、削除するための、大幅に単純なワークフロー。仮想マシンを作成、起動、接続、移動します。さらに多くのことができます。
- **強力なクラスター全体の監視。** ダッシュボードには、クラスター内のすべてのサーバーにわたってメモリと CPU の使用率、ストレージ容量、IOPS、スループット、待機時間がリアルタイムでグラフ化されます。適切でない場合は明確なアラートが生成されます。
- **ソフトウェア定義ネットワーク (SDN) のサポート。** 仮想ネットワーク、サブネット、仮想ネットワークへの仮想マシンの接続、および SDN インフラストラクチャの監視を行います。

Microsoft によって積極的に開発されているハイパー集約型インフラストラクチャの Windows 管理センターです。 既存の機能を向上させ、新機能を追加する頻繁な更新プログラムを受信します。

## <a name="before-you-start"></a>開始する前に

Windows 管理センターでハイパー集約型インフラストラクチャとしてクラスターを管理するには、Windows Server 2016 または Windows Server 2019 を実行している必要があります。また、Hyper-v と記憶域スペースダイレクトが有効になっている必要があります。 必要に応じて、Windows 管理センターを使用して、ソフトウェアで定義されたネットワークを有効にし、管理することもできます。

> [!Tip]
> Windows 管理センターでは、Windows Server 2012 以降で使用可能なすべてのワークロードをサポートするクラスターに対して、汎用的な管理エクスペリエンスを提供します。 このような場合は、クラスターを Windows 管理センターに追加するときに、[**ハイパー収束クラスター**ではなく[**フェールオーバークラスター**](manage-failover-clusters.md) ] を選択します。

### <a name="prepare-your-windows-server-2016-cluster-for-windows-admin-center"></a>Windows 管理センター用に Windows Server 2016 クラスターを準備する

ハイパー収束インフラストラクチャの windows 管理センターは、Windows Server 2016 のリリース後に追加された管理 Api に依存します。 Windows 管理センターを使用して Windows Server 2016 クラスターを管理するには、次の2つの手順を実行する必要があります。

1. クラスター内のすべてのサーバーに、 [Windows server 2016 (KB4103723) 以降の2018-05 の累積的な更新プログラム](https://support.microsoft.com/help/4103723/windows-10-update-kb4103723)がインストールされていることを確認します。 この更新プログラムをダウンロードしてインストールするには、[**設定**] [  >  **更新プログラム & セキュリティ**  >  **Windows Update**にアクセスし、[ **Microsoft Update の更新プログラムをオンラインで確認**する] を選択します。
2. クラスターで管理者として次の PowerShell コマンドレットを実行します。

```powershell
    Add-ClusterResourceType -Name "SDDC Management" -dll "$env:SystemRoot\Cluster\sddcres.dll" -DisplayName "SDDC Management"
```

> [!Tip]
> クラスター内の任意のサーバーで、コマンドレットを1回だけ実行する必要があります。 Windows PowerShell でローカルに実行するか、Credential Security Service Provider (CredSSP) を使用してリモートで実行することができます。 構成によっては、Windows 管理センター内からこのコマンドレットを実行できない場合があります。

### <a name="prepare-your-windows-server-2019-cluster-for-windows-admin-center"></a>Windows 管理センター用に Windows Server 2019 クラスターを準備する

クラスターで Windows Server 2019 が実行されている場合、上記の手順は必要ありません。 次のセクションで説明されているように、クラスターを Windows 管理センターに追加するだけで十分です。

### <a name="configure-software-defined-networking-optional"></a>ソフトウェアで定義されたネットワークを構成する (省略可能) ###

次の手順でソフトウェア定義ネットワーク (SDN) を使用するように、Windows Server 2016 または2019を実行しているハイパー集約型インフラストラクチャを構成できます。

1. ハイパー集約型インフラストラクチャホストにインストールした os と同じ OS の VHD を準備します。 この VHD は、すべての NC/SLB/GW Vm に使用されます。
2. SDN Express の下にあるすべてのフォルダーとファイルをからダウンロード [https://github.com/Microsoft/SDN/tree/master/SDNExpress](https://github.com/Microsoft/SDN/tree/master/SDNExpress) します。
3. 展開コンソールを使用して別の VM を準備します。 この VM は SDN ホストにアクセスできる必要があります。 また、VM には RSAT Hyper-v ツールがインストールされている必要があります。
4. SDN Express 用にダウンロードしたすべてのものをデプロイコンソール VM にコピーします。 この**Sdnexpress**フォルダーを共有します。 次のように、構成ファイル8で定義されているように、すべてのホストが**Sdnexpress**共有フォルダーにアクセスできることを確認します。
   ```
    \\$env:Computername\SDNExpress
   ```
5. OS の VHD を、デプロイコンソール VM の**Sdnexpress**フォルダーの下の**images**フォルダーにコピーします。
6. 環境のセットアップを使用して SDN Express 構成を変更します。 環境情報に基づいて SDN Express 構成を変更した後、次の2つの手順を完了します。
7. 管理者特権で PowerShell を実行して SDN を展開します。

```powershell
    .\SDNExpress.ps1 -ConfigurationDataFile .\your_fabricconfig.PSD1 -verbose
```

デプロイには約 30 ~ 45 分かかります。

## <a name="get-started"></a>はじめに

デプロイされたハイパースレッディングインフラストラクチャは、Windows 管理センターを使用して管理できます。

### <a name="install-windows-admin-center"></a>Windows Admin Center をインストールする

Windows 管理センターをまだダウンロードしていない場合はインストールします。 起動して実行する最速の方法は、Windows 10 コンピューターにインストールし、サーバーをリモートで管理することです。 これには、5分未満の時間がかかります。 [今すぐダウンロード](https://aka.ms/windowsadmincenter)するか、[他のインストールオプションの詳細をご](../deploy/install.md)確認ください。

### <a name="add-hyper-converged-cluster"></a>ハイパー収束クラスターの追加

クラスターを Windows 管理センターに追加するには、次のようにします。

1. [すべての接続] の下にある [ **+ 追加**] をクリックします。
2. ハイパー集約された**クラスター接続**を追加することを選択します。
3. クラスターの名前を入力し、メッセージが表示されたら、使用する資格情報を入力します。
4. [**追加**] をクリックして完了します。

クラスターが接続の一覧に追加されます。 これをクリックすると、ダッシュボードが起動します。

![ハイパー収束クラスター接続の追加](../media/manage-hyper-converged/add-hyper-converged-cluster-connection.gif)

### <a name="add-sdn-enabled-hyper-converged-cluster-windows-admin-center-preview"></a>SDN が有効なハイパー収束クラスターの追加 (Windows 管理センタープレビュー)

最新の Windows 管理センタープレビューでは、ハイパー集約型インフラストラクチャのソフトウェア定義ネットワーク管理がサポートされています。 ハイパー収束クラスター接続にネットワークコントローラーの REST URI を追加することにより、統合されたクラスターマネージャーを使用して SDN リソースを管理し、SDN インフラストラクチャを監視できます。

1. [すべての接続] の下にある [ **+ 追加**] をクリックします。
2. ハイパー集約された**クラスター接続**を追加することを選択します。
3. クラスターの名前を入力し、メッセージが表示されたら、使用する資格情報を入力します。
4. 続行するに**は、ネットワークコントローラーの構成**を確認してください。
5. **ネットワークコントローラーの URI**を入力し、[**検証**] をクリックします。
6. [**追加**] をクリックして完了します。

クラスターが接続の一覧に追加されます。 これをクリックすると、ダッシュボードが起動します。

![SDN が有効なハイパー収束クラスター接続を追加する](../media/manage-hyper-converged/add-snd-enabled-hci-connection.png)

> [!Important]
> Northbound 通信用の Kerberos 認証を使用する SDN 環境は、現在サポートされていません。

## <a name="frequently-asked-questions"></a>よく寄せられる質問

### <a name="are-there-differences-between-managing-windows-server-2016-and-windows-server-2019"></a>Windows Server 2016 と Windows Server 2019 の管理には違いがありますか。

はい。 ハイパースレッディングインフラストラクチャの windows 管理センターは、Windows Server 2016 と Windows Server 2019 の両方のエクスペリエンスを向上させる更新プログラムを頻繁に受信します。 ただし、一部の新機能は、Windows Server 2019 でのみ使用できます。たとえば、重複除去と圧縮の切り替えスイッチなどです。

### <a name="can-i-use-windows-admin-center-to-manage-storage-spaces-direct-for-other-use-cases-not-hyper-converged-such-as-converged-scale-out-file-server-sofs-or-microsoft-sql-server"></a>Windows 管理センターを使用して、収束スケールアウトファイルサーバー (SoFS) や Microsoft SQL Server など、他のユースケースの記憶域スペースダイレクトを管理できますか。

ハイパー集約型インフラストラクチャの Windows 管理センターでは、記憶域スペースダイレクトの他のユースケースに特に管理オプションや監視オプションは提供されません。たとえば、ファイル共有を作成することはできません。 ただし、ダッシュボードと主要機能 (ボリュームの作成やドライブの交換など) は、記憶域スペースダイレクトクラスターに対して機能します。

### <a name="whats-the-difference-between-a-failover-cluster-and-a-hyper-converged-cluster"></a>フェールオーバークラスターとハイパー集約クラスターの違いは何ですか。

一般に、"ハイパー収束" という用語は、同じクラスターサーバー上で Hyper-v と記憶域スペースダイレクトを実行して、コンピューティングリソースと記憶域リソースを仮想化することを意味します。 Windows 管理センターのコンテキストで、[接続] 一覧から [ **+ 追加**] をクリックすると、**フェールオーバークラスター接続**またはハイパー集約された**クラスター接続**のいずれかを選択できます。

- **フェールオーバークラスター接続**は、フェールオーバークラスターマネージャーデスクトップアプリの後継です。 Microsoft SQL Server を含む任意のワークロードをサポートするすべてのクラスターに、使い慣れた汎用管理エクスペリエンスを提供します。 Windows Server 2012 以降で使用できます。

- **ハイパー収束クラスター接続**は、記憶域スペースダイレクトと hyper-v 向けにカスタマイズされたすべての新しいエクスペリエンスです。 ダッシュボードを備え、監視のためのグラフとアラートが重視されています。 Windows Server 2016 および Windows Server 2019 で使用できます。

### <a name="why-do-i-need-the-latest-cumulative-update-for-windows-server-2016"></a>Windows Server 2016 の最新の累積的な更新プログラムが必要なのはなぜですか。

ハイパースレッディングインフラストラクチャ用の windows 管理センターは、Windows Server 2016 のリリース以降に開発された管理 Api に依存します。 これらの Api は、2018-05 2018 年5月8の時点で利用可能な、 [Windows Server 2016 用の累積的な更新プログラム (KB4103723)](https://support.microsoft.com/help/4103723/windows-10-update-kb4103723)に追加されています。

### <a name="how-much-does-it-cost-to-use-windows-admin-center"></a>Windows Admin Center を使用するにはいくらかかりますか。

Windows Admin Center には、Windows 以外の追加コストはかかりません。

Windows Admin Center (別のダウンロードとして利用可能) は、Windows Supplemental EULA に基づいて使用許諾されているため、Windows Server または Windows 10 の有効なライセンスと共に追加コストなしで使用することができます。

### <a name="does-windows-admin-center-require-system-center"></a>Windows Admin Center に System Center は必要ですか。

いいえ。

### <a name="does-it-require-an-internet-connection"></a>インターネットに接続する必要がありますか。

いいえ。

Windows 管理センターは Microsoft Azure クラウドとの強力で便利な統合機能を備えていますが、ハイパー集約型インフラストラクチャのコア管理と監視のエクスペリエンスは、完全にオンプレミスにあります。 インターネットに接続せずにインストールして使用することができます。

## <a name="things-to-try"></a>対処方法

作業を開始するだけであれば、次の簡単なチュートリアルでは、Windows 管理センターでのハイパー集約インフラストラクチャの構成と動作について説明しています。 適切な略しを使用して、運用環境に注意してください。 これらのビデオは、Windows 管理センターバージョン1804と、Windows Server 2019 の Insider Preview ビルドで記録されています。

### <a name="manage-storage-spaces-direct-volumes"></a>記憶域スペースダイレクトボリュームの管理

<ul>
               <li>(0:37) <a href="https://youtu.be/o66etKq70N8">3 方向ミラーボリュームを作成する方法</a></li>
               <li>(1:17)<a href="https://youtu.be/R72QHudqWpE">ミラーアクセラレータのパリティボリュームを作成する方法</a></li>
               <li>(1:02)<a href="https://youtu.be/j59z7ulohs4">ボリュームを開いてファイルを追加する方法</a></li>
               <li>(0:51)<a href="https://youtu.be/PRibTacyKko">重複除去と圧縮を有効にする方法</a></li>
               <li>(0:47)<a href="https://youtu.be/hqyBzipBoTI">ボリュームを拡張する方法</a></li>
               <li>(0:26)<a href="https://youtu.be/DbjF8r2F6Jo">ボリュームを削除する方法</a></li>
</ul>

<table>
    <tr style="border: 0;">
        <td style="padding: 5px; border: 0;">
            <strong>ボリュームの作成、3方向ミラー</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/o66etKq70N8" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
        <td style="padding: 5px; border: 0;">
            <strong>ボリュームの作成、ミラーアクセラレータのパリティ</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/R72QHudqWpE" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 5px; border: 0;">
            <strong>ボリュームを開き、ファイルを追加する</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/j59z7ulohs4" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
        <td style="padding: 5px; border: 0;">
            <strong>重複除去と圧縮を有効にする</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/PRibTacyKko" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 5px; border: 0;">
            <strong>ボリュームの展開</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/hqyBzipBoTI" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
        <td style="padding: 5px; border: 0;">
            <strong>ボリュームの削除</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/DbjF8r2F6Jo" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
    </tr>
</table>

### <a name="create-a-new-virtual-machine"></a>新しい仮想マシンを作成します

1. 左側のナビゲーションウィンドウで [ **Virtual Machines** ] ツールをクリックします。
2. Virtual Machines ツールの上部で、[**インベントリ**] タブを選択し、[**新規**] をクリックして新しい仮想マシンを作成します。
3. 仮想マシン名を入力し、第1世代と第2世代の仮想マシンを選択します。
4. その後、uou は、最初に仮想マシンを作成するホストを選択するか、推奨されるホストを使用します。
5. 仮想マシンファイルのパスを選択します。 ドロップダウンリストからボリュームを選択するか、[**参照**] をクリックしてフォルダーピッカーを使用してフォルダーを選択します。 仮想マシンの構成ファイルと仮想ハードディスクファイルは、 `\Hyper-V\[virtual machine name]` 選択したボリュームまたはパスのパスにある1つのフォルダーに保存されます。
6. 仮想プロセッサの数を選択して、入れ子になった仮想化を有効にするかどうか、メモリ設定、ネットワークアダプター、仮想ハードディスクを構成し、.iso イメージファイルからオペレーティングシステムをインストールするか、ネットワークからインストールするかを選択します。
7. **[作成]** をクリックして、バーチャル マシンを作成します。
8. 仮想マシンが作成され、仮想マシンの一覧に表示されたら、仮想マシンを起動できます。
9. 仮想マシンが起動したら、VMConnect を使用して仮想マシンのコンソールに接続し、オペレーティングシステムをインストールできます。 一覧から仮想マシンを選択し、[**その他**の  >  **接続**] をクリックして .rdp ファイルをダウンロードします。 リモートデスクトップ接続アプリで .rdp ファイルを開きます。 これは仮想マシンのコンソールに接続しているため、Hyper-v ホストの管理者の資格情報を入力する必要があります。

[詳細については、Windows 管理センターを使用した仮想マシンの管理に関するページをご覧](manage-virtual-machines.md)ください。

### <a name="pause-and-safely-restart-a-server"></a>サーバーを一時停止して安全に再起動する

1. **ダッシュボード**で、左側のナビゲーションから [**サーバー** ] を選択するか、ダッシュボードの右下隅にあるタイルの [ **VIEW servers >** ] リンクをクリックします。
2. 上部にある [**概要**] から [**インベントリ**] タブに切り替えます。
3. サーバーの名前をクリックしてサーバーを選択し、**サーバー**の詳細ページを開きます。
4. [**メンテナンスのためにサーバーを一時停止する] を**クリックします。 続行しても問題ない場合は、仮想マシンがクラスター内の他のサーバーに移動されます。 このエラーが発生すると、サーバーの状態がドレインされます。 必要に応じて、[仮想マシン **> インベントリ**] ページで仮想マシンの移動を見ることができます。このページでは、ホストサーバーがグリッドで明確に表示されます。 すべてのバーチャルマシンが移動されると、サーバーの状態は [**一時停止**] になります。
5. Windows 管理センターのサーバーごとの管理ツールにアクセスするには、[**サーバーの管理**] をクリックします。
6. [**再起動**]、[**はい]** の順にクリックします。 [接続] の一覧に戻ります。
7. **ダッシュボード**に戻ると、サーバーはダウンしている間、赤で色付けされます。
8. バックアップが完了したら、 **[サーバー] ページに**移動し、[**メンテナンスからサーバーを再開**する] をクリックして、サーバーの状態を単に up に戻します。 時間の経過とともに、仮想マシンは元の状態に戻ります。ユーザーの操作は必要ありません。

### <a name="replace-a-failed-drive"></a>障害が発生したドライブを交換する

1. ドライブに障害が発生すると、**ダッシュボード**の左上の**アラート**領域にアラートが表示されます。
2. また、左側にあるナビゲーションから **[ドライブ]** を選択するか、右下隅にあるタイルで **[VIEW DRIVES >]\(ドライブの表示 >\)** リンクをクリックして、ドライブを参照してその状態を自分で確認することもできます。 [**インベントリ**] タブでは、グリッドは並べ替え、グループ化、およびキーワード検索をサポートしています。
3. **ダッシュボード**からアラートをクリックすると、ドライブの物理的な場所などの詳細が表示されます。
4. 詳細については、 **[ドライブ]** 詳細ページへの **[Go to drive]\(ドライブに移動\)** ショートカットをクリックします。
5. ハードウェアでサポートされている場合は、 **[Turn light on/off]\(ライトをオンにする/オフにする\)** をクリックして、ドライブのインジケーター ライトを制御できます。
6. 記憶域スペース ダイレクトは、障害が発生したドライブを自動的に廃止して退避させます。 これが発生すると、ドライブの状態は廃止になり、記憶域容量バーは空になります。
7. 障害が発生したドライブを取り外し、代わりのものを挿入します。
8. **[ドライブ] > [インベントリ]** に新しいドライブが表示されます。 しばらくしてアラートが消去されると、ボリュームは OK 状態に戻り、記憶域は新しいドライブに再調整されます。ユーザー操作は不要です。

### <a name="manage-virtual-networks-sdn-enabled-hci-clusters-using-windows-admin-center-preview"></a>仮想ネットワークを管理する (Windows 管理センタープレビューを使用して SDN 対応 HCI クラスター)

1. 左側のナビゲーションから [**仮想ネットワーク**] を選択します。
2. [**新規**] をクリックして新しい仮想ネットワークとサブネットを作成するか、既存の仮想ネットワークを選択して [**設定**] をクリックし、その構成を変更します。
3. 既存の仮想ネットワークをクリックすると、仮想ネットワークのサブネットへの VM 接続と、仮想ネットワークのサブネットに適用されるアクセス制御リストが表示されます。

![仮想ネットワークの管理](../media/manage-hyper-converged/manage-virtual-networks.png)

### <a name="connect-a-virtual-machine-to-a-virtual-network-sdn-enabled-hci-clusters-using-windows-admin-center-preview"></a>仮想マシンを仮想ネットワークに接続する (Windows 管理センタープレビューを使用して SDN 対応 HCI クラスター)

1. 左側のナビゲーションから [ **Virtual Machines** ] を選択します。
2. 既存の仮想マシンを選択し > [**設定**] をクリックし > [**設定**] の [**ネットワーク**] タブを開きます。
3. 仮想マシンを仮想ネットワークに接続するように**Virtual Network**と**仮想サブネット**のフィールドを構成します。

仮想マシンの作成時に仮想ネットワークを構成することもできます。

![仮想マシンを仮想ネットワークに接続する](../media/manage-hyper-converged/connect-vm-to-virtual-network.png)

### <a name="monitor-software-defined-networking-infrastructure-sdn-enabled-hci-clusters-using-windows-admin-center-preview"></a>ソフトウェアによるネットワークインフラストラクチャの監視 (Windows 管理センタープレビューを使用した SDN 対応 HCI クラスター)

1. 左側のナビゲーションから [ **SDN 監視**] を選択します。
2. ネットワークコントローラー、ソフトウェア Load Balancer、仮想ゲートウェイの正常性に関する詳細情報を表示し、仮想ゲートウェイプール、パブリックおよびプライベート IP プールの使用状況と SDN ホストの状態を監視します。

![SDN インフラストラクチャを監視する](../media/manage-hyper-converged/sdn-monitoring.png)

## <a name="give-us-feedback"></a>フィードバックの送信

ご意見をお寄せください。 頻繁に更新される最も重要な利点は、作業内容と改善が必要な機能を確認することです。 検討している内容を確認するには、次の方法を使用します。

- [UserVoice で機能要求を送信して投票する](https://windowsserver.uservoice.com/forums/295071/category/319162?query=%5Bhci%5D)
- [Microsoft Tech Community で Windows 管理センターフォーラムに参加する](https://techcommunity.microsoft.com/t5/Windows-Server-Management/bd-p/WindowsServerManagement)
- ツイート`@servermgmt`

### <a name="additional-references"></a>その他の参照情報

- [Windows Admin Center](../overview.md)
- [記憶域スペース ダイレクト](../../../storage/storage-spaces/storage-spaces-direct-overview.md)
- [Hyper-V](../../../virtualization/hyper-v/hyper-v-on-windows-server.md)
- [ソフトウェア定義ネットワーク](../../../networking/sdn/software-defined-networking.md)