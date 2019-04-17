---
title: Windows Admin Center でハイパーコンバージド インフラストラクチャを管理します。
description: Windows Admin Center (Project Honolulu) で、ハイパーコンバージド インフラストラクチャを管理します。
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 03/01/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 9ce4381735746ace6358aa2cb30f8b341c576054
ms.sourcegitcommit: e558dda2774345e9ad17ff04b759f68c59d88139
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2019
ms.locfileid: "9262845"
---
# Windows Admin Center でハイパーコンバージド インフラストラクチャを管理します。

>適用対象: Windows Admin Center、Windows Admin Center Preview

## ハイパーコンバージド インフラストラクチャします。

ハイパーコンバージド インフラストラクチャは、ソフトウェア定義のコンピューティング、ストレージ、および高パフォーマンスの高いを提供する 1 つのクラスターと簡単に拡張可能な仮想化にネットワークを統合します。 この機能は、[記憶域スペース ダイレクト](https://docs.microsoft.com/windows-server/storage/storage-spaces/storage-spaces-direct-overview)、[ソフトウェア定義ネットワーク](https://docs.microsoft.com/en-us/windows-server/networking/sdn/software-defined-networking)および[HYPER-V](https://docs.microsoft.com/windows-server/virtualization/hyper-v/hyper-v-on-windows-server)と Windows Server 2016 で導入されました。

> [!Tip]
> ハイパーコンバージド インフラストラクチャを取得しようとしているかどうか。 Microsoft では、パートナーからこれらの[Windows Server ソフトウェア定義](https://microsoft.com/wssd)ソリューションをお勧めします。 設計、アセンブル、され互換性と取得するための信頼性と迅速に実行されていることを確認するには、当社の参照アーキテクチャに照らして検証します。

> [!IMPORTANT]
> この記事で説明されている機能の一部は、Windows Admin Center Preview で利用可能なのみです。 [このバージョンを取得する方法](http://aka.ms/windowsadmincenter)

## Windows Admin Center とは

[Windows Admin Center](../understand/windows-admin-center.md)は、Windows Server、サーバー マネージャーのような従来の「インボックス」ツールを後続の次世代の管理ツールです。 無料し、インストールされているし、インターネット接続がない場合に使うことができます。 Windows Admin Center を使用して、管理および Windows Server 2016 または Windows Server 2019 を実行しているハイパーコンバージド インフラストラクチャを監視することができます。

![ハイパーコンバージド クラスターのダッシュ ボード](../media/manage-hyper-converged/hci-dashboard-v1809.png)

## 主な機能

Windows Admin Center でハイパーコンバージド インフラストラクチャの概要は次のとおりです。

- **統一された単一のウィンドウの-まとめられたコンピューティング、ストレージ、およびネットワークのすぐにします。** 仮想マシン、ホスト サーバー、ボリューム、ドライブ、および 1 つの目的に特化した、一貫性があり、相互接続されたエクスペリエンス内で詳細を表示します。
- **作成および記憶域スペースと HYPER-V 仮想マシンを管理します。** 根本的に単純なワークフローを作成、開く、サイズ変更、およびボリュームを削除するには作成、開始、接続し、仮想マシンの移動その他。
- **強力なクラスター全体を監視します。** ダッシュ ボード グラフ メモリと CPU 使用率、記憶域の容量、IOPS、スループット、および待機時間で何かが適切でないとき、明確なアラートを持つ、クラスター内のすべてのサーバー間で、リアルタイムします。
- **ソフトウェア定義ネットワーク (SDN) のサポート。** 管理し [サブネットの仮想ネットワークを監視して、仮想マシンを仮想ネットワークに接続および SDN インフラストラクチャを監視します。

Windows Admin Center でハイパーコンバージド インフラストラクチャの Microsoft によってアクティブに開発中です。 既存の機能を向上し、新しい機能を追加する頻繁に更新プログラムを受け取ります。

## 開始前の作業

Windows Admin Center でハイパーコンバージド インフラストラクチャとして、クラスターを管理する必要がありますが実行されているは、Windows Server 2016 または Windows Server 2019 では、し、HYPER-V と記憶域スペース ダイレクトを有効にします。 必要に応じて、それも含むことが有効になっているし、Windows Admin Center を通じて管理されているソフトウェア定義ネットワークします。

> [!Tip]
> Windows Admin Center では、汎用的な管理は、Windows Server 2012 以降に利用可能な任意のワークロードをサポートする、クラスターのエクスペリエンスも提供しています。 Windows Admin Center に、クラスターを追加するときより適切なサウンドこの場合は、**ハイパーコンバージド クラスター**ではなく、[**フェールオーバー クラスター**](manage-failover-clusters.md)を選択します。

### Windows Admin center、Windows Server 2016 のクラスターを準備します。

Windows Admin Center でハイパーコンバージド インフラストラクチャは、Windows Server 2016 にリリースされた後に Api が追加の管理に依存します。 Windows Admin Center で、Windows Server 2016 のクラスターを管理するには、これら 2 つの手順を実行する必要があります。

1. すべてのサーバー、クラスター内の[2018 05 Windows Server 2016 (KB4103723) の累積的な更新プログラム](https://support.microsoft.com/help/4103723/windows-10-update-kb4103723)がインストールされていることを確認またはそれ以降。 ダウンロードして、この更新プログラムのインストール、**設定**に移動します。 > **& セキュリティを更新** > **Windows Update**や**Microsoft Update から更新プログラムのオンライン チェック**を] を選択します。
2. クラスター上で管理者として次の PowerShell コマンドレットを実行します。

```powershell
    Add-ClusterResourceType -Name "SDDC Management" -dll "$env:SystemRoot\Cluster\sddcres.dll" -DisplayName "SDDC Management"
```

> [!Tip]
> のみ、任意のサーバー、クラスター内で 1 回、コマンドレットを実行する必要があります。 Windows PowerShell でのローカルに実行またはリモートで実行する資格情報のセキュリティ サービス プロバイダー (CredSSP) を使用できます。 構成によっては、Windows Admin Center 内からこのコマンドレットを実行できない場合があります。

### Windows Admin Center 用、Windows Server 2019 クラスターを準備します。

クラスターは、Windows Server 2019 を実行する場合は、上記の手順は必要ありません。 次のセクションで説明するよう Windows Admin Center をクラスターに追加し、ことをお勧め go!

### ソフトウェア定義ネットワーク (省略可能) を構成します。 ###

次の手順でソフトウェア定義ネットワーク (SDN) を使用するには、Windows Server 2016 または 2019 を実行して、ハイパーコンバージド インフラストラクチャを構成することができます。

1. ハイパーコンバージド インフラストラクチャのホストにインストールされている os が同じいる OS の VHD を準備します。 この VHD は、すべてのゲートウェイ/NC/SLB Vm に対して使用されます。
2. すべてのフォルダーと SDN の Express から下にあるファイルをダウンロード[https://github.com/Microsoft/SDN/tree/master/SDNExpress](https://github.com/Microsoft/SDN/tree/master/SDNExpress)します。
3. 展開のコンソールを使用して別の VM を準備します。 この VM は、SDN のホストにアクセスできる必要があります。 また、VM には、インストールされている RSAT HYPER-V ツールが必要です。
4. 展開コンソール VM に SDN Express をダウンロードしたすべての情報をコピーします。 この**SDNExpress**フォルダーを共有します。 すべてのホスト アクセスできるように**SDNExpress**共有フォルダーでは、構成ファイルの行 8 で定義されています。
```
    \\$env:Computername\SDNExpress
```
5. OS の VHD を展開本体 VM で**SDNExpress**フォルダーの下**の画像**フォルダーにコピーします。
6. 環境のセットアップを使用して SDN が高速構成を変更します。 環境の情報に基づく SDN が高速構成を変更した後は、次の 2 つの手順を完了します。
7. SDN の展開に管理者特権で PowerShell を実行します。

```powershell
    .\SDNExpress.ps1 -ConfigurationDataFile .\your_fabricconfig.PSD1 -verbose 
```

展開は、約 30 ~ 45 分かかります。

## 概要

ハイパーコンバージド インフラストラクチャを展開すると、Windows Admin Center を使用して管理できます。

### Windows Admin Center のインストール

いない場合、ダウンロードして Windows Admin Center をインストールします。 Windows 10 コンピューターにインストールし、サーバーをリモートで管理すること取得する方法を直感的実行中です。 これにより、5 分未満がかかります。 [今すぐダウンロード](https://aka.ms/windowsadmincenter)または[その他のインストール オプションの詳細について説明します](../deploy/install.md)。

### ハイパーコンバージド クラスターを追加します。

Windows Admin Center のクラスターを追加します。

1. すべての接続 [ **+ 追加]** をクリックします。
2. **ハイパーコンバージド クラスターの接続**を追加する場合に選択します。
3. クラスターの名前を入力し、使用する資格情報を要求します。
4. 終了するための**追加**] をクリックします。

クラスターは、接続の一覧に追加されます。 ダッシュ ボードの起動をクリックします。

![ハイパーコンバージド クラスターの接続を追加します。](../media/manage-hyper-converged/add-hyper-converged-cluster-connection.gif)

### ハイパーコンバージド クラスターの SDN が有効な (Windows Admin Center Preview) を追加します。

最新の Windows Admin Center Preview では、ハイパーコンバージド インフラストラクチャのソフトウェア定義ネットワークの管理をサポートしています。 ネットワーク コント ローラーの残りの部分の URI を追加すると、ハイパーコンバージド クラスターの接続、SDN リソースを管理および SDN インフラストラクチャを監視するハイパーコンバージド クラスター マネージャーを使用することができます。

1. すべての接続 [ **+ 追加]** をクリックします。
2. **ハイパーコンバージド クラスターの接続**を追加する場合に選択します。
3. クラスターの名前を入力し、使用する資格情報を要求します。
4. 続行する**ネットワーク コント ローラーの構成**を確認します。
5. **ネットワーク コント ローラーの URI**を入力し、[**検証**] をクリックします。
6. 終了するための**追加**] をクリックします。

クラスターは、接続の一覧に追加されます。 ダッシュ ボードの起動をクリックします。

![ハイパーコンバージド クラスターの SDN 有効になっている接続を追加します。](../media/manage-hyper-converged/add-snd-enabled-hci-connection.png)

> [!Important]
> SDN 環境間の通信の Kerberos 認証では現在サポートされていません。

## よく寄せられる質問

### Windows Server 2016 および Windows Server 2019 を管理するための相違点はありますか。

はい、できます。 Windows Admin Center でハイパーコンバージド インフラストラクチャのでは、Windows Server 2016 および Windows Server 2019 の両方のエクスペリエンスを向上させる頻繁に更新を受信します。 ただし、一部の新機能では、Windows Server 2019 – 重複除去と圧縮のトグル スイッチなどの利用可能なのみです。

### Windows Admin Center を使用して他のユース ケース (いないハイパーコンバージド)、コンバージドのスケール アウト ファイル サーバー (SoFS) または Microsoft SQL Server などの記憶域スペース ダイレクトを管理できますか。

Windows Admin Center でハイパーコンバージド インフラストラクチャのでは、管理や記憶域スペース ダイレクトの他のユース ケースの専用の監視オプションは提供されません: たとえば、ファイル共有を作成できません。 ただし、ボリュームの作成や、ドライブを交換など、ダッシュ ボードとコアの機能は、記憶域スペース ダイレクト クラスターの動作します。

### フェールオーバー クラスター、ハイパーコンバージド クラスターの違いは何ですか。

一般に、HYPER-V と記憶域スペース ダイレクトを同じで実行されていることを指します「、ハイパーコンバージド」には、コンピューティングと記憶域リソースの仮想化のサーバーがクラスター化します。 Windows Admin Center のコンテキストで **+ 追加**接続の一覧からをクリックすると、**フェールオーバー クラスター接続**または**ハイパーコンバージド クラスターの接続**の追加の間で選択できます。

- **フェールオーバー クラスターの接続**では、フェールオーバー クラスター マネージャーのデスクトップ アプリを後続タスクです。 Microsoft SQL Server を含む、任意のワークロードをサポートしている任意のクラスターの使い慣れた、汎用的な管理エクスペリエンスを提供します。 Windows Server 2012 の利用可能な以降をお勧めします。

- **ハイパーコンバージド クラスターの接続**は、記憶域スペース ダイレクトおよび HYPER-V に合わせた、まったく新しいエクスペリエンスです。 ダッシュ ボードを備えており、監視のためのグラフとアラートが強調されます。 これは、Windows Server 2016 および Windows Server 2019 利用できます。

### Windows Server 2016 の最新の累積的な更新プログラムが必要する理由

Windows Admin Center でハイパーコンバージド インフラストラクチャは、Windows Server 2016 のリリース後は、Api が開発した管理によって異なります。 これらの Api は、 [Windows Server 2016 (KB4103723) の累積的な更新プログラムを 2018 05](https://support.microsoft.com/help/4103723/windows-10-update-kb4103723)、2018 年 5 月 8日以降で利用可能なに追加されます。

### Windows Admin Center を使用するにはいくらかかりますか。

Windows Admin Center には、Windows 以外の追加コストはありません。

Windows Admin Center (別のダウンロードとして利用可能) を使用するには追加コストなしで Windows Server または Windows 10 の有効なライセンスを持つ - Windows 補足 EULA は許諾します。

### Windows Admin Center に System Center は必要ですか。

いいえ。

### インターネット接続が必要ですか。

いいえ。

Windows Admin Center、強力で、Microsoft Azure クラウド、core の管理、およびハイパーコンバージド インフラストラクチャの監視エクスペリエンスの便利な統合が完全には、オンプレミスします。 インストールされているし、インターネット接続がない場合に使用されることができます。

## 対処方法

いるだけの取得を開始した場合は、Windows Admin Center でハイパーコンバージド インフラストラクチャ用の構成し、動作を理解に役立ついくつかのクイック チュートリアルを次に示します。 適切な判断を練習、運用環境に注意してください。 これらのビデオは、Windows Admin Center バージョン 1804 および Windows Server 2019 の Insider Preview ビルドで記録されています。

### 記憶域スペース ダイレクトのボリュームを管理します。

<ul>
               <li>(0:37) <a href="https://youtu.be/o66etKq70N8">3 方向ミラーリング ボリュームを作成する方法</a></li>
               <li>(1:17) <a href="https://youtu.be/R72QHudqWpE">- ミラーリングによってパリティ ボリュームを作成する方法</a></li>
               <li>(1:02)<a href="https://youtu.be/j59z7ulohs4">ボリュームを開くし、ファイルを追加する方法</a></li>
               <li>(0:51)<a href="https://youtu.be/PRibTacyKko">重複除去と圧縮有効にする方法</a></li>
               <li>(0:47)<a href="https://youtu.be/hqyBzipBoTI">ボリュームを拡張する方法</a></li>
               <li>(0:26)<a href="https://youtu.be/DbjF8r2F6Jo">ボリュームを削除する方法</a></li>
</ul>

<table>
    <tr style="border: 0;">
        <td style="padding: 5px; border: 0;">
            <strong>3 方向ミラーリングのボリュームを作成します。</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/o66etKq70N8" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
        <td style="padding: 5px; border: 0;">
            <strong>ミラーリングによってパリティ ボリュームを作成します。</strong>
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
            <strong>ボリュームを展開します。</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/hqyBzipBoTI" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
        <td style="padding: 5px; border: 0;">
            <strong>ボリュームを削除します。</strong>
            <iframe width="375" height="210" src="https://www.youtube-nocookie.com/embed/DbjF8r2F6Jo" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen="allowfullscreen"></iframe>
        </td>
    </tr>
</table>

### 新しい仮想マシンを作成する

1. 左側のナビゲーション ウィンドウから**仮想マシン**をクリックします。
2. 仮想マシンのツールの上部には、**インベントリ**] タブを選択し、新しい仮想マシンの作成を**新規作成**] をクリックします。
3. 仮想マシンの名前を入力し、1 と 2 世代仮想マシン間で選択します。
4. いたを最初に、仮想マシンを作成または推奨のホストを使用するホストを選択できます。
5. 仮想マシンのファイルのパスを選択します。 ドロップダウン リストからボリュームを選択するか、**参照**フォルダー ピッカーを使用してフォルダーを選択する] をクリックします。 仮想マシン構成ファイルと仮想ハード ディスク ファイルは、1 つのフォルダーの下に保存されます、`\Hyper-V\[virtual machine name]`選択したボリュームまたはパスのパス。
6. 入れ子になった仮想化が有効になっているメモリの設定、ネットワーク アダプター、仮想ハード_ディスクを構成し、.iso イメージ ファイルから、またはネットワークからオペレーティング システムをインストールするかどうかを選択するかどうかは、仮想プロセッサの数を選択します。
7. **作成**仮想マシンを作成する] をクリックします。
8. 仮想マシンを作成し、仮想マシンの一覧に表示される、仮想マシンを開始できます。
9. 仮想マシンが起動されると、オペレーティング システムをインストールする VMConnect 経由で、仮想マシンのコンソールに接続できます。 一覧から、仮想マシンを選択し、[**詳細**] をクリックして > .rdp ファイルをダウンロードして**接続**します。 リモート デスクトップ接続アプリで .rdp ファイルを開きます。 これは、仮想マシンのコンソールに接続しているため、HYPER-V ホストの管理者の資格情報を入力する必要があります。

[Windows Admin Center で仮想マシンの管理について詳しく説明します](manage-virtual-machines.md)。

### 一時停止し、サーバーを安全に再起動

1. **ダッシュ ボード**で、左側にあるか、タイル上で、ダッシュ ボードの右下隅の**サーバーの表示 _gt**リンクをクリックして、ナビゲーションから**サーバー**を選択します。
2. 上部で、[**概要**から [**インベントリ**] タブに切り替えます。
3. サーバーを選択するには、**サーバー**の詳細ページを開くには、その名前をクリックします。
4. **メンテナンスのためサーバーを一時停止**をクリックします。 安全に続行は、これにより、クラスター内の他のサーバーに仮想マシンが移動します。 サーバーは、この処理中もステータスのドレインがあります。 する場合は、**仮想マシン _gt インベントリ**] ページで、そのホスト サーバーが明確に、グリッド内に表示される場所に移動する仮想マシンを監視することができます。 すべての仮想マシンが移動する場合、サーバーの状態が**一時停止**になります。
5. Windows Admin Center ですべてのサーバーごとの管理ツールにアクセスする**管理サーバー**をクリックします。
6. **再起動**し、[**はい]** をクリックします。 接続の一覧に戻る kicked されます。
7. **ダッシュ ボード**にもう一度サーバー、赤い停止中にします。
8. もう一度上げる必要があるが、もう一度**サーバー**のページに移動し、**メンテナンスから再開サーバー**を単にサーバーの状態を設定する] をクリックします。 時刻の時の仮想マシンが戻る – ユーザー操作は必要ありません。

### 障害が発生したドライブを交換します。

1. とき、ドライブが失敗し、**ダッシュ ボード**の左上の**アラート**の領域で警告が表示されます。
2. 左側のナビゲーションから**ドライブ**を選択するか、ドライブを参照して、それらの状態を自分で確認に右下隅のタイルに**表示ドライブ _gt**リンクをクリックします。 **インベントリ**] タブでは、グリッドは、並べ替え、グループ化、およびキーワード検索をサポートします。
3. **ダッシュ ボード**からアラートをクリックして、ドライブの物理的な場所などの詳細を参照してください。
4. 詳細についてはを**ドライブ**の詳細ページに、**ドライブに移動**のショートカットをクリックします。
5. ハードウェア サポートする場合、ドライブのライトを制御するための**オン/オフのライトを有効にする**をクリックできます。
6. 記憶域スペース ダイレクトに自動的にによるし、障害が発生したドライブを evacuates します。 ドライブのステータスを廃棄すると、これが発生した場合、その記憶域容量のバーが空です。
7. 障害が発生したドライブを削除し、その代替を挿入します。
8. **ドライブの _gt インベントリ**] で、新しいドライブが表示されます。 時刻の時にアラートはクリア ボリュームは、[ok] の状態に戻す修復し記憶域は、新しいドライブ上に再調整 – ユーザー操作は必要ありません。

