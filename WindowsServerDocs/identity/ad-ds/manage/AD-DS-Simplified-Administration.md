---
ms.assetid: f74eec9a-2485-4ee0-a0d8-cce01250a294
title: AD DS の簡略化された管理
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: e1989630cadd7d63f8ed041174135722d568484f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80824425"
---
# <a name="ad-ds-simplified-administration"></a>AD DS の簡略化された管理

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックでは、Windows Server 2012 ドメインコントローラーの展開と管理の機能と利点、および以前のオペレーティングシステムの DC 展開と新しい Windows Server 2012 の実装の違いについて説明します。  
  
Windows Server 2012 では、次世代の Active Directory Domain Services 簡略化された管理が導入され、Windows 2000 Server 以来、最も革新的なドメインの再構想でした。 AD DS の簡略化された管理は、Active Directory の 12 年に及ぶ実績から学んだ教訓を活かし、アーキテクトや管理者にとってサポート性、柔軟性、直感性に優れた管理エクスペリエンスを提供します。 このことは、既存テクノロジの新しいバージョンを創出すると共に、Windows Server 2008 R2 でリリースされたコンポーネントの機能を拡張することを意味していました。  
  
AD DS の簡略化された管理とは、ドメイン展開の再イメージ化です。  
  
- AD DS の役割の展開は、新しいサーバー マネージャー アーキテクチャに組み込まれ、リモート インストールが可能になりました。  
- AD DS の展開と構成のエンジンは、新しい AD DS 構成ウィザードを使用するときも、Windows PowerShell になりました。  
- スキーマ拡張、フォレストの準備、およびドメインの準備は自動的にドメイン コントローラーの昇格の一部となり、スキーマ マスターなどの特殊なサーバー上での別個のタスクが必要なくなりました。  
- 昇格機能には、新しいドメイン コントローラーに対するフォレストとドメインの準備状態を検証する前提条件のチェックが含まれており、昇格に失敗する可能性が低減されます。  
- Windows PowerShell の Active Directory モジュールには、レプリケーション トポロジ管理、ダイナミック アクセス制御、およびその他の操作のためのコマンドレットが含まれるようになりました。  
- Windows Server 2012 のフォレストの機能レベルでは新しい機能は実装されず、ドメインの機能レベルは Kerberos の新機能のサブセットについてのみ必要となるので、管理者は同種のドメイン コントローラー環境を頻繁に用意する必要性から解放されます。  
- 自動展開とロールバック保護の機能を加えるため、仮想化ドメイン コントローラーに対する完全サポートを追加しました。  
   - 仮想化ドメインコントローラーの詳細については、「 [ &#40;Active Directory Domain Services&#41; AD DS &#40;仮想化&#41;レベル100の概要](../../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md)」を参照してください。

さらに、管理および保守に関する機能強化も多数あります。  

- Active Directory 管理センターには、GUI による Active Directory のごみ箱、細かい設定が可能なパスワード ポリシー管理、および Windows PowerShell 履歴ビューアーが含まれます。
- 新しいサーバー マネージャーには、パフォーマンス監視、ベスト プラクティス分析、重要サービス、およびイベント ログのための AD DS 固有のインターフェイスがあります。  
- グループ管理サービス アカウントは、同じセキュリティ プリンシパルを使っている複数のコンピューターをサポートします。  
- 稼働期間の長い Active Directory ドメインの管理状態を向上させるため、相対識別子 (RID) の発行と監視に関して機能を強化しました。  

次のように、Windows Server 2012 に含まれるその他の新機能の利益 AD DS ます。  

- NIC チーミングおよびデータ センター ブリッジング  
- DNS セキュリティ、および起動後に AD 統合ゾーンを使用できるまでの時間の短縮化  
- Hyper-V の信頼性とスケーラビリティの向上  
- BitLocker ネットワーク ロック解除  
- その他の Windows PowerShell コンポーネント管理モジュール  

## <a name="adprep-integration"></a>ADPREP の統合

Active Directory フォレストのスキーマ拡張とドメインの準備は、ドメイン コントローラー構成プロセスに統合されるようになりました。 新しいドメイン コントローラーを既存のフォレスト内に昇格する場合は、構成プロセスでアップグレードの状態が検出され、スキーマ拡張とドメインの準備のフェーズが同時に行われます。 最初の Windows Server 2012 ドメイン コントローラーをインストールするユーザーは、Enterprise Admins グループおよび Schema Admins グループのメンバーであるか、有効な代替資格情報を提供する必要があります。  
  
フォレストとドメインの別々の準備のために、Adprep.exe は DVD に収録されています。 Windows Server 2012 に付属するツールのバージョンは、Windows Server 2008 x64 および Windows Server 2008 R2 と下位互換性があります。 Adprep.exe は、ADDSDeployment ベースのドメイン コントローラー構成ツールと同様に、リモートでの forestprep と domainprep もサポートしています。  
  
Adprep および以前のオペレーティング システムでのフォレストの準備については、「 [Adprep の実行 (Windows Server 2008 R2)](https://technet.microsoft.com/library/dd464018(WS.10).aspx)」を参照してください。  

## <a name="server-manager-ad-ds-integration"></a>サーバー マネージャー AD DS の統合

![簡略化された管理](media/AD-DS-Simplified-Administration/ADDS_SMI_TR_Dashboard.png)  
  
サーバー マネージャーは、サーバー管理タスクのハブとして機能します。 そのダッシュボードスタイルのパネルでは、インストールされている役割とリモート サーバー グループのビューが定期的に更新されます。 サーバー マネージャーでは、コンソールにアクセスしなくても、ローカル サーバーとリモート サーバーの集中管理が可能です。  
  
Active Directory Domain Services は、これらのハブの役割の1つです。ドメインコントローラーまたは Windows 8 のリモートサーバー管理ツールでサーバーマネージャーを実行すると、フォレスト内のドメインコントローラーに関する最新の重要な問題が表示されます。  
  
次の表示があります。  
  
- サーバーの可用性  
- CPU とメモリの高い使用率に関するパフォーマンス モニターの警告  
- AD DS に固有の Windows サービスの状態  
- ディレクトリ サービス関連の最新の警告とイベント ログ内のエラー エントリ  
- Microsoft が推奨する一連の規則に対するドメイン コントローラーのベスト プラクティス分析  

## <a name="active-directory-administrative-center-recycle-bin"></a>Active Directory 管理センターのごみ箱

![簡略化された管理](media/AD-DS-Simplified-Administration/ADDS_SMI_TR_ADAC.png)  
  
Windows Server 2008 R2 では Active Directory のごみ箱が導入されました。このごみ箱は、バックアップからの復元、AD DS サービスの再開、またはドメイン コントローラーの再起動を行わずに、削除された Active Directory オブジェクトを回復します。  
  
Windows Server 2012 では、Active Directory 管理センターの新しいグラフィカル インターフェイスを使って、Windows PowerShell ベースの既存の復元機能を強化しています。 これにより管理者は、ごみ箱を有効にして、削除されたオブジェクトをフォレストのドメイン コンテキスト内で特定または復元できます。これらすべての操作を Windows PowerShell コマンドレットを直接実行せずに行うことができます。 Active Directory 管理センターと Active Directory のごみ箱はバックグラウンドで Windows PowerShell を使用します。したがって、以前のスクリプトや手順は今も有効です。  
  
Active Directory のごみ箱については、「 [Active Directory のごみ箱の手順ガイド (Windows Server 2008 R2)](https://technet.microsoft.com/library/dd392261(WS.10).aspx)」を参照してください。  
  
## <a name="active-directory-administrative-center-fine-grained-password-policy"></a>Active Directory 管理センターの細かい設定が可能なパスワード ポリシー

![簡略化された管理](media/AD-DS-Simplified-Administration/ADDS_SMI_TR_FGPP.png)  
  
Windows Server 2008 では、細かい設定が可能なパスワード ポリシー (FGPP) が導入されました。管理者は、ドメインごとに複数のパスワード ポリシーとアカウント ロックアウト ポリシーを構成できます。 この機能によってドメインは、ユーザーとグループに基づいてパスワード規則の制限を強めたり弱めたりする柔軟性のあるソリューションになることができます。 管理用のインターフェイスはなく、管理者が Ldp.exe または Adsiedit.msc を使って構成する必要がありました。 Windows Server 2008 R2 では、Windows PowerShell の Active Directory モジュールが導入され、管理者は細かい設定が可能なパスワード ポリシー (FGPP) のためのコマンドライン インターフェイスを利用できるようになりました。  
  
Windows Server 2012 では、細かい設定が可能なパスワード ポリシーのためのグラフィカル インターフェイスが用意されています。 Active Directory 管理センターは、この新しいダイアログのホームであり、すべての管理者が簡素化された FGPP 管理を利用できます。  
  
細かい設定が可能なパスワード ポリシーの詳細については、「 [ステップ バイ ステップ ガイド - 細かい設定が可能なパスワードおよびアカウント ロックアウトのポリシー設定 (Windows Server 2008 R2)](https://technet.microsoft.com/library/cc770842(WS.10).aspx)」を参照してください。  
  
## <a name="active-directory-administrative-center-windows-powershell-history-viewer"></a>Active Directory 管理センターの Windows PowerShell 履歴ビューアー

![簡略化された管理](media/AD-DS-Simplified-Administration/ADDS_SMI_TR_HistoryViewer.png)  
  
Windows Server 2008 R2 では、Active Directory 管理センターが導入されました。これは、Windows 2000 で作成された、古い Active Directory ユーザーとコンピューター スナップインに代わるものでした。 Active Directory 管理センターは、当時新しかった Windows PowerShell の Active Directory モジュールのためのグラフィカルな管理インターフェイスを提供します。  
  
Active Directory モジュールには 100 を超えるコマンドレットがありますが、その習得は管理者にとって困難となる場合もあります。 Windows PowerShell は Windows 管理の戦略に深く統合されていることから、Active Directory 管理センターにはコマンドレットの実行をグラフィカル インターフェイスで見ることができるビューアーが含まれるようになりました。 履歴の検索、コピー、消去、およびメモの追加を、シンプルなインターフェイスを使って行うことができます。 その目的は、管理者がグラフィカル インターフェイスを使ってオブジェクトを作成または変更した後、それを履歴ビューアー内で確認することで、Windows PowerShell スクリプトに関する知識を深め、スクリプト サンプルを変更できるようにすることです。  

## <a name="ad-replication-windows-powershell"></a>AD レプリケーションのための Windows PowerShell

![簡略化された管理](media/AD-DS-Simplified-Administration/ADDS_PSNewADReplSite.png)  
  
Windows Server 2012 では、Windows PowerShell の Active Directory モジュールに Active Directory レプリケーション用のコマンドレットが追加されています。 これらのコマンドレットにより、新しい、または既存のサイト、サブネット、接続、サイト リンク、およびブリッジの構成ができるようになります。 また、Active Directory レプリケーションのメタデータ、レプリケーションの状態、キュー、および最新のベクター情報を返すこともできます。 新たに導入されたレプリケーションのコマンドレットと、展開のコマンドレットおよび他の既存の AD DS コマンドレットとが組み合わさったことによって、管理者は Windows PowerShell だけでフォレストを管理できるようになりました。 グラフィカル インターフェイスを使わずに Windows Server 2012 のプロビジョニングと管理を行いたいと考えている管理者にとっては新しい機会が生まれます。それによって、オペレーティング システムの攻撃の要件とサービスの要件が低くなります。 このことは、Secret Internet Protocol Router (SIPR) や企業 DMZ など、セキュリティ レベルの高いネットワークにサーバーを展開するときに特に重要となります。  
  
AD DS のサイト トポロジとレプリケーションの詳細については、「 [Windows Server テクニカル リファレンス](https://technet.microsoft.com/library/cc739127(WS.10).aspx)」を参照してください。  

## <a name="rid-management-and-issuance-improvements"></a>RID の管理と発行の機能強化

Windows 2000 Active Directory では、RID マスターが導入されました。これは、ユーザー、グループ、コンピューターといったセキュリティ トラスティのセキュリティ識別子 (SID) を作成するために、相対識別子のプールをドメイン コントローラーに対して発行します。  既定では、このグローバル RID 空間は、ドメイン内で作成される合計 2<sup>30</sup> (つまり 1,073,741,823) 個の SID に制限されています。 SID をプールに戻したり、再発行したりすることはできません。 時間の経過と共に、大規模なドメインでは RID の残数が少なくなったり、何らかのアクシデントによって RID が無駄に減り、最終的に枯渇したりする場合があります。  
  
Windows Server 2012 では、RID の発行と管理に関する多数の問題に対処しています。それらの問題は、1999 年に最初の Active Directory ドメインが作成されて以降、AD DS が進化を続ける過程で、お客様と Microsoft カスタマー サポートによって発見されたものです。 次のようなクラスがあります。  

- RID 消費の警告が定期的にイベント ログに書き込まれます。  
- 管理者が RID プールを無効にすると、イベントがログに記録されます。  
- RID ポリシーの RID ブロック サイズの上限が適用されるようになりました。  
- グローバル ID 空間が少なくなると、RID の人為的シーリングが適用され、ログに記録されるようになりました。これによって管理者は、グローバル空間が枯渇する前に対策を講じることができます。
- グローバル RID 空間は 1 ビット増加できるようになり、そのサイズは 2 倍の 2<sup>31</sup> (2,147,483,648 個の SID) になります。  

RID および RID マスターの詳細については、「 [セキュリティ識別子のしくみ](https://technet.microsoft.com/library/cc778824(WS.10).aspx)」を参照してください。  
  
## <a name="ad-ds-role-deployment-and-management-architecture"></a>AD DS の役割の展開と管理のためのアーキテクチャ

サーバー マネージャーおよび Windows PowerShell の ADDSDeployment モジュールは、AD DS の役割を展開または管理するときの機能に関して、次のコア アセンブリに依存します。  

- Microsoft.ADroles.Aspects.dll  
- Microsoft.ADroles.Instrumentation.dll  
- Microsoft.ADRoles.ServerManager.Common.dll  
- Microsoft.ADRoles.UI.Common.dll  
- Microsoft.DirectoryServices.Deployment.Types.dll  
- Microsoft.DirectoryServices.ServerManager.dll  
- Addsdeployment.psm1  
- Addsdeployment.psd1  

どちらも、リモートからの役割のインストールと構成に関して、Windows PowerShell およびそのリモート呼び出しコマンドに依存します。  

![簡略化された管理](media/AD-DS-Simplified-Administration/ADDS_SMI_TR_DepDLLs.png)  

また、Windows Server 2012 では、次のサービスの一部として、以前の昇格操作の多くを LSASS.EXE からリファクターします。  

- DS 役割サーバー サービス (DsRoleSvc)  
- DSRoleSvc.dll (DsRoleSvc サービスによって読み込まれる)  

仮想ドメイン コントローラーの昇格、降格、または複製を行うためには、このサービスが存在して実行されている必要があります。 AD DS の役割のインストールでは、このサービスが追加され、開始の種類として [手動] が既定で設定されます。 このサービスは無効にしないでください。  

## <a name="adprep-and-prerequisite-checking-architecture"></a>ADPrep および前提条件チェックのためのアーキテクチャ

Adprep をスキーマ マスター上で実行する必要はなくなりました。 Windows Server 2008 x64 以降を搭載したコンピューターであればリモートで実行できます。  
  
> [!NOTE]  
> Adprep は LDAP で Schxx.ldf ファイルをインポートし、インポート中にスキーマ マスターへの接続が失われた場合は自動的に再接続しません。 インポート プロセスの一環として、スキーマ マスターは特定のモードに設定され、自動再接続は無効にされます。その理由は、接続が失われた後に LDAP が再接続する場合、再確立された接続が特定のモードに入らないためです。 その場合、スキーマは正しく更新されません。  
  
前提条件チェックによって、特定の条件が満たされることが保証されます。 そのような条件は AD DS のインストールが成功するために必要とされます。 満たされない必須条件がある場合は、それらを解決したうえで、インストールを続行できます。 フォレストまたはドメインの準備ができていないことも検出されるので、その場合は Adprep 展開コードが自動的に実行されます。  

### <a name="adprep-executables-dlls-ldfs-files"></a>ADPrep の実行可能ファイル、DLL、LDF、およびファイル

- ADprep.dll  
- Ldifde.dll  
- Csvde.dll  
- Sch14.ldf ～ Sch56.ldf  
- Schupgrade.cat  
- *dcpromo.csv  

以前 ADprep.exe に格納されていた AD 準備コードは、adprep.dll 内にリファクターされています。 これによって、ADPrep.exe と Windows PowerShell の ADDSDeployment モジュールの両方が同じタスクのライブラリを使用し、同じ機能を持つことができます。 Adprep.exe はインストール メディアに収録されていますが、自動プロセスがこれを直接呼び出すことはありません。管理者だけが手動で実行します。 Windows Server 2008 x64 以降のオペレーティング システム上でのみ実行できます。 Ldifde.exe と csvde.exe も準備プロセスによって読み込まれる DLL としてリファクターされたバージョンを持ちます。 スキーマ拡張では、以前のオペレーティング システム バージョンと同様、署名確認される LDF ファイルを使用します。  
  
![簡略化された管理](media/AD-DS-Simplified-Administration/ADDS_SMI_TR_AdprepDLLs.png)  
  
> [!IMPORTANT]  
> Windows Server 2012 用の 32 ビット Adprep32.exe ツールはありません。 フォレストとドメインを準備するには、ドメイン コントローラーとして実行される、メンバー サーバーとして実行される、またはワークグループ内で実行される、1 台以上の Windows Server 2008 x64、Windows Server 2008 R2、または Windows Server 2012 コンピューターが必要です。 Adprep.exe は Windows Server 2003 x64 上では実行されません。  
  
## <a name="prerequisite-checking"></a><a name="BKMK_PrereuisiteChecking"></a>前提条件の確認

Windows PowerShell の ADDSDeployment マネージ コードに組み込まれている前提条件チェック システムは、操作に基づいてさまざまなモードで動作します。 次の表に、各テストについて、それがいつ使用され、何がどのような方法で検証されるのかについて説明します。 検証が失敗し、エラー情報だけでは問題のトラブルシューティングを行えない場合に、この表が役立ちます。  
  
これらのテストのログは、 **DirectoryServices-Deployment** 操作イベント ログ チャネルのタスク カテゴリ **Core**に、常にイベント ID **103**で記録されます。  
  
### <a name="prerequisite-windows-powershell"></a>前提条件のための Windows PowerShell

ドメイン コントローラー展開のすべてのコマンドレットには、対応する Windows PowerShell の ADDSDeployment コマンドレットがあります。 これらのコマンドレットは、その関連するコマンドレットとほぼ同じ引数を持ちます。  

- Test-ADDSDomainControllerInstallation  
- Test-ADDSDomainControllerUninstallation  
- Test-ADDSDomainInstallation  
- Test-ADDSForestInstallation  
- Test-ADDSReadOnlyDomainControllerAccountCreation  

通常、これらのコマンドレットを実行する必要はありません。既定で、展開コマンドレットと一緒に自動的に実行されます。  

#### <a name="prerequisite-tests"></a><a name="BKMK_ADDSInstallPrerequisiteTests"></a>前提条件テスト

||||  
|-|-|-|  
|テスト名|プロトコル<p>使用される|説明と注意事項|  
|VerifyAdminTrusted<p>ForDelegationProvider|LDAP|既存のパートナー ドメイン コントローラーに対する "コンピューターとユーザー アカウントに委任時の信頼を付与" (SeEnableDelegationPrivilege) 特権がユーザーにあることを検証します。 構成された tokenGroups 属性へのアクセスが必要になります。<p>Windows Server 2003 ドメイン コントローラーに接続するときは使用されません。 昇格の前にこの特権を手動で確認する必要があります。|  
|VerifyADPrep<p>Prerequisites (フォレスト)|LDAP|rootDSE namingContexts 属性およびスキーマ名前付けコンテキストの fsmoRoleOwner 属性を使って、スキーマ マスターを検出して接続します。 AD DS のインストールにとってどの準備操作 (forestprep、domainprep、または rodcprep) が必要なのかを判断します。 スキーマ objectVersion が想定されていることと、それがさらに拡張を必要としているかどうかを検証します。|  
|VerifyADPrep<p>Prerequisites (ドメインおよび RODC)|LDAP|rootDSE namingContexts 属性およびインフラストラクチャ コンテナーの fsmoRoleOwner 属性を使って、インフラストラクチャ マスターを検出して接続します。 RODC のインストールの場合、このテストはドメイン名前付けマスターを検出し、それがオンラインであることを確認します。|  
|CheckGroup<p>[メンバーシップ]|LDAP、<p>SMB 経由の RPC (LSARPC)|操作に応じて、ユーザーが Domain Admins グループまたは Enterprise Admins グループのメンバーであることを検証します (ドメイン コントローラーの追加または降格の場合は DA、ドメインの追加または削除の場合は EA)。|  
|CheckForestPrep<p>GroupMembership|LDAP、<p>SMB 経由の RPC (LSARPC)|ユーザーが Schema Admins グループおよび Enterprise Admins グループのメンバーであることと、既存のドメイン コントローラーに対する "監査とセキュリティ ログの管理" (SeSecurityPrivilege) 特権を持っていることを検証します。|  
|CheckDomainPrep<p>GroupMembership|LDAP、<p>SMB 経由の RPC (LSARPC)|ユーザーが Domain Admins グループのメンバーであることと、既存のドメイン コントローラーに対する "監査とセキュリティ ログの管理" (SeSecurityPrivilege) 特権を持っていることを検証します。|  
|CheckRODCPrep<p>GroupMembership|LDAP、<p>SMB 経由の RPC (LSARPC)|ユーザーが Enterprise Admins グループのメンバーであることと、既存のドメイン コントローラーに対する "監査とセキュリティ ログの管理" (SeSecurityPrivilege) 特権を持っていることを検証します。|  
|VerifyInitSync<p>AfterReboot|LDAP|スキーマ マスターが rootDSE 属性 becomeSchemaMaster に対してダミー値を設定して再起動してから 1 回以上レプリケートしていることを検証します。|  
|VerifySFUHotFix<p>Applied|LDAP|既存のフォレスト スキーマに既知の問題、"OID が 1.2.840.113556.1.4.7000.187.102 の UID 属性に対する SFU2 拡張" が含まれていないことを検証します。<p>([https://support.microsoft.com/kb/821732](https://support.microsoft.com/kb/821732))|  
|VerifyExchange<p>SchemaFixed|LDAP、WMI、DCOM、RPC|既存のフォレストスキーマにまだ2000問題が含まれていないことを検証する: Exch、Exch-Ms-exch-labeleduri、Exch ([https://support.microsoft.com/kb/314649](https://support.microsoft.com/kb/314649)) を使用します。|  
|VerifyWin2KSchema<p>一貫性|LDAP|既存のフォレスト スキーマに一貫性のある (サード パーティによって間違って変更されていない) コアの属性とクラスがあることを検証します。|  
|DCPromo|RPC 経由の DRSR<p>LDAP、<p>DNS<p>SMB 経由の RPC (SAMR)|プロモーション コードに渡されるコマンド ライン構文を検証し、昇格をテストします。 フォレストまたはドメインを新規に作成する場合、既存のフォレストまたはドメインがないことを検証します。|  
|VerifyOutbound<p>ReplicationEnabled|LDAP、SMB 経由の DRSR、SMB 経由の RPC (LSARPC)|レプリケーション パートナーとして指定された既存のドメイン コントローラーで出力方向のレプリケーションが有効であることを検証します。そのために、NTDS 設定オブジェクトの NTDSDSA_OPT_DISABLE_OUTBOUND_REPL (0x00000004) のオプション属性を確認します。|  
|VerifyMachineAdmin<p>Password|RPC 経由の DRSR<p>LDAP、<p>DNS<p>SMB 経由の RPC (SAMR)|DSRM のセーフ モードのパスワード セットがドメインの複雑さの要件を満たしていることを検証します。|  
|VerifySafeModePassword|*該当なし*|ローカルの Administrator パスワード セットが、コンピューター セキュリティ ポリシーの複雑さの要件を満たしていることを検証します。|  
