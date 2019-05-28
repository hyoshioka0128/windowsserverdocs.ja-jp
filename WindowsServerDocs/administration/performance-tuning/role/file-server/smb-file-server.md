---
title: SMB ファイル サーバーのパフォーマンス チューニング
description: SMB ファイル サーバーのパフォーマンス チューニング
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
author: phstee
ms.author: NedPyle; Danlo; DKruse
ms.date: 4/14/2017
ms.openlocfilehash: 337716792a4bb3cf730b723df3abe1029631426b
ms.sourcegitcommit: 8ba2c4de3bafa487a46c13c40e4a488bf95b6c33
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/25/2019
ms.locfileid: "66222503"
---
# <a name="performance-tuning-for-smb-file-servers"></a>SMB ファイル サーバーのパフォーマンス チューニング

## <a name="smb-configuration-considerations"></a>SMB の構成に関する考慮事項
任意のサービスや、ファイル サーバーとクライアントを必要としない機能を有効にしないでください。 SMB 署名、クライアント側のキャッシュ、ファイル システムのミニ フィルター、検索サービス、スケジュールされたタスク、NTFS 暗号化、NTFS 圧縮、IPSEC、ファイアウォール フィルター、Teredo、および SMB が含まれますが暗号化されます。

高パフォーマンス モードを含めることができる C 状態を変更またはオペレーティング システムの電源管理のモードと BIOS 設定されている、必要に応じて確認します。 最新、最も力が最も高速のストレージとネットワーク デバイス ドライバーがインストールされていることを確認します。

ファイル サーバーで実行される一般的な操作は、ファイルをコピーします。 Windows Server では、コマンド プロンプトを使用して実行できるいくつかの組み込みのファイル コピー ユーティリティがあります。 Robocopy をお勧めします。 Windows Server 2008 r2 で導入された、 **/mt** Robocopy のオプションが複数の小さなファイルをコピーするときに、複数のスレッドを使用して、リモート ファイル転送速度を大幅に改善できます。 使用してお勧め、 **/log**コンソール出力を NUL デバイスまたはファイルにログをリダイレクトすることで軽減するオプション。 追加することをお勧め Xcopy を使用すると、 **/q**と **/k**オプション、既存のパラメーターにします。 前者のオプション オーバーヘッドが削減 CPU コンソール出力を減らすことでされ、後者のネットワーク トラフィックが減少します。

## <a name="smb-performance-tuning"></a>SMB のパフォーマンス チューニング


ファイル サーバーのパフォーマンスと使用可能なチューニングは、各クライアントとサーバー間でネゴシエートされる SMB プロトコルにおよび、配置されたファイル サーバーの機能に依存します。 現在使用可能な最も高いプロトコルのバージョンでは、Windows Server 2016 および Windows 10 での SMB 3.1.1 です。 SMB のバージョンが Windows PowerShell を使用して、ネットワーク上で使用が確認できます**Get SMBConnection**クライアントと**Get SMBSession |FL**サーバー。

### <a name="smb-30-protocol-family"></a>SMB 3.0 プロトコル ファミリ