### 仮想ネットワーク (SDN が有効な HCI クラスターが Windows Admin Center Preview を使用して) の管理します。

1. 左側のナビゲーションから**仮想ネットワーク**を選択します。
2. 新しい仮想ネットワークとサブネット、作成または既存の仮想ネットワークを選択し、構成を変更する**設定**] をクリックしての**新規作成**] をクリックします。
3. 仮想ネットワークのサブネットに VM 接続を表示して、アクセス制御リストの仮想ネットワークのサブネットに適用する既存の仮想ネットワークをクリックします。

![仮想ネットワークを管理します。](../media/manage-hyper-converged/manage-virtual-networks.png)

### 仮想マシンを仮想ネットワーク (SDN が有効な HCI クラスターが Windows Admin Center Preview を使用して) に接続します。

1. 左側のナビゲーションから**仮想マシン**を選択します。
2. 既存の仮想マシン _gt クリックを選択して**設定**_gt が**設定**で**ネットワーク**] タブを開きます。
3. 仮想マシンを仮想ネットワークに接続する**仮想ネットワーク**と**仮想サブネット**のフィールドを構成します。

仮想マシンを作成するときは、仮想ネットワークを構成することもできます。

![仮想マシンを仮想ネットワークに接続します。](../media/manage-hyper-converged/connect-vm-to-virtual-network.png)

