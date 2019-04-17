---
title: "記憶域レプリカについてよく寄せられる質問"
ms.prod: windows-server-threshold
manager: siroy
ms.author: nedpyle
ms.technology: storage-replica
ms.topic: get-started-article
author: nedpyle
ms.date: 07/20/2017
ms.assetid: 12bc8e11-d63c-4aef-8129-f92324b2bf1b
ms.openlocfilehash: f29ca24a39e00f5142fe700e6abb09d1673acf7b
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2017
---
# <a name="frequently-asked-questions-about-storage-replica"></a>記憶域レプリカについてよく寄せられる質問

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックには、記憶域レプリカに関してよく寄せられる質問 (FAQ) に対する回答が含まれています。

## <a name="FAQ1"></a> 記憶域レプリカは Nano Server でサポートされますか?  
対応  

> [!NOTE]
> セットアップ中に、**記憶域**の Nano Server パッケージを使用する必要があります。 Nano Server のデプロイの詳細については、「[Getting Started with Nano Server (Nano Server の概要)](https://technet.microsoft.com/library/mt126167.aspx)」を参照してください。  

PowerShell を使用して、記憶域レプリカを次のように Nano Server にインストールします。  

1. Nano Server をクライアントの信頼リストに追加します。  
   > [!NOTE]
   > この手順は、コンピューターが Active Directory Domain Services フォレストメンバーでない場合、または信頼されていないフォレストにある場合にのみ必要です。 この手順により、セキュリティ上の理由によって既定で無効になっている PSSession リモート処理に、NTLM のサポートが追加されます。 詳細については、「[PowerShell リモート処理のセキュリティに関する考慮事項](https://msdn.microsoft.com/powershell/scriptiwinrmsecurity)」を参照してください。  

   ```  
       Set-Item WSMan:\localhost\Client\TrustedHosts "<computer name of Nano Server>"  
   ```  
2.  記憶域レプリカの機能をインストールするには、管理コンピューターから次のコマンドレットを実行します。  

    ```  
    Install-windowsfeature -Name storage-replica,RSAT-Storage-Replica -ComputerName <nano server> -Restart -IncludeManagementTools  
    ```  

    Windows Server 2016 内の Nano Server で `Test-SRTopology` コマンドレットを使用するには、CredSSP でリモート スクリプトを呼び出す必要があります。 他の記憶域レプリカのコマンドレットとは異なり、`Test-SRTopology` はソース サーバーでローカルに実行する必要があります。   
(リモート PSSession を通じた) Nano Server で、次のコマンドレットを使用します。  

    >[!NOTE]
    >`Test-SRTopology` コマンドレットでは、Kerberos のダブル ホップ サポートに CREDSSP が必要ですが、分散システムの資格情報を自動的に処理する他の記憶域レプリカのコマンドレットでは必要ありません。 一般的な状況では、CREDSSP の使用はお勧めしません。 CREDSSP の代替手段については、次のマイクロソフトのブログ記事を確認してください: 「PowerShell Remoting Kerberos Double Hop Solved Securely (PowerShell リモート処理での Kerberos ダブル ホップを安全に解決)」 - https://blogs.technet.microsoft.com/ashleymcglone/2016/08/30/powershell-remoting-kerberos-double-hop-solved-securely/ 

        Enable-WSManCredSSP -role server       

    管理コンピューターで次のコマンドレットを使用します。  

         Enable-WSManCredSSP Client -DelegateComputer <remote server name>  

         $CustomCred = Get-Credential  

         Invoke-Command -ComputerName sr-srv01 -ScriptBlock { Test-SRTopology <commands> } -Authentication Credssp -Credential $CustomCred  

       その後、結果を管理コンピューターにコピーするか、パスを共有します。 Nano Server には必要なグラフィック ライブラリがないため、結果を処理してグラフのレポート ファイルを提供する Test-SRTopology を使用できます。 以下に例を示します。  

        Test-SRTopology -GenerateReport -DataPath \\sr-srv05\c$\temp  


## <a name="FAQ2"></a> 初期同期中にレプリケーションの進行状況を確認するにはどうすればよいですか?  
レプリケーション先のサーバーの記憶域レプリカの管理者イベント ログに表示される Event 1237 メッセージに、コピーされたバイト数および残りのバイト数が 10 秒間隔で表示されます。 1 つまたは複数のレプリケートされたボリュームに対して **\Storage Replica Statistics\Total Bytes Received** が表示されるレプリケーション先で、記憶域レプリカのパフォーマンス カウンターを使用することもできます。 Windows PowerShell を使用して、レプリケーション グループをクエリすることもできます。 たとえば、このサンプル コマンドはレプリケーション先にあるグループの名前を取得し、**Replication 2** という名前の 1 つのグループをクエリして、10 秒間隔で進行状況を表示します。  

```  
Get-SRGroup

do{
    $r=(Get-SRGroup -Name "Replication 2").replicas
    [System.Console]::Write("Number of remaining bytes {0}`n", $r.NumOfBytesRemaining)
    Start-Sleep 10
}until($r.ReplicationStatus -eq 'ContinuouslyReplicating')
Write-Output "Replica Status: "$r.replicationstatus

```  

## <a name="FAQ3"></a>レプリケーションに特定のネットワーク インターフェイスが使用されるように指定できますか?  

はい、`Set-SRNetworkConstraint` を使用して指定できます。 このコマンドレットはインターフェイス層で動作し、クラスター シナリオおよび非クラスター シナリオの両方で使用されます。  
たとえば、(各ノード上の) スタンドアロン サーバーでは次のコマンドを実行します。  

```  
Get-SRPartnership  

Get-NetIPConfiguration  
```  
(両方のサーバーの) ゲートウェイとインターフェイスの情報およびパートナーシップの方向に注意してください。 次に、次のコマンドを実行します。  

```  
Set-SRNetworkConstraint -SourceComputerName sr-srv06 -SourceRGName rg02 -  
SourceNWInterface 2 -DestinationComputerName sr-srv05 -DestinationNWInterface 3 -DestinationRGName rg01  

Get-SRNetworkConstraint  

Update-SmbMultichannelConnection  

```  

ストレッチ クラスター上でネットワークの制約を構成するには、次のコマンドを実行します。  

    Set-SRNetworkConstraint -SourceComputerName sr-srv01 -SourceRGName group1 -SourceNWInterface "Cluster Network 1","Cluster Network 2" -DestinationComputerName sr-srv03 -DestinationRGName group2 -DestinationNWInterface "Cluster Network 1","Cluster Network 2"  

## <a name="FAQ4"></a> 1 対多のレプリケーションまたは (A から B、B から Cの) 推移的なレプリケーションを構成することはできますか?  
Windows Server 2016 では構成できません。 このリリースでは、サーバー、クラスター、またはストレッチ クラスター ノードの 1 対 1 のレプリケーションのみがサポートされます。 これは、今後のリリースで変更される可能性があります。 当然ながら、各種サーバーの特定のボリューム ペアを、方向を指定してレプリケーションするよう構成することはできます。 たとえば、サーバー 1 の D ボリュームをサーバー 2 に、E ボリュームをサーバー 3 からレプリケートできます。

## <a name="FAQ5"></a> 記憶域レプリカによってレプリケートされたボリュームを拡大または圧縮することはできますか?  
ボリュームは、拡大 (拡張) できますが、圧縮できません。 既定では、記憶域レプリカを使うと管理者はレプリケートされたボリュームを拡張できません。サイズ変更前に、ソース グループで `Set-SRGroup -AllowVolumeResize $TRUE` オプションを使ってください。 以下に例を示します。

1. ソース コンピューターに対して使います。 `Set-SRGroup -Name YourRG -AllowVolumeResize $TRUE`
2. 希望する方法を使ってボリュームを拡大する
3. ソース コンピューターに対して使います。 `Set-SRGroup -Name YourRG -AllowVolumeResize $FALSE` 

## <a name="FAQ6"></a>読み取り専用アクセスでレプリケーション先のボリュームをオンラインで取り込むことはできますか?  
Windows Server 2016 RTM (いわゆる "RS1" リリース) ではできません。 記憶域レプリカは、レプリケーションが開始されると宛先ボリュームをマウント解除します。 

ただし、Windows Server バージョン 1709 では、宛先の記憶域をマウントするオプションを選択できるようになりました。この機能は "テスト フェールオーバー" と呼ばれます。 これを実行するには、現在、宛先でレプリケートされていない、未使用の、NTFS または ReFS でフォーマットされたボリュームが必要です。 次に、レプリケートされた記憶域のスナップショットを、テストやバックアップの目的で、一時的にマウントすることができます。 

たとえば、宛先サーバー "SRV2" のレプリケーション グループ "RG2" 内にボリューム "D:" をレプリケートしており、SRV2 にレプリケートされていない "T:" ドライブがある場合に、テスト フェールオーバーを作成するには、次の操作を実行します。

 `Mount-SRDestination -Name RG2 -Computername SRV2 -TemporaryPath T:\`
 
レプリケートされたボリューム D: は SRV2 でアクセスできるようになります。 読み取りと書き込みを通常どおり実行することも、そこからファイルをコピーすることもできます。また、安全に保管するために別の場所に保存するオンライン バックアップも実行できます。

テスト フェールオーバーのスナップショットを削除してその変更を破棄するには:

 `Dismount-SRDestination -Name RG2 -Computername SRV2`
 
テスト フェールオーバー機能は、短期的な一時的な操作としてのみ使用する必要があります。 長期的に使用するための機能ではありません。 使用中の場合、レプリケーションは実際の宛先ボリュームまで継続されます。 

## <a name="FAQ7"></a>ストレッチ クラスターでスケール アウト ファイル サーバー (SOFS) を構成することはできますか?  
技術的には可能ですが、SOFS に接続するコンピューティング ノード内にサイト認識がないため、この構成は Windows Server 2016 では推奨されません。 一般的に待機時間がサブミリ秒になるキャンパス距離のネットワークを使用している場合、この構成は、通常は問題なく機能します。   

クラスター間のレプリケーションを構成している場合、記憶域レプリカは、2 つの記憶域クラスター間でのレプリケート中の記憶域スペース ダイレクトの使用も含め、スケールアウト ファイル サーバーを完全にサポートします。  

## <a name="FAQ8"></a>記憶域レプリカを使用したストレッチ クラスターで記憶域スペース ダイレクトを構成することはできますか?  
Windows Server 2016 ではサポートされていない構成です。  これは、今後のリリースで変更される可能性があります。 クラスター間のレプリケーションを構成している場合、記憶域レプリカは、記憶域スペース ダイレクトの使用も含め、スケールアウト ファイル サーバーと Hyper-V Server を完全にサポートします。  

## <a name="FAQ9"></a>非同期レプリケーションを構成するにはどうすればよいですか?  

`New-SRPartnership -ReplicationMode` を指定して引数 **Asynchronous** を入力します。 既定では、記憶域レプリカのすべてのレプリケーションは同期です。 `Set-SRPartnership -ReplicationMode` でモードを変更することもできます。  

## <a name="FAQ10"></a>ストレッチ クラスターの自動フェールオーバーを回避するにはどうすればよいですか?  
自動フェールオーバーを回避するには、PowerShell を使用して `Get-ClusterNode -Name "NodeName").NodeWeight=0` を構成します。 これにより、障害復旧サイト内の各ノードの票が削除されます。 その後、プライマリ サイト内のノードの `Start-ClusterNode -PreventQuorum` および障害サイト内のノードの `Start-ClusterNode -ForceQuorum` を使用して、フェールオーバーを強制することができます。 自動フェールオーバーを防止するためのグラフィカルなオプションはなく、自動フェールオーバーの防止は推奨されません。  

## <a name="FAQ11"></a>仮想マシンの回復性を無効にするにはどうすればよいですか?  
新しい Hyper-V 仮想マシンの回復性機能の実行を阻止して、Hyper-V 仮想マシンが障害回復サイトにフェールオーバーする代わりに仮想マシンを一時停止するには、次のコマンドを実行します。 `(Get-Cluster).ResiliencyDefaultPeriod=0`  

## <a name="FAQ12"></a> 初期同期にかかる時間を短縮するにはどうすればよいですか?  

初期同期の間を短縮する 1 つの方法として、仮想プロビジョニングされた記憶域を使用できます。 記憶域レプリカは、クエリを実行し、非クラスター化記憶域スペース、Hyper-V の動的ディスク、SAN LUN を含む、仮想プロビジョニングされたストレージを自動的に使用します。  

また、シードされたデータ ボリュームを使用することで、使用帯域幅の低減や、場合によっては時間の短縮ができます。具体的には、復元されたバックアップ、古いスナップショット、以前のレプリケーション、コピーされたファイルなどにより、レプリケーション先のボリュームにプライマリ ボリュームからのデータの一部が含まれていることを確認したうえで、シード オプションをフェールオーバー クラスター マネージャーや `New-SRPartnership` 内で使用します。 ボリュームがほぼ空の場合は、シード同期を使用すると、時間と使用帯域幅を低減できます。

## <a name="FAQ13"></a> レプリケーションを管理するユーザーを委任することはできますか?  

Windows Server 2016 では、`Grant-SRDelegation` コマンドレットを使用してユーザーを委任できます。 これにより、サーバー間、クラスター間で特定のユーザーを設定して、クラスターのレプリケーション シナリオを、ローカルの管理者グループのメンバーにならずにレプリケーションを作成、変更、削除する権限が付与されているとして拡張することができます。 以下に例を示します。  

    Grant-SRDelegation -UserName contso\tonywang  

このコマンドレットは、変更が有効になるように、管理しようと計画しているサーバーからユーザーがログオフおよびログオンする必要があることを通知します。 `Get-SRDelegation` と `Revoke-SRDelegation` を使用して、さらにこれを制御できます。  

## <a name="FAQ13"></a> レプリケートされたボリュームのバックアップと復元オプションを確認できますか?
記憶域レプリカは、ソース ボリュームのバックアップと復元をサポートします。 さらに、ソース ボリュームのスナップショットの作成と復元もサポートします。 記憶域レプリカによって保護されている間はマウントもアクセスもできないため、レプリケーション先のボリュームをバックアップまたは復元することはできません。 ソース ボリュームが失われる障害が発生した場合、`Set-SRPartnership` を使用して以前のレプリケーション先ボリュームを昇格します。読み取りと書き込みが可能になったソースによって、失われたソース ボリュームをバックアップまたは復元できるようになります。 `Remove-SRPartnership` と `Remove-SRGroup` を使用して、このボリュームを読み取りと書き込みが可能なボリュームとして再マウントすることもできます。
アプリケーション整合性のスナップショットを定期的に作成するために、ソース サーバーで VSSADMIN.EXE を使用して、レプリケートされたデータ ボリュームのスナップショットを作成できます。 たとえば、F: ボリュームを記憶域レプリカでレプリケートしている場合は次のようになります。

    vssadmin create shadow /for=F:
その後、レプリケーションの方向を切り替えた後、レプリケーションを削除した後、または同じソース ボリューム上にいる場合、任意のスナップショットをその時点に復元できます。 たとえば、依然として F: を使用している場合は次のようになります。

    vssadmin list shadows
     vssadmin revert shadow /shadow={shadown copy ID GUID listed previously}
スケジュールされたタスクを使用して、このツールが定期的に実行されるようにスケジュールすることもできます。 VSS の使用方法の詳細については、[Vssadmin](https://technet.microsoft.com/library/cc754968.aspx) を確認してください。 ログ ボリュームのバックアップは不要であり、行う価値もありません。 バックアップしようとすると、VSS によって無視されます。
Windows Server バックアップ、Microsoft Azure Backup、Microsoft DPM、またはその他のスナップショット、VSS、仮想マシン、またはファイルベースのテクノロジの使用は、ボリューム層内で動作する限り、記憶域レプリカでサポートされます。 記憶域レプリカは、ブロックベースのバックアップと復元はサポートしません。

## <a name="FAQ14"></a> 帯域幅の使用が制限されるようにレプリケーションを構成できますか?
はい、SMB 帯域幅リミッターを介して構成できます。 これは記憶域レプリカのすべてのトラフィックのグローバル設定であるため、このサーバーからのすべてのレプリケーションに影響を与えます。 これは通常、すべてのデータを転送する必要がある、記憶域レプリカの初期同期のセットアップでのみ必要です。 初期同期後に必要な場合は、ネットワーク帯域幅が IO ワークロードに対して狭すぎます。IO を削減するか、帯域幅を拡大してください。

これは非同期レプリケーションでのみ使用する必要があります (注: 初期同期は、同期を指定した場合でも常に非同期になります)。
ネットワーク QoS ポリシーを使用して、記憶域レプリカのトラフィックを形成することもできます。 一致率の高いシード記憶域レプリカのレプリケーションを使用した場合も、全体的な初期同期の帯域幅使用が大幅に削減されます。


帯域幅の制限を設定するには、次のコマンドを使用します。

    Set-SmbBandwidthLimit  -Category StorageReplication -BytesPerSecond x

帯域幅の制限を確認するには、次のコマンドを使用します。

    Get-SmbBandwidthLimit -Category StorageReplication

帯域幅の制限を削除するには、次のコマンドを使用します。

    Remove-SmbBandwidthLimit -Category StorageReplication
    
## <a name="FAQ15"></a>記憶域レプリカに必要なネットワーク ポートを教えてください。
記憶域レプリカは、レプリケーションと管理において SMB と WSMAN を利用します。 つまり、次のポートが必要です。

   445 (SMB - レプリケーション転送プロトコル) 5445 (iWARP SMB - iWARP RDMA ネットワークを使っている場合のみ必要) 5895 (WSManHTTP - WMI/CIM/PowerShell の管理プロトコル)

注: Test-SRTopology コマンドレットには ICMPv4/ICMPv6 が必要ですが、レプリケーションや管理には使うことができません。

## <a name="FAQ15"></a>ログ ボリュームのベスト プラクティスについて教えてください。
最適なログのサイズは、環境とワークロードによって大きく異なり、実際のワークロードで実行される書き込み IO の量によって決まります。 

1.  ログの大きさは、処理速度には影響を与えません。
2.  ログのサイズ、またデータ ボリュームが、たとえば、10 GB か 10 TB かは、パフォーマンスに影響を及ぼしません。

サイズの大きいログは、単純に、一杯になるまでに多くの書き込み IO を収集して保持できます。これにより、ログのソースと保存先コンピューターの間での、長時間にわたるサービス中断に対処できます (ネットワークの切断や保存先コンピューターのオフラインなど)。 ログが 10 時間分の書き込みを保持できる場合、ネットワークが 2 時間ダウンしても、ネットワークの復旧時にソース側から保存先に対して同期されていない変更の差分を素早く同期すれば、短時間で保護された状態に回復します。 しかし保持されるログが 10 時間分である場合に、ネットワークが 2 日間ダウンすると、ソース側はビットマップと呼ばれる別のログから再生する必要があるため、同期状態への回復に時間がかかります。同期された後は、元どおりログを使用できます。

ログの処理速度は、SR パフォーマンス カウンターによって把握でき、それに基づいて判断を下すことができます。 また、Test-SRTopology コマンドレットも同じ機能を備えています。 基本的には、既存のワークロードに対する書き込み IO を検討して、ログに対する 1 分、1 時間、1 日当たりの IO フローの量を判断します。

記憶域レプリカのすべての書き込みパフォーマンスはログに依存します。 ログのパフォーマンスは、レプリケーションのパフォーマンスにとって重要です。 ログ ボリュームには、ログではすべての書き込み IO がシリアル化、シーケンス化されるため、ログ ボリュームはデータ ボリュームよりも高速に動作するデバイスを使用する必要があります。 ログ ボリュームでは、常に SSD などのフラッシュ メディアを使う必要があります。 ログ ボリューム上では、他のワークロードの実行を絶対に許可しないでください。同様に、SQL データベースのログ ボリューム上で他のワークロードの実行を許可しないでください。 

繰り返しますが、ログ ストレージには、データ ストレージよりも高速に動作するデバイスを使用することをお勧めします。またログ ボリュームは、絶対に他のワークロードに使用しないでください

## <a name="FAQ16"></a>ストレッチ クラスター トポロジ、クラスター間トポロジ、クラスター サーバー トポロジを使い分ける方法について教えてください。  
記憶域レプリカには、ストレッチ クラスター、クラスター間、サーバー間の 3 つの主要な構成があります。 それぞれの構成には、異なる利点があります。

ストレッチ クラスター トポロジは、Hyper-V プライベート クラウド クラスターや SQL Server FCI など、オーケストレーションを使用した自動フェールオーバーを必要とするワークロードに最適です。 また、フェールオーバー クラスター マネージャーを使用したグラフィカル インターフェイスが組み込まれています。 このトポロジでは、永続的予約を介して、従来の非対称クラスター共有記憶域アーキテクチャである記憶域スペース、SAN、iSCSI、および RAID が使用されます。 これは、2 ノード以上の構成で実行できます。

クラスター間トポロジでは、2 つの独立したクラスターが使用されます。特に 2 番目のサイトが障害回復用にプロビジョニングされていて、日常的な用途に使用されず、手動のフェールオーバーを必要とする場合に最適です。 オーケストレーションは手動で実行します。 ストレッチ クラスターと異なり、この構成では記憶域スペース ダイレクトを使用できます。 これは、4 ノード以上の構成で実行できます。 

サーバー間トポロジは、クラスター化できないハードウェアを実行しているユーザーに最適です。 この構成では、手動によるフェールオーバーとオーケストレーションが必要です。 ブランチ オフィスと集中管理データセンターの間の展開で、特に非同期レプリケーションを使用する場合に最適です。 この構成では、多くの場合、単一マスター障害回復シナリオに使用される DFSR で保護されたファイル サーバーのインスタンスを置き換えることができます。

このトポロジは、すべての場合において、物理ハードウェアでの実行と仮想マシンでの実行の両方をサポートします。 仮想マシンで使用する場合、基盤のハイパーバイザーは Hyper-V である必要はなく、VMware、KVM、Xen なども使用できます。

記憶域レプリカには、同じコンピューター上の 2 つの異なるボリュームへのレプリケーションを指定するサーバー内モードも使用できます。

## <a name="FAQ17"></a> 記憶域レプリカやこのガイドの問題を報告する方法を教えてください。  
記憶域レプリカの技術的サポートが必要な場合は、[Microsoft TechNet フォーラム](https://social.technet.microsoft.com/Forums/windowsserver/en-US/home?forum=WinServerPreview)から投稿できます。 記憶域レプリカに関する質問や、このドキュメントに関する問題は、srfeed@microsoft.com に電子メールを送信することもできます。 設計変更をご依頼の場合は、お客様のアイデアに対して他のお客様からのサポートやフィードバックが得られる、https://windowsserver.uservoice.com サイトをお勧めします。



## <a name="related-topics"></a>関連トピック  
- [記憶域レプリカの概要](storage-replica-overview.md) 
- [共有記憶域を使用したストレッチ クラスター レプリケーション](stretch-cluster-replication-using-shared-storage.md)  
- [サーバー間の記憶域レプリケーション](server-to-server-storage-replication.md)  
- [クラスター間の記憶域のレプリケーション](cluster-to-cluster-storage-replication.md)  
- [記憶域レプリカ: 既知の問題](storage-replica-known-issues.md)  

## <a name="see-also"></a>関連項目  
- [記憶域の概要](../storage.md)  
- [Windows Server 2016 の記憶域スペース ダイレクト](../storage-spaces/storage-spaces-direct-overview.md)  
