---
ms.assetid: ba7f2b9f-7351-4680-b7d8-a5f270614f1c
title: Active Directory Domain Services のインストールと削除の新機能
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 66455a9ec4eb8a6ff6bfcfa387aeb59acb3ddcc2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59821353"
---
# <a name="whats-new-in-active-directory-domain-services-installation-and-removal"></a>Active Directory Domain Services のインストールと削除の新機能

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

Windows Server 2012 active Directory Domain Services (AD DS) の展開とは、簡単かつ Windows Server の以前のバージョンよりも高速です。 AD DS のインストール処理は Windows PowerShell 上に構築され、サーバー マネージャーに統合されています。 これまで Active Directory 環境へのドメイン コントローラーの導入に必要だった多くの手順が削減されています。 このため、新しい Active Directory 環境を以前よりも簡単かつ効率的に作成することができます。 新しい AD DS 展開プロセスにより、インストールをブロックするようなエラーが発生する可能性が最小限に抑えられます。  
  
また、AD DS サーバーの役割のバイナリ (AD DS サーバーの役割) を複数のサーバーに同時にインストールできます。 AD DS インストール ウィザードを個々のサーバーでリモートから実行することもできます。 これらの機能強化では、特に多くのドメイン コント ローラーが異なる地域のオフィスに展開する必要がある大規模でグローバルな展開の場合、Windows Server 2012 を実行するドメイン コント ローラーを展開する際の柔軟性を提供します。  
  
AD DS のインストールには、次の特長があります。  
  
- **AD DS インストール処理への Adprep.exe の統合。** さまざまな資格情報を使用したり、Adprep.exe ファイルをコピーしたり、ログオンして特定のドメイン コントローラーを指定する必要があるなどの、これまで Active Directory を準備するために必要だったわずらわしい手順がすべて簡略化または自動化されています。 これにより、AD DS のインストールに必要な時間が削減され、ドメイン コントローラーの昇格を妨げるエラーが発生する可能性が軽減されます。  

   新しいドメイン コントローラーのインストールよりも先に adprep.exe コマンドを実行するのが望ましい環境の場合は、AD DS インストールとは別に adprep.exe コマンドを実行できます。 64 ビット バージョンの Windows Server 2008 以降を実行するサーバーから必要なすべてのコマンドを実行できるように、Windows Server 2012 バージョンの adprep.exe はリモートで実行されます。  

- **新しい AD DS インストールは Windows PowerShell 上に構築され、リモートで呼び出し可能。** 新しい AD DS インストールがサーバー マネージャーに統合されたため、同じインターフェイスを使用して、他のサーバーの役割をインストールするときに使用する AD DS をインストールすることができます。 Windows PowerShell ユーザーの場合、AD DS 展開コマンドレットにより機能と柔軟性が向上します。 コマンド ラインと GUI インストール オプションの間には機能パリティがあります。  
- **新しい AD DS インストールにおける前提条件の検証。** 発生する可能性のあるエラーが、インストールの開始前に特定されます。 エラーの発生要因を事前に取り除くことができるため、アップグレードが不完全に終わる心配はありません。 たとえば、adprep /domainprep の実行が必要な場合、インストール ウィザードでユーザーにこの操作を実行する十分な権限があるか確認されます。  
- **関連するオプションをまとめてウィザードのページ数を最小限にし、昇格の過程で選択する最も一般的なオプションの要件を反映した順序で構成ページをグループ化。** インストールの過程で選択するさまざまなオプションが、より適切なコンテキストで提供されます。  
- **GUI でのインストール時に指定されたすべてのオプションを含む Windows PowerShell スクリプトをエクスポート可能。** インストールまたは削除の終わりに、設定を Windows PowerShell スクリプトにエクスポートし、同じ操作を自動化するために使用することができます。  
- **再起動の前に重要なレプリケーションのみが行われる。** 新しいスイッチによって、再起動の前に重要でないデータのレプリケーションを許可できます。 詳細については、「 [ADDSDeployment cmdlet arguments](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_Params)」を参照してください。  

## <a name="BKMK_ADConfigurationWizard"></a>Active Directory Domain Services 構成ウィザード

