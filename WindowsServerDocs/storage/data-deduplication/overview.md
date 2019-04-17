---
ms.assetid: 4b844404-36ba-4154-aa5d-237a3dd644be
title: "データ重複除去の概要"
ms.technology: storage-deduplication
ms.prod: windows-server-threshold
ms.topic: article
author: wmgries
manager: klaasl
ms.author: wgries
ms.date: 05/09/2017
ms.openlocfilehash: 4344108f96d14475c15a31bd1ab917e7fc78ef9f
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2017
---
# <a name="data-deduplication-overview"></a>データ重複除去の概要

> 適用対象: Windows Server (半期チャネル)、Windows Server 2016

## <a name="what-is-dedup"></a>データ重複除去とは何ですか。

データ重複除去は、省略して重複除去とも呼ばれ、冗長なデータによる記憶域コストへの影響を軽減するために役立つ Windows Server 2016 の機能です。 有効にすると、データ重複除去により、ボリューム上の重複している部分が検索され、ボリューム上のデータが検査されて、ボリューム上の空き領域が最適化されます。 ボリューム上のデータセットの重複する部分は、1 回だけ保存され、さらに節減するために (必要に応じて) 圧縮されます。 データ重複除去では、データの忠実性や完全性を損なうことなく冗長性を最適化します。 データ重複除去のしくみの詳細については、「[データ重複除去のしくみ](understand.md#how-does-dedup-work)」 セクション (「[データ重複除去とは](understand.md)」ページ) を参照してください。

> [!Important]  
> [KB4025334](https://support.microsoft.com/kb/4025334) には、信頼性についての重要な修正データを含め、重複除去に関する修正のロールアップが含まれているため、Windows Server 2016 でデータ重複除去を使う場合はインストールすることを強くお勧めします。

## <a name="why-is-dedup-useful"></a>データ重複除去はなぜ有用ですか。

記憶域管理者はデータ重複除去を使用して、重複データに関連するコストを削減できます。 大規模なデータセットには**<u>大量の</u>**重複が存在することが多く、データを格納するコストを増しています。 以下に例を示します。

- ユーザー ファイル共有は同じ、または類似するファイルのコピーを多く含むことがあります。
- 仮想化ゲストは VM 間でほぼ同じであることがあります。
- 毎日のバックアップ スナップショットの内容は、わずかな違いであることがあります。

データ重複除去から得られる領域の節約は、データセットや、ボリューム上のワークロードに依存します。 重複の多いデータセットでは、最大 95% の最適化率、つまり記憶域使用率が 20 分の 1 になることがあります。 以下の表は、各種コンテンツに対して重複除去を行った場合の標準的な削減効果を示しています。

| シナリオ       | コンテンツ                                        | 標準的な削減効果 |
|----------------|------------------------------------------------|-----------------------|
| ユーザー ドキュメント | Office ドキュメント、写真、ミュージック、ビデオなど  | 30 ～ 50%                |
| 展開共有 | ソフトウェア バイナリ、cab ファイル、シンボルなど | 70 ～ 80%                |
| 仮想化ライブラリ | ISO、仮想ハード ディスク ファイルなど  | 80 ～ 95%                |
| 一般的なファイル共有 | 上記すべて                           | 50 ～ 60%                |

## <a id="when-can-dedup-be-used"></a>データ重複除去はどのような場合に使用できますか。  
<table>
    <tbody>
        <tr>
            <td style="text-align:center;min-width:150px;vertical-align:center;"><img src="media/overview-clustered-gpfs.png" alt="Illustration of file servers" /></td>
            <td style="vertical-align:top">
                <b>汎用ファイル サーバー</b><br />
汎用ファイル サーバーは、次に示す任意の種類の共有を含む可能性のある一般的な用途のファイル サーバーです。 <ul>
                    <li>チームの共有</li>
                    <li>ユーザー ホーム フォルダー</li>
                    <li><a href="https://technet.microsoft.com/library/dn265974.aspx">ワーク フォルダー</a></li>
                    <li>ソフトウェア開発用の共有</li>
                </ul>
汎用ファイル サーバーでは、同じファイルの多くのコピーまたはバージョンを複数のユーザーが所有する傾向があるため、データ重複除去の有力候補です。 ソフトウェア開発用の共有は、多くのバイナリがビルドごとに基本的に変更されていないため、データ重複除去の恩恵を受けることになります。 
            </td>
        </tr>
        <tr>
            <td style="text-align:center;min-width:150px;vertical-align:center;"><img src="media/overview-vdi.png" alt="Illustration of VDI servers" /></td>
            <td style="vertical-align:top">
                <b>仮想デスクトップ インフラストラクチャ (VDI) の展開</b><br />
<a href="https://technet.microsoft.com/library/cc725560.aspx">リモート デスクトップ サービス</a>などの VDI サーバーは、組織がユーザーにデスクトップをプロビジョニングするための軽量のオプションになります。 組織がこのようなテクノロジに頼る理由はさまざまです。 <ul>
                    <li><b>アプリケーションの展開</b>: 社内全体にアプリケーションをすばやく展開できます。 これは、頻繁に更新されるアプリケーション、使用頻度の低いアプリケーション、または管理しにくいアプリケーションがあるときに特に便利です。</li>
                    <li><b>アプリケーションの統合</b>: 一連の集中管理された仮想マシンからアプリケーションをインストールし、実行すると、クライアント コンピューターでアプリケーションを更新する必要がなくなります。 このオプションで、アプリケーションにアクセスするために必要なネットワーク帯域幅の量も減少します。</li>
                    <li><b>リモート アクセス</b>: ユーザーは自宅のコンピューター、キオスク、処理能力の低いハードウェア、Windows 以外のオペレーティング システムなどのデバイスからエンタープライズ アプリケーションにアクセスできます。</li>
                    <li><b>ブランチ オフィス アクセス</b>: VDI 展開は一元化されたデータ ストアにアクセスする必要のあるブランチ オフィスの作業者に対してアプリケーションのパフォーマンスを向上することができます。 データ負荷の高いアプリケーションは、低速な接続用に最適化されたクライアント/サーバー プロトコルに対応していないことがあります。</li>
                </ul>
VDI 展開では、ユーザー用にリモート デスクトップを駆動する仮想ハード ディスクが実質的に同じであるためデータ重複除去の有力候補です。 さらに、データ重複除去は、いわゆる「*VDI ブート ストーム*」を軽減できます。VDI ブート ストームとは、多くのユーザーが 1 日の始まりに同時に自分のデスクトップにログオンして記憶域のパフォーマンスが低下する状況です。
            </td>
        </tr>
        <tr>
            <td style="text-align:center;min-width:150px;vertical-align:center;"><img src="media/overview-backup.png" alt="Illustration of backup applications" /></td>
            <td style="vertical-align:top">
                <b>仮想化されたバックアップ アプリケーションなどのバックアップ先</b><br />
バックアップ スナップショット間には大幅な重複があるため、<a href="https://technet.microsoft.com/library/hh758173.aspx">Microsoft Data Protection Manager (DPM)</a> などのバックアップ アプリケーションはデータ重複除去の有力候補です。
            </td>
        </tr>
        <tr>
            <td style="text-align:center;min-width:150px;vertical-align:center;"><img src="media/overview-other.png" alt="Illustration of other workloads" /></td>
            <td style="vertical-align:top">
                <b>その他のワークロード</b><br />
                [その他のワークロードもデータ重複除去の有力候補になります](install-enable.md#enable-dedup-candidate-workloads)。
            </td>
        </tr>
    </tbody>
</table>
