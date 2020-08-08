---
ms.assetid: ba7f2b9f-7351-4680-b7d8-a5f270614f1c
title: Active Directory Domain Services のインストールと削除の新機能
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.openlocfilehash: 7444fcc6807e43192e68c006dcd49464a503976b
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87953299"
---
# <a name="whats-new-in-active-directory-domain-services-installation-and-removal"></a>Active Directory Domain Services のインストールと削除の新機能

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

Windows Server 2012 の Active Directory Domain Services (AD DS) の展開は、Windows Server の以前のバージョンよりも簡単かつ高速に行うことができます。 AD DS のインストール処理は Windows PowerShell 上に構築され、サーバー マネージャーに統合されています。 これまで Active Directory 環境へのドメイン コントローラーの導入に必要だった多くの手順が削減されています。 このため、新しい Active Directory 環境を以前よりも簡単かつ効率的に作成することができます。 新しい AD DS 展開プロセスにより、インストールをブロックするようなエラーが発生する可能性が最小限に抑えられます。

また、AD DS サーバーの役割のバイナリ (AD DS サーバーの役割) を複数のサーバーに同時にインストールできます。 AD DS インストール ウィザードを個々のサーバーでリモートから実行することもできます。 これらの機能強化により、特に、多数のドメインコントローラーを異なる地域のオフィスに展開する必要がある大規模なグローバル展開の場合に、Windows Server 2012 を実行するドメインコントローラーを展開するための柔軟性が向上します。

AD DS のインストールには、次の特長があります。

- **AD DS インストール処理への Adprep.exe の統合。** さまざまな資格情報を使用したり、Adprep.exe ファイルをコピーしたり、ログオンして特定のドメイン コントローラーを指定する必要があるなどの、これまで Active Directory を準備するために必要だったわずらわしい手順がすべて簡略化または自動化されています。 これにより、AD DS のインストールに必要な時間が削減され、ドメイン コントローラーの昇格を妨げるエラーが発生する可能性が軽減されます。

   新しいドメイン コントローラーのインストールよりも先に adprep.exe コマンドを実行するのが望ましい環境の場合は、AD DS インストールとは別に adprep.exe コマンドを実行できます。 Windows Server 2012 バージョンの adprep.exe はリモートで実行されるため、Windows Server 2008 以降の64ビットバージョンを実行しているサーバーから必要なすべてのコマンドを実行できます。

- **新しい AD DS インストールは Windows PowerShell 上に構築され、リモートで呼び出し可能。** 新しい AD DS インストールがサーバー マネージャーに統合されたため、同じインターフェイスを使用して、他のサーバーの役割をインストールするときに使用する AD DS をインストールすることができます。 Windows PowerShell ユーザーの場合、AD DS 展開コマンドレットにより機能と柔軟性が向上します。 コマンド ラインと GUI インストール オプションの間には機能パリティがあります。
- **新しい AD DS インストールにおける前提条件の検証。** 発生する可能性のあるエラーが、インストールの開始前に特定されます。 エラーの発生要因を事前に取り除くことができるため、アップグレードが不完全に終わる心配はありません。 たとえば、adprep /domainprep の実行が必要な場合、インストール ウィザードでユーザーにこの操作を実行する十分な権限があるか確認されます。
- **関連するオプションをまとめてウィザードのページ数を最小限にし、昇格の過程で選択する最も一般的なオプションの要件を反映した順序で構成ページをグループ化。** インストールの過程で選択するさまざまなオプションが、より適切なコンテキストで提供されます。
- **GUI でのインストール時に指定されたすべてのオプションを含む Windows PowerShell スクリプトをエクスポート可能。** インストールまたは削除の終わりに、設定を Windows PowerShell スクリプトにエクスポートし、同じ操作を自動化するために使用することができます。
- **再起動の前に重要なレプリケーションのみが行われる。** 新しいスイッチによって、再起動の前に重要でないデータのレプリケーションを許可できます。 詳細については、「[ADDSDeployment コマンドレットの引数](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_Params)」を参照してください。

## <a name="the-active-directory-domain-services-configuration-wizard"></a><a name="BKMK_ADConfigurationWizard"></a>Active Directory ドメイン サービス構成ウィザード

