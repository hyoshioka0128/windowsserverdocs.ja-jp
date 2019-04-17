---
ms.assetid: f74eec9a-2485-4ee0-a0d8-cce01250a294
title: "AD DS の簡略化された管理"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 6232e281c47f3b5b4627bc9d8ccf53269aafc390
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="ad-ds-simplified-administration"></a>AD DS の簡略化された管理

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックでは、新しい機能と Windows Server 2012 ドメイン コント ローラーの展開と管理、および以前のオペレーティング システムの DC 展開と、新しい Windows Server 2012 実装との違いの利点について説明します。  
  
Windows Server 2012 では、Active Directory ドメイン サービス簡略化された管理の次世代を紹介しは、最も革新ドメイン構想の見直し Windows 2000 Server 以来します。 AD DS の簡略化された管理受け取り Active Directory の 12 年から得られた教訓よりサポート可能なより柔軟なより直感的な管理エクスペリエンスの設計者および管理者します。 Windows Server 2008 R2 でリリースされたコンポーネントの機能を拡張すると、既存のテクノロジの新しいバージョンを作成するようになります。  
  
AD DS の簡略化された管理は、ドメインの展開の再イメージ化、です。  
  
-   AD DS の役割の展開は、新しいサーバー マネージャー アーキテクチャの一部になり、リモート インストールを可能  
  
-   AD DS の展開と構成のエンジンが、Windows PowerShell で新しい AD DS 構成ウィザードを使用する場合でも  
  
-   スキーマの拡張、フォレストの準備、およびドメインの準備のドメイン コント ローラーの昇格の一部では自動的に必要としない、スキーマ マスターなどの特殊なサーバー上の別のタスク  
  
-   昇格ようになりましたにはが、新しいドメイン コント ローラー、障害が発生したプロモーションの機会を削減するフォレストおよびドメインの準備を検証する前提条件のチェックが含まれます  
  
-   Windows PowerShell 用 active Directory モジュールには、レプリケーション トポロジの管理、ダイナミック アクセス制御、およびその他の操作用のコマンドレット  
  
-   同種のドメイン コント ローラー環境に必要な Windows Server 2012 フォレストのレベルでは新しい機能が実装されていませんし、ドメインの機能レベルは、頻繁の管理者の軽減、Kerberos の新機能のサブセットにのみ必要な機能  
  
-   仮想化ドメイン コント ローラー、自動化された展開とロールバック保護を含めるために追加完全にサポート  
  
