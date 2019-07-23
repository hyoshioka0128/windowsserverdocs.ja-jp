---
ms.assetid: e4c31187-f15f-410b-bb79-8d63e2f2b421
title: ドメイン コントローラーを Windows Server 2012 R2 または Windows Server 2012 にアップグレードする
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 6dda30bd15bedab8ea5ca8ca2e9597e1cc196e43
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66443055"
---
# <a name="upgrade-domain-controllers-to-windows-server-2012-r2-and-windows-server-2012"></a>ドメイン コントローラーを Windows Server 2012 R2 または Windows Server 2012 にアップグレードする

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

このトピックでは、Windows Server 2012 R2 および Windows Server 2012 の Active Directory Domain Services に関する背景情報を提供し、Windows Server 2008 または Windows Server 2008 R2 からドメイン コント ローラーをアップグレードするプロセスについて説明します。  
  
## <a name="BKMK_UpgradeWorkflow"></a>ドメイン コント ローラーのアップグレード手順  
ドメインをアップグレードするのに推奨される方法は、新しいバージョンの Windows Server を実行するドメイン コントローラーを昇格させる一方で、必要に応じて古いドメイン コントローラーを降格させる方法です。 この方法は、既存のドメイン コントローラーのオペレーティング システムをアップグレードする方法としてお勧めします。 この一覧は、新しいバージョンの Windows Server を実行するドメイン コント ローラーを昇格する前にする一般的な手順について説明します。  
  