Windows Server 2012 以降では、Active Directory Domain Services 構成ウィザードは、ドメイン コント ローラーをインストールするときに、設定を指定するユーザー インターフェイス (UI) オプションとして、レガシ Active Directory ドメイン サービス インストール ウィザードを置き換えます。 Active Directory ドメイン サービス構成ウィザードは、役割の追加ウィザードの完了後に開始されます。  

> [!WARNING]  
> Windows Server 2012 以降では、従来の Active Directory ドメイン サービス インストール ウィザード (dcpromo.exe) は推奨されません。  

[Active Directory Domain Services のインストール&#40;レベル 100&#41;](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md)、UI の手順の役割のバイナリを AD DS サーバーをインストールする役割の追加ウィザードを開始する方法を表示して、Active Directory Domain Services を実行し、構成ウィザードを使用して、ドメイン コント ローラーのインストールを完了します。 Windows PowerShell の例では、AD DS 展開コマンドレットを使用して両方の手順を完了する方法を示しています。  
  
## <a name="BKMK_NewAdprep"></a>Adprep.exe の統合

1 つだけのバージョンの Adprep.exe は Windows Server 2012 以降では、(32 ビットのバージョンが存在しない adprep32.exe)。 Adprep コマンドは、既存の Active Directory ドメインまたはフォレストに Windows Server 2012 を実行するドメイン コント ローラーをインストールするときに、必要に応じて自動的に実行されます。  
  
adprep 操作は自動的に実行されますが、Adprep.exe を別途実行することができます。 たとえば、AD DS をインストールするユーザーが、Adprep /forestprep を実行するための必要条件である Enterprise Admins グループのメンバーでない場合は、コマンドを別途実行する必要があります。 Adprep.exe を実行する、インプレース アップグレードを計画している場合、最初の Windows Server 2012 ドメイン コント ローラーにのみがある (つまり、インプレースにプランが Windows Server 2012 を実行するドメイン コント ローラーのオペレーティング システムをアップグレードする)。  
  
Adprep.exe は、Windows Server 2012 のインストール ディスクの \support\adprep フォルダーにあります。Adprep の Windows Server 2012 のバージョンでは、リモートで実行できます。  
  
Windows Server 2012 バージョンの adprep.exe は、64 ビット バージョンの Windows Server 2008 またはそれ以降を実行する任意のサーバーで実行できます。 サーバーには、フォレストのスキーマ マスターと、ドメイン コントローラーを追加するドメインのインフラストラクチャ マスターへのネットワーク接続が必要です。 それらのいずれかの役割が Windows Server 2003 を実行するサーバーでホストされている場合は、adprep をリモートで実行する必要があります。 adprep を実行するサーバーはドメイン コントローラーである必要はありません。 このサーバーはドメインに参加するか、ワークグループに含めることができます。  

> [!NOTE]  
> Windows Server 2003 を実行しているサーバーで Windows Server 2012 バージョンの adprep.exe を実行しようとすると、次のエラーが表示されます。  
>   
> Adprep.exe は有効な Win32 アプリケーションではありません。  

![新着情報](media/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal/AdprepNotValid.gif)  

Adprep.exe で返される他のエラーの解決方法については、「 [Known issues](../../ad-ds/deploy/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal.md#BKMK_KnownIssues)」を参照してください。  

### <a name="group-membership-check-against-windows-server-2003-operations-master-roles"></a>Windows Server 2003 操作マスターの役割に対するグループ メンバーシップの確認

Adprep では、コマンド (/forestprep、/domainprep、または /rodcprep) ごとに、グループ メンバーシップの確認を実行して、指定された資格情報が特定のグループのアカウントを表しているかどうか確認します。 この確認を実行するために、Adprep は操作マスターの役割の所有者にアクセスします。 操作マスターが Windows Server 2003 を実行しているときに、Adprep.exe を実行してグループ メンバーシップの確認がどのような場合でも実行されるようにするときは、/user および /userdomain コマンド ライン パラメーターを指定する必要があります。  
  
/User および/userdomain は、Windows Server 2012 で Adprep.exe の新しいパラメーターです。 これらのパラメーターではぞれぞれ、adprep コマンドを実行するユーザーのユーザー アカウント名とユーザー ドメインを指定します。 Adprep.exe コマンドライン ユーティリティでは、/userdomain および /user のどちらかを指定して、もう一方を省略することはできません。  
  
ただし、Windows PowerShell またはサーバー マネージャーを使用して Adprep 操作を AD DS インストールの一部として実行することもできます。 これらのエクスペリエンスでは、adprep.exe と同じ基になる実装 (adprep.dll) を共有します。 Windows PowerShell およびサーバー マネージャーのエクスペリエンスでは、それぞれ個別に資格情報を入力しますが、adprep.exe と同じ要件は必要ありません。 Windows PowerShell またはサーバー マネージャーを使用して、/user の値を adprep.dll に渡すことはできますが、/userdomain の値を adprep.dll に渡すことはできません。 /User が指定されて、/userdomain が指定されていない場合は、ローカル コンピューターのドメインを使用して、チェックを実行します。 コンピューターがドメインに参加していない場合、グループ メンバーシップは確認できません。  
  
グループ メンバーシップを確認できない場合、adprep のログ ファイルに警告メッセージが表示され、次のメッセージが続きます。  

```
Adprep was unable to check the specified user's group membership. This could happen if the FSMO role owner <DNS host name of operations master> is running Windows Server 2003 or lower version of Windows.  
```

/user パラメーターおよび /userdomain パラメーターを指定せずに Adprep.exe を実行し、操作マスターで Windows Server 2003 を実行している場合、Adprep.exe は現在のログオン ユーザーのドメイン内のドメイン コントローラーにアクセスします。 現在のログオン ユーザーがドメイン ユーザーではない場合、Adprep.exe ではグループ メンバーシップの確認を実行できません。 また、スマート カード資格情報が使用されている場合、/user と /userdomain の両方を指定しても、Adprep.exe ではグループ メンバーシップの確認を実行できません。  
  
Adprep が正常に完了した場合、何も操作は必要ありません。 実行中にアクセス エラーで Adprep が失敗したら、正しいメンバーシップを持つアカウントを指定します。 詳細については、「 [Credential requirements to run Adprep.exe and install Active Directory Domain Services](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_Creds)」を参照してください。  
  
### <a name="syntax-for-adprep-in-windows-server-2012"></a>Windows Server 2012 の Adprep の構文

adprep を AD DS インストールとは別に実行するには、次の構文を使用します。  

```
Adprep.exe /forestprep /forest <forest name> /userdomain <user domain name> /user <user name> /password *  
```

詳細なログを生成するには、コマンドで /logdsid を使用します。 adprep.log は、%windir%\System32\Debug\Adprep\Logs に置かれます。  

### <a name="running-adprep-using-smartcard"></a>スマート カードを使用した adprep の実行

Windows Server 2012 バージョンの adprep.exe は、資格情報としてスマート カードを使用して、コマンドラインを使用してスマート カードの資格情報を指定する簡単な方法はありません。 これを行うためには、PowerShell コマンドレットの Get-Credential を使用してスマート カードの資格情報を取得する方法があります。 次に、 `@@...`として表示される、返された PSCredential オブジェクトのユーザー名を使用します。 パスワードは、スマート カードの PIN です。  

/user が指定されている場合、Adprep.exe には /userdomain が必要です。 スマート カード資格情報の場合、/userdomain はスマート カードで表されている、基になるユーザー アカウントのドメインにする必要があります。  

### <a name="adprep-domainprep-gpprep-command-is-not-run-automatically"></a>adprep /domainprep /gpprep コマンドは自動的に実行されません。

adprep /domainprep /gpprep コマンドは、AD DS インストールの一部として実行されません。 このコマンドでは、ポリシーの結果セット (RSoP) 計画モード機能に必要なアクセス許可を設定します。 このコマンドの詳細については、 [Microsoft サポート技術情報の記事 324392](https://support.microsoft.com/kb/324392)を参照してください。 コマンドを Active Directory ドメインで実行する必要がある場合、AD DS インストールとは別にコマンドを実行できます。 Windows Server 2003 SP1 以降を実行するドメイン コントローラーの展開準備でコマンドが既に実行されている場合は、コマンドをもう一度実行する必要はありません。  

実行中の adprep/domainprep/gpprep ことがなく既存のドメインに Windows Server 2012 を実行するドメイン コント ローラーを安全に追加できますが、RSOP 計画モードは正しく機能しません。  

## <a name="BKMK_PrereqCheck"></a>AD DS インストールの前提条件の検証

AD DS インストール ウィザードでは、インストールが開始される前に次の前提条件が満たされているか確認が行われます。 これにより、インストールをブロックする可能性のある問題を修正することができます。  
  
たとえば、Adprep 関連の前提条件には次が含まれます。  

- Adprep 資格情報の確認:adprep の実行が必要な場合、ユーザーに操作を実行する十分な権限があるか確認します。  
- スキーマ マスターの可用性のチェック:インストール ウィザードで adprep /forestprep の実行が必要なことが確認されたら、スキーマ マスターがオンラインになっているか確認され、オンラインでない場合は失敗します。  
- インフラストラクチャ マスターの可用性のチェック:インストール ウィザードで adprep /domainprep の実行が必要なことが確認されたら、インフラストラクチャ マスターがオンラインになっているか確認され、オンラインでない場合は失敗します。

従来の Active Directory インストール ウィザード (dcpromo.exe) から継承されている、その他の前提条件のチェックは次のとおりです。  

- フォレスト名の確認:フォレスト名が有効で、現在その名前が存在していないことを確認します。  
- NetBIOS 名の確認:指定されている NetBIOS 名が有効で、既存の名前と競合しないことを確認します。  
- コンポーネント パスの確認:Active Directory データベース、ログ、および SYSVOL のパスが有効で、それらに使用できるディスク領域が十分であることを確認します。  
- 子ドメイン名の確認:親ドメイン名および新しい子ドメイン名が有効で、既存のドメインと競合しないことを確認します。  
- ツリー ドメイン名の確認:指定されたツリー名が有効で、現在その名前が存在していないことを確認します。  

## <a name="BKMK_SystemReqs"></a>システム要件

Windows Server 2012 のシステム要件は、Windows Server 2008 R2 から変更されていません。 詳細については、次を参照してください。 [Windows Server 2008 R2 SP1 のシステム要件](https://www.microsoft.com/windowsserver2008/en/us/system-requirements.aspx)(https://www.microsoft.com/windowsserver2008/en/us/system-requirements.aspx)します。  

機能によっては、追加の要件がある場合があります。 たとえば、仮想ドメイン コント ローラーの複製機能が必要ですが、PDC エミュレーターは、HYPER-V の役割がインストールされた Windows Server 2012 を実行するコンピューターと Windows Server 2012 を実行します。  

## <a name="BKMK_KnownIssues"></a>既知の問題

このセクションでは、Windows Server 2012 で AD DS のインストールに影響を与える既知の問題の一部を示します。 その他の既知の問題については、「[ドメイン コントローラーの展開のトラブルシューティング](../../ad-ds/deploy/Troubleshooting-Domain-Controller-Deployment.md)」を参照してください。  

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
- **ターゲット サーバーがインストールする前に、ドメインに参加していない場合、スマート カードの資格情報を使用して、追加のドメイン コント ローラーのインストールが失敗します。**  

   この場合、次のエラー メッセージが返されます。  

   レプリケーション ソース ドメイン コントローラー *source domain controller name* に接続できません。 (例外:ログインに失敗しました: ユーザー名が不明またはパスワードが無効です)  

   ターゲット サーバーをドメインに参加させ、スマート カードを使用してインストールを実行すると、インストールは成功します。  
  
- **ADDSDeployment モジュールは 32 ビット プロセスで実行されません。** ADDSDeployment コマンドレットおよびネイティブの 64 ビット プロセスをサポートしていないその他のコマンドレットを含むスクリプトを使用して Windows Server 2012 の展開と構成を自動化している場合、スクリプト、ADDSDeployment を示すエラーで失敗します。コマンドレットが見つかりません。  

   この場合は、ADDSDeployment コマンドレットを、ネイティブの 64 ビット プロセスをサポートしていないコマンドレットとは別に実行する必要があります。  

- Resilient File System という名前の Windows Server 2012 では、新しいファイル システムです。 Resilient File System (ReFS) でフォーマットされたデータ ボリュームに Active Directory データベース、ログ ファイル、または SYSVOL を格納しないでください。 ReFS の詳細については、次を参照してください。 [Windows の次世代ファイル システムを構築します。ReFS](http://blogs.msdn.com/b/b8/archive/2012/01/16/building-the-next-generation-file-system-for-windows-refs.aspx)します。  
- サーバー マネージャーで、サーバーを Server Core インストールで AD DS または他のサーバーの役割を実行し、Windows Server 2012 にアップグレードした場合でも、期待どおりに、収集されるイベントと状態、サーバーの役割は赤の状態で表示できます。 Windows Server 2012 にも影響ベータ リリースの Server Core インストールを実行するサーバー。  

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

- レプリカ ドメイン コントローラーのインストール時に、インストール資格情報に対してターゲット サーバーのローカル Administrator アカウントが指定され、ローカル Administrator アカウントのパスワードが Domain Admin アカウントのパスワードと一致している。 この場合、インストール ウィザードを完了し、「アクセスが拒否されました」エラーが発生する前に、インストールを開始できます。  

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

   エラーの原因がローカルの Administrator アカウントおよびパスワードの指定である場合、エラーから回復するには、オペレーティング システムを再インストールし、インストールを完了できなかったドメイン コントローラーのアカウントの [メタデータ クリーンアップを実行](https://technet.microsoft.com/library/cc816907(WS.10).aspx) してから、Domain Admin 資格情報を使用して AD DS のインストールを再試行する必要があります。 インストールが正常に完了しなかった場合でも、サーバーでは AD DS がインストールされていると示されるので、サーバーを再起動してもこのエラー状態は解決されません。  

### <a name="BKMK_nonnormalDNSNameWarning"></a>Active Directory Domain Services 構成ウィザードでは、正規化されていない DNS 名を指定するときに警告が表示されます。

新しいドメインまたはフォレストを作成するときに、正規化されていない国際化文字を含む DNS ドメイン名を指定すると、Active Directory Domain Services 構成ウィザードに、名前の DNS クエリが失敗する可能性があることを示す警告が表示されます。 [配置構成] ページで DNS ドメイン名が指定されている場合でも、ウィザードの [前提条件のチェック] ページに後で警告が表示されます。  

Füßball.com または 'ΣΤ'.com のように、正規化されていない名前を使用して、DNS ドメイン名が指定されている場合 (正規化されたバージョン: füssball.com と βστα)、WinHTTP でアクセスしようとするクライアント アプリケーションは名前解決 Api を呼び出す前に、名前を正規化します。 ユーザーは、いくつかのダイアログ ボックスで、"'ΣΤ'.com"を型する場合、は、「βστα」と DNS サーバーは一致が"'ΣΤ'.com"のリソース レコードを持つように DNS クエリが送信されます。 ユーザーは名前を解決できません。  

次の例で、正規化されていない IDN 名を使用するときに発生する可能性のある問題の 1 つについて説明します。  

1. 正規化されていない名前を使用して、ドメインが作成され、dns サーバーに登録されている: füßball.com  
2. マシン"nps"は、ドメインに参加しているし、登録されているその名前を取得: nps.füßball.com  
3. クライアント アプリケーションが、サーバー nps.füßball.com に接続しようとしています。  
4. クライアント アプリケーションは、名前解決 Api を呼び出して名前 nps.füßball.com の解決を試みます。  
5. 正規化により名前 nps.füssball.com に変換を取得および nps.füßball.com としてネットワーク経由でクエリを実行  
6. クライアント アプリケーションは登録済みの名前は nps.füßball.com であるために、名前を解決するのにはできません。  

Active Directory ドメイン サービス構成ウィザードの [前提条件のチェック] ページに警告が表示される場合は、[配置構成] ページに戻り、正規化された DNS ドメイン名を指定します。 Windows PowerShell を使用して新しいドメインをインストールしている場合は、-DomainName オプションで正規化された DNS 名を指定します。  

IDN の詳細については、「 [Handling Internationalized Domain Names (IDNs) (国際化ドメイン名 (IDN) の処理)](https://msdn.microsoft.com/library/windows/desktop/dd318142(v=vs.85).aspx)」を参照してください。  