仮想化ドメイン コント ローラーの詳細については、次を参照してください。 [Introduction to Active Directory ドメイン サービス (&) #40 です。AD DS & #41 です。仮想化 (&) #40 です。Level 100 & #41 です。](../../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md).  
  
さらに、たくさんの管理と保守に関する機能強化。  
  
-   Active Directory 管理センターには、グラフィカルな Active Directory のごみ箱、細かいパスワード ポリシーの管理、および Windows PowerShell 履歴ビューアーが含まれます。  
  
-   新しいサーバー マネージャーのパフォーマンスの監視、ベスト プラクティス分析、重要なサービス、およびイベント ログに AD DS 固有のインターフェイスには  
  
-   グループ管理サービス アカウントは、同じセキュリティ プリンシパルを使用して複数のコンピューターをサポートします。  
  
-   相対識別子 (RID) の発行と管理性の向上成熟した Active Directory ドメイン内の監視の機能強化  
  
最後に、AD DS は、他の新機能、Windows Server 2012 でなどからの利益を上げます。  
  
-   NIC チーミングおよびデータ センター ブリッジング  
  
-   DNS セキュリティ、および起動後に高速な AD 統合ゾーンの可用性  
  
-   HYPER-V の信頼性とスケーラビリティの向上  
  
-   BitLocker ネットワーク ロック解除します。  
  
-   その他の Windows PowerShell コンポーネント管理モジュール  
  
## <a name="technical-overview"></a>技術概要  
  
### <a name="adprep-integration"></a>ADPREP の統合  
Active Directory フォレストのスキーマ拡張とドメインの準備できるようになりましたが、ドメイン コント ローラー構成プロセスに統合します。 既存のフォレストに新しいドメイン コント ローラーを昇格する場合は、プロセスは、アップグレードの状態を検出し、スキーマ拡張とドメインの準備のフェーズが自動的に実行します。 最初の Windows Server 2012 ドメイン コント ローラーをインストールするユーザーは、Enterprise Admin 特権と Schema Admin であるか、有効な代替資格情報を提供する必要がありますもします。  
  
Adprep.exe は DVD の別のフォレストおよびドメインの準備に残ります。 Windows Server 2012 に含まれているツールのバージョンは x64 Windows Server 2008 および Windows Server 2008 R2 に下位互換性を保つです。 Adprep.exe は、リモートでの forestprep と domainprep、ADDSDeployment ベースのドメイン コント ローラー構成ツールと同じようにもサポートします。  
  
Adprep および以前のオペレーティング システムのフォレストの準備については、次を参照してください。 [Adprep の実行 (Windows Server 2008 R2)](https://technet.microsoft.com/library/dd464018(WS.10).aspx)します。  
  
### <a name="server-manager-ad-ds-integration"></a>サーバー マネージャー AD DS の統合  
![簡略化された管理](media/AD-DS-Simplified-Administration/ADDS_SMI_TR_Dashboard.png)  
  
サーバー マネージャーは、サーバーの管理タスクのハブとして機能します。 そのダッシュ ボード スタイルのパネルでは、インストールされている役割とリモート サーバー グループのビューを定期的に更新します。 サーバー マネージャーでは、コンソールへのアクセスを必要とせず、ローカルおよびリモートのサーバーの一元管理を提供します。  
  
Active Directory ドメイン サービスは; これらのハブの役割の 1 つドメイン コント ローラーまたは Windows 8 でのリモート サーバー管理ツールでサーバー マネージャーを実行して、フォレスト内のドメイン コント ローラーで最近の重要な問題を確認します。  
  
これらのビューは、次のとおりです。  
  
-   サーバーの可用性  
  
-   CPU とメモリ使用率が高くのパフォーマンス モニターの警告  
  
-   AD DS に固有の Windows サービスの状態  
  
-   ディレクトリ サービスに関連する警告およびエラーで最近エントリは、イベント ログ  
  
-   マイクロソフトの推奨の規則のセットに対するドメイン コント ローラーのベスト プラクティス分析  
  
### <a name="active-directory-administrative-center-recycle-bin"></a>Active Directory 管理センターのごみ箱  
![簡略化された管理](media/AD-DS-Simplified-Administration/ADDS_SMI_TR_ADAC.png)  
  
Windows Server 2008 R2 では、Active Directory のごみ箱、削除された Active Directory オブジェクトをバックアップから復元する、AD DS サービスを再開またはドメイン コント ローラーを再起動せず回復が導入されました。  
  
Windows Server 2012 では、Active Directory 管理センターで新しいグラフィカル インターフェイスを持つ既存の Windows PowerShell ベースの復元機能が向上します。 これにより、管理者は、ごみ箱を有効にして特定またはすべての Windows PowerShell コマンドレットを直接実行せず、フォレストのドメイン コンテキストで削除されたオブジェクトを復元できます。 Active Directory 管理センターと Active Directory のごみ箱 Windows PowerShell を使用については、下にあるため、前のスクリプトや手順は今も有効です。  
  
詳細については、Active Directory に関する[ごみ箱は、Active Directory のごみ箱ステップ バイ ステップ ガイド (Windows Server 2008 R2) の「](https://technet.microsoft.com/library/dd392261(WS.10).aspx)します。  
  
### <a name="active-directory-administrative-center-fine-grained-password-policy"></a>Active Directory 管理センターの詳細なパスワード ポリシー  
![簡略化された管理](media/AD-DS-Simplified-Administration/ADDS_SMI_TR_FGPP.png)  
  
Windows Server 2008 では、管理者が 1 ドメインあたり複数のパスワードとアカウント ロックアウトのポリシーを構成する細かいパスワード ポリシーが導入されました。 これにより、ドメイン ユーザーとグループに基づいてパスワード規則の詳細またはより制限の緩いを強制する柔軟なソリューションです。 ありませんでした管理用のインターフェイスと必要な管理者が Ldp.exe または Adsiedit.msc を使用して構成します。 Windows Server 2008 R2 では、FGPP をコマンド ライン インターフェイスを管理者に付与された Windows PowerShell 用 Active Directory モジュールが導入されました。  
  
Windows Server 2012 では、細かいパスワード ポリシーをグラフィカル インターフェイスが表示されます。 Active Directory 管理センターは、この新しいダイアログで、すべての管理者に簡素化された FGPP 管理をもたらすのホームです。  
  
細かいパスワード ポリシーについては、次を参照してください。 [AD DS の細かいパスワードとアカウント ロックアウト ポリシーのステップ バイ ステップ ガイド (Windows Server 2008 R2)](https://technet.microsoft.com/library/cc770842(WS.10).aspx)します。  
  
### <a name="active-directory-administrative-center-windows-powershell-history-viewer"></a>Active Directory 管理センターの Windows PowerShell 履歴ビューアー  
![簡略化された管理](media/AD-DS-Simplified-Administration/ADDS_SMI_TR_HistoryViewer.png)  
  
Windows Server 2008 R2 では、古い Active Directory ユーザーとコンピューター スナップインで作成された Windows 2000 での置き換えを Active Directory 管理センターが導入されました。 Active Directory 管理センターでは、Windows PowerShell を選び、新しい Active Directory モジュールにグラフィカル管理インターフェイスを作成します。  
  
100 コマンドレット経由で Active Directory モジュールが含まれますが、管理者の習得困難となります。 Windows PowerShell は、Windows の管理の戦略に大きく統合、ため Active Directory 管理センターがコマンドレットの実行をグラフィカル インターフェイスを表示することができます、ビューアーには含まれています。 検索、コピー、履歴を消去して利用できるシンプルなインターフェイスでメモを追加します。 目的は、管理者がグラフィカル インターフェイスを使用して作成し、オブジェクトを変更し、それらを詳細について Windows PowerShell のスクリプト サンプルを変更するには、履歴ビューアーで確認します。  
  
### <a name="ad-replication-windows-powershell"></a>AD レプリケーションの Windows PowerShell  
![簡略化された管理](media/AD-DS-Simplified-Administration/ADDS_PSNewADReplSite.png)  
  
Windows Server 2012 では、Active Directory レプリケーションの他のコマンドレットを Active Directory Windows PowerShell モジュールに追加します。 これらは、新規または既存のサイト、サブネット、接続、サイト リンク、およびブリッジの構成を許可します。 Active Directory のレプリケーション メタデータ、レプリケーションの状態、キュー、および最新のベクター情報を返すこともできます。 展開やその他の既存の AD DS コマンドレットと組み合わせる - レプリケーション コマンドレットの導入できるようになりますだけで Windows PowerShell を使用してフォレストを管理します。 これにより、管理者をプロビジョニングおよび Windows Server 2012 を管理せず、グラフィカル インターフェイスをオペレーティング システムの攻撃対象領域を削減したいとサービスの要件のための新しい機会が作成されます。 これは、機能は、サーバー シークレット Internet Protocol Router (SIPR) や企業 Dmz などの高度なセキュリティのネットワークを展開する場合に特に重要です。  
  
AD DS のサイト トポロジとレプリケーションの詳細については、次を参照してください。、 [Windows Server テクニカル リファレンス](https://technet.microsoft.com/library/cc739127(WS.10).aspx)します。  
  
### <a name="rid-management-and-issuance-improvements"></a>RID の管理と発行の機能強化  
Windows 2000 Active Directory には、セキュリティ トラスティのセキュリティ識別子 (Sid) を作成するために、ドメイン コント ローラーへの相対識別子の場合は、どの問題プールなどのユーザー、グループ、およびコンピューター、RID マスターが導入されました。  既定では、このグローバル RID 空間が有効になって<sup>30</sup> (つまり 1,073, 741,823) 個の Sid がドメインに作成します。 Sid は、プールに戻るかの再発行を依頼ことはできません。 時間の経過と共に、大規模なドメインが残り少なくなったら、Rid を開始または事故が不要な RID の枯渇し、最終的に枯渇する可能性があります。  
  
Windows Server 2012 のユーザーと AD DS と Microsoft カスタマー サポートで検出された、RID の発行と管理の問題の数が成長 1999 年に最初の Active Directory ドメインの作成後アドレス。 これらは次のとおりです。  
  
-   定期的な RID 消費の警告は、イベント ログに書き込まれます  
  
-   イベント ログと管理者には、RID プールが無効になります。  
  
-   RID ブロック サイズが適用されるようになりました RID ポリシーの最大上限  
  
-   RID の人為的シーリングができるようになりました適用され、グローバル RID 空間が少ない、管理者がアクションを実行する、グローバル空間が枯渇する前にログに記録  
  
-   グローバル RID 空間サイズの 2 倍の 1 ビット増加できる<sup>31</sup> (2,147, 483,648 Sid)  
  
Rid および RID マスターの詳細については、確認[セキュリティ識別子のしくみ](https://technet.microsoft.com/library/cc778824(WS.10).aspx)します。  
  
## <a name="new-ad-ds-deployment-architecture"></a>新しい AD DS 展開アーキテクチャ  
  
### <a name="ad-ds-role-deployment-and-management-architecture"></a>AD DS の役割の展開と管理アーキテクチャ  
サーバー マネージャーと ADDSDeployment Windows PowerShell は、展開または AD DS の役割を管理するときの機能に関して次のコア アセンブリに依存します。  
  
-   Microsoft.ADroles.Aspects.dll  
  
-   Microsoft.ADroles.Instrumentation.dll  
  
-   Microsoft.ADRoles.ServerManager.Common.dll  
  
-   Microsoft.ADRoles.UI.Common.dll  
  
-   Microsoft.DirectoryServices.Deployment.Types.dll  
  
-   Microsoft.DirectoryServices.ServerManager.dll  
  
-   Addsdeployment.psm1  
  
-   Addsdeployment.psd1  
  
どちらもは、Windows PowerShell とそのリモート呼び出しコマンドのリモートの役割のインストールと構成に依存します。  
  
![簡略化された管理](media/AD-DS-Simplified-Administration/ADDS_SMI_TR_DepDLLs.png)  
  
Windows Server 2012 には、LSASS から以前の昇格操作の数もリファクタリングしました。実行可能ファイルでの一部として。  
  
-   DS 役割サーバー サービス (DsRoleSvc)  
  
-   DSRoleSvc.dll (DsRoleSvc サービスによって読み込まれる)  
  
このサービスは、存在し、昇格、降格、または仮想ドメイン コント ローラーを複製するために実行中である必要があります。 AD DS の役割のインストールでは、このサービスを追加し、既定では、マニュアルの開始の種類を設定します。 このサービスを無効にしないでください。  
  
### <a name="adprep-and-prerequisite-checking-architecture"></a>ADPrep および前提条件チェックのアーキテクチャ  
Adprep は不要になった、スキーマ マスタで実行されている必要があります。 以降 x64 Windows Server 2008 を実行しているコンピューターからリモートで実行できます。  
  
> [!NOTE]  
> Adprep は LDAP で Schxx.ldf ファイルをインポートと、インポート中にスキーマ マスターへの接続が失われた場合に自動的に再接続しませんされません。 インポート プロセスの一環として、スキーマ マスターは特定のモードで設定し、再確立された接続は特定のモードではない場合は、接続が失われた後、LDAP が再接続自動再接続は無効になります。 その場合は、スキーマは正しく更新されません。  
  
前提条件のチェックは、特定の条件に該当することを確認します。 これらの条件は AD DS が正常にインストールに必要です。 必要ないくつかの条件がない場合は true は、インストールを続行する前に解決できます。 検出したこと、フォレストまたはドメイン準備ができていない、Adprep 展開コードが自動的に実行できるようにします。  
  
#### <a name="adprep-executables-dlls-ldfs-files"></a>ADPrep の実行可能ファイル、Dll、ldf、およびファイル  
  
-   ADprep.dll  
  
-   Ldifde.dll  
  
-   Csvde.dll  
  
-   Sch14.ldf ~ Sch56.ldf  
  
-   Schupgrade.cat  
  
-   *dcpromo.csv  
  
以前 ADprep.exe に格納されていた AD 準備コードは、adprep.dll 内にリファクターします。 これにより、ADPrep.exe と Windows PowerShell の ADDSDeployment モジュールの両方を同じタスクのライブラリを使用し、同じ機能を備えています。 Adprep.exe はインストール メディアに含まれていますが、自動化されたプロセスは直接呼び出すことは-管理者のみがそれを手動で実行します。 Windows Server 2008 x64 および以降のオペレーティング システムでのみ実行できます。 Ldifde.exe と csvde.exe も必要リファクターされたバージョンを準備プロセスによって読み込まれる Dll として。 スキーマの拡張機能は、署名確認される LDF ファイルと同様に、以前のオペレーティング システム バージョンでも使用します。  
  
![簡略化された管理](media/AD-DS-Simplified-Administration/ADDS_SMI_TR_AdprepDLLs.png)  
  
> [!IMPORTANT]  
> Windows Server 2012 用の 32 ビット Adprep32.exe ツールはありません。 少なくとも 1 つの x64 Windows Server 2008、Windows Server 2008 R2、またはフォレストとドメインを準備するドメイン コント ローラーとして、メンバ サーバー、またはワークグループを実行している、Windows Server 2012 コンピューターが必要です。 Adprep.exe は、Windows Server 2003 x64 では実行されません。  
  
#### <a name="BKMK_PrereuisiteChecking"></a>前提条件のチェック  
前提条件チェックの ADDSDeployment Windows PowerShell のマネージ コードに組み込まれているシステムは、操作に基づいてさまざまなモードで動作します。 次の表は、それを使用すると、各テスト方法の説明と新機能を検証について説明します。 これらのテーブルは、ここで、検証に失敗して、エラーは、問題をトラブルシューティングするための十分な問題がある場合に役立ちます。 可能性があります。  
  
これらのテストのログイン、 **Directoryservices-deployment**タスク カテゴリの下の操作イベント ログ チャネル**コア**、常にイベント ID **103**します。  
  
##### <a name="prerequisite-windows-powershell"></a>前提条件となる Windows PowerShell  
すべてのドメイン コント ローラーの展開コマンドレットの Windows PowerShell の ADDSDeployment コマンドレットがあります。 その関連するコマンドレットとほぼ同じ引数であります。  
  
-   テスト ADDSDomainControllerInstallation  
  
-   Test-addsdomaincontrolleruninstallation  
  
-   テスト ADDSDomainInstallation  
  
-   テスト ADDSForestInstallation  
  
-   テスト ADDSReadOnlyDomainControllerAccountCreation  
  
通常、これらのコマンドレットを実行する必要はありません。自動的に既定では、展開コマンドレットを実行します。  
  
##### <a name="BKMK_ADDSInstallPrerequisiteTests"></a>前提条件のテスト  
  
||||  
|-|-|-|  
|テスト名|プロトコル<br /><br />使用|説明と注意事項|  
|VerifyAdminTrusted<br /><br />ForDelegationProvider|LDAP|「有効にするコンピューターとユーザー アカウントに委任に対して信頼される」があることを検証、既存のパートナー ドメイン コント ローラー (SeEnableDelegationPrivilege) 特権します。 これには、構成された tokenGroups 属性へのアクセスが必要です。<br /><br />Windows Server 2003 ドメイン コント ローラーに接続するときは使用されません。 昇格の前にこの特権を手動で確認する必要があります。|  
|VerifyADPrep<br /><br />Prerequisites (フォレスト)|LDAP|RootDSE namingContexts 属性およびスキーマ名前付けコンテキストの fsmoRoleOwner 属性を使用してスキーマ マスターを検出します。 どの準備操作 (forestprep、domainprep、または rodcprep) が AD DS のインストールに必要なを決定します。 検証スキーマ objectVersion が想定し、かどうか、さらに拡張モジュールが必要です。|  
|VerifyADPrep<br /><br />Prerequisites (ドメインおよび RODC)|LDAP|検出して、インフラストラクチャ マスターが rootDSE namingContexts 属性およびインフラストラクチャ コンテナーの fsmoRoleOwner 属性を使用してを接続します。 RODC のインストールの場合は、このテストは、ドメイン名前付けマスターを検出し、オンラインであることを確認します。|  
|CheckGroup<br /><br />メンバーシップ|LDAP では、<br /><br />経由で SMB RPC (LSARPC)|検証、ユーザーが操作 (の追加または EA を追加または削除、ドメインのドメイン コント ローラーを降格の場合は DA) によっては、Domain Admins グループまたは Enterprise Admins グループのメンバー|  
|CheckForestPrep<br /><br />GroupMembership|LDAP では、<br /><br />経由で SMB RPC (LSARPC)|検証ユーザー Schema Admins のメンバーでは Enterprise Admins グループおよび管理の監査を持つとセキュリティ イベント ログ (SesScurityPrivilege) 特権を既存のドメイン コント ローラー|  
|CheckDomainPrep<br /><br />GroupMembership|LDAP では、<br /><br />経由で SMB RPC (LSARPC)|ユーザーを検証 Domain Admins グループのメンバーであるが、管理の監査とセキュリティ イベント ログ (SesScurityPrivilege) 特権を既存のドメイン コント ローラー|  
|CheckRODCPrep<br /><br />GroupMembership|LDAP では、<br /><br />経由で SMB RPC (LSARPC)|ユーザーを検証の Enterprise Admins グループのメンバーであるが、管理の監査とセキュリティ イベント ログ (SesScurityPrivilege) 特権を既存のドメイン コント ローラー|  
|VerifyInitSync<br /><br />AfterReboot|LDAP|スキーマ マスターがレプリケートされている少なくとも 1 回して再起動 rootDSE 属性 becomeSchemaMaster に対してダミー値を設定してからの検証します。|  
|VerifySFUHotFix<br /><br />適用|LDAP|検証の既存のフォレスト スキーマに OID が 1.2.840.113556.1.4.7000.187.102 の UID 属性に対する SFU2 拡張既知の問題にはが含まれていません。<br /><br />([https://support.microsoft.com/kb/821732](https://support.microsoft.com/kb/821732))|  
|VerifyExchange<br /><br />SchemaFixed|LDAP、WMI、DCOM、RPC|既存のフォレストを検証するスキーマは Exchange 2000 の拡張機能 ms 問題にはがまだ含まれて-こと-アシスタント-名前、ms-こと-LabeledURI、および ms こと自社識別子 ([https://support.microsoft.com/kb/314649](https://support.microsoft.com/kb/314649))|  
|VerifyWin2KSchema<br /><br />整合性|LDAP|検証の既存のフォレスト スキーマが一貫性のある (サード パーティによって間違っていない変更) コアの属性とクラスです。|  
|DCPromo|RPC 経由の DRSR<br /><br />LDAP では、<br /><br />DNS<br /><br />RPC over SMB (SAMR)|プロモーション コードやテストの昇格に渡されるコマンドラインの構文を検証します。 検証、フォレストまたはドメインが存在しない場合は、新規に作成します。|  
|VerifyOutbound<br /><br />ReplicationEnabled|LDAP、SMB 経由で SMB RPC (LSARPC) 経由の DRSR|オンにするオプションの属性を NTDS 設定オブジェクトの NTDSDSA_OPT_DISABLE_OUTBOUND_REPL (0x00000004) の出力方向のレプリケーションには、レプリケーション パートナーとして指定された既存のドメイン コント ローラーを検証します。|  
|VerifyMachineAdmin<br /><br />パスワード|RPC 経由の DRSR<br /><br />LDAP では、<br /><br />DNS<br /><br />RPC over SMB (SAMR)|DSRM がドメインの複雑さの条件を満たしている用に設定されてセーフ モードのパスワードを検証します。|  
|VerifySafeModePassword|*該当なし*|ローカル管理者パスワード セットを満たしているコンピューター セキュリティ ポリシー要件を確認します。|  
  


