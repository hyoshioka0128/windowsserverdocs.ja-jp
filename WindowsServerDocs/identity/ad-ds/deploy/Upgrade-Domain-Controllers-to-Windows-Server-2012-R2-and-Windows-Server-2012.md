---
ms.assetid: e4c31187-f15f-410b-bb79-8d63e2f2b421
title: "ドメイン コント ローラーを Windows Server 2012 R2 および Windows Server 2012 にアップグレードします。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: e317c5a939d417bac844c4080223d7b5e0eec149
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="upgrade-domain-controllers-to-windows-server-2012-r2-and-windows-server-2012"></a>ドメイン コント ローラーを Windows Server 2012 R2 および Windows Server 2012 にアップグレードします。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックでは、Windows Server 2012 R2 および Windows Server 2012 での Active Directory ドメイン サービスに関する背景情報を提供し、Windows Server 2008 または Windows Server 2008 R2 からドメイン コント ローラーをアップグレードするプロセスについて説明します。  
  
-   [ドメイン コント ローラーのアップグレード手順](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_UpgradeWorkflow)  
  
-   [Windows Server 2012 の新機能ですか。](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_WhatsNewEight)  
  
-   [Windows Server 2012 R2 で AD DS の新機能ですか。](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_NewWS2012R2)  
  
-   [Windows Server 2012 で AD DS の新機能ですか。](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_WhatsNewAD)  
  
-   [AD DS サーバー役割のインストールの変更](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_InstallationChanges)  
  
-   [推奨されなくなった機能および Windows Server 2012 で AD DS に関連する動作の変更](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_DeprecatedFeatures)  
  
-   [オペレーティング システムの要件](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_SysReqs)  
  
-   [サポートされる一括アップグレード パス](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_UpgradePaths)  
  
-   [機能レベルの機能と要件](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_FunctionalLevels)  
  
-   [その他のサーバーの役割と Windows オペレーティング システムと AD DS の相互運用](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_ServerRoles)  
  
-   [操作マスターの役割](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_OpsMasters)  
  
-   [Windows Server 2012 を実行するドメイン コント ローラーの仮想化](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_Virtual)  
  
-   [Windows Server 2012 サーバーの管理](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_Admin)  
  
-   [アプリケーションの互換性](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_AppCompat)  
  
-   [既知の問題](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_KnownIssues)  
  
## <a name="BKMK_UpgradeWorkflow"></a>ドメイン コント ローラーのアップグレード手順  
ドメインをアップグレードすることをお勧めは新しいバージョンの Windows Server を実行し、以前のドメイン コント ローラーに応じてを降格するドメイン コント ローラーに昇格することです。 そのメソッドは、既存のドメイン コント ローラーのオペレーティング システムをアップグレードすることをお勧めします。 この一覧は、新しいバージョンの Windows Server を実行するドメイン コント ローラーを昇格する前に実行する一般的な手順について説明します。  
  