Windows Server 2012 以降では、ドメインコントローラーをインストールするときに設定を指定するために、Active Directory Domain Services 構成ウィザードによってレガシ Active Directory ドメインサービスインストールウィザードがユーザーインターフェイス (UI) オプションとして置き換えられます。 Active Directory ドメイン サービス構成ウィザードは、役割の追加ウィザードの完了後に開始されます。

> [!WARNING]
> レガシ Active Directory ドメインサービスインストールウィザード (dcpromo.exe) は、Windows Server 2012 以降では非推奨とされます。

[インストール Active Directory Domain Services &#40;レベル 100&#41;](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md)の場合、UI の手順に従って、役割の追加ウィザードを起動して AD DS サーバーの役割バイナリをインストールし、Active Directory Domain Services 構成ウィザードを実行してドメインコントローラーのインストールを完了する方法を説明します。 Windows PowerShell の例では、AD DS 展開コマンドレットを使用して両方の手順を完了する方法を示しています。

## <a name="adprepexe-integration"></a><a name="BKMK_NewAdprep"></a>Adprep.exe の統合

Windows Server 2012 以降、Adprep.exe のバージョンは1つだけです (32 ビットバージョンはありません adprep32.exe)。 Adprep コマンドは、Windows Server 2012 を実行するドメインコントローラーを既存の Active Directory ドメインまたはフォレストにインストールするときに、必要に応じて自動的に実行されます。

adprep 操作は自動的に実行されますが、Adprep.exe を別途実行することができます。 たとえば、AD DS をインストールするユーザーが、Adprep /forestprep を実行するための必要条件である Enterprise Admins グループのメンバーでない場合は、コマンドを別途実行する必要があります。 ただし、最初の Windows Server 2012 ドメインコントローラーのインプレースアップグレードを計画している場合にのみ adprep.exe を実行する必要があります (つまり、Windows Server 2012 を実行するドメインコントローラーのオペレーティングシステムをインプレースアップグレードする予定がある場合)。

Adprep.exe は、Windows Server 2012 インストールディスクの \support\adprep フォルダーにあります。Windows Server 2012 バージョンの adprep は、リモートで実行できます。

Windows Server 2012 バージョンの adprep.exe は、Windows Server 2008 以降の64ビットバージョンを実行している任意のサーバーで実行できます。 サーバーには、フォレストのスキーマ マスターと、ドメイン コントローラーを追加するドメインのインフラストラクチャ マスターへのネットワーク接続が必要です。 それらのいずれかの役割が Windows Server 2003 を実行するサーバーでホストされている場合は、adprep をリモートで実行する必要があります。 adprep を実行するサーバーはドメイン コントローラーである必要はありません。 このサーバーはドメインに参加するか、ワークグループに含めることができます。

> [!NOTE]
> Windows server 2003 を実行しているサーバーで Windows Server 2012 バージョンの adprep.exe を実行しようとすると、次のエラーが表示されます。
>
> Adprep.exe は有効な Win32 アプリケーションではありません。

![新機能](media/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal/AdprepNotValid.gif)

Adprep.exe で返される他のエラーの解決方法については、「[既知の問題](../../ad-ds/deploy/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal.md#BKMK_KnownIssues)」を参照してください。

### <a name="group-membership-check-against-windows-server-2003-operations-master-roles"></a>Windows Server 2003 操作マスターの役割に対するグループ メンバーシップの確認

Adprep では、コマンド (/forestprep、/domainprep、または /rodcprep) ごとに、グループ メンバーシップの確認を実行して、指定された資格情報が特定のグループのアカウントを表しているかどうか確認します。 この確認を実行するために、Adprep は操作マスターの役割の所有者にアクセスします。 操作マスターが Windows Server 2003 を実行しているときに、Adprep.exe を実行してグループ メンバーシップの確認がどのような場合でも実行されるようにするときは、/user および /userdomain コマンド ライン パラメーターを指定する必要があります。

/User と/userdomain は、Windows Server 2012 の Adprep.exe 用の新しいパラメーターです。 これらのパラメーターではぞれぞれ、adprep コマンドを実行するユーザーのユーザー アカウント名とユーザー ドメインを指定します。 Adprep.exe コマンドライン ユーティリティでは、/userdomain および /user のどちらかを指定して、もう一方を省略することはできません。

ただし、Windows PowerShell またはサーバー マネージャーを使用して Adprep 操作を AD DS インストールの一部として実行することもできます。 これらのエクスペリエンスでは、adprep.exe と同じ基になる実装 (adprep.dll) を共有します。 Windows PowerShell およびサーバー マネージャーのエクスペリエンスでは、それぞれ個別に資格情報を入力しますが、adprep.exe と同じ要件は必要ありません。 Windows PowerShell またはサーバー マネージャーを使用して、/user の値を adprep.dll に渡すことはできますが、/userdomain の値を adprep.dll に渡すことはできません。 /User が指定されていて、/userdomain が指定されていない場合は、ローカルコンピューターのドメインがチェックの実行に使用されます。 コンピューターがドメインに参加していない場合、グループ メンバーシップは確認できません。

グループ メンバーシップを確認できない場合、adprep のログ ファイルに警告メッセージが表示され、次のメッセージが続きます。

```
Adprep was unable to check the specified user's group membership. This could happen if the FSMO role owner <DNS host name of operations master> is running Windows Server 2003 or lower version of Windows.
```

/user パラメーターおよび /userdomain パラメーターを指定せずに Adprep.exe を実行し、操作マスターで Windows Server 2003 を実行している場合、Adprep.exe は現在のログオン ユーザーのドメイン内のドメイン コントローラーにアクセスします。 現在のログオン ユーザーがドメイン ユーザーではない場合、Adprep.exe ではグループ メンバーシップの確認を実行できません。 また、スマート カード資格情報が使用されている場合、/user と /userdomain の両方を指定しても、Adprep.exe ではグループ メンバーシップの確認を実行できません。

Adprep が正常に完了した場合、何も操作は必要ありません。 実行中にアクセス エラーで Adprep が失敗したら、正しいメンバーシップを持つアカウントを指定します。 詳細については、「[Adprep.exe を実行して Active Directory Domain Services をインストールするための資格情報要件](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_Creds)」を参照してください。

### <a name="syntax-for-adprep-in-windows-server-2012"></a>Windows Server 2012 の Adprep の構文

adprep を AD DS インストールとは別に実行するには、次の構文を使用します。

```
Adprep.exe /forestprep /forest <forest name> /userdomain <user domain name> /user <user name> /password *
```

詳細なログを生成するには、コマンドで /logdsid を使用します。 adprep.log は、%windir%\System32\Debug\Adprep\Logs に置かれます。

### <a name="running-adprep-using-smartcard"></a>スマート カードを使用した adprep の実行

Windows Server 2012 バージョンの adprep.exe は、スマートカードを使用して資格情報として機能しますが、コマンドラインからスマートカードの資格情報を指定する簡単な方法はありません。 これを行うためには、PowerShell コマンドレットの Get-Credential を使用してスマート カードの資格情報を取得する方法があります。 次に、`@@...` として表示される、返された PSCredential オブジェクトのユーザー名を使用します。 パスワードは、スマート カードの PIN です。

/user が指定されている場合、Adprep.exe には /userdomain が必要です。 スマート カード資格情報の場合、/userdomain はスマート カードで表されている、基になるユーザー アカウントのドメインにする必要があります。

### <a name="adprep-domainprep-gpprep-command-is-not-run-automatically"></a>adprep /domainprep /gpprep コマンドは自動的に実行されません。

adprep /domainprep /gpprep コマンドは、AD DS インストールの一部として実行されません。 このコマンドでは、ポリシーの結果セット (RSoP) 計画モード機能に必要なアクセス許可を設定します。 このコマンドの詳細については、[Microsoft サポート技術情報の記事 324392](https://support.microsoft.com/kb/324392) を参照してください。 コマンドを Active Directory ドメインで実行する必要がある場合、AD DS インストールとは別にコマンドを実行できます。 Windows Server 2003 SP1 以降を実行するドメイン コントローラーの展開準備でコマンドが既に実行されている場合は、コマンドをもう一度実行する必要はありません。

Adprep/domainprep/gpprep を実行しなくても、Windows Server 2012 を実行するドメインコントローラーを既存のドメインに安全に追加できますが、RSOP 計画モードは正しく機能しません。

## <a name="ad-ds-installation-prerequisite-validation"></a><a name="BKMK_PrereqCheck"></a>AD DS インストールの前提条件の検証

AD DS インストール ウィザードでは、インストールが開始される前に次の前提条件が満たされているか確認が行われます。 これにより、インストールをブロックする可能性のある問題を修正することができます。

たとえば、Adprep 関連の前提条件には次が含まれます。

- Adprep 資格情報の確認: adprep の実行が必要な場合、ユーザーに操作を実行する十分な権限があるか確認します。
- スキーマ マスターの可用性のチェック: インストール ウィザードで adprep /forestprep の実行が必要なことが確認されたら、スキーマ マスターがオンラインになっているか確認され、オンラインでない場合は失敗します。
- インフラストラクチャ マスターの可用性のチェック: インストール ウィザードで adprep /domainprep の実行が必要なことが確認されたら、インフラストラクチャ マスターがオンラインになっているか確認され、オンラインでない場合は失敗します。

従来の Active Directory インストール ウィザード (dcpromo.exe) から継承されている、その他の前提条件のチェックは次のとおりです。

- フォレスト名の確認: フォレスト名が有効で、現在その名前が存在していないことを確認します。
- NetBIOS 名の確認: 指定されている NetBIOS 名が有効で、既存の名前と競合しないことを確認します。
- コンポーネント パスの確認: Active Directory データベース、ログ、および SYSVOL のパスが有効で、それらに使用できるディスク領域が十分であることを確認します。
- 子ドメイン名の確認: 親ドメイン名および新しい子ドメイン名が有効で、既存のドメインと競合しないことを確認します。
- ツリー ドメイン名の確認: 指定されたツリー名が有効で、現在その名前が存在していないことを確認します。

## <a name="system-requirements"></a><a name="BKMK_SystemReqs"></a>システム要件

Windows server 2012 のシステム要件は、Windows Server 2008 R2 から変更されていません。 詳細については、「 [Windows Server 2008 R2 SP1 のシステム要件](https://www.microsoft.com/windowsserver2008/en/us/system-requirements.aspx)」 () を参照してください https://www.microsoft.com/windowsserver2008/en/us/system-requirements.aspx) 。

機能によっては、追加の要件がある場合があります。 たとえば、仮想ドメインコントローラーの複製機能を使用するには、PDC エミュレーターが Windows Server 2012 を実行し、Hyper-v の役割がインストールされた Windows Server 2012 を実行しているコンピューターが必要です。

## <a name="known-issues"></a><a name="BKMK_KnownIssues"></a>既知の問題

このセクションでは、Windows Server 2012 での AD DS のインストールに影響する既知の問題の一部を示します。 その他の既知の問題については、「[ドメイン コントローラーの展開のトラブルシューティング](../../ad-ds/deploy/Troubleshooting-Domain-Controller-Deployment.md)」を参照してください。

- リモートで adprep /forestprep を実行しているときにスキーマ マスターへの WMI アクセスが Windows ファイアウォールによってブロックされると、次のエラーが %systemroot%\system32\debug\adprep にある adprep のログに記録されます。

   ```
   Adprep encountered a Win32 error.
   Error code: 0x6ba Error message: The RPC server is unavailable.
   ```

   この場合は、スキーマ マスターで adprep /forestprep を直接実行するか、次のコマンドのいずれかを実行して Windows ファイアウォールを通過する WMI トラフィックを許可することでエラーを回避できます。

   Windows Server 2008 以降の場合:

   ```
   netsh advfirewall firewall set rule group="windows management instrumentation (wmi)" new enable=yes
   ```

   Windows Server 2003 の場合:

   ```
   netsh firewall set service RemoteAdmin enable
   ```

   adprep が完了したら、次のコマンドのいずれかを実行して WMI トラフィックをもう一度ブロックできます。

   ```
   netsh advfirewall firewall set rule group="windows management instrumentation (wmi)" new enable=no
   ```

   ```
   netsh firewall set service remoteadmin disable
   ```

- Ctrl キーを押しながら C キーを押して、Install-ADDSForest コマンドレットをキャンセルすることができます。 キャンセルによってインストールが停止し、サーバーの状態に対して行われたすべての変更が元に戻ります。 ただし、キャンセル コマンドが実行された後も、制御は Windows PowerShell に返されず、コマンドレットが無制限にハングする可能性があります。
- **インストール前にターゲット サーバーがドメインに参加していない場合、スマート カード資格情報を使用した追加のドメイン コントローラーのインストールは失敗します。**

   この場合、次のエラー メッセージが返されます。

   レプリケーション ソース ドメイン コントローラー *source domain controller name* に接続できません。 (例外: ログインに失敗しました: ユーザー名が不明またはパスワードが無効です)

   ターゲット サーバーをドメインに参加させ、スマート カードを使用してインストールを実行すると、インストールは成功します。

- **ADDSDeployment モジュールは 32 ビット プロセスで実行されません。** ADDSDeployment コマンドレットを含むスクリプトと、ネイティブ64ビットプロセスをサポートしない他のコマンドレットを使用して、Windows Server 2012 の展開と構成を自動化する場合、スクリプトは ADDSDeployment コマンドレットが見つからないことを示すエラーで失敗することがあります。

   この場合は、ADDSDeployment コマンドレットを、ネイティブの 64 ビット プロセスをサポートしていないコマンドレットとは別に実行する必要があります。

- Windows Server 2012 には、回復力のあるファイルシステムという名前の新しいファイルシステムがあります。 Resilient File System (ReFS) でフォーマットされたデータ ボリュームに Active Directory データベース、ログ ファイル、または SYSVOL を格納しないでください。 ReFS の詳細については、「[Windows の次世代ファイル システム ReFS の構築 (Building the next generation file system for Windows: ReFS)](https://blogs.msdn.com/b/b8/archive/2012/01/16/building-the-next-generation-file-system-for-windows-refs.aspx)」を参照してください。
- サーバーマネージャーでは、Server Core インストール上で AD DS またはその他のサーバーの役割を実行していて、Windows Server 2012 にアップグレードされているサーバーでは、イベントと状態が想定どおりに収集されていても、サーバーの役割が赤の状態で表示されることがあります。 プレリリース版の Windows Server 2012 の Server Core インストールを実行するサーバーも影響を受ける可能性があります。

### <a name="active-directory-domain-services-installation-hangs-if-an-error-prevents-critical-replication"></a>エラーが発生して重要なレプリケーションが実行されないと、Active Directory ドメイン サービスのインストールがハングする

重要なレプリケーション フェーズ中に AD DS インストールでエラーが発生すると、インストールは無制限にハングする可能性があります。 たとえば、ネットワーク エラーにより重要なレプリケーションが完了できないと、インストールは続行されません。

サーバー マネージャーを使用してインストールしているとき、インストールの進行状況ページは開いたままでも、画面にエラーが表示されず、進行状況が約 15 分間変更されない場合があります。 Windows PowerShell を使用している場合、Windows PowerShell ウィンドウに表示される進行状況は 15 分以上変更されません。

この問題が発生した場合は、ターゲット サーバーの %systemroot%\debug フォルダーにある dcpromo.log ファイルを確認してください。 ログ ファイルには通常、レプリケーション エラーが繰り返し発生していることが示されています。 この問題の既知の原因は次のとおりです。

- ネットワークの問題により、昇格されているターゲット サーバーと、レプリケーション ソースのドメイン コントローラーの間で、重要なレプリケーションが実行されなかった。

   たとえば、dcpromo.log には次のように表示されます。

   ```
   05/02/2012 14:16:46 [INFO] EVENTLOG (Error): NTDS Replication / DS RPC Client : 1963
   Internal event: The following local directory service received an exception from a remote procedure call (RPC) connection. Extensive RPC information was requested. This is intermediate information and might not contain a possible cause.
   Process ID:
   500
   Reported error information:
   Error value:
   Could not find the domain controller for this domain. (1908)
   directory service:
   <domain>.com
   Extensive error information:
   Error value:
   A security package specific error occurred. 1825
   directory service:
   <DC Name>
   ```

   インストール プロセスでは重要なレプリケーションが無制限に再試行されるため、基になるネットワークの問題が解決されると、ドメイン コントローラーのインストールが続行されます。 必要に応じて、ipconfig、nslookup、netmon などのツールを使用してネットワークの問題を調べてください。 昇格するドメイン コントローラーと AD DS のインストール時に選択したレプリケーション パートナーの間で接続が確立されていることを確認します。 また、名前解決が機能していることを確認します。

   ネットワーク接続と名前解決に関する AD DS のインストール要件は、インストールが開始される前の前提条件の確認中に検証されます。 ただし、前提条件の検証が実行されてからインストールが完了する前に、いくつかのエラー状態が発生する可能性があります (レプリケーション パートナーがインストール中に使用できなくなった場合など)。

- レプリカ ドメイン コントローラーのインストール時に、インストール資格情報に対してターゲット サーバーのローカル Administrator アカウントが指定され、ローカル Administrator アカウントのパスワードが Domain Admin アカウントのパスワードと一致している。 この場合は、インストールウィザードを完了し、"アクセスが拒否されました" エラーが発生する前にインストールを開始することができます。

   たとえば、dcpromo.log には次のように表示されます。

   ```
   03/30/2012 11:36:51 [INFO] Creating the NTDS Settings object for this Active Directory Domain Controller on the remote AD DC DC2.contoso.com...
   03/30/2012 11:36:51 [INFO] EVENTLOG (Error): NTDS Replication / DS RPC Client : 1963Internal event: The following local directory service received an exception from a remote procedure call (RPC) connection. Extensive RPC information was requested. This is intermediate information and might not contain a possible cause.
   Process ID:
   508
   Reported error information:
   Error value:
   Access is denied. (5)
   directory service:
   DC2.contoso.com
   ```

   エラーの原因がローカルの Administrator アカウントおよびパスワードの指定である場合、エラーから回復するには、オペレーティング システムを再インストールし、インストールを完了できなかったドメイン コントローラーのアカウントの[メタデータ クリーンアップを実行](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc816907(v=ws.10))してから、Domain Admin 資格情報を使用して AD DS のインストールを再試行する必要があります。 インストールが正常に完了しなかった場合でも、サーバーでは AD DS がインストールされていると示されるので、サーバーを再起動してもこのエラー状態は解決されません。

### <a name="active-directory-domain-services-configuration-wizard-warns-when-a-non-normalized-dns-name-is-specified"></a><a name="BKMK_nonnormalDNSNameWarning"></a>正規化されていない DNS 名が指定されている場合、Active Directory ドメイン サービス構成ウィザードで警告が表示される

新しいドメインまたはフォレストを作成するときに、正規化されていない国際化文字を含む DNS ドメイン名を指定すると、Active Directory ドメイン サービス構成ウィザードに、名前の DNS クエリが失敗する可能性があることを示す警告が表示されます。 [配置構成] ページで DNS ドメイン名が指定されている場合でも、ウィザードの [前提条件のチェック] ページに後で警告が表示されます。

DNS ドメイン名が、füßball や ' ΣΤ ' .com などの非正規化された名前を使用して指定されている場合 (正規化されたバージョンは füssball.com およびβστα.)、WinHTTP でアクセスしようとするクライアントアプリケーションは名前解決 Api を呼び出す前に名前を正規化します。 ユーザーが一部のダイアログで "' ΣΤ ' .com" と入力すると、DNS クエリは "βστα." として送信され、DNS サーバーは "' ΣΤ ' .com" のリソースレコードと一致しません。 ユーザーは名前を解決できません。

次の例で、正規化されていない IDN 名を使用するときに発生する可能性のある問題の 1 つについて説明します。

1. 正規化されていない名前を使用しているドメインは、dns サーバー: füßball に作成され、登録されます。
2. コンピューター "nps" はドメインに参加し、登録されている名前を取得します。 füßball
3. クライアントアプリケーションがサーバー nps に接続しようとしています。 füßball
4. クライアントアプリケーションは、名前解決 Api を呼び出して füßball という名前の解決を試みます。
5. 正規化のため、名前は nps.füssball.com に変換され、ネットワーク経由で nps. füßball として照会されます。
6. 登録された名前が nps. füßball であるため、クライアントアプリケーションは名前を解決できません。

Active Directory ドメイン サービス構成ウィザードの [前提条件のチェック] ページに警告が表示される場合は、[配置構成] ページに戻り、正規化された DNS ドメイン名を指定します。 Windows PowerShell を使用して新しいドメインをインストールしている場合は、-DomainName オプションで正規化された DNS 名を指定します。

IDN の詳細については、「[Handling Internationalized Domain Names (IDNs) (国際化ドメイン名 (IDN) の処理)](/windows/win32/intl/handling-internationalized-domain-names--idns)」を参照してください。
