---
ms.assetid: ba7f2b9f-7351-4680-b7d8-a5f270614f1c
title: "新; s での新しい Active Directory ドメイン サービスのインストールと削除"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 814a6f1af9144db28e81163b21cb5da4b6e51b3b
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="what39s-new-in-active-directory-domain-services-installation-and-removal"></a>新; s での新しい Active Directory ドメイン サービスのインストールと削除

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックについて説明します。  
  
-   [Active Directory ドメイン サービス構成ウィザード](../../ad-ds/deploy/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal.md#BKMK_ADConfigurationWizard)  
  
-   [Adprep.exe の統合](../../ad-ds/deploy/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal.md#BKMK_NewAdprep)  
  
-   [AD DS インストールの前提条件の検証](../../ad-ds/deploy/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal.md#BKMK_PrereqCheck)  
  
-   [システム要件](../../ad-ds/deploy/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal.md#BKMK_SystemReqs)  
  
-   [既知の問題](../../ad-ds/deploy/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal.md#BKMK_KnownIssues)  
  
Windows Server 2012 の active Directory ドメイン サービス (AD DS) の展開はシンプルかつ Windows Server の以前のバージョンよりも高速です。 AD DS インストール プロセスは Windows PowerShell 上に構築できるようになりましたし、サーバー マネージャーには、統合します。 ドメイン コントローラーを既存の Active Directory 環境に導入するために必要なステップ数が減少します。 これにより、簡単かつ効率的に新しい Active Directory 環境を作成するプロセスです。 新しい AD DS 展開プロセスは、それ以外の場合のインストールがブロックされているエラーの可能性を最小限に抑えます。  
  
さらに、同時に複数のサーバーで、AD DS サーバー役割のバイナリ (つまり、AD DS サーバー役割) をインストールできます。 AD DS インストール ウィザードは個々 のサーバーでリモートで実行することもできます。 これらの機能強化は、特に多くのドメイン コントローラーをさまざまな地域に事務所に展開する必要がある大規模でグローバルな展開の場合、Windows Server 2012 を実行するドメイン コントローラーを展開するための柔軟性を提供します。  
  
AD DS のインストールには、次の機能が含まれています。  
  
-   **AD DS インストール処理への Adprep.exe の統合。** さまざまな資格情報を使用して、Adprep.exe ファイルをコピーまたは特定のドメイン コントローラーにログオンする必要がなどの既存の Active Directory を準備するために必要だったわずらわしい手順がすべて簡略化または自動化します。 これは、AD DS をインストールするために必要な時間が短縮され、それ以外の場合のドメイン コントローラーの昇格を妨げるエラーを減らします。  
  
    新しいドメイン コントローラーのインストールの前に adprep.exe コマンドを実行する方が、環境を実行できます adprep.exe コマンドとは別に、AD DS インストールします。 64 ビット版 Windows Server 2008 以降を実行しているサーバーからすべての必要なコマンドを実行するため、Windows Server 2012 バージョンの adprep.exe はリモートで実行されます。  
  
-   **新しい AD DS のインストールは Windows PowerShell 上に構築し、リモートから呼び出すことができます。** 新しい AD DS のインストールが他のサーバーの役割をインストールするときに使用する AD DS をインストールする、同じインターフェイスを使用できるように、サーバー マネージャーでは、統合されています。 Windows PowerShell ユーザーの場合は、AD DS 展開コマンドレットは、機能と柔軟性を提供します。 機能するパリティ コマンド ラインと GUI インストール オプションです。  
  
-   **新しい AD DS のインストールには、前提条件の検証が含まれています。** 潜在的なエラーは、インストールが開始される前に識別されます。 結果の不完全なアップグレードが気にせずに発生する前に、エラー条件を解決できます。 たとえば場合、adprep /domainprep 実行する必要があります、インストール ウィザードでは、ユーザーが操作を実行する十分な権限を持っていることを確認します。  
  
-   **ウィザード ページの数を最小限にグループ化されている関連するオプションの最も一般的なプロモーション オプションの要件を反映した順序で構成ページをグループ化します。** これは、インストールの過程より適切なコンテキストを提供します。  
  
-   **グラフィカル インストール時に指定されたすべてのオプションを含む Windows PowerShell スクリプトをエクスポートすることができます。** インストールまたは削除の終わりには、同じ操作を自動化することで使用するための Windows PowerShell スクリプトに、設定をエクスポートすることができます。  
  
-   **再起動の前に重要なレプリケーションのみに発生します。** 再起動の前に重要でないデータのレプリケーションを許可するように新しいスイッチ。 詳細については、次を参照してください。[ADDSDeployment コマンドレット引数](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_Params)します。  
  
### <a name="BKMK_ADConfigurationWizard"></a>Active Directory ドメイン サービス構成ウィザード  
Windows Server 2012 以降では、Active Directory ドメイン サービス構成ウィザードは、ドメイン コントローラーをインストールするときに、設定を指定するユーザー インターフェイス (UI) オプションとして、従来の Active Directory ドメイン サービス インストール ウィザードを置き換えます。 役割の追加ウィザードが完了したら、Active Directory ドメイン サービス構成ウィザードが開始されます。  
  
> [!WARNING]  
> 従来の Active Directory ドメイン サービス インストール ウィザード (dcpromo.exe) は、Windows Server 2012 で始まる推奨されなくなりました。  
  
[Active Directory ドメイン サービス (&) #40; をインストールします。Level 100 & #41 です。](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md)を UI 手順の役割のバイナリを AD DS サーバーをインストールする役割の追加ウィザードを開始する方法を表示して、ドメイン コントローラーのインストールを完了する Active Directory ドメイン サービス構成ウィザードを実行します。 Windows PowerShell の例では、AD DS 展開コマンドレットを使用して両方の手順を完了する方法を説明します。  
  
### <a name="BKMK_NewAdprep"></a>Adprep.exe の統合  
Windows Server 2012 以降では、1 つだけのバージョンは Adprep.exe (32 ビット バージョンの adprep32.exe はありません)。 Adprep コマンドは、既存の Active Directory ドメインまたはフォレストに Windows Server 2012 を実行するドメイン コントローラーをインストールするときに、必要に応じて自動的に実行されます。  
  
Adprep 操作の実行が自動的とは別に Adprep.exe を実行できます。 たとえば、AD DS をインストールするユーザーは、Adprep を実行するために必要な Enterprise Admins グループのメンバーではない /forestprep、コマンドを別途実行する必要があります。 のみ実行する必要が adprep.exe インプレース アップグレードを計画している場合、最初の Windows Server 2012 ドメイン コントローラーが、(つまり、インプレースのプランが Windows Server 2012 を実行するドメイン コントローラーのオペレーティング システムをアップグレードする)。  
  
Adprep.exe は Windows Server 2012 インストール ディスクの \support\adprep フォルダーにあります。Adprep の Windows Server 2012 バージョンは、リモートで実行することです。  
  
Windows Server 2012 バージョンの adprep.exe は、64 ビット版 Windows Server 2008 以降を実行している任意のサーバーで実行できます。 サーバーには、フォレストとドメイン コントローラーを追加するドメインのインフラストラクチャ マスターのスキーマ マスターへのネットワーク接続が必要があります。 Windows Server 2003 を実行しているサーバーでホストされているこれらの役割のいずれかが場合、は、adprep をリモートで実行する必要があります。 Adprep を実行するサーバーは、ドメイン コントローラーである必要はありません。 ドメインに参加するか、ワークグループ内であることができます。  
  
> [!NOTE]  
> Windows Server 2003 を実行しているサーバーで、Windows Server 2012 バージョンの adprep.exe を実行しようとすると、次のエラーが表示されます。  
>   
> Adprep.exe は有効な Win32 アプリケーションではありません。  
  
![新機能します。](media/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal/AdprepNotValid.gif)  
  
Adprep.exe で返されるその他のエラーを解決する方法については、次を参照してください。[既知の問題](../../ad-ds/deploy/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal.md#BKMK_KnownIssues)します。  
  
#### <a name="group-membership-check-against-windows-server-2003-operations-master-roles"></a>Windows Server 2003 操作マスターの役割に対するグループ メンバーシップの確認  
各コマンド (/forestprep、/domainprep、または /rodcprep)、Adprep は指定された資格情報が特定のグループ アカウントを表すかどうかを確認するグループ メンバーシップの確認を実行します。 このチェックを実行するには、は、Adprep は操作マスターの役割所有者を接続します。 指定する必要がある場合は、操作マスタは、Windows Server 2003 を実行している、/user と /userdomain グループ メンバーップを確認する Adprep.exe を実行する場合、コマンド ライン パラメータのチェックは、すべてのケースで実行されます。  
  
/user と /userdomain は新しいパラメーター、Windows Server 2012 で Adprep.exe します。 これらのパラメーターを指定、ユーザー アカウント名とユーザーのドメイン、それぞれに、adprep コマンドを実行しているユーザーのします。 いずれかを指定する、Adprep.exe コマンド ライン ユーティリティ ブロック /userdomain と /user もう一方を省略することができます。  
  
ただし、Adprep 操作は、Windows PowerShell またはサーバー マネージャーを使用して AD DS のインストールの一部としても実行できます。 これらのエクスペリエンスは、adprep.exe と同じ基になる実装 (adprep.dll) を共有します。 Windows PowerShell およびサーバー マネージャーのエクスペリエンスでは、入力、これがなくても同じ要件 adprep.exe を個別に資格情報があります。 Windows PowerShell またはサーバー マネージャーを使用することは値を渡す /user ではなく /userdomain adprep.dll にします。 場合 /user が指定されているが、/userdomain が指定されていない、ローカル コンピューターのドメインは、チェックを実行するために使用します。 コンピューターがドメインに参加してでない場合は、グループのメンバーップを確認できません。  
  
グループのメンバーップを確認することはできず、Adprep adprep のログ ファイルに警告メッセージが表示が続行します。  
  
```  
Adprep was unable to check the specified user's group membership. This could happen if the FSMO role owner <DNS host name of operations master> is running Windows Server 2003 or lower version of Windows.  
```  
  
指定せずに Adprep.exe を実行する場合、/user と /userdomain パラメーターと、操作マスタが Windows Server 2003 を実行している、Adprep.exe は現在のログオン ユーザーのドメインのドメイン コントローラーを接続します。 現在のログオン ユーザーがドメイン アカウントでない場合、Adprep.exe は、グループ メンバーシップの確認を実行できません。 Adprep.exe も実行できませんグループ メンバーシップの確認スマート カードの資格情報を使用している場合場合でも、両方を指定しないでください /user と /userdomain します。  
  
Adprep が正常に完了した場合、操作は必要はありません。 実行中にアクセス エラーで Adprep が失敗した場合は、正しいメンバーシップを持つアカウントを提供します。 詳細については、次を参照してください。[資格情報の Adprep.exe を実行して Active Directory ドメイン サービスをインストールするための要件](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md#BKMK_Creds)します。  
  
#### <a name="syntax-for-adprep-in-windows-server-2012"></a>Windows Server 2012 の Adprep の構文  
Adprep を AD DS のインストールからとは別に実行するのにには、次の構文を使用します。  
  
```  
Adprep.exe /forestprep /forest <forest name> /userdomain <user domain name> /user <user name> /password *  
```  
  
使用 /logdsid を生成するために、コマンドでさらに詳細なログ記録します。 Adprep.log は windir%\System32\Debug\Adprep\Logs にあります。  
  
#### <a name="running-adprep-using-smartcard"></a>スマート カードを使用して adprep の実行  
Windows Server 2012 バージョンの adprep.exe は、スマート カードを使用して、資格情報としては機能しますが、コマンド ラインからスマート カードの資格情報を指定する簡単な方法はありません。 1 つの方法では、PowerShell コマンドレットの Get-Credential でスマート カードの資格情報を取得します。 ユーザーに表示される、返された PSCredential オブジェクトの名前を使用して`@@...`します。 パスワードは、スマート カードの PIN です。  
  
Adprep.exe が必要です /userdomain 場合 /user を指定します。 スマート カードの資格情報、/userdomain、スマート カードで表される、基になるユーザー アカウントのドメインにする必要があります。  
  
#### <a name="adprep-domainprep-gpprep-command-is-not-run-automatically"></a>Adprep /domainprep /gpprep コマンドが自動的に実行されていません  
Adprep /domainprep /gpprep コマンドは、AD DS のインストールの一部としては実行されません。 このコマンドは、計画モード機能の結果のポリシー セット (RSOP) に必要なアクセス許可を設定します。 このコマンドの詳細については、次を参照してください。[Microsoft サポート技術情報の記事 324392](https://support.microsoft.com/kb/324392)します。 コマンドは、Active Directory ドメインで実行する必要がある場合、AD DS のインストールから単独で実行できます。 コマンドが Windows Server 2003 SP1 を実行するドメイン コントローラーの展開の準備に既に実行されているか、後で、コマンドは、もう一度実行する必要はありません。場合、  
  
Adprep を実行せず、既存のドメインに Windows Server 2012 を実行するドメイン コントローラーを安全に追加できます /domainprep /gpprep、RSOP 計画モードは正しく機能しませんが、します。  
  
### <a name="BKMK_PrereqCheck"></a>AD DS インストールの前提条件の検証  
AD DS インストール ウィザードでは、インストールが開始される前に、次の前提条件を満たしていることを確認します。 これにより、インストールをブロックする可能性のある問題を修正する可能性があります。  
  
たとえば、Adprep 関連の前提条件は次のとおりです。  
  
-   Adprep 資格情報の確認: adprep を実行する必要がある場合、インストール ウィザードでは、ユーザーが必要な Adprep 操作を実行するための十分な権限を持っているか確認します。  
  
-   スキーマ マスターの可用性のチェック: インストール ウィザードでその adprep が判断した場合 /forestprep 実行する必要があります、スキーマ マスターがオンラインでは、それ以外の場合に失敗したことを確認します。  
  
-   インフラストラクチャ マスターの可用性のチェック: インストール ウィザードでその adprep が判断した場合 /domainprep 実行する必要があります、インフラストラクチャ マスターがオンラインでは、それ以外の場合に失敗したことを確認します。  
  
従来の Active Directory インストール ウィザード (dcpromo.exe) から継承されているその他の前提条件チェックは次のとおりです。  
  
-   フォレスト名の確認: により、フォレスト名が有効になり、現在存在していません。  
  
-   NetBIOS 名の確認: NetBIOS 名が有効と競合しない既存の名前に付属しているチェックします。  
  
-   コンポーネント パスの確認: Active Directory データベース、ログ、および SYSVOL のパスが有効であると、それらに使用できる十分なディスク領域があることを確認します。  
  
-   子ドメイン名の確認: 親と新しい子ドメイン名が有効であると、既存のドメインと競合しないことによりようになります。  
  
-   ツリー ドメイン名の確認: により、指定されたツリー名が有効であることが現在ないです。  
  
## <a name="BKMK_SystemReqs"></a>システム要件  
Windows Server 2012 のシステム要件は、Windows Server 2008 R2 から変更されていません。 詳細については、次を参照してください。[Windows Server 2008 R2 SP1 のシステム要件を持つ](https://www.microsoft.com/windowsserver2008/en/us/system-requirements.aspx)(https://www.microsoft.com/windowsserver2008/en/us/system-requirements.aspx)。  
  
一部の機能は、その他の要件を持つことができます。 たとえば、仮想ドメイン コントローラーの複製機能いる必要があります、PDC エミュレーターとインストールされている Hyper-V の役割を持つ Windows Server 2012 を実行しているコンピューターの Windows Server 2012 を実行します。  
  
## <a name="BKMK_KnownIssues"></a>既知の問題  
このセクションでは、Windows Server 2012 で AD DS のインストールに影響を与える既知の問題の一部を示します。 その他の既知の問題を参照してください。[ドメイン コントローラーの展開のトラブルシューティング](../../ad-ds/deploy/Troubleshooting-Domain-Controller-Deployment.md)します。  
  
-   Adprep をリモートで実行すると、Windows ファイアウォールが、スキーマ マスターへの WMI アクセスがブロックされている場合 /forestprep、systemroot%\system32\debug\adprep で adprep のログに次のエラーが記録されます。  
  
    ```  
    Adprep encountered a Win32 error.   
    Error code: 0x6ba Error message: The RPC server is unavailable.  
    ```  
  
    実行中か adprep によって、エラーを回避するこの例では、/forestprep 直接スキーマ マスタでまたはを実行できる Windows ファイアウォールを通過する WMI トラフィックを許可するように、次のコマンドのいずれかです。  
  
    Windows server 2008 以降。  
  
    ```  
    netsh advfirewall firewall set rule group="windows management instrumentation (wmi)" new enable=yes  
    ```  
  
    Windows server 2003 の場合。  
  
    ```  
    netsh firewall set service RemoteAdmin enable  
    ```  
  
    Adprep が完了したら、もう一度 WMI トラフィックをブロックする次のコマンドのいずれかを実行できます。  
  
    ```  
    netsh advfirewall firewall set rule group="windows management instrumentation (wmi)" new enable=no  
    ```  
  
    ```  
    netsh firewall set service remoteadmin disable  
    ```  
  
-   Install-ADDSForest コマンドレットをキャンセルするには、ctrl キーを押しながら C を入力することができます。 取り消しが、インストールを停止し、サーバーの状態に加えられた変更が元に戻ります。 キャンセル コマンドが発行されると、コントロールは、Windows PowerShell に返されないと、コマンドレットが無制限にハングします。  
  
-   **ターゲット サーバーがインストールする前に、ドメインに参加していない場合、スマート カードの資格情報を使用して、追加のドメイン コントローラーのインストールが失敗します。**  
  
    返されるエラー メッセージはここでは。  
  
    レプリケーション ソース ドメイン コントローラーに接続できません。*ソース ドメイン コントローラー名*します。 (例外: ログイン: ユーザー名が不明またはパスワードが間違って)  
  
    ターゲット サーバーをドメインに参加するスマート カードを使用してインストールを実行して、インストールが成功した場合。  
  
-   **ADDSDeployment モジュールは、32 ビット プロセスでは実行されません。** スクリプトを含む ADDSDeployment コマンドレットおよびネイティブの 64 ビット プロセスをサポートしていないその他のコマンドレットを使用して Windows Server 2012 の展開と構成を自動化している場合、スクリプトは、ADDSDeployment コマンドレットが見つからないことを示すエラーで失敗ことができます。  
  
    この場合は、ネイティブの 64 ビット プロセスをサポートしていないコマンドレットから ADDSDeployment コマンドレットを個別に実行する必要があります。  
  
-   Resilient File System という名前の Windows Server 2012 で、新しいファイル システムがあります。 Resilient File System (ReFS) でフォーマットされたデータ ボリュームに Active Directory データベース、ログ ファイル、または SYSVOL を格納しないでください。 ReFS の詳細については、次を参照してください。[Windows 用の次世代ファイル システムの構築: ReFS](http://blogs.msdn.com/b/b8/archive/2012/01/16/building-the-next-generation-file-system-for-windows-refs.aspx)します。  
  
-   サーバー マネージャーで、サーバーを Server Core インストールで AD DS または他のサーバーの役割を実行し、Windows Server 2012 にアップグレードした場合でも、イベントや状態が期待どおりに収集された、サーバーの役割は赤の状態で表示できます。 Windows Server 2012 も影響する段階のリリースの Server Core インストールを実行しているサーバー。  
  
### <a name="active-directory-domain-services-installation-hangs-if-an-error-prevents-critical-replication"></a>エラーが発生して重要なレプリケーション active Directory ドメイン サービスのインストールがハングします。  
AD DS のインストールには、重要なレプリケーション フェーズ中にエラーが発生すると、インストールは無制限にハングことができます。 たとえば、ネットワーク エラーにより、重要なレプリケーションを完了するが、インストールは続行できません。  
  
サーバー マネージャーを使用してをインストールする場合、インストールの進行状況] ページを開いたままし、画面で、報告されたエラーはありませんが、進行状況は約 15 分間を変更できませんを参照して可能性があります。 Windows PowerShell を使用している場合、Windows PowerShell ウィンドウに表示される進行状況は 15 分以上変更されません。  
  
この問題が発生した場合は、ターゲット サーバー上に %systemroot%\debug dcpromo.log ファイルを確認します。 ログ ファイルには、通常のレプリケーションに何度もエラーが表示されます。 この問題の既知の原因は次のとおりです。  
  
-   ネットワーク上の問題では、昇格されているターゲット サーバーと、レプリケーション ソース ドメイン コント ローラーの間での重要なレプリケーションしないようにします。  
  
    たとえば、dcpromo.log を示しています。  
  
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
  
    インストール プロセスでは、重要なレプリケーションが無制限に再試行、ため基礎となるネットワークの問題が解決される場合、ドメイン コント ローラーのインストールを実行します。 必要に応じて、ipconfig、nslookup、netmon などのツールを使用してネットワークの問題を調査します。 昇格するドメイン コント ローラーの間の接続が存在することを確認し、AD DS のインストール中にレプリケーション パートナーを選択します。 また、名前解決が機能を確認します。  
  
    ネットワーク接続と名前解決のための AD DS のインストール要件は、インストールが開始される前に、前提条件の確認中に検証されます。 一部のエラー状況は、時間に前提条件の検証が発生し、インストールが完了する前に場合など、レプリケーション パートナーが使用できなくなったのインストール中に発生する可能性が。  
  
-   レプリカ ドメイン コント ローラーのインストール時に、インストール資格情報のターゲット サーバーのローカル管理者アカウントが指定されているし、ローカル Administrator アカウントのパスワードが Domain Admin アカウントのパスワードと一致します。 この場合、インストール ウィザードを完了し、「アクセスが拒否されました」エラーが発生する前に、インストールを開始できます。  
  
    たとえば、dcpromo.log を示しています。  
  
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
  
    ローカル管理者アカウントとパスワードを指定して、エラーの原因がある場合、回復するためにする必要があります、オペレーティング システムを再インストール[メタデータのクリーンアップを実行](https://technet.microsoft.com/library/cc816907(WS.10).aspx)のインストールを完了し、再試行 Domain Admin 資格情報を使用して AD DS のインストールに失敗したドメイン コント ローラーのアカウントです。 サーバーは AD DS がインストールされている場合でも、インストールが正常に完了していないことを示すために、サーバーの再起動はこのエラーが発生しない修正します。  
  
### <a name="BKMK_nonnormalDNSNameWarning"></a>Active Directory ドメイン サービス構成ウィザードでは、正規化されていない DNS 名が指定されている場合に警告が表示されます。  
新しいドメインを作成する場合、またはフォレストとは、正規化されていない国際化文字を含む DNS ドメイン名を指定する場合、Active Directory ドメイン サービス構成ウィザードは、名前の DNS クエリが失敗することが警告を表示します。 [配置構成] ページで、DNS ドメイン名が指定されていますが、[前提条件のチェック] ページで、ウィザードで後で、警告が表示されます。  
  
DNS ドメイン名が füßball.com または 'ΣΤ'.com のように正規化されていない、名前で指定されている場合 (正規化されたバージョンが: füssball.com と βστα.com)、WinHTTP によるアクセスにしようとするクライアント アプリケーションは名前解決の Api を呼び出す前に、名前を正規化します。 場合は、ユーザーの種類"'ΣΤ'.com"のいくつかのダイアログ ボックスで、"βστα.com"とない DNS サーバーと一致するので、"'ΣΤ'.com"のリソース レコードを DNS クエリが送信されます。 ユーザーは名前を解決することができません。  
  
次の例では、正規化されていない IDN 名を使用するときに発生する問題の 1 つについて説明します。  
  
1.  非正規名を使用して、ドメインが作成され、dns サーバーに登録されている: füßball.com  
  
2.  マシン"nps"は、ドメインに参加しているし、登録の名前を取得します nps.füßball.com。  
  
3.  クライアント アプリケーションが、サーバー nps.füßball.com に接続しようとしています。  
  
4.  クライアント アプリケーションは、名前解決の Api を呼び出して名前 nps.füßball.com の解決を試みます。  
  
5.  正規化のため、名前 nps.füssball.com に変換し、nps.füßball.com としてネットワーク経由で照会  
  
6.  クライアント アプリケーションができないため、登録済みの名前は nps.füßball.com 名前を解決するのには  
  
Active Directory ドメイン サービス構成ウィザードの [前提条件のチェック] ページで、警告が表示されている場合は、配置構成] ページに戻るし、正規化された DNS ドメイン名を指定します。 Windows PowerShell を使用して新しいドメインをインストールする場合は、-domainname オプションの正規化された DNS 名を指定します。  
  
Idn の詳細については、次を参照してください。 [Handling Internationalized Domain Names (IDNs)](https://msdn.microsoft.com/library/windows/desktop/dd318142(v=vs.85).aspx)します。  
  