SMB 3.0 は Windows Server 2012 で導入された、Windows Server 2012 R2 (SMB 3.02) および Windows Server 2016 (SMB 3.1.1) でさらに強化されています。 このバージョンでは、ファイル サーバーのパフォーマンスと可用性が大幅に改善するテクノロジが導入されました。 詳細については、次を参照してください。[の SMB の Windows Server 2012 および 2012 R2 2012](https://aka.ms/smb3plus)と[3.1.1 の SMB の新](https://aka.ms/smb311)します。



### <a name="smb-direct"></a>SMB ダイレクト

SMB ダイレクトには、高スループットの低待機時間と CPU 使用率が低いと RDMA のネットワーク インターフェイスを使用する機能が導入されました。

SMB は、rdma 対応のネットワークが検出されるたびに自動的に RDMA 機能を使用する試みます。 ただし、何らかの理由により、SMB クライアントは、RDMA のパスを使用して接続する失敗した場合、単に引き続き TCP/IP 接続の代わりに使用します。 また、TCP/IP スタックを実装するために SMB ダイレクトと互換性があるすべての RDMA インターフェイスが必要ですし、SMB マルチ チャネルはそのことを認識します。

SMB ダイレクトは必要ありませんが、任意の SMB 構成に ' s 常に低待機時間と CPU 使用率が低い方のためお勧めします。

SMB ダイレクトの詳細については、次を参照してください。 [SMB ダイレクトとファイル サーバーのパフォーマンスを向上させる](https://aka.ms/smbdirect)します。

### <a name="smb-multichannel"></a>SMB マルチチャネル

SMB マルチ チャネルは、によりファイル サーバーは、同時に複数のネットワーク接続を使用して、スループットの向上を提供します。

SMB マルチ チャネルの詳細については、次を参照してください。[展開 SMB マルチ チャネル](https://aka.ms/smbmulti)します。

### <a name="smb-scale-out"></a>SMB スケール アウト

SMB スケール アウトには、クラスターのすべてのノードに共有を表示するクラスター構成の SMB 3.0 ことができます。 このアクティブ/アクティブ構成できるようになりますスケール ファイル サーバー クラスターにさらに、複数のボリューム、共有、およびクラスター リソースで複雑な構成なし。 最大共有帯域幅は、すべてのファイル サーバー クラスター ノードの帯域幅の合計です。 帯域幅の合計は、1 つのクラスター ノードの帯域幅によって制限されなくではなく、補助記憶域システムの機能によって異なります。 ノードを追加することで合計の帯域幅を増大することができます。

SMB スケール アウトに関する詳細については、次を参照してください。[スケール アウト ファイル サーバーのアプリケーション データの概要](https://technet.microsoft.com/library/hh831349.aspx)とブログの投稿[は、質問をスケール アウトするかどうかスケール アウト、](http://blogs.technet.com/b/filecab/archive/2013/12/05/to-scale-out-or-not-to-scale-out-that-is-the-question.aspx)します。

### <a name="performance-counters-for-smb-30"></a>SMB 3.0 のパフォーマンス カウンター

Windows Server 2012 で導入された次の SMB のパフォーマンス カウンターと SMB 2 および以降のバージョンのリソースの使用状況を監視するとカウンターの基準セットと見なされます。 パフォーマンス カウンターをローカルにログ (.blg) の生パフォーマンス カウンター ログ。 低コストでワイルドカード文字を使用してすべてのインスタンスを収集する (\*)、し、後の処理中に Relog.exe を使用して特定のインスタンスを抽出します。

-   **SMB クライアント共有**

    これらのカウンターは、SMB 2.0 または以降のバージョンを使用しているクライアントがアクセスしているサーバーでファイル共有についての情報を表示します。

    場合する ' の Windows での通常のディスク カウンターご存知特定似ていますがわかります。 ある ' s ことがないです。 SMB クライアント共有のパフォーマンス カウンターは、ディスクのカウンターを正確に一致するように設計されました。 この方法をアプリケーションでのディスク パフォーマンスのチューニングについては、簡単に再利用現在があります。 カウンターのマッピングに関する詳細については、次を参照してください。[共有クライアントのパフォーマンス カウンターに関するブログあたり](http://blogs.technet.com/b/josebda/archive/2012/11/19/windows-server-2012-file-server-tip-new-per-share-smb-client-performance-counters-provide-great-insight.aspx)します。

-   **SMB サーバー共有**

    これらのカウンターは、サーバー上の SMB 2.0 または以上のファイル共有に関する情報を表示します。

-   **SMB サーバー セッション**

    これらのカウンターは、SMB 2.0 以降を使用する SMB サーバー セッションに関する情報を表示します。

    サーバー側 (サーバー共有またはサーバーのセッション) でのカウンターの有効化すると、高い IO ワークロードのパフォーマンスに大きな影響があります。

-   **再開キー フィルター**

    これらのカウンターは、再開キー フィルターに関する情報を表示します。

-   **SMB ダイレクトの接続**

    これらのカウンターは、接続アクティビティのさまざまな側面を測定します。 コンピューターには、SMB ダイレクトの複数の接続を持つことができます。 SMB ダイレクト接続カウンターは、IP アドレスとポート、場所、最初の IP アドレスとポート、接続のローカル エンドポイントを表すし、接続のリモート エンドポイントを表す 2 つ目の IP アドレスとポートのペアとして各接続を表します。

-   **物理ディスク、SMB、CSV FS パフォーマンス カウンターのリレーションシップ**

    物理ディスク、SMB、および CSV FS (ファイル システム) のカウンターに関連付ける方法の詳細については、ブログの投稿を参照してください。[クラスターの共有ボリュームのパフォーマンス カウンター](http://blogs.msdn.com/b/clustering/archive/2014/06/05/10531462.aspx)します。

## <a name="tuning-parameters-for-smb-file-servers"></a>SMB ファイル サーバーのチューニング パラメーター


次の REG\_DWORD のレジストリ設定の SMB ファイル サーバーのパフォーマンスに影響することができます。

-   **Smb2CreditsMin**と**Smb2CreditsMax**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanServer\Parameters\Smb2CreditsMin
    ```

    ```
    HKLM\System\CurrentControlSet\Services\LanmanServer\Parameters\Smb2CreditsMax
    ```

    既定値は、それぞれ 512 および 8192 です。 これらのパラメーターでは、サーバーで動的に指定された境界内のクライアント操作の同時実行をスロットルすることができるようにします。 一部のクライアントは、高帯域幅、待機時間の長いリンク経由でファイルをコピーより高い同時実行制限は、たとえば、スループットの向上を実現可能性があります。
    
    >[!TIP]
    > Windows 10 および Windows Server 2016 では、前に、クライアントに付与されるクレジット数変化に動的に Smb2CreditsMin とネットワーク待機時間に基づいて最適なクレジットを付与する数を判断しようとしています。 アルゴリズムに基づいて Smb2CreditsMax の間証明書やクレジットの使用量。 Windows 10 および Windows Server 2016 では、SMB サーバーは、クレジットの最大数は構成済みの要求時にクレジットを無条件に付与に変更されました。 この変更の一環として、制限メカニズムで、サーバーがメモリ不足の場合は、各接続のクレジットのウィンドウのサイズを軽減しますが、クレジットが削除されました。 サーバーがメモリ不足ためときの調整をトリガーした、カーネルのメモリ不足イベントが通知のみ (< は数 MB) に役に立ちません。 サーバーが不要になったクレジットの windows を縮小するため Smb2CreditsMin 設定は不要になったし、は無視されます。

    > SMB クライアント共有を監視する\\クレジット失速数/秒をクレジットに問題があるかどうかを参照してください。

- **AdditionalCriticalWorkerThreads**

    ```
    HKLM\System\CurrentControlSet\Control\Session Manager\Executive\AdditionalCriticalWorkerThreads
    ```

    既定では 0 で、重要な追加のカーネルのワーカー スレッドが追加されません。 この値は、先行読み取りとライト ビハインド要求をファイル システム キャッシュを使用するスレッドの数に影響します。 この値を増やすと、記憶域サブシステムの I/O キューに登録の詳細は、多くの論理プロセッサと強力な記憶域ハードウェアのシステムでは特に、I/O パフォーマンスを向上できますを許可できます。

    >[!TIP]
    > 値がキャッシュ マネージャーの量のデータのダーティの場合に増やす必要があります (キャッシュのパフォーマンス カウンター\\ダーティ ページ) は拡大して大部分 (約 25% を超える) の使用にメモリの読み取り I/o のシステムが多くの同期を行っているかどうかまたはします。

-   **MaxThreadsPerQueue**

    ```
    HKLM\System\CurrentControlSet\Services\LanmanServer\Parameters\MaxThreadsPerQueue
    ```

    既定値は 20 です。 この値を増やすと、ファイル サーバーは、サービスの同時実行要求に使用できるスレッドの数が発生します。 アクティブな接続の数が多いを処理する必要があり、ストレージ帯域幅などのハードウェア リソースが十分な場合は、サーバーのスケーラビリティ、パフォーマンス、および応答時間が向上して値を大きくできます。

    >[!TIP]
    > 値を大きく必要があることを示していますが、SMB2 作業キューが非常に大きな増大かどうか (パフォーマンス カウンター 'サーバー ワーク キュー\\キューの長さ\\SMB2 非ブロッキング\*' ~ 100 を超えた状態が)。

    >[!Note]
    >Windows 10 および Windows Server 2016 で MaxThreadsPerQueue は使用できません。 スレッド プールのスレッドの数になります"20 * NUMA ノード内のプロセッサの数"です。  

-   **AsynchronousCredits**

    ``` 
    HKLM\System\CurrentControlSet\Services\LanmanServer\Parameters\AsynchronousCredits
    ```

    既定値は 512 文字です。 このパラメーターは、1 つの接続で許可される同時実行の非同期 SMB コマンドの数を制限します。 場合によっては (場合など、バック エンドの IIS サーバーとフロント エンド サーバーがある) (のファイルは、具体的には、通知要求を変更) は、大量の同時実行を必要とします。 このような場合をサポートするためにこのエントリの値を増やすことができます。

### <a name="smb-server-tuning-example"></a>SMB サーバーのチューニングの例

次の設定は、多くの場合のファイル サーバーのパフォーマンスのためにコンピューターを最適化できます。 この設定は、すべてのコンピューターに最適で妥当というわけでありません。 個々の設定を適用する前に、その影響を評価する必要があります。

| パラメーター                       | Value | Default |
|---------------------------------|-------|---------|
| AdditionalCriticalWorkerThreads | 64    | 0       |
| MaxThreadsPerQueue              | 64    | 20      |


### <a name="smb-client-performance-monitor-counters"></a>SMB クライアントのパフォーマンス モニター カウンター

SMB クライアント カウンターに関する詳細については、次を参照してください。 [Windows Server 2012 ファイル サーバー ヒント。新しい共有/SMB クライアントのパフォーマンス カウンターの見識を提供する](http://blogs.technet.com/b/josebda/archive/2012/11/19/windows-server-2012-file-server-tip-new-per-share-smb-client-performance-counters-provide-great-insight.aspx)します。
