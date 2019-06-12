---
title: 保護されたファブリックの診断ツールを使用したトラブルシューティング
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 07691d5b-046c-45ea-8570-a0a85c3f2d22
manager: dongill
author: huu
ms.technology: security-guarded-fabric
ms.openlocfilehash: 0fb257f693cc27c0bc6dd18fc89e8dc6328ee638
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447341"
---
# <a name="troubleshooting-using-the-guarded-fabric-diagnostic-tool"></a>保護されたファブリックの診断ツールを使用したトラブルシューティング

>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、ツールの使用、保護されたファブリック診断を特定し、展開、構成、および保護されたファブリック インフラストラクチャの継続的な操作で一般的なエラーの修復について説明します。 これには、ホスト ガーディアン サービス (HGS)、保護されたすべてのホストおよび DNS と Active Directory などのサポートのサービスが含まれます。 診断ツールは、開始点と障害を解決して、正しく構成されていない資産の特定の管理者を提供する、問題のある保護されたファブリックの方針で初回の実行に使用できます。 このツールは、動作して、保護されたファブリックのサウンドの把握に代わるものではありませんし、日常の操作中に発生した最も一般的な問題を迅速に確認する役割を果たします。

このトピックで使用されるコマンドレットのドキュメントで確認できます[TechNet](https://technet.microsoft.com/library/mt718834.aspx)します。

[!INCLUDE [Guarded fabric diagnostics tool](../../../includes/guarded-fabric-diagnostics-tool.md)] 

# <a name="quick-start"></a>クイック スタート

保護されたホストまたは HGS ノードのいずれかを診断するには、ローカルの管理者特権で Windows PowerShell セッションから、次の呼び出し。
```PowerShell
Get-HgsTrace -RunDiagnostics -Detailed
```
自動的に現在のホストの役割を検出され、自動的に検出できる関連する問題の診断されます。  存在するためのすべてのこのプロセス中に生成された結果が表示されます、`-Detailed`スイッチします。

このトピックの残りの部分はの高度な使用状況に関する詳細なチュートリアルを提供`Get-HgsTrace`一度に複数のホストを診断し、複雑なクロス ノード構成の誤りを検出するように作業を行うことです。

## <a name="diagnostics-overview"></a>診断の概要
保護されたファブリックの診断はすべてのホストとシールドされた仮想マシンで使用できるツールと Server Core を実行しているホストを含む、インストールされている機能に関連します。  現在、診断は、次の機能/パッケージに含まれています。

1. ホスト ガーディアン サービスの役割
2. Host Guardian Hyper-V サポート
3. Fabric Management 用の VM シールド ツール
4. リモート サーバー管理ツール (RSAT)

これは、診断ツールはすべての保護されたホスト、HGS ノード、特定ファブリックの管理サーバー、および、Windows 10 のワークステーションを利用できることを意味[RSAT](https://www.microsoft.com/download/details.aspx?id=45520)をインストールします。  診断は、保護されたホストまたは; 保護されたファブリックでの HGS ノードを診断する目的で上記のマシンのいずれかから呼び出すことができます。リモートのトレースのターゲットを使用して、診断は検索し、診断を実行しているコンピューター以外のホストに接続します。

診断の対象となるすべてのホストは"トレース target"と呼ばれます  トレースのターゲットは、そのホスト名とロールによって識別されます。  ロールには、保護されたファブリックで特定のトレースのターゲットを実行する関数について説明します。  現在、サポートの対象トレース`HostGuardianService`と`GuardedHost`ロール。  ただし、運用環境で、これを行っていない必要が、ホストを一度に複数のロールを占有する可能性があります、これは、診断はサポートされてもに注意してください。  HGS と HYPER-V ホストを別々 に保存して、常に異なる。

管理者を実行して、診断タスクを開始できます`Get-HgsTrace`します。  このコマンドは実行時に指定するスイッチに基づく 2 つの異なる機能を実行します。 トレース コレクションおよび診断します。  この 2 つの結合は、保護されたファブリックの診断ツールの全体を構成します。  明示的に必須では、最も役に立つの診断には、トレースのターゲットで管理者の資格情報を使用してのみ収集するトレースが必要です。  トレースの収集を実行するユーザーでは、十分な特権が保持されている、渡す他のすべてのユーザーが昇格を必要とするトレースが失敗します。  これにより、過小特権を持つオペレーターがトリアージを実行する場合に、部分的な診断できます。 

### <a name="trace-collection"></a>トレースの収集
既定では、`Get-HgsTrace`のみのトレースを収集およびして一時フォルダーに保存されます。  トレースは、という名前の対象となるホスト、ホストを構成する方法について説明する特殊な形式のファイルに入力した後、フォルダーの形式になります。  トレースには、トレースを収集する診断が起動された方法を説明するメタデータも含まれます。  このデータは、手動の診断を実行するときに、ホストについての情報をリハイド レートする診断によって使用されます。

必要に応じて、トレースを手動で確認できます。  すべての形式は、人間が判読できる (XML) または標準のツールを使用して簡単に検査する可能性があります (例: X509 証明書と Windows Crypto シェル拡張機能)。  トレースは、手動の診断用に設計されていないと、詳細は常にこと、ただしの診断機能を使って、トレースの処理に効果的な`Get-HgsTrace`します。

トレース コレクションの実行結果は、特定のホストの正常性に関する情報を加えないでください。  これらは、単に、トレースが正常に収集されたを示します。  診断機能を使用する必要がある`Get-HgsTrace`をトレースが失敗した環境を示すかどうかを判断します。

使用して、`-Diagnostic`パラメーター、トレース コレクションを指定された診断の運用に必要なトレースだけを制限することができます。  これには、診断の呼び出しに必要なアクセス許可と収集されるデータ量が削減されます。

### <a name="diagnosis"></a>診断
指定された、によって収集されたトレースを診断できます`Get-HgsTrace`を使用してトレースの場所、`-Path`パラメーターと指定する、`-RunDiagnostics`スイッチします。  さらに、`Get-HgsTrace`で実行できるコレクションと診断が 1 回提供することで、`-RunDiagnostics`スイッチとトレースのターゲットの一覧。  トレースのターゲットが指定されていない場合、現在のコンピューターは、その役割がインストールされている Windows PowerShell モジュールを調べることで推測で、暗黙のターゲットとして使用されます。

診断がどのトレース対象、診断のセットを示す階層形式で結果を提供し、個々 の診断は、特定のエラーを担当します。  エラーには、どのようなアクションは、[次へ] 実行する必要がありますか判断ができる場合の推奨解決策と修復が含まれます。  既定では、成功および関係のない結果が表示されません。  診断テストのすべてを表示するには、指定、`-Detailed`スイッチします。  これによりすべての結果をそれらの状態に関係なく表示されます。

使用して実行される診断のセットを制限することは、`-Diagnostic`パラメーター。  これにより、診断のクラスをトレースのターゲットに対して実行する必要がありますを指定する他のすべて非表示にするとします。  診断の使用可能なクラスの例についてには、ネットワーク、ベスト プラクティス、およびクライアントが含まれます。 ハードウェア。  参照してください、[コマンドレットのドキュメント](https://technet.microsoft.com/library/mt718831.aspx)使用可能な診断の最新の一覧を検索します。

> [!WARNING]
> 診断は、厳密な監視とインシデント対応のパイプラインに代わるものではありません。  System Center Operations Manager のパッケージは、保護されたファブリックと問題を早期に検出して監視できるさまざまなイベント ログ チャネルを監視するために使用できます。  診断は、迅速にこれらのエラーのトリアージし、一連の措置の確立に使用できます。

## <a name="targeting-diagnostics"></a>ターゲットの診断

`Get-HgsTrace` トレースのターゲットに対して動作します。  トレースの対象は、HGS ノードまたは保護されたファブリック内で保護されたホストに対応するオブジェクトです。  拡張機能として考えることができます、`PSSession`ファブリック内のホストの役割などの診断でのみ必要な情報を含むです。  ターゲットにすることができます (例: ローカルまたは手動の診断) を暗黙的に生成されたで明示的にまたは、`New-HgsTraceTarget`コマンド。

### <a name="local-diagnosis"></a>ローカルの診断

既定では、 `Get-HgsTrace` (つまり、コマンドレットが呼び出されている)、localhost をターゲットにします。  これは暗黙のローカルの対象として呼ばれます。  暗黙のローカルの対象は、ターゲットが指定されていない場合のみ使用、`-Target`パラメーターとの既存のトレースではありません。 は、「、`-Path`します。

暗黙のローカルの対象では、ロールの推定を使用して、保護されたファブリックで、現在のホストが果たす役割を決定します。  これは、ほぼどのような機能は、システムにインストールされているに対応するインストール済みの Windows PowerShell モジュールに基づきます。  有無、`HgsServer`モジュールは、役割を果たすトレースの対象になります`HostGuardianService`かどうか、`HgsClient`モジュールは、役割を果たすトレース対象により`GuardedHost`します。  特定のホストに存在する場合は両方として扱われます両方のモジュールがある可能性があります、`HostGuardianService`と`GuardedHost`します。

そのため、診断を収集するための既定の呼び出しをローカルでトレースします。
```PowerShell
Get-HgsTrace
```
...次のと同等です。
```PowerShell
New-HgsTraceTarget -Local | Get-HgsTrace
```
> [!TIP]
> `Get-HgsTrace` または経由で直接、パイプライン経由でターゲットを受け入れることができる、`-Target`パラメーター。  違いはありません、2 つの間動作不可能な状態です。

### <a name="remote-diagnosis-using-trace-targets"></a>リモート診断を使用してトレースのターゲット

リモート接続情報を持つトレースのターゲットを生成することによって、ホストをリモートで診断を行うことができます。  必要なは、ホスト名と一連の資格情報の Windows PowerShell リモート処理を使用して接続できます。
```PowerShell
$server = New-HgsTraceTarget -HostName "hgs-01.secure.contoso.com" -Role HostGuardianService -Credential (Enter-Credential)
Get-HgsTrace -RunDiagnostics -Target $server
```
この例は、リモート ユーザーの資格情報を収集するためのプロンプトを生成し、診断があるリモート ホストを使用してを実行するは`hgs-01.secure.contoso.com`トレースの収集を完了します。  結果のトレースは、localhost にダウンロードし、診断し。  診断の結果を実行するときに表示と同じには[ローカル診断](#local-diagnosis)します。  同様に、リモート システムにインストールされている Windows PowerShell モジュールに基づくに推測できるロールを指定する必要はありません。

リモート診断では、リモート ホストにすべてのアクセスに対して Windows PowerShell リモート処理で使用します。  そのため、トレースのターゲットがある Windows PowerShell リモート処理が有効になっている前提条件が (を参照してください[を有効にする PSRemoting](https://technet.microsoft.com/library/hh849694.aspx))、localhost が適切であると、ターゲットへの接続を起動用に構成します。

> [!NOTE]
> ほとんどの場合、ローカル ホストは、同じ Active Directory フォレストの一部であるし、有効な DNS ホスト名を使用するために必要なはのみです。  WinRM の設定などの追加の構成を実行する必要がありますが、環境がフェデレーションのより複雑なモデルを使用して、または接続の直接の IP アドレスを使用する、[信頼されたホスト](https://technet.microsoft.com/library/ff700227.aspx)します。

トレース対象が正しくインスタンス化されを使用して接続を受け入れるために構成されていることを確認することができます、`Test-HgsTraceTarget`コマンドレット。
```PowerShell
$server = New-HgsTraceTarget -HostName "hgs-01.secure.contoso.com" -Role HostGuardianService -Credential (Enter-Credential)
$server | Test-HgsTraceTarget
```
このコマンドは返します`$True`場合にのみ`Get-HgsTrace`トレースのターゲットでリモート診断セッションを確立することになります。  失敗した場合、このコマンドレットは、Windows PowerShell リモート処理接続のトラブルシューティングを行うための関連するステータス情報を返します。

#### <a name="implicit-credentials"></a>暗黙的な資格情報

リモート診断トレースの対象をリモートで接続するための十分な特権を持つユーザーからを実行する場合に資格情報を指定する必要はありません`New-HgsTraceTarget`します。  `Get-HgsTrace`コマンドレットは接続を開くときに、コマンドレットを呼び出すユーザーの資格情報を自動的に再利用します。

> [!WARNING]
> 「次ホップ」と呼ばれるものを実行するときに特に、資格情報を再利用にいくつかの制限が適用されます。  これは、リモート セッション内から別のマシンの資格情報を再利用するときに発生します。  必要があります[セットアップ CredSSP](https://technet.microsoft.com/library/hh849872.aspx)がこのシナリオをサポートするためには、保護されたファブリックの管理とトラブルシューティングの範囲外です。

#### <a name="using-windows-powershell-just-enough-administration-jea-and-diagnostics"></a>Windows PowerShell を使用して Just Enough Administration (JEA) と診断

リモート診断では、Windows PowerShell の JEA の制約があるエンドポイントの使用をサポートします。 既定値を使用して既定では、リモートのトレースの対象との接続は`microsoft.powershell`エンドポイント。  トレースの対象に、`HostGuardianService`ロールも試みますを使用して、 `microsoft.windows.hgs` HGS がインストールされているときに構成されているエンドポイント。

カスタム エンドポイントを使用する場合は、使用してトレース対象の構築中にセッション構成名を指定する必要があります、`-PSSessionConfigurationName`パラメーターなどの下。

```PowerShell
New-HgsTraceTarget -HostName "hgs-01.secure.contoso.com" -Role HostGuardianService -Credential (Enter-Credential) -PSSessionConfigurationName "microsoft.windows.hgs"
```

#### <a name="diagnosing-multiple-hosts"></a>複数のホストを診断します。

複数のトレースのターゲットを渡すことができます`Get-HgsTrace`一度にします。  これには、ローカルおよびリモートのターゲットの組み合わせが含まれます。  各ターゲットを順番にトレースして、すべてのターゲットからのトレースを同時に診断がし。  診断ツールは、複雑なクロス ノード構成の誤りと思われる場合は検出可能なを識別するために、デプロイの知識の向上を使用できます。  ターゲットの複数のホストを呼び出すときにトレースまたはで同時に (手動診断) 場合、複数のホストから提供する必要がありますのみこの機能を使用して`Get-HgsTrace`(リモート診断) の場合。

保護されたホストのいずれかが起動に使用されるファブリック HGS の 2 つのノードから成るトリアージし、2 つの保護されたホストをリモート診断の使用例を次に示します`Get-HgsTrace`します。

```PowerShell
$hgs01 = New-HgsTraceTarget -HostName "hgs-01.secure.contoso.com" -Credential (Enter-Credential)
$hgs02 = New-HgsTraceTarget -HostName "hgs-02.secure.contoso.com" -Credential (Enter-Credential)
$gh01 = New-HgsTraceTarget -Local
$gh02 = New-HgsTraceTarget -HostName "guardedhost-02.contoso.com"
Get-HgsTrace -Target $hgs01,$hgs02,$gh01,$gh02 -RunDiagnostics
```

> [!NOTE]
> 複数のノードを診断するときに、全体の保護されたファブリックを診断する必要はありません。  多くの場合は、特定のエラー状態には、関連するすべてのノードを含めるだけで十分です。  これは、通常は、保護されたホスト、およびいくつかの HGS クラスターからノードのサブセットです。

## <a name="manual-diagnosis-using-saved-traces"></a>保存済みのトレースを使用して手動の診断

もう一度トレースを収集せず、診断を再実行する場合もありますか、ファブリック内のホストのすべてを同時にリモートで診断するために必要な資格情報がない可能性があります。  手動診断を行うことができますも全体 fabric トリアージを使用して、メカニズムは、 `Get-HgsTrace`、リモートのトレースのコレクションを使用せずにします。

手動診断を実行する前に、トリアージ、ファブリック内の各ホストの管理者が利用可能で、あなたに代わってコマンドを実行することを確認する必要があります。  診断トレースの出力では、ユーザーが他のユーザーにこの情報を公開する安全なかどうかを判断する責任を負うことは一般に、機密情報として表示されるすべての情報は公開されません。

> [!NOTE]
> トレースはされていない匿名化され、ネットワークの構成、PKI の設定、他の構成は、個人情報と見なされることを明らかです。  そのため、トレースは、必ず、組織内の信頼されたエンティティに転送され、公開投稿されたことはありません。

手動診断を実行するための手順は次のとおりです。

1. 各ホストの管理者が実行される要求`Get-HgsTrace`既知を指定する`-Path`一連の診断結果のトレースに対して実行します。  例:

   ```PowerShell
   Get-HgsTrace -Path C:\Traces -Diagnostic Networking,BestPractices
   ```
2. 各ホストの管理者が結果のトレース フォルダーをパッケージ化し、送信するよう依頼します。  ファイル共有、またはその他の動作のポリシーと、組織が確立されている手順に基づくメカニズムを使用して、電子メール経由でこのプロセスを推進できます。

3. ないその他の内容またはフォルダーの 1 つのフォルダーには、受信したすべてのトレースをマージします。

    * たとえば、するが、という名前の 4 つのマシンから収集されたトレースを管理者の送信 HGS-01、HGS-02、RR1N2608 12、想定しています RR1N2608 13。  各管理者は送信フォルダーを同じ名前です。  次のように表示されるディレクトリ構造を組み立てる場合します。

      ```
      FabricTraces
      |- HGS-01
      |  |- TargetMetadata.xml
      |  |- Metadata.xml
      |  |- [any other trace files for this host]
      |- HGS-02
      |  |- [...]
      |- RR1N2608-12
      |  |- [...]
      |- RR1N2608-13
         |- [..]
      ```

4. 組み立てられたトレース フォルダーへのパスを提供する診断の実行、`-Path`パラメーターと指定する、`-RunDiagnostics`トレースを収集する管理者を求め、これらの診断とスイッチします。  診断は、パス内で検出されたホストにアクセスすることはできませんし、事前収集されたトレースのみを使用して試行はそのためと想定されます。  トレースが存在しないか破損している場合、診断が影響を受けるテストのみが失敗して、通常どおりに進行します。  例:

   ```PowerShell
   Get-HgsTrace -RunDiagnostics -Diagnostic Networking,BestPractices -Path ".\FabricTraces"
   ```

### <a name="mixing-saved-traces-with-additional-targets"></a>追加のターゲットでトレースを保存の混在

場合によっては、一連の機能追加のホストのトレースに追加する事前収集されたトレースするがあります。  トレースし、診断の 1 回の呼び出しで診断が他のターゲットを事前に収集されたトレースを混在させることになります。

次の手順を収集し、上記で指定したトレース フォルダーをアセンブルするには、呼び出す`Get-HgsTrace`事前収集されたトレース フォルダーに見つかりません。 別のトレースのターゲットを持つ。

```PowerShell
$hgs03 = New-HgsTraceTarget -HostName "hgs-03.secure.contoso.com" -Credential (Enter-Credential)
Get-HgsTrace -RunDiagnostics -Target $hgs03 -Path .\FabricTraces
``` 

診断コマンドレットは、事前収集されたすべてのホストとすると、トレースする必要がある 1 つの追加のホストを確認し、必要なトレースを実行します。  すべての事前収集された、新しく収集されたトレースの合計を診断しされます。  結果のトレース フォルダーは、新旧両方のトレースが含まれます。