### ソフトウェア定義ネットワーク インフラストラクチャの監視 (Windows Admin Center Preview を使用して SDN が有効な HCI クラスター)

1. 左側のナビゲーションから**SDN の監視**を選択します。
2. ネットワーク コント ローラー、ソフトウェア ロード バランサー、仮想ゲートウェイの正常性に関する詳細情報を表示し、仮想ゲートウェイ プール、パブリック シンボルとプライベート IP プールの使用量と SDN ホストのステータスを監視します。

![SDN インフラストラクチャの監視](../media/manage-hyper-converged/sdn-monitoring.png)

## フィードバック

これは、お客様のフィードバックの概要ができました。 頻繁に更新プログラムの最も重要な利点は、何が動作するいると改善が必要なものです。 何を考えているを知らせ、いくつかの方法を示します。

- [提出し、UserVoice の機能の要求を投票](https://windowsserver.uservoice.com/forums/295071/category/319162?query=%5Bhci%5D)
- [Windows Admin Center で Microsoft テクニカル コミュニティ フォーラムに参加します。](https://techcommunity.microsoft.com/t5/Windows-Server-Management/bd-p/WindowsServerManagement)
- ツイートする `@servermgmt`

### 関連項目

- [Windows Admin Center](../understand/windows-admin-center.md)
- [記憶域スペース ダイレクト](https://docs.microsoft.com/windows-server/storage/storage-spaces/storage-spaces-direct-overview)
- [Hyper-V](https://docs.microsoft.com/windows-server/virtualization/hyper-v/hyper-v-on-windows-server)
- [ソフトウェア定義ネットワーク](https://docs.microsoft.com/windows-server/networking/sdn/software-defined-networking)