1.  Verify the target server meets [system requirements](https://technet.microsoft.com/library/dn303418.aspx).  
  
2.  確認[アプリケーションの互換性](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_AppCompat)します。  
  
3.  セキュリティ設定を確認します。 For more information, see [Deprecated features and behavior changes related to AD DS in Windows Server 2012](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_DeprecatedFeatures) and [Secure default settings in Windows Server 2008 and Windows Server 2008 R2](https://technet.microsoft.com/library/upgrade-domain-controllers-to-windows-server-2008-r2(WS.10).aspx#BKMK_SecureDefault).  
  
4.  インストールを実行するコンピューターからターゲット サーバーへの接続を確認します。  
  
5.  必要な操作マスターの役割の可用性を確認します。  
  
    -   既存のドメインまたはフォレストでの Windows Server 2012 を実行する最初の DC をインストールするには、インストールを実行するコンピューターには、adprep/forestprep を実行するためにスキーマ マスターと adprep/domainprep を実行するためにインフラストラクチャ マスターへの接続が必要があります。  
  
    -   フォレスト スキーマが既に拡張ドメイン内の最初の DC をインストールするには、インフラストラクチャ マスターへの接続のみ必要。  
  
    -   既存のフォレストにドメインを削除またはをインストールするには、ドメイン名前付けマスターへの接続する必要があります。  
  
    -   任意のドメイン コント ローラーのインストールには、RID マスターへの接続も必要です。  
  
    -   既存のフォレスト内の最初の読み取り専用ドメイン コント ローラーをインストールする場合はの各アプリケーション ディレクトリ パーティション、ドメインでない名前付けコンテキストまたは NDNC とも呼ばれる、インフラストラクチャ マスターへの接続をする必要があります。  
  
6.  必ず、AD DS のインストールを実行するために必要な資格情報を指定してください。  
  
    |インストールの操作|資格情報の要件|  
    |-----------------------|---------------------------|  
    |新しいフォレストをインストールします。|ターゲット サーバーのローカル管理者アカウント|  
    |既存のフォレストに新しいドメインをインストールします。|Enterprise Admins|  
    |既存のドメインに追加の DC をインストールします。|Domain Admins|  
    |Adprep/forestprep を実行します。|Schema Admins、Enterprise Admins、Domain Admins|  
    |Adprep/domainprep を実行します。|Domain Admins|  
    |Adprep/domainprep/gpprep を実行します。|Domain Admins|  
    |Adprep/rodcprep を実行します。|Enterprise Admins|  
  
    AD DS をインストールするアクセス許可を委任することができます。 For more information, see [Installation Management Tasks](https://technet.microsoft.com/library/cc773327(WS.10).aspx).  
  
新しいと Windows PowerShell コマンドレットおよびサーバー マネージャーを使用して Windows Server 2012 のレプリカ ドメイン コント ローラーに昇格するステップ バイ ステップの手順については、次のリンクを参照してください。  
  
-   [Active Directory ドメイン サービス (レベル 100) のインストールします。](https://technet.microsoft.com/library/hh472162.aspx)  
  
-   [フォレストをインストールする新しい Windows Server 2012 Active Directory (レベル 200)](https://technet.microsoft.com/library/jj574166.aspx)  
  
-   [レプリカ Windows Server 2012 ドメイン コントローラーを既存のドメイン (レベル 200) のインストールします。](https://technet.microsoft.com/library/jj574134.aspx)  
  
-   [Windows Server 2012 の新しい Active Directory 子ドメインまたはツリー ドメイン (レベル 200) をインストールします。](https://technet.microsoft.com/library/jj574105.aspx)  
  
-   [Windows Server 2012 の Active Directory インストール Read-Only ドメイン コントローラー (RODC) (レベル 200)](https://technet.microsoft.com/library/jj574152.aspx)  
  
-   [Windows Server 2012 ドメイン コント ローラーのセットアップ (EN-US) のステップバイ ステップ ガイド](https://social.technet.microsoft.com/wiki/contents/articles/12370.step-by-step-guide-for-setting-up-windows-server-2012-domain-controller-en-us.aspx)  
  
## <a name="BKMK_WhatsNewEight"></a>Windows Server 2012 の新機能ですか。  
サーバーの役割別に新機能とテクノロジ エリアが次の表に一覧表示します。 For more whitepapers, video demonstrations, and presentations about other features in Windows Server 2012, see [Server and Cloud Platform](https://www.microsoft.com/server-cloud/default.aspx).  
  
||||  
|-|-|-|  
|[Active Directory 証明書サービス (AD CS)](https://technet.microsoft.com/library/hh831373.aspx)|[Active Directory Rights Management サービス (AD RMS)](https://technet.microsoft.com/library/hh831554.aspx)|[BitLocker ドライブ暗号化](https://technet.microsoft.com/library/hh831412.aspx)|  
|[BranchCache](https://technet.microsoft.com/library/jj127252.aspx)|[動的ホスト構成プロトコル (DHCP)](https://technet.microsoft.com/library/jj200226.aspx)|[ドメイン ネーム システム (DNS)](https://technet.microsoft.com/library/jj200224.aspx)|  
|[フェールオーバー クラスタ リング](https://technet.microsoft.com/library/hh831414.aspx)|[ファイル サーバー リソース マネージャー](https://technet.microsoft.com/library/hh831746.aspx)|[グループ ポリシー](https://technet.microsoft.com/library/jj574108.aspx)|  
|[Hyper-v の概要](https://technet.microsoft.com/library/hh831410.aspx)|[IP アドレス管理 (IPAM)](https://technet.microsoft.com/library/jj200214.aspx)|[Kerberos 認証](https://technet.microsoft.com/library/hh831747.aspx)|  
|[管理されたサービス アカウント](https://technet.microsoft.com/library/hh831451.aspx)|[ネットワー キング](https://technet.microsoft.com/library/jj200215.aspx)|[リモート デスクトップ サービス](https://technet.microsoft.com/library/hh831527.aspx)|  
|[セキュリティ監査](https://technet.microsoft.com/library/hh849638.aspx)|[サーバー マネージャー](https://blogs.technet.com/b/servermanager/archive/2012/06/27/server-manager-power-of-many-simplicity-of-one.aspx)|[スマート カード](https://technet.microsoft.com/library/hh849637.aspx)|  
|[TLS/SSL (Schannel SSP)](https://technet.microsoft.com/library/hh831771.aspx)|[Windows 展開サービス](https://technet.microsoft.com/library/hh974416.aspx)|[Windows PowerShell 3.0](https://technet.microsoft.com/library/hh857339)|  
  
### <a name="automatic-maintenance-and-changes-to-restart-behavior-after-updates-are-applied-by-windows-update"></a>更新プログラムが Windows Update によって適用された後の再起動の動作に自動のメンテナンスと変更  
前の Windows 8 のリリースでは、Windows Update は、更新プログラムを確認し、ダウンロードしてインストールを独自の内部スケジュールを管理します。 Windows Update エージェントが常に実行されていること、バック グラウンドでメモリやその他のシステム リソースを消費することが必要です。  
  
Windows 8 and Windows Server 2012 introduce a new feature called [Automatic Maintenance](https://msdn.microsoft.com/library/windows/desktop/hh848037(v=vs.85).aspx). 自動メンテナンスは、それ自身のスケジューリングの管理に使用される各と実行ロジックのさまざまな機能を統合します。 This consolidation allows for all these components to use far less system resources, work consistently, respect the new [Connected Standby](https://msdn.microsoft.com/library/windows/hardware/jj248729.aspx) state for new device types, and consume less battery on portable devices.  
  
Windows Update は、Windows 8 および Windows Server 2012 での自動メンテナンスの一部であるために、更新プログラムをインストールする日時を設定するための独自の内部スケジュールは不要になったに有効です。 To help ensure consistent and predictable restart behavior for all devices and computers in your enterprise, including those that run Windows 8 and Windows Server 2012, see Microsoft KB article [2885694](https://support.microsoft.com/kb/2885694) (or see October 2013 cumulative rollup [2883201](https://support.microsoft.com/kb/2883201)), then configure policy settings described in the WSUS blog post [Enabling a more predictable Windows Update experience for Windows 8 and Windows Server 2012 (KB 2885694)](http://blogs.technet.com/b/wsus/archive/2013/10/08/enabling-a-more-predictable-windows-update-experience-for-windows-8-and-windows-server-2012-kb-2885694.aspx).  
  

## <a name="BKMK_NewWS2012R2"></a>Windows Server 2012 R2 で AD DS の新機能ですか。  
次の表は、Windows Server 2012 R2 では、AD DS 関連の新機能が利用可能なより詳細な情報へのリンクをまとめたものです。 For a more detailed explanation of some features, including their requirements, see [What's New in Active Directory in Windows Server 2012 R2](https://technet.microsoft.com/library/dn268294.aspx).  
  
|機能|説明|  
|-----------|---------------|  
|[ワークプ レース ジョイン](https://technet.microsoft.com/library/dn280945.aspx)|インフォメーション ワーカーが自分個人のデバイスを会社のリソースとサービスにアクセスする社内参加をできます。|  
|[Web アプリケーション プロキシ](https://technet.microsoft.com/library/dn280942.aspx)|新しいリモート アクセス役割サービスを使用して web アプリケーションへのアクセスを提供します。|  
|[Active Directory フェデレーション サービス](https://technet.microsoft.com/library/hh831502.aspx)|AD FS があり、簡素化された展開をユーザーが個人のデバイスからリソースにアクセスし、IT 部門がアクセス制御の管理を有効にする機能を強化します。|  
|[SPN と UPN の一意性](https://technet.microsoft.com/library/dn535779.aspx)|Windows Server 2012 R2 を実行するドメイン コント ローラーが重複するサービス プリンシパル名 (Spn) の作成をブロックし、ユーザー プリンシパル名 (Upn) します。|  
|[Winlogon 自動再起動サインオン (ARSO)](https://technet.microsoft.com/library/dn535772.aspx)|有効にはロック画面アプリケーションを再起動して、Windows 8.1 デバイスで利用可能です。|  
|[TPM キーの構成証明](https://technet.microsoft.com/library/dn581921.aspx)|Ca が暗号によって証明書要求者の秘密キーでトラステッド プラットフォーム モジュール (TPM) によってが実際に保護されている発行された証明書の証明を有効にします。|  
|[資格情報の保護と管理](https://technet.microsoft.com/library/dn408190.aspx)|新しい資格情報の保護とドメイン認証制御を資格情報の盗用を減らすためにします。|  
|[ファイル レプリケーション サービス (FRS) の廃止](https://technet.microsoft.com/library/dn535775.aspx)|Windows Server 2003 ドメインの機能レベルは、機能レベルは FRS を使用して SYSVOL をレプリケートするためにも廃止されています。 Windows Server 2012 R2 を実行しているサーバーに新しいドメインを作成する場合は、ドメインの機能レベルする必要のある Windows Server 2008 以降。 Windows Server 2003 ドメイン機能レベルを持つ既存のドメインに Windows Server 2012 R2 を実行するドメイン コント ローラーを追加することができます。そのレベルの新しいドメインを作成することはできませんだけです。|  
|[新しいドメインとフォレストの機能レベル](../active-directory-functional-levels.md)|Windows Server 2012 R2 の新しい機能レベルがあります。 Windows Server 2012 R2 DFL で新機能を利用できます。|  
|[LDAP クエリ オプティマイザーの変更点](https://technet.microsoft.com/library/dn535775.aspx)|LDAP 検索効率および複雑なクエリの LDAP 検索時間においてパフォーマンスが向上します。|  
|[1644 イベントの改善](https://technet.microsoft.com/library/dn535775.aspx)|LDAP 検索結果の統計情報は、イベントのトラブルシューティングを支援する ID 1644 に追加されました。|  
|[Active Directory レプリケーション スループットの向上](https://technet.microsoft.com/library/dn535775.aspx)|AD レプリケーション スループット 40 mbps から約 600 Mbps に調整します。|  
  
## <a name="BKMK_WhatsNewAD"></a>Windows Server 2012 で AD DS の新機能ですか。  
次の表は、Windows Server 2012 では、AD DS 関連の新機能が利用可能なより詳細な情報へのリンクをまとめたものです。 For a more detailed explanation of some features, including their requirements, see [What's New in Active Directory Domain Services (AD DS)](https://technet.microsoft.com/library/hh831477.aspx).  
  
|機能|説明|  
|-----------|---------------|  
|Active Directory-Based Activation (AD BA) see [Volume Activation Overview](https://technet.microsoft.com/library/hh831612.aspx)|配布とボリューム ソフトウェア ライセンスの管理を構成するタスクを簡略化します。|  
|[Active Directory フェデレーション サービス (AD FS)](https://technet.microsoft.com/library/hh831502.aspx)|追加の役割のインストール サーバー マネージャーを使用した、信頼のセットアップ、自動的な信頼管理、SAML プロトコルのサポート、およびを簡略化します。|  
|Active Directory の失われたページのフラッシュ イベント|NTDS ISAM イベント 530 が jet エラー-1119 が失われたページのフラッシュ イベントを Active Directory データベースを検出するために記録されます。|  
|[Active Directory のごみ箱のユーザー インターフェイス](https://technet.microsoft.com/library/hh831702.aspx#ad_recycle_bin_mgmt)|Active Directory 管理センター (ADAC) は、最初に Windows Server 2008 R2 で導入されたごみ箱機能の GUI 管理を追加します。|  
|[Active Directory レプリケーションおよびトポロジの Windows PowerShell コマンドレット](https://technet.microsoft.com/library/hh831757.aspx)|作成と管理の Active Directory サイト、サイト リンク、接続オブジェクトをサポートしている Windows PowerShell の使用とします。|  
|[ダイナミック アクセス制御](https://technet.microsoft.com/library/hh831717.aspx)|従来のアクセス制御モデルを強化する新しい信頼性情報ベースの承認プラットフォーム。|  
|[詳細なパスワード ポリシーのユーザー インターフェイス](https://technet.microsoft.com/library/hh831702.aspx#fine_grained_pswd_policy_mgmt)|ADAC には、作成、編集と Windows Server 2008 で最初に追加された Pso の割り当てのための GUI サポートが追加されます。|  
|[グループ管理サービス アカウント (gMSA)](https://technet.microsoft.com/library/hh831782.aspx)|新しいセキュリティ プリンシパル型 gMSA と呼ばれます。 複数のホストで実行されているサービスは、同じ gMSA アカウントの下で実行できます。|  
|[DirectAccess オフライン ドメイン参加](https://technet.microsoft.com/library/jj574150.aspx)|DirectAccess の前提条件を含めることでオフライン ドメイン参加を拡張します。|  
|[仮想ドメイン コント ローラー (DC) の複製による迅速な展開](https://technet.microsoft.com/library/hh831734.aspx#virtualized_dc_cloning)|Windows PowerShell コマンドレットを使用して既存の仮想ドメイン コント ローラーを複製することによって、仮想化 Dc を迅速に展開できます。|  
|[RID プールの変更](https://technet.microsoft.com/library/jj574229.aspx)|新しい監視イベントとクォータ、グローバル RID プールの過剰な消費を防ぐために追加します。 必要に応じて、グローバル RID プールのサイズが 2 倍元のプールがなくなった場合します。|  
|セキュリティで保護されたタイム サービス|ネットワークからシークレットを削除し、MD5 ハッシュ機能を削除する、Windows 8 タイム クライアントでの認証に、サーバーを必要とするして W32tm のセキュリティを強化します。|  
|[仮想化 Dc に対する USN ロールバック保護](https://technet.microsoft.com/library/hh831734.aspx#safe_virt_dc)|不要になった仮想化 Dc のスナップショット バックアップを誤って復元、USN ロールバックが発生します。|  
|[Windows PowerShell 履歴ビューアー](https://technet.microsoft.com/library/hh831702.aspx#windows_powershell_history_viewer)|管理者が ADAC を使用して、実行される Windows PowerShell コマンドを表示できるようにします。|  
  
### <a name="BKMK_"></a>更新プログラムが Windows Update によって適用された後の再起動の動作に自動のメンテナンスと変更  
前の Windows 8 のリリースでは、Windows Update は、更新プログラムを確認し、ダウンロードしてインストールを独自の内部スケジュールを管理します。 Windows Update エージェントが常に実行されていること、バック グラウンドでメモリやその他のシステム リソースを消費することが必要です。  
  
Windows 8 and Windows Server 2012 introduce a new feature called [Automatic Maintenance](https://msdn.microsoft.com/library/windows/desktop/hh848037(v=vs.85).aspx). 自動メンテナンスは、それ自身のスケジューリングの管理に使用される各と実行ロジックのさまざまな機能を統合します。 This consolidation allows for all these components to use far less system resources, work consistently, respect the new [Connected Standby](https://msdn.microsoft.com/library/windows/hardware/jj248729.aspx) state for new device types, and consume less battery on portable devices.  
  
Windows Update は、Windows 8 および Windows Server 2012 での自動メンテナンスの一部であるために、更新プログラムをインストールする日時を設定するための独自の内部スケジュールは不要になったに有効です。 すべてのデバイスと Windows 8 および Windows Server 2012 を実行しているものを含む、社内のコンピューターに対して一貫性と予測可能性の再起動の動作を確保するには、次のグループ ポリシー設定を構成できます。  
  
-   **コンピューターの構成 |ポリシー |管理用テンプレート |Windows コンポーネント |Windows Update |自動更新を構成します。**  
  
-   **コンピューターの構成 |ポリシー |管理用テンプレート |Windows コンポーネント |Windows Update |ログオンしたユーザーに自動的に再起動しません。**  
  
-   **コンピューターの構成 |ポリシー |管理用テンプレート |Windows コンポーネント |メンテナンス スケジューラ |メンテナンス ランダム遅延**  
  
次の表は、必要な再起動の動作を提供するこれらの設定を構成する方法の例をいくつかを示します。  
  
|||  
|-|-|  
|**シナリオ**|**推奨される構成**|  
|**WSUS 管理**<br /><br />-毎週 1 回の更新プログラムをインストールします。<br />-午後 11 時で金曜日を再起動します。|マシンの自動インストールに、目的の時間まで自動再起動を防ぐための設定します。<br /><br />**ポリシー**: (有効)、自動更新を構成します。<br /><br />自動更新の構成: 4 - 自動ダウンロードしインストール日時を指定<br /><br />**ポリシー**: ログオンしたユーザー (無効) に自動的に再起動しません。<br /><br />**WSUS 期限**: 金曜日に午後 11 時の設定|  
|**WSUS 管理**<br /><br />-さまざまな時間/日付にわたってインストールをずらす|同時に更新するコンピューターのグループごとのターゲット グループを設定します。<br /><br />前のシナリオに対して上記の手順を使用します。<br /><br />別のターゲット グループに対して異なる期限を設定します。|  
|**非 WSUS 管理 - 期限のサポートなし**<br /><br />-異なる時刻でのインストールをずらす|**ポリシー**: (有効)、自動更新を構成します。<br /><br />自動更新の構成: 4 - 自動ダウンロードしインストール日時を指定<br /><br />**Registry key:** Enable the registry key discussed in Microsoft KB article [2835627](https://support.microsoft.com/kb/2835627)<br /><br />**ポリシー:**自動メンテナンス ランダム遅延 (有効)<br /><br />設定**定期メンテナンス ランダム遅延**6 時間のランダム遅延の次の動作を提供する PT6H します。<br /><br />構成されたメンテナンス時刻 plus ランダム遅延で更新がインストールされます。<br /><br />-の各コンピューターは行わちょうど 3 日後の再起動します。<br /><br />または、コンピューターのグループごとに異なるメンテナンス時刻を設定します。|  
  
Windows エンジニア リング チームがこれらの変更を実装する理由の詳細についてを参照してください[Windows Update での自動更新後に再起動を最小限に抑える](http://blogs.msdn.com/b/b8/archive/2011/11/14/minimizing-restarts-after-automatic-updating-in-windows-update.aspx)します。  
  
## <a name="BKMK_InstallationChanges"></a>AD DS サーバー役割のインストールの変更  
Windows Server 2008 R2 から Windows Server 2003、実行、x86 または X64 バージョンの Active Directory インストール ウィザード、Dcpromo.exe、Dcpromo.exe を実行する前に Adprep.exe コマンド ライン ツールが省略可能なバリエーションまたは無人インストール用メディアからインストールする必要があります。  
  
Windows PowerShell の ADDSDeployment モジュールを使用して Windows Server 2012 以降では、コマンド ライン インストールが実行されます。 サーバー マネージャーでは、まったく新しい AD DS 構成ウィザードを使用して、GUI ベースの昇格が実行されます。 インストール プロセスを簡略化するには、ADPREP が AD DS のインストールに統合されているし、必要に応じて自動的に実行します。 AD DS の Windows PowerShell ベースの構成ウィザードが、スキーマおよびインフラストラクチャ マスターの役割でのドメイン Dc の追加、関連するドメイン コント ローラー上で必要な adprep をリモートで実行で自動的に検出します。  
  
AD DS インストール ウィザードにおける前提条件の確認は、インストールが開始される前に、潜在的なエラーを特定します。 部分的に完全なアップグレードから出された問題を回避するためエラー条件を修正することができます。 ウィザードでは、グラフィカル インストール時に指定されたすべてのオプションを含む Windows PowerShell スクリプトをエクスポートします。  
  
まとめると、AD DS のインストールの変更は DC の役割のインストール プロセスを簡略化し、グローバル地域やドメインの間で複数のドメイン コント ローラーを展開する場合は特に、管理上のエラーが発生する可能性を低減します。  
More detailed information on GUI and Windows PowerShell-based installations, including command line syntax and step-by-step wizard instructions, see [Install Active Directory Domain Services](https://technet.microsoft.com/library/hh472162.aspx). 既存のフォレスト内の Windows Server 2012 Dc のインストールの独立した Active Directory フォレストのスキーマ変更の導入を管理する管理者は、Adprep.exe コマンドを管理者特権のコマンド プロンプトで実行もできます。  
  
## <a name="BKMK_DeprecatedFeatures"></a>推奨されなくなった機能および Windows Server 2012 で AD DS に関連する動作の変更  
AD DS に関連するいくつかの変更があります。  
  
-   **Adprep32.exe の廃止**  
  
    Adprep.exe のバージョンを 1 つだけが存在し、Windows Server 2008 を実行する 64 ビット サーバーに、必要に応じて実行またはそれ以降であることができます。 リモートで実行することができ、操作マスターの役割がホストされている 32 ビット オペレーティング システムまたは Windows Server 2003 を対象とする場合は、リモートで実行する必要があります。  
  
-   **Dcpromo.exe の廃止**  
  
    Windows Server 2012 でのみ実行できます応答ファイルまたはコマンド ライン パラメータを新しい Windows PowerShell インストール オプションの既存の自動化を移行する期間を設けるためには、Dcpromo は廃止されています。  
  
-   **ユーザー アカウントに対する LMHash の無効化にします。**  
  
    Windows Server 2008、Windows Server 2008 R2 および Windows Server 2012 でのテンプレートは、Windows 2000 および Windows Server 2003 ドメイン コント ローラーのセキュリティ テンプレートで無効になっている NoLMHash ポリシーを有効にするセキュリティの既定値をセキュリティで保護します。 Disable the NoLMHash policy for LMHash-dependent clients as required, using the steps in KB article [946405](https://support.microsoft.com/kb/946405).  
  
Windows Server 2008 以降では、ドメイン コント ローラーもがある Windows Server 2003 または Windows 2000 を実行するドメイン コント ローラーと比べ、次の既定のセキュリティ設定します。  
  
|||||  
|-|-|-|-|  
|暗号化の種類またはポリシー|Windows Server 2008 の既定値|Windows Server 2012 および Windows Server 2008 R2 の既定|コメント|  
|AllowNT4Crypto|無効になっています。|無効になっています。|サード パーティ サーバー メッセージ ブロック (SMB) クライアントは、ドメイン コント ローラーのセキュリティで保護された既定の設定と互換性のあることがあります。 すべてのケースでの相互運用性、セキュリティという代償がのみを許可するようにこれらの設定を緩和できます。 For more information, see [article 942564](https://go.microsoft.com/fwlink/?LinkId=164558) in the Microsoft Knowledge Base (https://go.microsoft.com/fwlink/?LinkId=164558).|  
|DES|有効になっています。|無効になっています。|[Article 977321](https://go.microsoft.com/fwlink/?LinkId=177717) in the Microsoft Knowledge Base (https://go.microsoft.com/fwlink/?LinkId=177717)|  
|統合認証のための CBT/拡張保護|該当なし|有効になっています。|See [Microsoft Security Advisory (937811)](https://go.microsoft.com/fwlink/?LinkId=164559) (https://go.microsoft.com/fwlink/?LinkId=164559) and [article 976918](https://go.microsoft.com/fwlink/?LinkId=178251) in the Microsoft Knowledge Base (https://go.microsoft.com/fwlink/?LinkId=178251).<br /><br />Review and install the hotfix in [article 977073](https://go.microsoft.com/fwlink/?LinkId=186394) (https://go.microsoft.com/fwlink/?LinkId=186394) in the Microsoft Knowledge Base as required.|  
|LMv2|有効になっています。|無効になっています。|[Article 976918](https://go.microsoft.com/fwlink/?LinkId=178251) in the Microsoft Knowledge Base (https://go.microsoft.com/fwlink/?LinkId=178251)|  
  
## <a name="BKMK_SysReqs"></a>オペレーティング システムの要件  
Windows Server 2012 の最小システム要件は次の表に一覧表示されます。 For more information about system requirements and pre-installation information, see [Installing Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx). 新しい Active Directory フォレストをインストールするための追加のシステム要件はありませんが、ドメイン コント ローラー、LDAP クライアント要求、および Active Directory 対応アプリケーションのパフォーマンスを向上するために Active Directory データベースの内容をキャッシュに十分なメモリを追加する必要があります。 既存のドメイン コント ローラーをアップグレードまたは新しいドメイン コント ローラーを既存のフォレストに追加する場合は、サーバーがディスク領域の要件を満たしていることを確認するには、次のセクションを確認します。  
  
|||  
|-|-|  
|プロセッサ|1.4 Ghz 64 ビット プロセッサ|  
|RAM|512 MB|  
|空きディスク領域の要件|32 GB|  
|画面の解像度|800 x 600 以上|  
|その他|DVD ドライブ、キーボード、インターネットへのアクセス|  
  
### <a name="BKMK_DiskSpaceDCWin8"></a>ドメイン コント ローラーをアップグレードするためのディスク領域の要件  
このセクションでは、Windows Server 2008 または Windows Server 2008 R2 からドメイン コント ローラーをアップグレードするのみのディスク領域の要件について説明します。 For more information about disk space requirements for upgrading domain controllers to earlier versions of Windows Server, see [Disk space requirements for upgrading to Windows Server 2008](https://technet.microsoft.com/library/cc754463(WS.10).aspx#BKMK_2008) or [Disk space requirements for upgrading to Windows Server 2008 R2](https://technet.microsoft.com/library/cc754463(WS.10).aspx#BKMK_2008R2).  
  
カスタムおよびアプリケーションに基づくスキーマの拡張機能、アプリケーション、管理者によって開始されるインデックス、およびオブジェクトと属性が、ドメイン コント ローラー (通常は 5 ~ 8 年) の展開寿命ディレクトリに追加されることの領域に対応するために Active Directory データベースとログ ファイルをホストしているディスクのサイズを変更します。 展開時にサイズ変更権限は、通常、適切な投資コストの増加展開後にディスク記憶域を展開するために必要と比較してです。 For more information, see [Capacity Planning for Active Directory Domain Services](https://social.technet.microsoft.com/wiki/contents/articles/14355.capacity-planning-for-active-directory-domain-services.aspx).  
  
アップグレードを計画しているドメイン コント ローラー上 (NTDS データベースを Active Directory をホストするドライブのことを確認します。DIT)、NTDS の 20% 以上に相当する空きディスク領域があります。DIT ファイル、オペレーティング システムのアップグレードを開始する前にします。 ボリュームに十分な空きディスク領域がある場合、アップグレードが失敗して、アップグレード互換性レポートには、十分な空きディスク領域を示すエラーが返されます。  
  
この場合、追加の領域を再キャプチャする Active Directory データベースのオフライン最適化を実行してくださいし、アップグレードを再試行できます。 For more information, see [Compact the Directory Database File (Offline Defragmentation)](https://technet.microsoft.com/library/cc794920(v=WS.10).aspx).  
  
### <a name="available-skus"></a>利用可能な Sku  
Windows Server の 4 エディションがあります: Foundation、Essentials、Standard および Datacenter します。   
AD DS の役割をサポートする 2 つのエディションは、Standard および Datacenter です。  
  
以前のリリースでは、Windows Server のエディションがごとにサポートされるサーバーの役割、プロセッサ数、および大容量メモリのサポート異なっていました。 Standard エディション、2 つの仮想インスタンスが許可されている Windows Server の Standard および Datacenter エディションがサポートしてすべての機能と基になるハードウェアが、仮想化権限の異なるし、Datacenter edition の無制限の仮想インスタンスが許可されます。  
  
### <a name="windows-client-and-windows-server-operating-systems-that-are-supported-to-join-windows-server-domains"></a>Windows クライアントおよび Windows Server ドメインへの参加にサポートされている Windows Server オペレーティング システム  
次の Windows クライアントおよび Windows Server オペレーティング システムは、Windows Server 2012 を実行するドメイン コント ローラーでドメイン メンバー コンピューターとしてサポートされている、またはそれ以降には。  
  
-   クライアント オペレーティング システム: Windows 8.1、Windows 8、Windows 7、Windows Vista 
  
    Windows 8.1 または Windows 8 を実行しているコンピューターは、その実行の以前のバージョンの Windows Server、Windows Server 2003 を含む、またはそれ以降のドメイン コント ローラーがあるドメインに参加することもできます。 ここでただし、Windows 8 の一部の機能追加の構成をする必要があります。 または利用できない可能性があります。 For more information about those features and other recommendations for managing Windows 8 clients in downlevel domains, see [Running Windows 8 member computers in Windows Server 2003 domains](https://social.technet.microsoft.com/wiki/contents/articles/17361.running-windows-8-member-computers-in-windows-server-2003-domains.aspx).  
  
-   サーバーのオペレーティング システム: Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008、Windows Server 2003 R2、Windows Server 2003  
  
## <a name="BKMK_UpgradePaths"></a>サポートされる一括アップグレード パス  
64 ビット バージョンの Windows Server 2008 または Windows Server 2008 R2 を実行するドメイン コント ローラーは、Windows Server 2012 にアップグレードすることができます。 Windows Server 2003 または 32 ビット バージョンの Windows Server 2008 を実行するドメイン コント ローラーをアップグレードすることはできません。 それらを置換するには、ドメインで、それ以降のバージョンの Windows Server を実行しているドメイン コント ローラーをインストールして、し、ドメイン コント ローラーを Windows Server 2003 を削除します。  
  
|これらのエディションを実行している場合|これらのエディションにアップグレードすることができます。|  
|-------------------------------------|-------------------------------------|  
|Windows Server 2008 Standard SP2<br /><br />OR<br /><br />Windows Server 2008 Enterprise SP2|Windows Server 2012 Standard<br /><br />OR<br /><br />Windows Server 2012 Datacenter|  
|Windows Server 2008 Datacenter SP2|Windows Server 2012 Datacenter|  
|Windows Web Server 2008|Windows Server 2012 Standard|  
|Windows Server 2008 R2 Standard SP1<br /><br />OR<br /><br />Windows Server 2008 R2 Enterprise SP1|Windows Server 2012 Standard<br /><br />OR<br /><br />Windows Server 2012 Datacenter|  
|Windows Server 2008 R2 Datacenter SP1|Windows Server 2012 Datacenter|  
|Windows Web Server 2008 R2|Windows Server 2012 Standard|  
  
For more information about supported upgrade paths, see [Evaluation Versions and Upgrade Options for Windows Server 2012](https://go.microsoft.com/fwlink/?LinkId=260917). Windows Server 2012 の評価版を製品版に直接実行するドメイン コント ローラーを変換することはできないことに注意してください。 代わりに、製品版を実行しているサーバーに追加のドメイン コント ローラーをインストールし、評価版で実行されているドメイン コント ローラーから AD DS を削除します。  
  
既知の問題により、Windows Server 2012 の Server Core インストールに Windows Server 2008 R2 の Server Core インストールを実行するドメイン コント ローラーをアップグレードすることはできません。 アップグレードは、アップグレード プロセスの終盤でブラック スクリーンにハングします。 以前のオペレーティング システム バージョンにロールバックするには、boot.ini ファイルでオプションを公開するこのような Dc を再起動します。 追加のリブート自動以前のオペレーティング システム バージョンにロールバックします。 解決策があるまでインプレースで Windows Server 2008 R2 の Server Core インストールを実行している既存のドメイン コント ローラーをアップグレードするのではなく、Windows Server 2012 の Server Core インストールを実行している、新しいドメイン コント ローラーをインストールすることをお勧めします。 For more information, see KB article [2734222](https://support.microsoft.com/kb/2734222).  
  
## <a name="BKMK_FunctionalLevels"></a>機能レベルの機能と要件  
 Windows Server 2012 では、Windows Server 2003 フォレストの機能レベルが必要です。 つまり、既存の Active Directory フォレストに Windows Server 2012 を実行するドメイン コント ローラーを追加する前に、フォレストの機能レベルが Windows Server 2003 以降である必要があります。 つまり、Windows Server 2008 R2、Windows Server 2008、または Windows Server 2003 を実行するドメイン コント ローラーが同じフォレストで動作できますが、Windows 2000 Server を実行しているドメイン コント ローラーがないは、サポートされており、Windows Server 2012 を実行しているドメイン コント ローラーのインストールがブロックされます。 Windows Server 2003 を実行するドメイン コント ローラーがフォレストに含まれている場合か、後で、フォレストの機能が、レベルが Windows 2000、インストールがブロックされてもします。  
  
Windows 2000 ドメイン コント ローラーは、Windows Server 2012 ドメイン コント ローラーをフォレストに追加する前に削除する必要があります。 この場合は、次のワークフローを検討してください。  
  
1.  またはを実行する Windows Server 2003 以降のドメイン コント ローラーをインストールします。 Windows Server の評価版では、これらのドメイン コント ローラーを展開できます。 This step also requires [running adprep.exe](https://technet.microsoft.com/library/dd464018(WS.10).aspx) for that operating system release as a prerequisite.  
  
2.  Windows 2000 ドメイン コント ローラーを削除します。 具体的には、正常に降格か、ドメインと使用されている Active Directory ユーザーとすべての削除されたドメイン コント ローラーのドメイン コント ローラー アカウントを削除するコンピューターから Windows Server 2000 ドメイン コント ローラーを強制的に削除します。  
  
3.  フォレストの機能レベルを Windows Server 2003 以上を生成します。  
  
4.  Windows Server 2012 を実行するドメイン コント ローラーをインストールします。  
  
5.  以前のバージョンの Windows Server を実行するドメイン コント ローラーを削除します。  
  
1 つの新しい機能を有効に、新しい Windows Server 2012 ドメインの機能レベル: **KDC で信頼性情報、複合認証、および Kerberos 防御をサポート**KDC 管理用テンプレート ポリシーが 2 つの設定 (**常に信頼性情報を提供**と**防御されていない認証要求を失敗**) Windows Server 2012 ドメインの機能レベルを必要とします。  
  
Windows Server 2012 フォレストの機能レベルが任意の新機能を提供していないが、フォレスト内に作成の任意の新しいドメインを Windows Server 2012 のドメイン機能レベルで自動的に動作するようになります。 Windows Server 2012 ドメインの機能レベルでは、信頼性情報、複合認証、および Kerberos 防御 KDC のサポートを超えるその他の新しい機能は提供されません。 ドメイン内の任意のドメイン コント ローラーが Windows Server 2012 が実行されているようになります。 別の機能レベルで使用できるその他の機能の詳細については、次を参照してください。[について Active Directory ドメイン サービス (AD DS) の機能レベル](../active-directory-functional-levels.md)します。  
  
ロールバックまたは次の例外を除き、フォレストの機能レベルを下げることはできません、フォレストの機能レベルを特定の値を設定した後: Windows Server 2012 へのフォレストの機能レベルを上げると、Windows Server 2008 R2 に下げることができます。 Active Directory のごみ箱が有効になっていない場合は、フォレストの機能レベルを Windows Server 2008 R2 または Windows Server 2008、Windows Server 2012、または Windows Server 2008 R2 から Windows Server 2008 にバックアップも下げることができます。 フォレストの機能レベルが Windows Server 2008 R2 に設定されている場合、できませんに降格する、たとえば、Windows Server 2003 します。  
  
ロールバックまたは次の例外を除き、ドメインの機能レベルを下げるドメインの機能レベルを特定の値を設定した後ことはできません。 を Windows Server 2008 R2 または Windows Server 2012 では、ドメインの機能レベルを上げると、フォレストの機能レベルが Windows Server 2008 またはそれ以下の場合は、ドメインの機能レベルをロールバックのオプションが Windows Server 2008 または Windows Server 2008 R2 にバックアップします。 Windows Server 2008 R2 または Windows Server 2008、Windows Server 2012 からのみ、または Windows Server 2008、Windows Server 2008 R2 からドメインの機能レベルを下げることができます。 ドメインの機能レベルが Windows Server 2008 R2 に設定されている場合、できませんに降格する、たとえば、Windows Server 2003 します。  
  
低い機能レベルで使用可能な機能の詳細については、次を参照してください。[について Active Directory ドメイン サービス (AD DS) の機能レベル](../active-directory-functional-levels.md)します。  
  
機能レベルは、Windows Server 2012 を実行するドメイン コント ローラーは、以前のバージョンの Windows Server を実行しているドメイン コント ローラーでのみ利用できる追加の機能を提供します。 たとえば、ドメイン コント ローラーを以前のバージョンの Windows Server を実行することはできませんは、Windows Server 2012 を実行するドメイン コント ローラーを仮想ドメイン コント ローラーの複製を使用できます。 仮想ドメイン コント ローラーの複製および Windows Server 2012 で仮想ドメイン コント ローラーの保護には、機能レベルの要件がありません。  
  
> [!NOTE]  
> Microsoft Exchange Server 2013 には、Windows server 2003 以降のフォレストの機能レベルが必要です。  
  
## <a name="BKMK_ServerRoles"></a>その他のサーバーの役割と Windows オペレーティング システムと AD DS の相互運用  
AD DS は、次の Windows オペレーティング システムでサポートされていません。  
  
-   Windows MultiPoint Server  
  
-   Windows Server 2012 Essentials  
  
次のサーバーの役割または役割サービスを実行しているサーバーで AD DS をインストールすることはできません。  
  
-   HYPER-V Server  
  
-   リモート デスクトップ接続ブローカー  
  
## <a name="BKMK_OpsMasters"></a>操作マスターの役割  
Windows Server 2012 の新機能では、操作マスターの役割に影響します。  
  
-   PDC エミュレーターでは、仮想ドメイン コント ローラーの複製をサポートするために Windows Server 2012 が実行されている必要があります。 Dc の複製について追加の前提条件があります。 For more information, see [Active Directory Domain Services (AD DS) Virtualization](https://technet.microsoft.com/library/hh831734.aspx).  
  
-   PDC エミュレーターは、Windows Server 2012 を実行すると、新しいセキュリティ プリンシパルが作成されます。  
  
-   RID マスターには新しい RID 発行および監視機能します。 イベント ロギングの向上、適切な制限を強化し、1 ビットのプール割り当てをする、緊急時に、全体的な RID を増やすこと。 詳細については、次を参照してください。 [RID 発行の管理](../../ad-ds/manage/Managing-RID-Issuance.md)します。  
  
> [!NOTE]  
> 操作マスターの役割は、AD DS のインストールで他の変更は Windows Server 2012 を実行しているすべてのドメイン コント ローラーでは既定で DNS サーバーの役割とグローバル カタログがインストールされていること。  
  
## <a name="BKMK_Virtual"></a>ドメイン コント ローラーの仮想化  
Windows Server 2012 以降の AD DS の機能強化には、ドメイン コント ローラーの安全な仮想化とドメイン コント ローラーの複製機能が有効にします。 新しいドメインと他の利点の追加のドメイン コント ローラーの迅速な展開をさらにドメイン コント ローラーを複製できます。 詳細については、次を参照してください。 [Introduction to Active Directory ドメイン サービス (&) #40 です。AD DS & #41 です。仮想化 (&) #40 です。Level 100 & #41 です。](../../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md).  
  
## <a name="BKMK_Admin"></a>Windows Server 2012 サーバーの管理  
Use the [Remote Server Administration Tools for Windows 8](https://www.microsoft.com/download/details.aspx?id=28972) to manage domain controllers and other servers that run  Windows Server 2012 . Windows 8 を実行しているコンピューターでは、Windows Server 2012 リモート サーバー管理ツールを実行できます。  
  
## <a name="BKMK_AppCompat"></a>アプリケーションの互換性  
次の表では、一般的な Active Directory 統合された Microsoft アプリケーションについて説明します。 テーブルでは、どのようなバージョンに、アプリケーションをインストールできる Windows Server および Windows Server 2012 Dc の導入がアプリケーションの互換性に影響するかどうかについて説明します。  
  
|製品|注意事項|  
|-----------|---------|  
|[Microsoft Configuration Manager 2007](http://blogs.technet.com/b/configmgrteam/archive/2012/09/10/support-questions-about-windows-8-and-windows-server-2012.aspx)|Configuration Manager 2007 SP2 (Configuration Manager 2007 R2 および Configuration Manager 2007 R3 が含まれています):<br /><br />Windows 8 Pro<br />Windows 8 Enterprise<br />Windows Server 2012 Standard<br />-Windows Server 2012 Datacenter**注:**が、これらは、クライアントとしてフル サポートされますが、Configuration Manager 2007 のオペレーティング システム展開機能を使用してこれらのオペレーティング システムを展開するためのサポートを追加する予定はありません。 また、サイト サーバーまたはサイト システムはサポートされません、SKU の Windows Server 2012 でします。|  
|[Microsoft SharePoint 2007](https://support.microsoft.com/kb/2728964)|Microsoft Office SharePoint Server 2007 は、Windows Server 2012 へのインストールはサポートされていません。|  
|[Microsoft SharePoint 2010](https://support.microsoft.com/kb/2724471)|インストールして操作する SharePoint 2010 Service Pack 2 が必要 <br />SharePoint 2010 を Windows Server 2012 サーバー<br /><br />インストールして、SharePoint 2010 Foundation を Windows Server 2012 のサーバーを操作する SharePoint 2010 Foundation Service Pack 2 が必要<br /><br />Windows Server 2012 で SharePoint Server 2010 (service pack) なしのインストール プロセスが失敗します。<br /><br />SharePoint Server 2010 の前提条件のインストーラー (PrerequisiteInstaller.exe) が失敗し、エラー「このプログラムには互換性の問題です」 "SharePoint をインストールできる場合ことを確認する & #124; は、「ヘルプを必要とせず、プログラムを実行する」] をクリックするとエラーが表示されます。Windows Server 2012。 (service pack なし)、SharePoint Server 2010 をインストールすることはできません"|  
|[Microsoft SharePoint 2013](https://technet.microsoft.com/library/cc262485(v=office.15).aspx)|ファームのデータベース サーバーの最小要件<br /><br />Windows Server 2008 R2 Service Pack 1 (SP1) の Standard、Enterprise、またはデータ センターまたは Windows Server 2012 Standard または Datacenter の 64 ビット エディションの 64 ビット版<br /><br />組み込みデータベースを持つ単一のサーバーの最小要件:<br /><br />Windows Server 2008 R2 Service Pack 1 (SP1) の Standard、Enterprise、またはデータ センターまたは Windows Server 2012 Standard または Datacenter の 64 ビット エディションの 64 ビット版<br /><br />フロント エンド web サーバーと、ファーム内のアプリケーション サーバーの最小要件:<br /><br />Windows Server 2008 R2 Service Pack 1 (SP1) の Standard、Enterprise、またはデータ センターまたは Windows Server 2012 Standard または Datacenter の 64 ビット エディションの 64 ビット エディションです。|  
|[Microsoft System Center Configuration Manager 2012](http://blogs.technet.com/b/configmgrteam/archive/2012/09/10/support-questions-about-windows-8-and-windows-server-2012.aspx)|System Center 2012 Configuration Manager Service Pack 1:<br /><br />Microsoft では、Service Pack 1 のリリースでは、クライアント サポート マトリックスに次のオペレーティング システムを追加します。<br /><br />Windows 8 Pro<br />Windows 8 Enterprise<br />Windows Server 2012 Standard<br />Windows Server 2012 Datacenter<br /><br />-サイト サーバー、SMS プロバイダー、および管理ポイントを含む、すべてのサイト サーバーの役割は、次のオペレーティング システム エディションのサーバーを展開できます。<br /><br />Windows Server 2012 Standard<br />Windows Server 2012 Datacenter|  
|[Microsoft Lync Server 2013](https://technet.microsoft.com/library/gg412883.aspx)|Lync Server 2013 では、Windows Server 2008 R2 または Windows Server 2012 が必要です。 Server Core インストールで実行することはできません。 It can be run on [virtual servers](https://technet.microsoft.com/library/gg399035.aspx).|  
|[Lync Server 2010](https://support.microsoft.com/kb/2777359)|Lync Server 2010 can be installed on a new (not upgraded) installation Windows Server 2012 if [October 2012 cumulative updates for Lync Server](https://support.microsoft.com/?kbid=2493736) are installed. Lync Server 2010 の既存のインストールの Windows Server 2012 へのオペレーティング システムのアップグレードはサポートされていません。 Microsoft Lync Server 2010 グループ チャット サーバーも Windows Server 2012 でサポートされていません。|  
|[System Center 2012 Endpoint Protection](http://blogs.technet.com/b/configmgrteam/archive/2012/09/10/support-questions-about-windows-8-and-windows-server-2012.aspx)|System Center 2012 Endpoint Protection Service Pack 1 では、次のオペレーティング システムが含まれるクライアント サポート マトリックスを更新します。<br /><br />Windows 8 Pro<br />Windows 8 Enterprise<br />Windows Server 2012 Standard<br />Windows Server 2012 Datacenter|  
|[System Center 2012 Forefront Endpoint Protection](http://blogs.technet.com/b/configmgrteam/archive/2012/09/10/support-questions-about-windows-8-and-windows-server-2012.aspx)|FEP 2010 更新プログラム ロールアップ 1 では、クライアント サポート マトリックスが更新を次のオペレーティング システムを含めます。<br /><br />Windows 8 Pro<br />Windows 8 Enterprise<br />Windows Server 2012 Standard<br />Windows Server 2012 Datacenter|  
|Forefront Threat Management Gateway (TMG)|Windows Server 2008 および Windows Server 2008 R2 でのみ実行 TMG はサポートされています。 For more information, see [System requirements for Forefront TMG](https://technet.microsoft.com/library/dd896981.aspx).|  
|Windows Server Update Services|WSUS のこのリリースでは、クライアントとしてに、Windows 8 ベースのコンピューターまたは Windows Server 2012 ベースのコンピュータをサポートしています。|  
|Windows Server Update Services 3.0|Update KB article [2734608](https://support.microsoft.com/kb/2734608) lets servers that are running Windows Server Update Services (WSUS) 3.0 SP2 provide updates to computers that are running Windows 8 or Windows Server 2012: **Note:** Customers with standalone WSUS 3.0 SP2 environments or System Center Configuration Manager 2007 Service Pack 2 environments with WSUS 3.0 SP2 require [2734608](https://support.microsoft.com/kb/2734608) to properly manage Windows 8-based computers or Windows Server 2012-based computers as clients.|  
|[Exchange 2013](https://technet.microsoft.com/library/bb691354.aspx)|Windows Server 2012 Standard および Datacenter は、次の役割のサポート: スキーマ マスター、グローバル カタログ サーバー、ドメイン コント ローラー、メールボックスとクライアント アクセス サーバーの役割<br /><br />フォレストの機能レベル: Windows Server 2003 以降<br /><br />ソース: Exchange 2013 のシステム要件|  
|Exchange 2010|[ソース: Exchange 2010 Service Pack 3](https://blogs.technet.com/b/exchange/archive/2012/09/25/announcing-exchange-2010-service-pack-3.aspx)<br /><br />メンバー サーバーの Windows Server 2012 には、Exchange 2010 Service Pack 3 をインストールすることができます。<br /><br />[Exchange 2010 System Requirements](https://technet.microsoft.com/library/aa996719(EXCHG.141).aspx) lists the latest supported schema master, global catalog and domain controller as Windows Server 2008 R2.<br /><br />フォレストの機能レベル: Windows Server 2003 以降|  
|SQL Server 2012|Source: KB [2681562](https://support.microsoft.com/kb/2681562)<br /><br />Windows Server 2012 では、SQL Server 2012 RTM がサポートされています。|  
|SQL Server 2008 R2|Source: KB [2681562](https://support.microsoft.com/kb/2681562)<br /><br />Windows Server 2012 にインストールする SQL Server 2008 R2 Service Pack 1 またはそれ以降が必要です。|  
|SQL Server 2008|Source: KB [2681562](https://support.microsoft.com/kb/2681562)<br /><br />Windows Server 2012 にインストールする SQL Server 2008 Service Pack 3 以降が必要です。|  
|SQL Server 2005|Source: KB [2681562](https://support.microsoft.com/kb/2681562)<br /><br />Windows Server 2012 でのインストールはサポートされていません。|  
  
## <a name="BKMK_KnownIssues"></a>既知の問題  
次の表は、AD DS のインストールに関連する既知の問題を示します。  
  
||||  
|-|-|-|  
|サポート技術情報の記事番号とタイトル|影響を受けるテクノロジ エリア|問題の説明]|  
|[2830145](https://support.microsoft.com/kb/2830145): SID S-1-18-1 and SID S-1-18-2 can't be mapped on Windows 7 or Windows Server 2008 R2-based computers in a domain environment|AD DS の管理/アプリケーションの互換性|SID S 1-18 1 と SID S 1 ~ 18 2、Windows Server 2012 の新機能で、マップ アプリケーションは、Windows 7 ベースまたは Windows Server 2008 R2 ベースのコンピューター上の Sid で解決できないために失敗する可能性があります。 この問題を解決するには、ドメイン内の Windows 7 および Windows Server 2008 R2 ベースのコンピューターに修正プログラムをインストールします。|  
|[2737129](https://support.microsoft.com/kb/2737129): Group Policy preparation is not performed when you automatically prepare an existing domain for Windows Server 2012|AD DS のインストール|Adprep/domainprep/gpprep は、ドメインで Windows Server 2012 を実行する最初の DC をインストールの一環として自動的には実行されません。 それがまだ実行されていたドメイン内場合、手動で実行する必要があります。|  
|[2737416](https://support.microsoft.com/kb/2737416): Windows PowerShell-based domain controller deployment repeats warnings|AD DS のインストール|警告は、前提条件の検証中に表示され、インストール中に再度ことができます。|  
|[2737424](https://support.microsoft.com/kb/2737424): "Format of the specified domain name is invalid" error when you try to remove Active Directory Domain Services from a domain controller|AD DS のインストール|作成済みの RODC アカウントがまだ存在するドメインの最後の DC を削除する場合、このエラーが表示されます。 これは、Windows Server 2012、Windows Server 2008 R2、および Windows Server 2008 に影響します。|  
|[2737463](https://support.microsoft.com/kb/2737463): Domain controller does not start, c00002e2 error occurs, or "Choose an option" is displayed|AD DS のインストール|管理者が Dism.exe、Pkgmgr.exe、または Ocsetup.exe を Directoryservices-domaincontroller 役割を削除する使用ために、DC は開始されません。|  
|[2737516](https://support.microsoft.com/kb/2737516): IFM verification limitations in Windows Server 2012 Server Manager|AD DS のインストール|サポート技術情報の記事で説明するように ifm による検証の制限事項ことができます。|  
|[2737535](https://support.microsoft.com/kb/2737535): Install-AddsDomainController cmdlet returns parameter set error for RODC|AD DS のインストール|作成済みの RODC アカウントでは既に設定されている引数を指定する場合、サーバーを RODC アカウントに接続しようとすると、エラーを受信できます。|  
|[2737560](https://support.microsoft.com/kb/2737560): "Unable to perform Exchange schema conflict check" error, and prerequisites check fails|AD DS のインストール|ドメイン コント ローラーにはネットワーク サービス、SeServiceLogonRight が不足しているために、既存のドメインで最初の Windows Server 2012 DC を構成するとき、または WMI または DCOM プロトコルがブロックされているために、前提条件の確認が失敗します。|  
|[2737797](https://support.microsoft.com/kb/2737797): AddsDeployment module with the -Whatif argument shows incorrect DNS results|AD DS のインストール|-Whatif パラメーターは、サーバーがインストールされていないが、これは、DNS を示しています。|  
|[2737807](https://support.microsoft.com/kb/2737807): The Next button is not available on the Domain Controller Options page|AD DS のインストール|ターゲット DC の IP アドレスは、既存のサブネットまたはサイトにマップされないか、DSRM パスワードは入力および確認が正しく行わされないために、ドメイン コント ローラー オプション] ページで、[次へ] ボタンが無効です。|  
|[2737935](https://support.microsoft.com/kb/2737935): Active Directory installation stalls at the "Creating the NTDS settings object" stage|AD DS のインストール|インストールがハングするは、ローカルの Administrator パスワードがドメインの Administrator パスワードと一致するか、ネットワークの問題のために重要なレプリケーションが完了するためです。|  
|[2738060](https://support.microsoft.com/kb/2738060): "Access is denied" error message when you create a child domain remotely by using Install-AddsDomain|AD DS のインストール|DNSDelegationCredential、パスワードが不良である場合に、Invoke-command コマンドレットを使用 Install-addsdomain を実行すると、エラーが表示されます。|  
|[2738697](https://support.microsoft.com/kb/2738697): "The server is not operational" domain controller configuration error when you configure a server by using Server Manager|AD DS のインストール|NTLM 認証が無効なために、ワークグループ コンピューターに AD DS をインストールしようとすると、このエラーが発生します。|  
|[2738746](https://support.microsoft.com/kb/2738746): You receive access denied errors after you log on to a local administrator domain account|AD DS のインストール|ビルトイン Administrator アカウントではなく、ローカル管理者アカウントを使用してログオンし、新しいドメインを作成すると、アカウントが Domain Admins グループに追加されません。|  
|[2743345](https://support.microsoft.com/kb/2743345): "The system cannot find the file specified" Adprep /gpprep error, or tool crashes|AD DS のインストール|このエラーは、インフラストラクチャ マスターが実装するために、adprep/gpprep を実行すると、不整合な名前空間|  
|[2743367](https://support.microsoft.com/kb/2743367): Adprep "not a valid Win32 application" error on Windows Server 2003, 64-bit version|AD DS のインストール|Windows Server 2012 Adprep は Windows Server 2003 で実行できないために、このエラーが発生します。|  
|[2753560](https://support.microsoft.com/kb/2753560): ADMT 3.2 and PES 3.1 installation errors on Windows Server 2012|ADMT|仕様で Windows Server 2012 で ADMT 3.2 はインストールできません。|  
|[2750857](https://support.microsoft.com/kb/2750857): DFS Replication diagnostic reports do not display correctly in Internet Explorer 10|DFS レプリケーション|DFS レプリケーション診断レポートが Internet Explorer 10 での変更によって正しく表示されません。|  
|[2741537](https://support.microsoft.com/kb/2741537): Remote Group Policy updates are visible to users|グループ ポリシー|これは、ログオンしている各ユーザーのコンテキストで実行するスケジュールされたタスクが原因です。 Windows タスク スケジューラの設計では、このシナリオでは対話的なプロンプトが必要です。|  
|[2741591](https://support.microsoft.com/kb/2741591): ADM files are not present in SYSVOL in the GPMC Infrastructure Status option|グループ ポリシー|GP のレプリケーションは、GPMC のインフラストラクチャの状態がカスタマイズされたフィルタ リング規則に従わないので、「進行中のレプリケーション」を報告できます。|  
|[2737880](https://support.microsoft.com/kb/2737880): "The service cannot be started" error during AD DS configuration|仮想 DC の複製|DS 役割サーバー サービスが無効なためにをインストールするか、AD DS を削除または、複製中にこのエラーが発生します。|  
|[2742836](https://support.microsoft.com/kb/2742836): Two DHCP leases are created for each domain controller when you use the VDC cloning feature|仮想 DC の複製|これは、複製されたドメイン コント ローラーの複製をもう一度複製が完了する前にもリースを受け取るために発生します。|  
|[2742844](https://support.microsoft.com/kb/2742844): Domain controller cloning fails and the server restarts in DSRM in Windows Server 2012|仮想 DC の複製|さまざまな理由は、サポート技術情報の記事に記載のいずれかの複製に失敗したため、複製された DC が DSRM で開始します。|  
|[2742874](https://support.microsoft.com/kb/2742874): Domain controller cloning does not re-create all service principal names|仮想 DC の複製|ドメインの名前変更プロセスの制限のため、いくつか 3 部構成 Spn は、複製された DC で再作成されません。|  
|[2742908](https://support.microsoft.com/kb/2742908): "No logon servers are available" error after cloning domain controller|仮想 DC の複製|これは、複製仮想化 DC の複製に失敗し、DC が DSRM で起動した後でログオンしようとすると、このエラーが発生します。 としてログオンします。 \administrator 複製の失敗をトラブルシューティングします。|  
|[2742916](https://support.microsoft.com/kb/2742916): Domain controller cloning fails with error 8610 in dcpromo.log|仮想 DC の複製|複製に失敗したため、PDC エミュレーターがドメイン パーティション、可能性の役割を転送するための入力方向のレプリケーションを実行していません。|  
|[2742927](https://support.microsoft.com/kb/2742927): "Index was out of range" New-AdDcCloneConfig error|仮想 DC の複製|管理者特権のコマンド プロンプトから、コマンドレットが実行されていないか、または、アクセス トークンに Administrators グループが含まれていないため、仮想 Dc の複製中、New-addccloneconfigfile コマンドレットを実行した後、エラーが表示されます。|  
|[2742959](https://support.microsoft.com/kb/2742959): Domain controller cloning fails with error 8437: "invalid parameter was specified for this replication operation"|仮想 DC の複製|無効な複製名または重複した NetBIOS 名が指定されているために、複製できませんでした。|  
|[2742970](https://support.microsoft.com/kb/2742970): DC Cloning fails with no DSRM, duplicate source and clone computer|仮想 DC の複製|仮想化された複製された DC でディレクトリ サービス修復モード (DSRM)、正しい場所に DCCloneConfig.xml ファイルが作成されていないため、またはソース DC が複製前に再起動されたため、ソース DC と重複する名前を使用してを起動します。|  
|[2743278](https://support.microsoft.com/kb/2743278): Domain controller cloning error 0x80041005|仮想 DC の複製|複製された DC は dsrm でブートする 1 つだけの WINS サーバーが指定されているためです。 WINS サーバーが指定されている場合は、優先と代替 WINS サーバーの両方を指定する必要があります。|  
|[2745013](https://support.microsoft.com/kb/2745013): "Server is not operational" error message if you run New-AdDcCloneConfigFile in Windows Server 2012|仮想 DC の複製|サーバーがグローバル カタログ サーバーに接続できないために、New-addccloneconfigfile コマンドレットを実行した後、このエラーが発生します。|  
|[2747974](https://support.microsoft.com/kb/2747974): Domain controller cloning event 2224 provides incorrect guidance|仮想 DC の複製|イベント ID 2224 には、複製前に管理されたサービス アカウントを削除する必要があります。 スタンドアロンの Msa を削除する必要がありますが、グループの Msa は複製をブロックしません。|  
|[2748266](https://support.microsoft.com/kb/2748266): You cannot unlock a BitLocker-encrypted drive after you upgrade to Windows 8|BitLocker|Windows 7 からアップグレードされたコンピューター上のドライブのロックを解除しようとすると、"アプリケーションが見つかりません"というエラーが表示されます。|  
  
## <a name="see-also"></a>参照してください。  
[Windows Server 2012 評価のリソース](https://technet.microsoft.com/evalcenter/hh708766.aspx)  
[Windows Server 2012 の評価ガイド](https://download.microsoft.com/download/5/B/2/5B254183-FA53-4317-B577-7561058CEF42/WS%202012%20Evaluation%20Guide.pdf)  
[Windows Server 2012 インストールし、展開](https://technet.microsoft.com/library/hh831620.aspx)  
  