1. 対象サーバーが [システム要件](https://technet.microsoft.com/library/dn303418.aspx)を満たしていることを確認します。  
2. 確認[アプリケーションの互換性](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_AppCompat)します。  
3. セキュリティ設定を確認します。 詳細については、次を参照してください。[非推奨の機能および動作変更は、Windows Server 2012 で AD DS に関連する](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_DeprecatedFeatures)と[Windows Server 2008 および Windows Server 2008 R2 の既定の設定をセキュリティで保護された](https://technet.microsoft.com/library/upgrade-domain-controllers-to-windows-server-2008-r2(WS.10).aspx#BKMK_SecureDefault)します。  
4. インストールを実行するコンピューターから対象サーバーに接続できることを確認します。  
5. 必要な操作マスターの役割を使用できることを確認します。  

   - 既存のドメインまたはフォレストで Windows Server 2012 を実行する最初の DC をインストールして adprep を実行するためにインフラストラクチャ マスターの adprep/forestprep を実行するにはスキーマ マスターへの接続、インストールを実行するマシンする必要があります/。domainprep します。  
   - フォレスト スキーマが既に拡張されているドメイン内で最初の DC をインストールする場合は、インフラストラクチャ マスターへの接続のみが必要になります。  
   - 既存のフォレスト内でドメインをインストールまたは削除する場合は、ドメイン名前付けマスターへの接続が必要になります。  
   - いずれの場合も、ドメイン コントローラーのインストールでは、RID マスターへの接続も必要です。  
   - 既存のフォレスト内で最初の読み取り専用のドメイン コントローラーをインストールするには、各アプリケーション ディレクトリ パーティション (ドメインでない名前付けコンテキスト (NDNC) とも呼ばれます) について、インフラストラクチャ マスターへの接続が必要です。  

6. AD DS インストールを実行するために必要な資格情報を指定します。  

   |インストール操作|資格情報の要件|  
   |-----------------------|---------------------------|  
   |新しいフォレストをインストールする|対象サーバーのローカル Administrator|  
   |既存のフォレスト内に新しいドメインをインストールする|Enterprise Admins|  
   |既存ドメイン内に追加 DC をインストールする|Domain Admins|  
   |adprep /forestprep を実行する|Schema Admins、Enterprise Admins、Domain Admins|  
   |adprep /domainprep を実行する|Domain Admins|  
   |adprep /domainprep /gpprep を実行する|Domain Admins|  
   |adprep /rodcprep を実行する|Enterprise Admins|  

   AD DS をインストールするためのアクセス許可は、委任することができます。 詳細については、 [インストールの管理タスク](https://technet.microsoft.com/library/cc773327(WS.10).aspx)に関するページを参照してください。  

Windows PowerShell コマンドレットまたはサーバー マネージャーを使用して新規またはレプリカの Windows Server 2012 ドメイン コントローラーを昇格させるための詳細な手順については、次のリンクを参照してください。  

- [Active Directory Domain Services (レベル 100) のインストールします。](https://technet.microsoft.com/library/hh472162.aspx)  
- [新しい Windows Server 2012 Active Directory フォレスト (レベル 200) のインストールします。](https://technet.microsoft.com/library/jj574166.aspx)  
- [既存のドメイン (レベル 200) でレプリカ Windows Server 2012 ドメイン コント ローラーをインストールします。](https://technet.microsoft.com/library/jj574134.aspx)  
- [インストール、Windows Server 2012 の新しい Active Directory 子ドメインまたはツリー ドメイン (レベル 200)](https://technet.microsoft.com/library/jj574105.aspx)  
- [Windows Server 2012 の Active Directory 読み取り専用ドメイン コント ローラー (RODC) (レベル 200) のインストールします。](https://technet.microsoft.com/library/jj574152.aspx)  
- [設定を Windows Server 2012 ドメイン コント ローラー (EN-US) のステップ バイ ステップ ガイド](https://social.technet.microsoft.com/wiki/contents/articles/12370.step-by-step-guide-for-setting-up-windows-server-2012-domain-controller-en-us.aspx)  

## <a name="windows-update-considerations"></a>Windows の更新に関する注意点

Windows 8 のリリース以前は、Windows Update 自身が、更新のチェック、ダウンロード、およびインストールを行うための内部スケジュールを管理していました。 そのためには、Windows Update エージェントが常にバックグラウンドで動作していなければならず、結果的にメモリなどのシステム リソースが消費されていました。  
  
Windows 8 と Windows Server 2012 には、 [自動メンテナンス](https://msdn.microsoft.com/library/windows/desktop/hh848037(v=vs.85).aspx)と呼ばれる新しい機能が導入されています。 自動メンテナンスでは、それ自身のスケジューリングと実行ロジックの管理に使用する多数のさまざまな機能が統合されています。 統合の結果、これらすべてのコンポーネントについて、消費されるシステム リソースが大幅に減り、連携動作に一貫性が生まれるようになりました。また、新しいデバイスの種類で [コネクト スタンバイ](https://msdn.microsoft.com/library/windows/hardware/jj248729.aspx) 状態が認識され、ポータブル デバイスでのバッテリー消費が少なくなりました。  
  
Windows Update は Windows 8 および Windows Server 2012 の自動メンテナンス機能の一部であるので、更新をインストールする日付と時刻を設定するための自身の内部スケジュールは有効ではなくなりました。 企業内において、Windows 8 および Windows Server 2012 搭載コンピューターを含むすべてのデバイスとコンピューターについて、その再起動後の動作に一貫性と予測可能性を持たせることができるようにするには、Microsoft サポート技術情報の記事 [2885694](https://support.microsoft.com/kb/2885694) (または 2013 年 10 月の累積的なロールアップ [2883201](https://support.microsoft.com/kb/2883201)) を参考にしてください。次に、WSUS ブログの [Windows 8 および Windows Server 2012 での、さらに予測可能な Windows Update エクスペリエンスの実現 (KB 2885694)](http://blogs.technet.com/b/wsus/archive/2013/10/08/enabling-a-more-predictable-windows-update-experience-for-windows-8-and-windows-server-2012-kb-2885694.aspx)に関する投稿で説明されているポリシー設定を構成します。  

## <a name="BKMK_NewWS2012R2"></a>Windows Server 2012 R2 で AD DS の新機能

次の表は、Windows Server 2012 R2 のAD DS 関連の新機能をまとめたものです。詳細情報がある場合は、リンクも示しています。 一部の機能に関する詳細 (要件など) については、「 [Windows Server の Active Directory の新機能](https://technet.microsoft.com/library/dn268294.aspx)」を参照してください。  

|機能|説明|  
|-----------|---------------|  
|[ワークプ レース ジョイン](https://technet.microsoft.com/library/dn280945.aspx)|インフォメーション ワーカーが企業のリソースとサービスにアクセスするために、個人のデバイスを社内コンピューターの一部として参加させることができるようにします。|  
|[Web アプリケーション プロキシ](https://technet.microsoft.com/library/dn280942.aspx)|新しいリモート アクセス役割サービスを使って Web アプリケーションへのアクセスを提供します。|  
|[Active Directory フェデレーション サービス (AD FS)](https://technet.microsoft.com/library/hh831502.aspx)|AD FS では、展開が簡素化され、ユーザーが個人のデバイスからリソースにアクセスできるようにすると共に、IT 部門がアクセス制御を行うことを支援できるようにするための機能が強化されています。|  
|[SPN と UPN の一意性](https://technet.microsoft.com/library/dn535779.aspx)|Windows Server 2012 R2 搭載のドメイン コントローラーは、重複するサービス プリンシパル名 (SPN) とユーザー プリンシパル名 (UPN) の作成をブロックします。|  
|[Winlogon 自動再起動サインオン (ARSO)](https://technet.microsoft.com/library/dn535772.aspx)|Windows 8.1 デバイス上でロック画面アプリケーションを再起動して利用できるようにします。|  
|[TPM キーの構成証明](https://technet.microsoft.com/library/dn581921.aspx)|証明書要求者の秘密キーがトラステッド プラットフォーム モジュール (TPM) によって実際に保護されることを、発行済みの証明書において CA が暗号によって証明できるようにします。|  
|[資格情報の保護と管理](https://technet.microsoft.com/library/dn408190.aspx)|資格情報の盗難を減らすための、新しい資格情報保護コントロールとドメイン認証コントロールがあります。|  
|[ファイル レプリケーション サービス (FRS) の廃止](https://technet.microsoft.com/library/dn535775.aspx)|Windows Server 2003 ドメインの機能レベルも廃止されています。機能レベルでは、SYSVOL をレプリケートするのに FRS を使用するからです。 つまり、Windows Server 2012 R2 搭載のサーバー上に新しいドメインを作成するとき、ドメインの機能レベルは Windows Server 2008 以降である必要があります。 Windows Server 2003 ドメイン機能レベル; を持つ既存のドメインに Windows Server 2012 R2 を実行するドメイン コント ローラーを追加することができます。また、そのレベルで新しいドメインを作成することはできませんだけです。|  
|[新しいドメインとフォレストの機能レベル](../active-directory-functional-levels.md)|Windows Server 2012 R2 の新しい機能レベルがあります。 Windows Server 2012 R2 DFL では新しい機能を利用できます。|  
|[LDAP クエリ オプティマイザーの変更](https://technet.microsoft.com/library/dn535775.aspx)|複雑なクエリの LDAP 検索効率および LDAP 検索時間においてパフォーマンスが向上しています。|  
|[1644 イベントの改善](https://technet.microsoft.com/library/dn535775.aspx)|トラブルシューティングを支援する目的で LDAP 検索結果の統計がイベント ID 1644 に追加されました。|  
|[Active Directory レプリケーション スループットの向上](https://technet.microsoft.com/library/dn535775.aspx)|AD レプリケーションの最大スループットを 40 Mbps から約 600 Mbps に調整します。|  

## <a name="BKMK_WhatsNewAD"></a>Windows Server 2012 における AD DS の新機能

次の表は、Windows Server 2012 のAD DS 関連の新機能をまとめたものです。詳細情報がある場合は、リンクも示しています。 それぞれの要件を含む、一部の機能の詳細な説明を参照してください。 [Active Directory Domain Services (AD DS) で新](https://technet.microsoft.com/library/hh831477.aspx)します。  
  
|機能|説明|  
|-----------|---------------|  
|Active Directory によるライセンス認証 (AD BA) (「 [ボリューム ライセンス認証の概要](https://technet.microsoft.com/library/hh831612.aspx)」を参照)|ボリューム ソフトウェア ライセンスの配布と管理を構成するタスクが簡略化されます。|  
|[Active Directory フェデレーション サービス (AD FS)](https://technet.microsoft.com/library/hh831502.aspx)|サーバー マネージャー経由のサーバーの役割のインストール、信頼のセットアップの単純化、自動的な信頼管理、SAML プロトコルのサポートなどが追加されます。|  
|Active Directory の失われたページのフラッシュ イベント|Active Directory データベースに対して、失われたページのフラッシュ イベントを検出できるように、NTDS ISAM イベント 530 が Jet エラー -1119 と共にログ出力されます。|  
|[Active Directory のごみ箱のユーザー インターフェイス](https://technet.microsoft.com/library/hh831702.aspx#ad_recycle_bin_mgmt)|Active Directory 管理センター (ADAC) により、最初は Windows Server 2008 R2 で導入されたごみ箱の機能の GUI 管理が追加されます。|  
|[Active Directory レプリケーションおよびトポロジの Windows PowerShell コマンドレット](https://technet.microsoft.com/library/hh831757.aspx)|Windows PowerShell の使用による Active Directory サイト、サイト リンク、接続オブジェクトなどの作成と管理がサポートされます。|  
|[ダイナミック アクセス制御](https://technet.microsoft.com/library/hh831717.aspx)|従来のアクセス制御モデルを拡張する、新しい信頼性情報ベースの承認プラットフォーム。|  
|[きめ細かなパスワード ポリシーのユーザー インターフェイス](https://technet.microsoft.com/library/hh831702.aspx#fine_grained_pswd_policy_mgmt)|ADAC により、最初は Windows Server 2008 で追加された PSO の作成、編集、および割り当ての GUI サポートが追加されます。|  
|[グループ管理サービス アカウント (gMSA)](https://technet.microsoft.com/library/hh831782.aspx)|gMSA と呼ばれる新しい種類のセキュリティ プリンシパル。 複数のホストで実行されるサービスは、同じ gMSA アカウントで実行できます。|  
|[DirectAccess オフライン ドメイン参加](https://technet.microsoft.com/library/jj574150.aspx)|DirectAccess の前提条件を含めることでオフラインのドメイン参加が拡張されます。|  
|[仮想ドメイン コント ローラー (DC) の複製による迅速な展開](https://technet.microsoft.com/library/hh831734.aspx#virtualized_dc_cloning)|Windows PowerShell コマンドレットを使用して既存のドメイン コントローラーを複製することにより、仮想化 DC を迅速に展開できます。|  
|[RID プールの変更](https://technet.microsoft.com/library/jj574229.aspx)|新しい監視イベントとクォータの追加により、グローバル RID プールの過剰な消費を防ぎます。 元のプールが枯渇した場合は、オプションでグローバル RID プールのサイズを 2 倍に拡張できます。|  
|セキュリティで保護されたタイム サービス|W32tm 用のセキュリティが拡張されます。ネットワークからシークレットを削除し、MD5 ハッシュ機能を削除して、Windows 8 タイム クライアントに対して認証を行うようにサーバーに求めます。|  
|[仮想化 Dc に対する USN ロールバック保護](https://technet.microsoft.com/library/hh831734.aspx#safe_virt_dc)|仮想化 DC のスナップショット バックアップを誤って復元しても、USN ロールバックが発生しなくなりました。|  
|[Windows PowerShell 履歴ビューアー](https://technet.microsoft.com/library/hh831702.aspx#windows_powershell_history_viewer)|ADAC を使用すると、管理者は、実行された Windows PowerShell コマンドを表示できます。|  
  
### <a name="BKMK_"></a>自動のメンテナンスや変更を Windows Update によって更新プログラムが適用された後の再起動の動作

Windows 8 のリリース以前は、Windows Update 自身が、更新のチェック、ダウンロード、およびインストールを行うための内部スケジュールを管理していました。 そのためには、Windows Update エージェントが常にバックグラウンドで動作していなければならず、結果的にメモリなどのシステム リソースが消費されていました。  
  
Windows 8 と Windows Server 2012 には、 [自動メンテナンス](https://msdn.microsoft.com/library/windows/desktop/hh848037(v=vs.85).aspx)と呼ばれる新しい機能が導入されています。 自動メンテナンスでは、それ自身のスケジューリングと実行ロジックの管理に使用する多数のさまざまな機能が統合されています。 統合の結果、これらすべてのコンポーネントについて、消費されるシステム リソースが大幅に減り、連携動作に一貫性が生まれるようになりました。また、新しいデバイスの種類で [コネクト スタンバイ](https://msdn.microsoft.com/library/windows/hardware/jj248729.aspx) 状態が認識され、ポータブル デバイスでのバッテリー消費が少なくなりました。  
  
Windows Update は Windows 8 および Windows Server 2012 の自動メンテナンス機能の一部であるので、更新をインストールする日付と時刻を設定するための自身の内部スケジュールは有効ではなくなりました。 企業内において、Windows 8 および Windows Server 2012 搭載コンピューターを含むすべてのデバイスとコンピューターについて、その再起動後の動作に一貫性と予測可能性を持たせることができるようにするには、次のグループ ポリシー設定を構成できます。  

- **コンピューターの構成 |ポリシー |管理用テンプレート |Windows コンポーネント |Windows Update |自動更新を構成します。**  
- **コンピューターの構成 |ポリシー |管理用テンプレート |Windows コンポーネント |Windows Update |ログオンしたユーザーを自動的に再起動しません。**  
- **コンピューターの構成 |ポリシー |管理用テンプレート |Windows コンポーネント |メンテナンス スケジューラ |メンテナンス ランダム遅延**  

次の表に、希望する再起動の動作になるようにこれらの設定を構成する方法の例をいくつか示します。  

|||  
|-|-|  
|**Scenario**|**推奨される構成**|  
|**WSUS の管理**<br /><br />-毎週 1 回の更新プログラムをインストールします。<br />-午後 11 時で金曜日を再起動します。|コンピューターを自動インストールに設定し、希望の時間まで自動再起動を禁止する<br /><br />**ポリシー**:自動更新を構成する (有効)<br /><br />自動更新の構成:4 - 自動ダウンロードしインストール日時を指定<br /><br />**ポリシー**:ログオンしているユーザー (無効) に自動的に再起動しません。<br /><br />**WSUS 期限**: 金曜日の 23:00 に設定する|  
|**WSUS の管理**<br /><br />-異なる時間/日の間でのインストールをずらす|一緒に更新する必要のあるさまざまなコンピューター グループのターゲット グループを設定する<br /><br />前のシナリオに対して上記の手順を使用する<br /><br />さまざまなターゲット グループに対して異なる期限を設定する|  
|**WSUS で管理されていない - 期限のサポートなし**<br /><br />-異なる時点でのインストールをずらす|**ポリシー**:自動更新を構成する (有効)<br /><br />自動更新の構成:4 - 自動ダウンロードしインストール日時を指定<br /><br />**レジストリ キー:** Microsoft サポート技術情報の記事で説明されているレジストリ キーを有効にする[2835627](https://support.microsoft.com/kb/2835627)<br /><br />**ポリシー:** 自動メンテナンス ランダム遅延 (有効)<br /><br />次の動作になるように、 **[定期メンテナンス ランダム遅延]** を [PT6H] (6 時間のランダム遅延) に設定する。<br /><br />-更新プログラムが構成されたメンテナンス時間を足したものランダムな遅延にインストールされます。<br /><br />-各マシン実行ちょうど 3 日後の再起動します。<br /><br />または、コンピューターのグループごとに異なるメンテナンス時刻を設定する|  

Windows エンジニアリング チームがこれらの変更点を実装した理由の詳細については、 [Windows Update での自動更新後の再起動の最小化](http://blogs.msdn.com/b/b8/archive/2011/11/14/minimizing-restarts-after-automatic-updating-in-windows-update.aspx)に関する投稿を参照してください。  

## <a name="BKMK_InstallationChanges"></a>AD DS サーバー役割のインストールの変更

Windows Server 2003 から Windows Server 2008 R2 では、Active Directory インストール ウィザード (Dcpromo.exe) を実行する前に、x86 バージョンまたは X64 バージョンの Adprep.exe コマンド ライン ツールを実行していました。また、Dcpromo.exe には、メディアからのインストールや無人インストールのオプションもありました。  
  
Windows Server 2012 以降では、Windows PowerShell の ADDSDeployment モジュール を使用することによって、コマンド ライン インストールを実行します。 サーバー マネージャーでは、まったく新しい AD DS 構成ウィザードを使用して、GUI ベースの昇格を行うことができます。 インストール プロセスを簡素化するために、ADPREP が AD DS のインストールに統合され、必要に応じて自動的に実行されるようになりました。 Windows PowerShell に基づく AD DS 構成ウィザードには、Dc が、追加し、関連するドメイン コント ローラーで必要な adprep をリモートで実行、ドメインのスキーマおよびインフラストラクチャ マスター役割が自動的に対象とします。  
  
AD DS のインストール ウィザードにおける前提条件チェックにより、発生する可能性のあるエラーが、インストールの開始前に特定されます。 エラーの発生要因を取り除くことができるため、アップグレードが不完全に終わる心配がなくなります。 ウィザードでは、GUI でのインストール時に指定されたすべてのオプションを反映した Windows PowerShell スクリプトがエクスポートされます。  
  
これらをまとめると、変更された AD DS インストールでは、DC の役割のインストール プロセスが簡素化され、管理上のエラーが減少するということになります。複数のドメイン コントローラーを、地域やドメインの垣根を越えてグローバルに展開する場合には特にその効果が発揮されます。  
コマンド ラインの構文やウィザード操作の詳しい手順など、GUI ベースおよび Windows PowerShell ベースのインストールに関する詳細については、「 [Active Directory ドメイン サービスをインストールする](https://technet.microsoft.com/library/hh472162.aspx)」を参照してください。 既存のフォレストにある Windows Server 2012 DC のインストールとは無関係に、Active Directory フォレスト内でスキーマ変更の導入を管理するには、管理者特権のコマンド プロンプトで Adprep.exe コマンドを実行できます。  

## <a name="BKMK_DeprecatedFeatures"></a>非推奨の機能および Windows Server 2012 で AD DS に関連する動作の変更

AD DS に関連する変更がいくつかあります。  

- **Adprep32.exe の廃止**
   - Adprep.exe のバージョンは 1 つだけになりました。Windows Server 2008 以降を搭載の 64 ビットのサーバーで、必要に応じて実行できます。 リモートで実行することもでき、対象の操作マスターの役割が 32 ビットのオペレーティング システムまたは Windows Server 2003 でホストされている場合は、リモートで実行する必要があります。  
- **Dcpromo.exe の廃止**
   - Windows Server 2012 でのみ実行できます応答ファイル、またはコマンド ライン パラメーターを新しい Windows PowerShell インストール オプションへの移行に期間を設けるが、Dcpromo は非推奨です。  
- **ユーザー アカウントに対する LMHash の無効化にします。**
  - Windows Server 2008、Windows Server 2008 R2、および Windows Server 2012 のセキュリティ テンプレートに用意されているセキュリティの既定値では、Windows 2000 および Windows Server 2003 ドメイン コントローラーのセキュリティ テンプレートで無効になっている NoLMHash ポリシーが有効になります。 LMHash に依存するクライアントについては、サポート技術情報の記事 [946405](https://support.microsoft.com/kb/946405)に記載されている手順に従い、必要に応じて NoLMHash ポリシーを無効にしてください。  

Windows Server 2008 以降では、ドメイン コント ローラーはまた、Windows Server 2003 または Windows 2000 を実行するドメイン コント ローラーと比べ、次の既定のセキュリティ設定をあります。

|||||  
|-|-|-|-|  
|暗号化の種類またはポリシー|Windows Server 2008 の既定値|Windows Server 2012 および Windows Server 2008 R2 の既定値|Comment|  
|AllowNT4Crypto|Disabled|Disabled|サード パーティ製のサーバー メッセージ ブロック (SMB) クライアントは、ドメイン コントローラー上の既定のセキュリティ設定と互換性がない場合があります。 どのような場合でも、これらの設定を緩和して相互運用を可能にすることもできますが、その際はセキュリティが低下します。 詳細については、次を参照してください。[記事 942564](https://go.microsoft.com/fwlink/?LinkId=164558)でマイクロソフト サポート技術情報 (https://go.microsoft.com/fwlink/?LinkId=164558) します。|  
|DES|有効|Disabled|[記事 977321](https://go.microsoft.com/fwlink/?LinkId=177717)マイクロソフト サポート技術情報 (https://go.microsoft.com/fwlink/?LinkId=177717)|  
|統合認証のための CBT/拡張保護|なし|有効|参照してください[マイクロソフト セキュリティ アドバイザリ (937811)](https://go.microsoft.com/fwlink/?LinkId=164559) (https://go.microsoft.com/fwlink/?LinkId=164559) と[記事 976918](https://go.microsoft.com/fwlink/?LinkId=178251)でマイクロソフト サポート技術情報 (https://go.microsoft.com/fwlink/?LinkId=178251) します。<br /><br />確認し、修正プログラムをインストール[記事 977073](https://go.microsoft.com/fwlink/?LinkId=186394) (https://go.microsoft.com/fwlink/?LinkId=186394) 必要に応じて、Microsoft サポート技術情報でします。|  
|LMv2|有効|Disabled|[記事 976918](https://go.microsoft.com/fwlink/?LinkId=178251)マイクロソフト サポート技術情報 (https://go.microsoft.com/fwlink/?LinkId=178251)|  

## <a name="BKMK_SysReqs"></a>オペレーティング システムの要件

Windows Server 2012 の最小システム要件は、次の表に表示されます。 システム要件とプレインストール情報の詳細については、「 [Windows Server 2012 のインストール](https://technet.microsoft.com/library/jj134246.aspx)」を参照してください。 新しい Active Directory フォレストをインストールするための追加システム要件はありませんが、ドメイン コントローラー、LDAP クライアント要求、および Active Directory 対応アプリケーションのパフォーマンスを向上させるには、Active Directory データベースの内容をキャッシュするための十分なメモリを追加する必要があります。 既存のドメイン コントローラーをアップグレードするか、新しいドメイン コントローラーを既存のフォレストに追加する場合は、次のセクションを参照して、サーバーがディスク領域の要件を満たしていることを確認してください。  

|||  
|-|-|  
|処理者|1.4 Ghz 64 ビット プロセッサ|  
|RAM|512 MB|  
|空きディスク領域の要件|32 GB|  
|画面解像度|800 x 600 以上|  
|その他|DVD ドライブ、キーボード、インターネット アクセス|  

### <a name="BKMK_DiskSpaceDCWin8"></a>ドメイン コント ローラーをアップグレードするためのディスク領域要件

このセクションでは、Windows Server 2008 または Windows Server 2008 R2 からドメイン コント ローラーのアップグレードのみのディスク領域要件について説明します。 ドメイン コントローラーを以前のバージョンの Windows Server にアップグレードする場合のディスク領域要件の詳細については、「 [Windows Server 2008 にアップグレードするためのディスク領域の要件](https://technet.microsoft.com/library/cc754463(WS.10).aspx#BKMK_2008) 」または「 [Windows Server 2008 R2 にアップグレードするためのディスク領域の要件](https://technet.microsoft.com/library/cc754463(WS.10).aspx#BKMK_2008R2)」を参照してください。  
  
Active Directory データベースおよびログ ファイルをホストするディスクの領域サイズは、カスタムおよびアプリケーション対応のスキーマ拡張や、アプリケーションおよび管理者によって開始されるインデックスのほか、ドメイン コントローラーの展開寿命 (一般的には 5 年から 8 年) の間にディレクトリに追加されるオブジェクトおよび属性が収まるように決定してください。 一般的に、展開時に適切なサイジングを行うことは、展開後にディスク領域を拡張する場合に必要となるコストの増加に比べると、有利な投資になります。 詳細については、 [Active Directory ドメイン サービスのキャパシティ プランニング](https://social.technet.microsoft.com/wiki/contents/articles/14355.capacity-planning-for-active-directory-domain-services.aspx)に関するページを参照してください。  
  
アップグレードするドメイン コントローラーについては、オペレーティング システムのアップグレードを開始する前に、Active Directory データベース (NTDS.DIT) をホストするドライブに NTDS.DIT ファイルの 20% 以上に相当する空きディスク領域があることを確認します。 対象のボリュームに十分な空きディスク領域がない場合は、アップグレードが失敗することがあります。その際、アップグレード互換性レポートによって、空きディスク領域が不十分であることを示すエラーが返されます。  
  
この場合、空き領域を再キャプチャするために Active Directory データベースのオフラインの最適化を実行し、アップグレードを再試行することができます。 詳細については、 [ディレクトリ データベース ファイルの圧縮 (オフラインの最適化)](https://technet.microsoft.com/library/cc794920(v=WS.10).aspx)に関するページを参照してください。  
  
### <a name="available-skus"></a>利用可能な SKU

Windows Server には、Foundation、Essentials、Standard、および Datacenter の 4 つのエディションがあります。
AD DS 役割をサポートするエディションは、Standard と Datacenter の 2 種類です。  
  
以前のリリースでは、Windows Server の各エディションは、サポートされるサーバーの役割とプロセッサ数、および大容量メモリのサポートの可否という点で異なっていました。 2 つの仮想インスタンスが Standard edition の許可されている Windows Server の Standard および Datacenter エディションのすべての機能と基になるハードウェアのサポートが、仮想化権限の変更し、無制限の仮想インスタンスがデータ センターの許可エディションです。  
  
### <a name="windows-client-and-windows-server-operating-systems-that-are-supported-to-join-windows-server-domains"></a>Windows Server ドメインへの参加がサポートされている Windows クライアントおよび Windows Server オペレーティング システム

次に示す Windows クライアントおよび Windows Server オペレーティング システムは、Windows Server 2012 以降を実行するドメイン コントローラーでドメイン メンバー コンピューターとしてサポートされます。  
  
- クライアント オペレーティング システム:Windows 8.1、Windows 8、Windows 7、Windows Vista
   - Windows 8.1 または Windows 8 を実行するコンピューターは、Windows Server 2003 以降を含む、以前のバージョンの Windows Server を実行するドメイン コントローラーをメンバーとするドメインに参加できます。 ただし、この場合、Windows 8 の一部の機能については利用する前に追加構成が必要になる場合があります。 そのような機能の詳細および Windows 8 クライアントをダウンレベルのドメインで管理するための推奨事項については、 [Windows Server 2003 ドメインでの Windows 8 メンバー コンピューターの実行](https://social.technet.microsoft.com/wiki/contents/articles/17361.running-windows-8-member-computers-in-windows-server-2003-domains.aspx)に関するページを参照してください。  
- サーバー オペレーティング システム:Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008、Windows Server 2003 R2、Windows Server 2003  

## <a name="BKMK_UpgradePaths"></a>サポートされているインプレース アップグレード パス

64 ビット バージョンの Windows Server 2008 または Windows Server 2008 R2 を実行するドメイン コント ローラーは、Windows Server 2012 にアップグレードできます。 Windows Server 2003 または 32 ビット バージョンの Windows Server 2008 を実行するドメイン コントローラーは、アップグレードできません。 このようなドメイン コントローラーを置き換えるには、以降のバージョンの Windows Server を実行するドメイン コントローラーをドメインにインストールし、Windows Server 2003 を実行するドメイン コントローラーを削除します。  

|使用しているエディション|アップグレード先のエディション|  
|-------------------------------------|-------------------------------------|  
|Windows Server 2008 Standard SP2<br /><br />または<br /><br />Windows Server 2008 Enterprise SP2|Windows Server 2012 Standard<br /><br />または<br /><br />Windows Server 2012 Datacenter|  
|Windows Server 2008 Datacenter SP2|Windows Server 2012 Datacenter|  
|Windows Web Server 2008|Windows Server 2012 Standard|  
|Windows Server 2008 R2 Standard SP1<br /><br />または<br /><br />Windows Server 2008 R2 Enterprise SP1|Windows Server 2012 Standard<br /><br />または<br /><br />Windows Server 2012 Datacenter|  
|Windows Server 2008 R2 Datacenter SP1|Windows Server 2012 Datacenter|  
|Windows Web Server 2008 R2|Windows Server 2012 Standard|  
  
サポートされるアップグレード パスの詳細については、「 [Windows Server 2012 の評価バージョンとアップグレード オプション](https://go.microsoft.com/fwlink/?LinkId=260917)」を参照してください。 Windows Server 2012 の評価版を実行するドメイン コントローラーを直接製品版に変換することはできません。 代わりに、まず製品版を実行するサーバーに追加のドメイン コントローラーをインストールし、評価版で実行されているドメイン コントローラーから AD DS を削除します。  
  
既知の問題により、Windows Server 2012 の Server Core インストールに Windows Server 2008 R2 の Server Core インストールを実行するドメイン コント ローラーをアップグレードすることはできません。 アップグレードしようとすると、アップグレード プロセスの終盤でブラック スクリーンになります。 このような DC をリブートすると、boot.ini ファイル内のオプションが前のオペレーティング システム バージョンにロールバックされます。 追加のリブートを行うと、前のオペレーティング システムに自動的にロールバックされます。 ソリューションを使用できるまでは、インプレース アップグレードの Windows Server の Server Core インストールを実行する既存のドメイン コント ローラーではなく、Windows Server 2012 の Server Core インストールを実行して、新しいドメイン コント ローラーをインストールすることをお勧め2008 R2。 詳細については、サポート技術情報の記事 [2734222](https://support.microsoft.com/kb/2734222)を参照してください。  

## <a name="BKMK_FunctionalLevels"></a>機能レベルの機能と要件

Windows Server 2012 では、Windows Server 2003 フォレストの機能レベルが必要です。 既存の Active Directory フォレストに Windows Server 2012 を実行するドメイン コント ローラーを追加する前に、フォレストの機能レベルが Windows Server 2003 以降である必要があります。 Windows Server 2008 R2、Windows Server 2008、または Windows Server 2003 を実行するドメイン コントローラーは同じフォレストで動作しますが、Windows 2000 Server を実行するドメイン コントローラーはサポートされていないため、Windows Server 2012 を実行するドメイン コントローラーのインストールをブロックします。 Windows Server 2003 以降を実行するドメイン コントローラーがフォレストに含まれており、フォレストの機能レベルが Windows 2000 のレベルである場合も、インストールがブロックされます。  
  
Windows 2000 のドメイン コントローラーは、フォレストに Windows Server 2012 のドメイン コントローラーを追加する前に削除する必要があります。 この場合、次に示すワークフローを検討してください。  

1. Windows Server 2003 以降を実行するドメイン コントローラーをインストールします。 これらのドメイン コントローラーは、Windows Server の評価版に展開できます。 この手順では、前提条件として、オペレーティング システムに応じた [adprep.exe の実行](https://technet.microsoft.com/library/dd464018(WS.10).aspx) も必要です。  
2. Windows 2000 ドメイン コントローラーを削除します。 具体的には、Windows Server 2000 ドメイン コントローラーをドメインから正常に降格するか強制的に削除し、Active Directory ユーザーとコンピューターを使用して、削除されたすべてのドメイン コントローラーのドメイン コントローラー アカウントを削除します。  
3. フォレストの機能レベルを Windows Server 2003 以上に昇格します。  
4. Windows Server 2012 を実行するドメイン コントローラーをインストールします。  
5. 以前のバージョンの Windows Server を実行するドメイン コントローラーを削除することはできません。  

1 つの新しい機能を有効に、新しい Windows Server 2012 ドメイン機能レベル: **KDC で信頼性情報、複合認証、および Kerberos 防御をサポート**KDC 管理用テンプレート ポリシーに 2 つの設定 (**常に信頼性情報を提供**と**防御されていない認証要求を失敗**) Windows Server 2012 ドメインの機能レベルを必要とします。  
  
Windows Server 2012 フォレストの機能レベルは、新機能を提供しませんが、フォレスト内に作成、新しいドメインを Windows Server 2012 のドメイン機能レベルで自動的に動作するようになります。 Windows Server 2012 ドメインの機能レベルでは、信頼性情報、複合認証、および Kerberos 防御 KDC のサポート以上の他の新機能は提供されません。 ただし、ドメイン内の任意のドメイン コント ローラーが Windows Server 2012 を実行するようになります。 別の機能レベルで使用できる他の機能の詳細については、「 [AD DS の機能レベルとは](../active-directory-functional-levels.md)」を参照してください。  
  
フォレストの機能レベルを特定の値に設定した後はロールバックするか、次の例外で、フォレストの機能レベルを下げることはできません。 Windows Server 2012 フォレストの機能レベルを上げると、Windows Server 2008 R2 に下げることができます。 Active Directory のごみ箱が有効にされていない場合は、フォレストの機能レベルを Windows Server 2008 R2 または Windows Server 2008、Windows Server 2012 または Windows Server 2008 R2 から Windows Server 2008 にバックアップも下げることができます。 フォレストの機能レベルが Windows Server 2008 R2 に設定されている場合ことはできませんロールバックすること、たとえば、Windows Server 2003 にします。  
  
ロールバックまたは例外を次のドメイン機能レベルを下げることはできません、ドメインの機能レベルを特定の値を設定した後: Windows Server 2008 R2 または Windows Server 2012 では、ドメイン機能レベルを上げる場合およびフォレストの機能。nal レベルが Windows Server 2008 か、ドメインの機能レベルが Windows Server 2008 を展開または Windows Server 2008 R2 のオプションが小さい。 Windows Server 2012 から Windows Server 2008 R2 または Windows Server 2008 からのみ、または Windows Server 2008、Windows Server 2008 R2 からドメインの機能レベルを低くことができます。 ドメインの機能レベルが Windows Server 2008 R2 に設定されている場合ことはできませんロールバックすること、たとえば、Windows Server 2003 にします。  
  
低い機能レベルで使用できる機能の詳細については、「 [AD DS の機能レベルとは](../active-directory-functional-levels.md)」を参照してください。  
  
機能のレベルは、Windows Server 2012 を実行するドメイン コント ローラーは、Windows Server の以前のバージョンを実行するドメイン コント ローラーでは使用できない追加機能を提供します。 たとえば、以前のバージョンの Windows Server を実行するドメイン コント ローラーのことはできませんに Windows Server 2012 を実行するドメイン コント ローラーの仮想ドメイン コント ローラーの複製に使用できます。 仮想ドメイン コント ローラーの複製と Windows Server 2012 で仮想ドメイン コント ローラー保護機能には、機能レベルの要件がありません。  

> [!NOTE]  
> Microsoft Exchange Server 2013 では、フォレストの機能レベルとして Windows server 2003 以上が必要です。  

## <a name="BKMK_ServerRoles"></a>その他のサーバーの役割と Windows オペレーティング システムと AD DS の相互運用

AD DS は、次の Windows オペレーティング システムではサポートされません。  
  
- Windows MultiPoint Server  
- Windows Server 2012 Essentials  
  
次のサーバー役割または役割サービスを実行するサーバーに、AD DS をインストールすることはできません。  
  
- Hyper-V Server  
- リモート デスクトップ接続ブローカー  
  
## <a name="BKMK_OpsMasters"></a>操作マスターの役割

Windows Server 2012 の新機能では、操作マスターの役割に影響します。  

- PDC エミュレーターには、仮想ドメイン コント ローラーの複製をサポートするために Windows Server 2012 を実行する必要があります。 DC の複製については、追加の前提条件があります。 詳細については、「 [Active Directory ドメイン サービス (AD DS) の仮想化](https://technet.microsoft.com/library/hh831734.aspx)」を参照してください。  
- PDC エミュレーターは Windows Server 2012 を実行すると、新しいセキュリティ プリンシパルが作成されます。  
- RID マスターには、新しい RID 発行および監視機能があります。 機能強化には、イベント ロギングの向上、適切な制限の向上、緊急時における RID プール割り当て全体の 1 ビット増加などがあります。 詳細については、「[RID 発行の管理](../../ad-ds/manage/Managing-RID-Issuance.md)」を参照してください。  

> [!NOTE]  
> 操作マスターの役割は、AD DS のインストールのもう 1 つの変更は DNS サーバーの役割とグローバル カタログが既定では Windows Server 2012 を実行するすべてのドメイン コント ローラーにインストールされていること。  

## <a name="BKMK_Virtual"></a>ドメイン コント ローラーの仮想化

Windows Server 2012 以降の AD DS の機能強化より安全な仮想化ドメイン コント ローラーとドメイン コント ローラーを複製する機能が有効にします。 同様に、ドメイン コントローラーを複製することで、新しいドメインに追加のドメイン コントローラーを迅速に展開できるなどのメリットがあります。 詳細については、次を参照してください。 [Active Directory Domain Services の概要&#40;AD DS&#41; Virtualization&#40;レベル 100&#41;](../../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md)します。  

## <a name="BKMK_Admin"></a>Windows Server 2012 サーバーの管理

使用して、 [Remote Server Administration Tools for Windows 8](https://www.microsoft.com/download/details.aspx?id=28972)ドメイン コント ローラーと Windows Server 2012 を実行している他のサーバーを管理します。 Windows 8 を実行しているコンピューターでは、Windows Server 2012 リモート サーバー管理ツールを実行できます。  

## <a name="BKMK_AppCompat"></a>アプリケーションの互換性

次の表は、Active Directory が統合されている一般的な Microsoft アプリケーションの一覧です。 アプリケーションをインストールできる Windows Server のバージョンと、Windows Server 2012 DC の導入がアプリケーションの互換性に影響するかどうかが示されています。  

|製品|メモ|  
|-----------|---------|  
|[Microsoft Configuration Manager 2007](http://blogs.technet.com/b/configmgrteam/archive/2012/09/10/support-questions-about-windows-8-and-windows-server-2012.aspx)|Configuration Manager 2007 SP2 (Configuration Manager 2007 R2 と Configuration Manager 2007 R3 が含まれます):<br /><br />Windows 8 Pro<br />-   Windows 8 Enterprise<br />-Windows Server 2012 Standard<br />-Windows Server 2012 Datacenter**に注意してください。** これらはクライアントとしてフル サポートされますが、Configuration Manager 2007 オペレーティング システム展開機能を使用してこれらをオペレーティング システムとして展開するためのサポートが追加される計画はありません。 また、Windows Server 2012 のいずれの SKU でも、サイト サーバーおよびサイト システムはサポートされません。|  
|[Microsoft SharePoint 2007](https://support.microsoft.com/kb/2728964)|Microsoft Office SharePoint Server 2007 は、Windows Server 2012 へのインストールがサポートされません。|  
|[Microsoft SharePoint 2010](https://support.microsoft.com/kb/2724471)|SharePoint 2010 Service Pack 2 にインストールして操作が必要です。 <br />SharePoint 2010 を Windows Server 2012 サーバー<br /><br />SharePoint 2010 Foundation を Windows Server 2012 サーバーにインストールして操作するには、SharePoint 2010 Foundation Service Pack 2 が必要です。<br /><br />SharePoint Server 2010 (Service Pack なし) を Windows Server 2012 にインストールするプロセスは失敗します。<br /><br />SharePoint Server 2010 の前提条件インストーラー (PrerequisiteInstaller.exe)「このプログラムには互換性の問題です」エラーで失敗します。 「ヘルプを使用せず、プログラムを実行する」をクリックすると、エラーを表示"SharePoint をインストールすることを確認する&#124;(service pack なし)、SharePoint Server 2010 を Windows にインストールすることはできません Server 2012"。|  
|[Microsoft SharePoint 2013](https://technet.microsoft.com/library/cc262485(v=office.15).aspx)|ファーム内のデータベース サーバーの最小要件:<br /><br />64 ビット エディションの Windows Server 2008 R2 Service Pack 1 (SP1) Standard、Enterprise、または Datacenter、あるいは 64 ビット エディションの Windows Server 2012 Standard または Datacenter<br /><br />組み込みデータベースを持つ単一サーバーの最小要件:<br /><br />64 ビット エディションの Windows Server 2008 R2 Service Pack 1 (SP1) Standard、Enterprise、または Datacenter、あるいは 64 ビット エディションの Windows Server 2012 Standard または Datacenter<br /><br />ファーム内のフロントエンド Web サーバーおよびアプリケーション サーバーの最小要件:<br /><br />64 ビット エディションの Windows Server 2008 R2 Service Pack 1 (SP1) Standard、Enterprise、または Datacenter、あるいは 64 ビット エディションの Windows Server 2012 Standard または Datacenter|  
|[Microsoft System Center Configuration Manager 2012](http://blogs.technet.com/b/configmgrteam/archive/2012/09/10/support-questions-about-windows-8-and-windows-server-2012.aspx)|System Center 2012 Configuration Manager Service Pack 1:<br /><br />Service Pack 1 のリリースで、クライアント サポート マトリックスに次のオペレーティング システムが追加されます。<br /><br />Windows 8 Pro<br />-   Windows 8 Enterprise<br />-Windows Server 2012 Standard<br />-Windows Server 2012 Datacenter<br /><br />サイト サーバーの役割はすべて (サイト サーバー、SMS プロバイダー、管理ポイントを含めて)、次のオペレーティング システム エディションのサーバーに展開できます。<br /><br />-Windows Server 2012 Standard<br />-Windows Server 2012 Datacenter|  
|[Microsoft Lync Server 2013](https://technet.microsoft.com/library/gg412883.aspx)|Lync Server 2013 には、Windows Server 2008 R2 または Windows Server 2012 が必要です。 Server Core インストールで実行することはできません。 [仮想サーバー](https://technet.microsoft.com/library/gg399035.aspx)で実行できます。|  
|[Lync Server 2010](https://support.microsoft.com/kb/2777359)|[Lync Server 用の累積的更新プログラム (2012 年 10 月)](https://support.microsoft.com/?kbid=2493736) がインストールされていれば、新しい (アップグレードされていない) Windows Server 2012 のインストールに Lync Server 2010 をインストールすることができます。 Lync Server 2010 の既存インストールのためにオペレーティング システムを Windows Server 2012 にアップグレードすることはできません。 Microsoft Lync Server 2010 グループ チャット サーバーも、Windows Server 2012 ではサポートされていません。|  
|[System Center 2012 Endpoint Protection](http://blogs.technet.com/b/configmgrteam/archive/2012/09/10/support-questions-about-windows-8-and-windows-server-2012.aspx)|System Center 2012 Endpoint Protection Service Pack 1 では、クライアント サポート マトリックスが更新され、次のオペレーティング システムが追加されます。<br /><br />Windows 8 Pro<br />-   Windows 8 Enterprise<br />-Windows Server 2012 Standard<br />-Windows Server 2012 Datacenter|  
|[System Center 2012 Forefront Endpoint Protection](http://blogs.technet.com/b/configmgrteam/archive/2012/09/10/support-questions-about-windows-8-and-windows-server-2012.aspx)|FEP 2010 更新プログラム ロールアップ 1 では、クライアント サポート マトリックスが更新され、次のオペレーティング システムが追加されます。<br /><br />Windows 8 Pro<br />-   Windows 8 Enterprise<br />-Windows Server 2012 Standard<br />-Windows Server 2012 Datacenter|  
|Forefront Threat Management Gateway (TMG)|TMG の実行がサポートされているのは、Windows Server 2008 および Windows Server 2008 R2 のみです。 詳細については、「 [Forefront TMG のシステム要件](https://technet.microsoft.com/library/dd896981.aspx)」を参照してください。|  
|Windows Server Update Services|このリリースの WSUS では既に、Windows 8 ベースのコンピューターまたは Windows Server 2012 コンピューターがクライアントとしてサポートされています。|  
|Windows Server Update Services 3.0|更新プログラム サポート技術情報の記事[2734608](https://support.microsoft.com/kb/2734608)サーバーにより Windows Server Update Services (WSUS) 3.0 SP2 を実行している Windows 8 または Windows Server 2012 を実行しているコンピューターへの更新を提供します。**注:** スタンドアロン WSUS 3.0 SP2 環境または System Center Configuration Manager 2007 Service Pack 2 環境と WSUS 3.0 SP2 のお客様が必要な[2734608](https://support.microsoft.com/kb/2734608) Windows 8 ベースのコンピューターまたは Windows Server 2012 が正しく管理するにはクライアントとして動作するコンピューター。|  
|[Exchange 2013](https://technet.microsoft.com/library/bb691354.aspx)|Windows Server 2012 Standard および Datacenter は、次の役割に対してサポートされています: スキーマ マスター、グローバル カタログ サーバー、ドメイン コントローラー、メールボックス サーバー、クライアント アクセス サーバー<br /><br />フォレストの機能レベル:Windows Server 2003 以降<br /><br />ソース:Exchange 2013 のシステム要件|  
|Exchange 2010|[ソース:Exchange 2010 Service Pack 3](https://blogs.technet.com/b/exchange/archive/2012/09/25/announcing-exchange-2010-service-pack-3.aspx)<br /><br />Exchange 2010 Service Pack 3 は、Windows Server 2012 メンバー サーバーにインストールできます。<br /><br />[Exchange 2010 のシステム要件](https://technet.microsoft.com/library/aa996719(EXCHG.141).aspx) には、サポートされている最新のスキーマ マスター、グローバル カタログ、およびドメイン コントローラーとして Windows Server 2008 R2 が記載されています。<br /><br />フォレストの機能レベル:Windows Server 2003 以降|  
|SQL Server 2012|ソース:KB [2681562](https://support.microsoft.com/kb/2681562)<br /><br />Windows Server 2012 では SQL Server 2012 RTM がサポートされています。|  
|SQL Server 2008 R2|ソース:KB [2681562](https://support.microsoft.com/kb/2681562)<br /><br />Windows Server 2012 にインストールするには、SQL Server 2008 R2 Service Pack 1 以上が必要です。|  
|SQL Server 2008|ソース:KB [2681562](https://support.microsoft.com/kb/2681562)<br /><br />Windows Server 2012 にインストールするには、SQL Server 2008 Service Pack 3 以上が必要です。|  
|SQL Server 2005|ソース:KB [2681562](https://support.microsoft.com/kb/2681562)<br /><br />Windows Server 2012 へのインストールがサポートされていません。|  

## <a name="BKMK_KnownIssues"></a>既知の問題

AD DS のインストールに関する既知の問題を次の表に示します。  

||||  
|-|-|-|  
|サポート技術情報の記事番号とタイトル|影響を受けるテクノロジ エリア|問題点/説明|  
|[2830145](https://support.microsoft.com/kb/2830145):ドメイン環境の Windows 7 または Windows Server 2008 R2 ベースのコンピューター上で SID S-1-18-1 および SID S-1-18-2 をマップできない|AD DS の管理/アプリケーションの互換性|Windows Server 2012 の新機能である SID S-1-18-1 および SID S-1-18-2 をマップするアプリケーションは失敗する可能性があります。それらの SID を Windows 7 ベースまたは Windows Server 2008 R2 ベースのコンピューター上で解決できないためです。 この問題を解決するには、ドメイン内の Windows 7 ベースおよび Windows Server 2008 R2 ベースのコンピューターに修正プログラムをインストールしてください。|  
|[2737129](https://support.microsoft.com/kb/2737129):Windows Server 2012 の既存のドメインを自動的に準備した場合、グループ ポリシーの準備が実行されない|AD DS のインストール|Windows Server 2012 を実行するドメイン内の最初の DC をインストールする場合、adprep /domainprep /gpprep は、インストールの一部として自動的には実行されません。 ドメイン内でそれまでに実行したことがない場合は、手動で実行する必要があります。|  
|[2737416](https://support.microsoft.com/kb/2737416):Windows PowerShell ベースのドメイン コントローラーの展開で、警告が繰り返し表示される|AD DS のインストール|警告は、前提条件の確認時に表示され、インストール中に再度表示されることがあります。|  
|[2737424](https://support.microsoft.com/kb/2737424):ドメイン コントローラーから Active Directory Domain Services を削除しようとすると、"指定されたドメイン名の形式は無効です" エラーが発生する|AD DS のインストール|事前作成された RODC アカウントがまだ存在する場合にドメイン内で最後の DC を削除しようとすると、このエラーが表示されます。 Windows Server 2012、Windows Server 2008 R2、および Windows Server 2008 に影響します。|  
|[2737463](https://support.microsoft.com/kb/2737463):ドメイン コントローラーが起動しない、c00002e2 エラーが発生する、または "オプションの選択" が表示される|AD DS のインストール|DC が起動しないのは、管理者が Dism.exe、Pkgmgr.exe、または Ocsetup.exe を使用して DirectoryServices-DomainController 役割を削除したためです。|  
|[2737516](https://support.microsoft.com/kb/2737516):Windows Server 2012 サーバー マネージャーでの IFM による検証の制限|AD DS のインストール|サポート技術情報の記事に記載されているように、IFM による検証には制限があります。|  
|[2737535](https://support.microsoft.com/kb/2737535):Install-AddsDomainController コマンドレットから、RODC のパラメーター セット エラーが返される|AD DS のインストール|事前作成済みの RODC アカウントに対して指定済みの引数を指定してサーバーを RODC アカウントに関連付けようとすると、エラーが発生することがあります。|  
|[2737560](https://support.microsoft.com/kb/2737560):"交換スキーマ競合チェックを実行できません" エラーが発生し、前提条件のチェックに失敗する|AD DS のインストール|既存のドメイン内で最初の Windows Server 2012 DC を構成する際に、前提条件のチェックに失敗します。これは、Network Service に対する SeServiceLogonRight が DC にないため、あるいは WMI または DCOM プロトコルがブロックされているためです。|  
|[2737797](https://support.microsoft.com/kb/2737797):AddsDeployment モジュールに -Whatif 引数が指定されている場合に表示される DNS 結果に誤りがある|AD DS のインストール|-Whatif パラメーターは、サーバーがインストールされていませんが、そのは DNS を示しています。|  
|[2737807](https://support.microsoft.com/kb/2737807):[ドメイン コントローラー オプション] ページで [次へ] ボタンを使用できない|AD DS のインストール|[ドメイン コントローラー オプション] ページの [次へ] ボタンが無効になっているのは、ターゲット DC の IP アドレスが既存のサブネットまたはサイトにマップされていないためか、DSRM パスワードの入力と確認が正しく行われていないためです。|  
|[2737935](https://support.microsoft.com/kb/2737935):Active Directory のインストールが "NTDS 設定オブジェクトを作成しています" の段階で動作しなくなる|AD DS のインストール|インストールがハングするのは、ローカルの Administrator パスワードがドメインの Administrator パスワードと一致するためか、ネットワークの問題によって重要なレプリケーションが完了しないためです。|  
|[2738060](https://support.microsoft.com/kb/2738060):Install-AddsDomain を使用してリモートで子ドメインを作成すると、"アクセスが拒否されました" エラー メッセージが表示される|AD DS のインストール|Install-ADDSDomain を Invoke-Command コマンドレットと共に実行した場合に、DNSDelegationCredential に指定されたパスワードに問題があると、エラーが発生します。|  
|[2738697](https://support.microsoft.com/kb/2738697):サーバー マネージャーを使用してサーバーを構成すると、ドメイン コントローラーの構成エラー "サーバーは使用可能ではありません" が発生する|AD DS のインストール|ワークグループ コンピューターに AD DS をインストールしようとすると、このエラーが発生します。これは、NTLM 認証が無効になっているためです。|  
|[2738746](https://support.microsoft.com/kb/2738746):ローカル管理者ドメイン アカウントにログオンした後に、アクセス拒否エラーが発生する|AD DS のインストール|組み込みの Administrator アカウントではなくローカルの Administrator アカウントを使用してログオンし、新しいドメインを作成した場合、このアカウントは Domain Admins グループに追加されません。|  
|[2743345](https://support.microsoft.com/kb/2743345):adprep /gpprep エラー "指定されたファイルが見つかりません" が表示されるか、ツールがクラッシュする|AD DS のインストール|このエラーは、インフラストラクチャ マスターにより実装されている名前空間が不適切であるために、adprep /gpprep を実行したときに発生します。|  
|[2743367](https://support.microsoft.com/kb/2743367):64 ビット バージョンの Windows Server 2003 で、Adprep に対する "有効な Win32 アプリケーションではありません" エラーが発生する|AD DS のインストール|Windows Server 2012 Adprep は Windows Server 2003 で実行できないために、このエラーが発生します。|  
|[2753560](https://support.microsoft.com/kb/2753560):Windows Server 2012 で ADMT 3.2 と PES 3.1 のインストール エラーが発生する|ADMT|設計上、ADMT 3.2 は Windows Server 2012 にインストールできません。|  
|[2750857](https://support.microsoft.com/kb/2750857):Internet Explorer 10 で、DFS レプリケーション診断レポートが正しく表示されない|DFS レプリケーション|Internet Explorer 10 での変更のため、DFS レプリケーション診断レポートが正しく表示されません。|  
|[2741537](https://support.microsoft.com/kb/2741537):リモートでのグループ ポリシーの更新がユーザーに対して表示される|グループ ポリシー|この状況は、スケジュールされたタスクが、ログオンしている各ユーザーのコンテキストで実行されることが原因で発生します。 Windows タスク スケジューラの仕様により、このシナリオでは対話的なプロンプトが必要です。|  
|[2741591](https://support.microsoft.com/kb/2741591):GPMC のインフラストラクチャ状態オプションで、SYSVOL に ADM ファイルが存在しない|グループ ポリシー|GP のレプリケーションは、GPMC のインフラストラクチャの状態がカスタマイズされたフィルタ リング規則に従っていないために、「レプリケーション進行中です」を報告できます。|  
|[2737880](https://support.microsoft.com/kb/2737880):AD DS の構成操作中に "サービスを開始できません" エラーが発生する|仮想 DC の複製|このエラーは、DS 役割サーバー サービスが無効になっているために、AD DS のインストール、削除、または複製の実行中に発生します。|  
|[2742836](https://support.microsoft.com/kb/2742836):VDC 複製機能の使用時に、各ドメイン コントローラーに対して DHCP リースが 2 つ作成される|仮想 DC の複製|この状況は、複製されたドメイン コントローラーが、複製前にもクローンの完了時にもリースを受け取ることが原因で発生します。|  
|[2742844](https://support.microsoft.com/kb/2742844):Windows Server 2012 で、ドメイン コントローラーの複製に失敗し、サーバーが DSRM で再起動される|仮想 DC の複製|複製された DC が DSRM で再起動されるのは、サポート技術情報の記事に記載されているさまざまな理由のいずれかによって複製に失敗したためです。|  
|[2742874](https://support.microsoft.com/kb/2742874):ドメイン コントローラーの複製で、すべてのサービス プリンシパル名が再作成されない|仮想 DC の複製|複製された DC で 3 部構成の SPN のうち再作成されないものがあるのは、ドメイン名の変更プロセスの制限が原因です。|  
|[2742908](https://support.microsoft.com/kb/2742908):ドメイン コントローラーの複製後に、"使用可能なログオン サーバーがない" というエラーが発生する|仮想 DC の複製|このエラーは、仮想 DC の複製後にログオンしようとすると発生します。これは、複製に失敗し、DC が DSRM で起動されたことが原因です。 複製の失敗に対するトラブルシューティングを行うには、.\administrator としてログオンしてください。|  
|[2742916](https://support.microsoft.com/kb/2742916):ドメイン コントローラーの複製に失敗し、dcpromo.log 内にエラー 8610 が出力される|仮想 DC の複製|PDC エミュレーターがドメイン パーティションについて入力方向のレプリケーションを実行していない場合、複製が失敗します。原因としては、役割が転送されていないことが考えられます。|  
|[2742927](https://support.microsoft.com/kb/2742927):New-AdDcCloneConfig で "インデックスが範囲外です" エラーが発生する|仮想 DC の複製|このエラーは、仮想 DC の複製中、New-ADDCCloneConfigFile コマンドレットの実行後に発生します。コマンドレットが管理者特権のコマンド プロンプトで実行されていないか、アクセス トークンに Administrators グループが含まれていないことが原因です。|  
|[2742959](https://support.microsoft.com/kb/2742959):ドメイン コントローラーの複製に失敗し、エラー 8437 "このレプリケーション操作に対して、無効なパラメーターが指定されました" が発生する|仮想 DC の複製|無効な複製名または重複した NetBIOS 名が指定されたことが原因で、複製に失敗しています。|  
|[2742970](https://support.microsoft.com/kb/2742970):DC の複製に失敗し、DSRM は発生せず、ソース コンピューターと複製コンピューターの重複が発生する|仮想 DC の複製|複製された仮想 DC は、ソース DC の重複名を使用してディレクトリ サービス復元モード (DSRM) で起動されます。これは、DCCloneConfig.xml ファイルが正しい場所に作成されていないか、ソース DC が複製前に再起動されたことが原因です。|  
|[2743278](https://support.microsoft.com/kb/2743278):ドメイン コントローラーの複製エラー 0x80041005|仮想 DC の複製|WINS サーバーが 1 つしか指定されていないために、複製された DC が DSRM で起動されます。 WINS サーバーを指定する場合は、優先 WINS サーバーと代替 WINS サーバーの両方を指定する必要があります。|  
|[2745013](https://support.microsoft.com/kb/2745013):Windows Server 2012 で New-AdDcCloneConfigFile を実行すると、エラー メッセージ "サーバーは使用可能ではありません" が表示される|仮想 DC の複製|このエラーは、サーバーがグローバル カタログ サーバーに接続できない場合に、New-ADDCCloneConfigFile コマンドレットの実行後に表示されます。|  
|[2747974](https://support.microsoft.com/kb/2747974):ドメイン コントローラーの複製イベント 2224 で不適切なガイダンスが表示される|仮想 DC の複製|イベント ID 2224 で表示される、管理されたサービス アカウントは複製前に削除する必要があるというメッセージは不適切です。 スタンドアロンの MSA は削除する必要がありますが、グループの MSA は複製をブロックしません。|  
|[2748266](https://support.microsoft.com/kb/2748266):Windows 8 へのアップグレード後、BitLocker の暗号化されたドライブのロックを解除できない|BitLocker|Windows 7 からアップグレードされたコンピューターのドライブのロックを解除しようとすると、"アプリケーションが見つかりません"というエラーを受信します。|  

## <a name="see-also"></a>関連項目

[Windows Server 2012 評価用リソース](https://technet.microsoft.com/evalcenter/hh708766.aspx)  
[Windows Server 2012 評価ガイド](https://download.microsoft.com/download/5/B/2/5B254183-FA53-4317-B577-7561058CEF42/WS%202012%20Evaluation%20Guide.pdf)  
[Windows Server 2012 インストールし、展開](https://technet.microsoft.com/library/hh831620.aspx)  
