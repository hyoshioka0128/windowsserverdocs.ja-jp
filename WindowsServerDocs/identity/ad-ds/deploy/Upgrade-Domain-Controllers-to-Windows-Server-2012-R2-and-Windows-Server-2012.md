---
ms.assetid: e4c31187-f15f-410b-bb79-8d63e2f2b421
title: ドメイン コントローラーを Windows Server 2012 R2 または Windows Server 2012 にアップグレードする
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: f211acd5e93f3f4654983e2c61d6b1a460415655
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2020
ms.locfileid: "87519380"
---
# <a name="upgrade-domain-controllers-to-windows-server-2012-r2-and-windows-server-2012"></a>ドメイン コントローラーを Windows Server 2012 R2 または Windows Server 2012 にアップグレードする

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

このトピックでは、windows server 2012 R2 および Windows Server 2012 の Active Directory Domain Services に関する背景情報を提供し、Windows Server 2008 または Windows Server 2008 R2 からドメインコントローラーをアップグレードするプロセスについて説明します。

## <a name="domain-controller-upgrade-steps"></a><a name="BKMK_UpgradeWorkflow"></a>ドメイン コントローラーのアップグレード手順
ドメインをアップグレードするのに推奨される方法は、新しいバージョンの Windows Server を実行するドメイン コントローラーを昇格させる一方で、必要に応じて古いドメイン コントローラーを降格させる方法です。 この方法は、既存のドメイン コントローラーのオペレーティング システムをアップグレードする方法としてお勧めします。 この一覧では、新しいバージョンの Windows Server を実行するドメインコントローラーを昇格する前に実行する一般的な手順について説明します。

1. 対象サーバーが[システム要件](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn303418(v=ws.11))を満たしていることを確認します。
2. [アプリケーションの互換性](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_AppCompat)を確認します。
3. セキュリティ設定を確認します。 詳細については、「[Windows Server 2012 で使用されていない AD DS 関連機能および動作変更](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_DeprecatedFeatures)」および「[Windows Server 2008 および Windows Server 2008 R2 のセキュリティで保護された既定の設定](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee522994(v=ws.10)#BKMK_SecureDefault)」を参照してください。
4. インストールを実行するコンピューターからターゲット サーバーに接続できることを確認します。
5. 必要な操作マスターの役割を使用できることを確認します。

   - 既存のドメインおよびフォレストで Windows Server 2012 を実行する最初の DC をインストールするには、インストールを実行するコンピューターが、adprep/forestprep を実行するためにスキーママスターに接続し、adprep/domainprep を実行するためにインフラストラクチャマスターに接続する必要があります。
   - フォレスト スキーマが既に拡張されているドメイン内で最初の DC をインストールする場合は、インフラストラクチャ マスターへの接続のみが必要になります。
   - 既存のフォレスト内でドメインをインストールまたは削除する場合は、ドメイン名前付けマスターへの接続が必要になります。
   - いずれの場合も、ドメイン コントローラーのインストールでは、RID マスターへの接続も必要です。
   - 既存のフォレスト内で最初の読み取り専用のドメイン コントローラーをインストールするには、各アプリケーション ディレクトリ パーティション (ドメインでない名前付けコンテキスト (NDNC) とも呼ばれます) について、インフラストラクチャ マスターへの接続が必要です。

6. AD DS インストールを実行するために必要な資格情報を指定します。

   |インストール操作|資格情報の要件|
   |-----------------------|---------------------------|
   |新しいフォレストをインストールする|ターゲット サーバーのローカル Administrator|
   |既存のフォレスト内に新しいドメインをインストールする|Enterprise Admins|
   |既存ドメイン内に追加 DC をインストールする|Domain Admins|
   |adprep /forestprep を実行する|Schema Admins、Enterprise Admins、Domain Admins|
   |adprep /domainprep を実行する|Domain Admins|
   |adprep /domainprep /gpprep を実行する|Domain Admins|
   |adprep /rodcprep を実行する|Enterprise Admins|

   AD DS をインストールするためのアクセス許可は、委任することができます。 詳細については、 [インストールの管理タスク](/previous-versions/windows/it-pro/windows-server-2003/cc773327(v=ws.10))に関するページを参照してください。

Windows PowerShell コマンドレットまたはサーバー マネージャーを使用して新規またはレプリカの Windows Server 2012 ドメイン コントローラーを昇格させるための詳細な手順については、次のリンクを参照してください。

- [Active Directory Domain Services をインストールする (レベル 100)](./install-active-directory-domain-services--level-100-.md)
- [Windows Server 2012 の新しい Active Directory フォレストをインストールする (レベル 200)](./install-a-new-windows-server-2012-active-directory-forest--level-200-.md)
- [Windows Server 2012 のレプリカ ドメイン コントローラーを既存のドメインにインストールする (レベル 200)](./install-a-replica-windows-server-2012-domain-controller-in-an-existing-domain--level-200-.md)
- [Windows Server 2012 の新しい Active Directory 子ドメインまたはツリー ドメインをインストールする (レベル 200)](./install-a-new-windows-server-2012-active-directory-child-or-tree-domain--level-200-.md)
- [Windows Server 2012 の Active Directory 読み取り専用ドメイン コントローラー (RODC) をインストールする (レベル 200)](./rodc/install-a-windows-server-2012-active-directory-read-only-domain-controller--rodc---level-200-.md)
- [ドメインコントローラーに関する Windows Server 2012 フォーラム](https://docs.microsoft.com/answers/topics/windows-server-2012.html)

## <a name="windows-update-considerations"></a>Windows Update に関する考慮事項

Windows 8 のリリース以前は、Windows Update 自身が、更新のチェック、ダウンロード、およびインストールを行うための内部スケジュールを管理していました。 そのためには、Windows Update エージェントが常にバックグラウンドで動作していなければならず、結果的にメモリなどのシステム リソースが消費されていました。

Windows 8 と Windows Server 2012 には、 [自動メンテナンス](/windows/win32/w8cookbook/automatic-maintenance)と呼ばれる新しい機能が導入されています。 自動メンテナンスでは、それ自身のスケジューリングと実行ロジックの管理に使用する多数のさまざまな機能が統合されています。 統合の結果、これらすべてのコンポーネントについて、消費されるシステム リソースが大幅に減り、連携動作に一貫性が生まれるようになりました。また、新しいデバイスの種類で [コネクト スタンバイ](/windows/win32/w8cookbook/automatic-maintenance) 状態が認識され、ポータブル デバイスでのバッテリー消費が少なくなりました。

Windows Update は Windows 8 および Windows Server 2012 の自動メンテナンス機能の一部であるので、更新をインストールする日付と時刻を設定するための自身の内部スケジュールは有効ではなくなりました。 企業内において、Windows 8 および Windows Server 2012 搭載コンピューターを含むすべてのデバイスとコンピューターについて、その再起動後の動作に一貫性と予測可能性を持たせることができるようにするには、Microsoft サポート技術情報の記事 [2885694](https://support.microsoft.com/kb/2885694) (または 2013 年 10 月の累積的なロールアップ [2883201](https://support.microsoft.com/kb/2883201)) を参考にしてください。次に、WSUS ブログの [Windows 8 および Windows Server 2012 での、さらに予測可能な Windows Update エクスペリエンスの実現 (KB 2885694)](/archive/blogs/wsus/enabling-a-more-predictable-windows-update-experience-for-windows-8-and-windows-server-2012-kb-2885694)に関する投稿で説明されているポリシー設定を構成します。

## <a name="whats-new-in-ad-ds-in-windows-server-2012-r2"></a><a name="BKMK_NewWS2012R2"></a>Windows Server 2012 R2 での AD DS の新機能

次の表は、Windows Server 2012 R2 のAD DS 関連の新機能をまとめたものです。詳細情報がある場合は、リンクも示しています。 一部の機能に関する詳細 (要件など) については、「 [Windows Server の Active Directory の新機能](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn268294(v=ws.11))」を参照してください。

|機能|説明|
|-----------|---------------|
|[社内参加](../../ad-fs/operations/join-to-workplace-from-any-device-for-sso-and-seamless-second-factor-authentication-across-company-applications.md)|インフォメーション ワーカーが企業のリソースとサービスにアクセスするために、個人のデバイスを社内コンピューターの一部として参加させることができるようにします。|
|[Web アプリケーション プロキシ](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn280942(v=ws.11))|新しいリモート アクセス役割サービスを使って Web アプリケーションへのアクセスを提供します。|
|[Active Directory フェデレーション サービス (AD FS)](../../active-directory-federation-services.md)|AD FS では、展開が簡素化され、ユーザーが個人のデバイスからリソースにアクセスできるようにすると共に、IT 部門がアクセス制御を行うことを支援できるようにするための機能が強化されています。|
|[SPN と UPN の一意性](../manage/component-updates/spn-and-upn-uniqueness.md)|Windows Server 2012 R2 搭載のドメイン コントローラーは、重複するサービス プリンシパル名 (SPN) とユーザー プリンシパル名 (UPN) の作成をブロックします。|
|[Winlogon 自動再起動サインオン (ARSO)](../manage/component-updates/winlogon-automatic-restart-sign-on--arso-.md)|Windows 8.1 デバイス上でロック画面アプリケーションを再起動して利用できるようにします。|
|[TPM キーの構成証明](../manage/component-updates/tpm-key-attestation.md)|証明書要求者の秘密キーがトラステッド プラットフォーム モジュール (TPM) によって実際に保護されることを、発行済みの証明書において CA が暗号によって証明できるようにします。|
|[資格情報の保護と管理](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn408190(v=ws.11))|資格情報の盗難を減らすための、新しい資格情報保護コントロールとドメイン認証コントロールがあります。|
|[ファイル レプリケーション サービス (FRS) の廃止](../manage/component-updates/directory-services-component-updates.md)|Windows Server 2003 ドメインの機能レベルも非推奨とされます。機能レベルでは、SYSVOL をレプリケートするのに FRS を使用するからです。 つまり、Windows Server 2012 R2 搭載のサーバー上に新しいドメインを作成するとき、ドメインの機能レベルは Windows Server 2008 以降である必要があります。 Windows server 2012 R2 を実行するドメインコントローラーを、Windows Server 2003 ドメインの機能レベルを持つ既存のドメインに追加することもできます。このレベルで新しいドメインを作成することはできません。|
|[新しいドメインとフォレストの機能レベル](../active-directory-functional-levels.md)|Windows Server 2012 R2 の新しい機能レベルがあります。 Windows Server 2012 R2 DFL では新しい機能を利用できます。|
|[LDAP クエリ オプティマイザーの変更点](../manage/component-updates/directory-services-component-updates.md)|複雑なクエリの LDAP 検索効率および LDAP 検索時間においてパフォーマンスが向上しています。|
|[1644 イベントの改善](../manage/component-updates/directory-services-component-updates.md)|トラブルシューティングを支援する目的で LDAP 検索結果の統計がイベント ID 1644 に追加されました。|
|[Active Directory レプリケーション スループットの向上](../manage/component-updates/directory-services-component-updates.md)|AD レプリケーションの最大スループットを 40 Mbps から約 600 Mbps に調整します。|

## <a name="whats-new-in-ad-ds-in-windows-server-2012"></a><a name="BKMK_WhatsNewAD"></a>Windows Server 2012 での AD DS の新機能

次の表は、Windows Server 2012 のAD DS 関連の新機能をまとめたものです。詳細情報がある場合は、リンクも示しています。 一部の機能 (要件を含む) の詳細については、「 [Active Directory Domain Services の新機能」 (AD DS)](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831477(v=ws.11))を参照してください。

|機能|説明|
|-----------|---------------|
|Active Directory によるライセンス認証 (AD BA) (「 [ボリューム ライセンス認証の概要](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831612(v=ws.11))」を参照)|ボリューム ソフトウェア ライセンスの配布と管理を構成するタスクが簡略化されます。|
|[Active Directory フェデレーション サービス (AD FS)](../../active-directory-federation-services.md)|サーバー マネージャー経由のサーバーの役割のインストール、信頼のセットアップの単純化、自動的な信頼管理、SAML プロトコルのサポートなどが追加されます。|
|Active Directory の失われたページのフラッシュ イベント|Active Directory データベースに対して、失われたページのフラッシュ イベントを検出できるように、NTDS ISAM イベント 530 が Jet エラー -1119 と共にログ出力されます。|
|[Active Directory のごみ箱のユーザー インターフェイス](../get-started/adac/introduction-to-active-directory-administrative-center-enhancements--level-100-.md#ad_recycle_bin_mgmt)|Active Directory 管理センター (ADAC) により、最初は Windows Server 2008 R2 で導入されたごみ箱の機能の GUI 管理が追加されます。|
|[Windows PowerShell コマンドレットを使用した Active Directory レプリケーションおよびトポロジ管理](../manage/powershell/introduction-to-active-directory-replication-and-topology-management-using-windows-powershell--level-100-.md)|Windows PowerShell の使用による Active Directory サイト、サイト リンク、接続オブジェクトなどの作成と管理がサポートされます。|
|[ダイナミック アクセス制御](../../solution-guides/dynamic-access-control--scenario-overview.md)|従来のアクセス制御モデルを拡張する、新しい信頼性情報ベースの承認プラットフォーム。|
|[詳細なパスワード ポリシーのユーザー インターフェイス](../get-started/adac/introduction-to-active-directory-administrative-center-enhancements--level-100-.md#fine_grained_pswd_policy_mgmt)|ADAC により、最初は Windows Server 2008 で追加された PSO の作成、編集、および割り当ての GUI サポートが追加されます。|
|[グループの管理されたサービス アカウント (gMSA)](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831782(v=ws.11))|gMSA と呼ばれる新しい種類のセキュリティ プリンシパル。 複数のホストで実行されるサービスは、同じ gMSA アカウントで実行できます。|
|[DirectAccess オフラインドメイン参加](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj574150(v=ws.11))|DirectAccess の前提条件を含めることでオフラインのドメイン参加が拡張されます。|
|[仮想ドメイン コントローラー (DC) の複製による迅速な展開](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj574150(v=ws.11)#virtualized_dc_cloning)|Windows PowerShell コマンドレットを使用して既存のドメイン コントローラーを複製することにより、仮想化 DC を迅速に展開できます。|
|[RID プールの変更](../manage/managing-rid-issuance.md)|新しい監視イベントとクォータの追加により、グローバル RID プールの過剰な消費を防ぎます。 元のプールが枯渇した場合は、オプションでグローバル RID プールのサイズを 2 倍に拡張できます。|
|セキュリティで保護されたタイム サービス|W32tm 用のセキュリティが拡張されます。ネットワークからシークレットを削除し、MD5 ハッシュ機能を削除して、Windows 8 タイム クライアントに対して認証を行うようにサーバーに求めます。|
|[仮想化 DC に対する USN ロールバック保護](../manage/managing-rid-issuance.md)|仮想化 DC のスナップショット バックアップを誤って復元しても、USN ロールバックが発生しなくなりました。|
|[Windows PowerShell 履歴ビューアー](../get-started/adac/introduction-to-active-directory-administrative-center-enhancements--level-100-.md#windows_powershell_history_viewer)|ADAC を使用すると、管理者は、実行された Windows PowerShell コマンドを表示できます。|

### <a name="automatic-maintenance-and-changes-to-restart-behavior-after-updates-are-applied-by-windows-update"></a><a name="BKMK_"></a>自動メンテナンスおよび更新後の再起動の動作に対する変更は、Windows Update によって適用されます。

Windows 8 のリリース以前は、Windows Update 自身が、更新のチェック、ダウンロード、およびインストールを行うための内部スケジュールを管理していました。 そのためには、Windows Update エージェントが常にバックグラウンドで動作していなければならず、結果的にメモリなどのシステム リソースが消費されていました。

Windows 8 と Windows Server 2012 には、 [自動メンテナンス](/windows/win32/w8cookbook/automatic-maintenance)と呼ばれる新しい機能が導入されています。 自動メンテナンスでは、それ自身のスケジューリングと実行ロジックの管理に使用する多数のさまざまな機能が統合されています。 統合の結果、これらすべてのコンポーネントについて、消費されるシステム リソースが大幅に減り、連携動作に一貫性が生まれるようになりました。また、新しいデバイスの種類で [コネクト スタンバイ](/windows/win32/w8cookbook/automatic-maintenance) 状態が認識され、ポータブル デバイスでのバッテリー消費が少なくなりました。

Windows Update は Windows 8 および Windows Server 2012 の自動メンテナンス機能の一部であるので、更新をインストールする日付と時刻を設定するための自身の内部スケジュールは有効ではなくなりました。 企業内において、Windows 8 および Windows Server 2012 搭載コンピューターを含むすべてのデバイスとコンピューターについて、その再起動後の動作に一貫性と予測可能性を持たせることができるようにするには、次のグループ ポリシー設定を構成できます。

- **コンピューターの構成|ポリシー|管理用テンプレート|Windows コンポーネント|Windows Update|自動更新を構成する**
- **コンピューターの構成|ポリシー|管理用テンプレート|Windows コンポーネント|Windows Update|ログオンしているユーザーがいる場合には自動的に再起動しない**
- **コンピューターの構成|ポリシー|管理用テンプレート|Windows コンポーネント|メンテナンス スケジューラ|メンテナンス ランダム遅延**

次の表に、希望する再起動の動作になるようにこれらの設定を構成する方法の例をいくつか示します。

|||
|-|-|
|**シナリオ**|**推奨構成**|
|**WSUS 管理**<p>-1 週間に1回更新プログラムをインストールする<br />-午後11時で金曜日を再起動します|コンピューターを自動インストールに設定し、希望の時間まで自動再起動を禁止する<p>**ポリシー**:自動更新を構成する (有効)<p>自動更新の構成: 4-自動ダウンロードし、インストールをスケジュールする<p>**ポリシー**: ログオンしているユーザーがいる場合は自動再起動しない (無効)<p>**WSUS 期限**: 金曜日の 23:00 に設定する|
|**WSUS 管理**<p>-異なる時間/日にインストールをずらす|一緒に更新する必要のあるさまざまなコンピューター グループのターゲット グループを設定する<p>前のシナリオに対して上記の手順を使用する<p>さまざまなターゲット グループに対して異なる期限を設定する|
|**WSUS で管理されていない-期限のサポートなし**<p>-異なるタイミングでインストールをずらす|**ポリシー**:自動更新を構成する (有効)<p>自動更新の構成: 4-自動ダウンロードし、インストールをスケジュールする<p>**レジストリ キー:** Microsoft サポート技術情報の記事 [2835627](https://support.microsoft.com/kb/2835627)<p>**ポリシー:** 自動メンテナンス ランダム遅延 (有効)<p>次の動作になるように、[**定期メンテナンス ランダム遅延**] を [PT6H] (6 時間のランダム遅延) に設定する。<p>-更新プログラムは、構成されたメンテナンス時間とランダムな遅延でインストールされます<p>-各マシンの再起動は、3日後に正確に実行されます。<p>または、コンピューターのグループごとに異なるメンテナンス時刻を設定する|

Windows エンジニアリング チームがこれらの変更点を実装した理由の詳細については、 [Windows Update での自動更新後の再起動の最小化](https://blogs.msdn.com/b/b8/archive/2011/11/14/minimizing-restarts-after-automatic-updating-in-windows-update.aspx)に関する投稿を参照してください。

## <a name="ad-ds-server-role-installation-changes"></a><a name="BKMK_InstallationChanges"></a>AD DS サーバー役割のインストールの変更

Windows Server 2003 から Windows Server 2008 R2 では、Active Directory インストール ウィザード (Dcpromo.exe) を実行する前に、x86 バージョンまたは X64 バージョンの Adprep.exe コマンド ライン ツールを実行していました。また、Dcpromo.exe には、メディアからのインストールや無人インストールのオプションもありました。

Windows Server 2012 以降では、Windows PowerShell の ADDSDeployment モジュール を使用することによって、コマンド ライン インストールを実行します。 サーバー マネージャーでは、まったく新しい AD DS 構成ウィザードを使用して、GUI ベースの昇格を行うことができます。 インストール プロセスを簡素化するために、ADPREP が AD DS のインストールに統合され、必要に応じて自動的に実行されるようになりました。 Windows PowerShell ベースの AD DS 構成ウィザードは、Dc を追加するドメインのスキーマおよびインフラストラクチャマスターの役割を自動的にターゲットとし、関連するドメインコントローラーで必要な ADPREP コマンドをリモートで実行します。

AD DS のインストール ウィザードにおける前提条件チェックにより、発生する可能性のあるエラーが、インストールの開始前に特定されます。 エラーの発生要因を取り除くことができるため、アップグレードが不完全に終わる心配がなくなります。 ウィザードでは、GUI でのインストール時に指定されたすべてのオプションを反映した Windows PowerShell スクリプトがエクスポートされます。

これらをまとめると、変更された AD DS インストールでは、DC の役割のインストール プロセスが簡素化され、管理上のエラーが減少するということになります。複数のドメイン コントローラーを、地域やドメインの垣根を越えてグローバルに展開する場合には特にその効果が発揮されます。
コマンド ラインの構文やウィザード操作の詳しい手順など、GUI ベースおよび Windows PowerShell ベースのインストールに関する詳細については、「 [Active Directory ドメイン サービスをインストールする](./install-active-directory-domain-services--level-100-.md)」を参照してください。 既存のフォレストにある Windows Server 2012 DC のインストールとは無関係に、Active Directory フォレスト内でスキーマ変更の導入を管理するには、管理者特権のコマンド プロンプトで Adprep.exe コマンドを実行できます。

## <a name="deprecated-features-and-behavior-changes-related-to-ad-ds-in-windows-server-2012"></a><a name="BKMK_DeprecatedFeatures"></a>Windows Server 2012 で非推奨とされた AD DS 関連機能および動作変更

AD DS に関連する変更がいくつかあります。

- **Adprep32.exe の廃止**
   - Adprep.exe のバージョンは 1 つだけになりました。Windows Server 2008 以降を搭載の 64 ビットのサーバーで、必要に応じて実行できます。 リモートで実行することもでき、対象の操作マスターの役割が 32 ビットのオペレーティング システムまたは Windows Server 2003 でホストされている場合は、リモートで実行する必要があります。
- **Dcpromo.exe の廃止**
   - Dcpromo は非推奨とされます。ただし、Windows Server 2012 では、応答ファイルまたはコマンドラインパラメーターを使用して引き続き実行できます。これにより、組織は既存の自動化を新しい Windows PowerShell インストールオプションに移行する時間を確保できます。
- **ユーザー アカウントに対する LMHash の無効化**
  - Windows Server 2008、Windows Server 2008 R2、および Windows Server 2012 のセキュリティ テンプレートに用意されているセキュリティの既定値では、Windows 2000 および Windows Server 2003 ドメイン コントローラーのセキュリティ テンプレートで無効になっている NoLMHash ポリシーが有効になります。 LMHash に依存するクライアントについては、サポート技術情報の記事 [946405](https://support.microsoft.com/kb/946405)に記載されている手順に従い、必要に応じて NoLMHash ポリシーを無効にしてください。

Windows Server 2008 以降のドメインコントローラーでは、Windows Server 2003 または Windows 2000 を実行するドメインコントローラーと比較して、次のセキュリティで保護された既定の設定も使用できます。

| 暗号化の種類またはポリシー | Windows Server 2008 の既定値 | Windows Server 2012 および Windows Server 2008 R2 の既定値 | コメント |
|--|--|--|--|
| AllowNT4Crypto | 無効 | 無効 | サード パーティ製のサーバー メッセージ ブロック (SMB) クライアントは、ドメイン コントローラー上の既定のセキュリティ設定と互換性がない場合があります。 どのような場合でも、これらの設定を緩和して相互運用を可能にすることもできますが、その際はセキュリティが低下します。 詳細については、Microsoft サポート技術情報の[記事 942564](https://go.microsoft.com/fwlink/?LinkId=164558) () を参照してください https://go.microsoft.com/fwlink/?LinkId=164558) 。 |
| DES | Enabled | 無効 | Microsoft サポート技術情報の[記事 977321](https://go.microsoft.com/fwlink/?LinkId=177717) (https://go.microsoft.com/fwlink/?LinkId=177717) |
| 統合認証のための CBT/拡張保護 | N/A | Enabled | Microsoft[セキュリティアドバイザリ (937811)](https://go.microsoft.com/fwlink/?LinkId=164559) ( https://go.microsoft.com/fwlink/?LinkId=164559) および Microsoft サポート技術情報の[記事 976918](https://go.microsoft.com/fwlink/?LinkId=178251) () を参照してください https://go.microsoft.com/fwlink/?LinkId=178251) 。<p>必要に応じて、Microsoft サポート技術情報の[記事 977073](https://go.microsoft.com/fwlink/?LinkId=186394)の修正プログラムを確認してインストールし https://go.microsoft.com/fwlink/?LinkId=186394) ます。 |
| LMv2 | Enabled | 無効 | Microsoft サポート技術情報の[記事 976918](https://go.microsoft.com/fwlink/?LinkId=178251) (https://go.microsoft.com/fwlink/?LinkId=178251) |

## <a name="operating-system-requirements"></a><a name="BKMK_SysReqs"></a>オペレーティング システムの要件

次の表に、Windows Server 2012 の最小システム要件を示します。 システム要件とプレインストール情報の詳細については、「 [Windows Server 2012 のインストール](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj134246(v=ws.11))」を参照してください。 新しい Active Directory フォレストをインストールするための追加システム要件はありませんが、ドメイン コントローラー、LDAP クライアント要求、および Active Directory 対応アプリケーションのパフォーマンスを向上させるには、Active Directory データベースの内容をキャッシュするための十分なメモリを追加する必要があります。 既存のドメイン コントローラーをアップグレードするか、新しいドメイン コントローラーを既存のフォレストに追加する場合は、次のセクションを参照して、サーバーがディスク領域の要件を満たしていることを確認してください。

| 要件 | [値] |
|--|--|
| プロセッサ | 1.4 Ghz 64 ビット プロセッサ |
| RAM | 512 MB |
| 空きディスク領域の要件 | 32 GB |
| 画面解像度 | 800 x 600 以上 |
| その他 | DVD ドライブ、キーボード、インターネット アクセス |

### <a name="disk-space-requirements-for-upgrading-domain-controllers"></a><a name="BKMK_DiskSpaceDCWin8"></a>ドメイン コントローラーをアップグレードするためのディスク領域の要件

このセクションでは、Windows Server 2008 または Windows Server 2008 R2 からドメインコントローラーをアップグレードする場合のみのディスク領域の要件について説明します。 ドメイン コントローラーを以前のバージョンの Windows Server にアップグレードする場合のディスク領域要件の詳細については、「 [Windows Server 2008 にアップグレードするためのディスク領域の要件](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754463(v=ws.10)#BKMK_2008) 」または「 [Windows Server 2008 R2 にアップグレードするためのディスク領域の要件](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754463(v=ws.10)#BKMK_2008R2)」を参照してください。

Active Directory データベースおよびログ ファイルをホストするディスクの領域サイズは、カスタムおよびアプリケーション対応のスキーマ拡張や、アプリケーションおよび管理者によって開始されるインデックスのほか、ドメイン コントローラーの展開寿命 (一般的には 5 年から 8 年) の間にディレクトリに追加されるオブジェクトおよび属性が収まるように決定してください。 一般的に、展開時に適切なサイジングを行うことは、展開後にディスク領域を拡張する場合に必要となるコストの増加に比べると、有利な投資になります。 詳細については、 [Active Directory ドメイン サービスのキャパシティ プランニング](https://docs.microsoft.com/windows-server/administration/performance-tuning/role/active-directory-server/capacity-planning-for-active-directory-domain-services)に関するページを参照してください。

アップグレードするドメイン コントローラーについては、オペレーティング システムのアップグレードを開始する前に、Active Directory データベース (NTDS.DIT) をホストするドライブに NTDS.DIT ファイルの 20% 以上に相当する空きディスク領域があることを確認します。 対象のボリュームに十分な空きディスク領域がない場合は、アップグレードが失敗することがあります。その際、アップグレード互換性レポートによって、空きディスク領域が不十分であることを示すエラーが返されます。

この場合、空き領域を再キャプチャするために Active Directory データベースのオフラインの最適化を実行し、アップグレードを再試行することができます。 詳細については、 [ディレクトリ データベース ファイルの圧縮 (オフラインの最適化)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc794920(v=ws.10))に関するページを参照してください。

### <a name="available-skus"></a>利用可能な SKU

Windows Server には、Foundation、Essentials、Standard、および Datacenter の 4 つのエディションがあります。
AD DS 役割をサポートするエディションは、Standard と Datacenter の 2 種類です。

以前のリリースでは、Windows Server の各エディションは、サポートされるサーバーの役割とプロセッサ数、および大容量メモリのサポートの可否という点で異なっていました。 Windows Server の Standard edition および Datacenter edition では、すべての機能と基になるハードウェアがサポートされますが、仮想化の権限は異なります。 Standard edition では2つの仮想インスタンスを使用でき、データセンターエディションでは無制限の仮想インスタンスを使用できます。

### <a name="windows-client-and-windows-server-operating-systems-that-are-supported-to-join-windows-server-domains"></a>Windows Server ドメインへの参加がサポートされている Windows クライアントおよび Windows Server オペレーティング システム

次に示す Windows クライアントおよび Windows Server オペレーティング システムは、Windows Server 2012 以降を実行するドメイン コントローラーでドメイン メンバー コンピューターとしてサポートされます。

- サーバー オペレーティング システム:Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、Windows Server 2008、Windows Server 2003 R2、Windows Server 2003

## <a name="supported-in-place-upgrade-paths"></a><a name="BKMK_UpgradePaths"></a>サポートされる一括アップグレード パス

Windows Server 2008 または Windows Server 2008 R2 の64ビットバージョンを実行するドメインコントローラーは、Windows Server 2012 にアップグレードできます。 Windows Server 2003 または 32 ビット バージョンの Windows Server 2008 を実行するドメイン コントローラーは、アップグレードできません。 このようなドメイン コントローラーを置き換えるには、以降のバージョンの Windows Server を実行するドメイン コントローラーをドメインにインストールし、Windows Server 2003 を実行するドメイン コントローラーを削除します。

| 使用しているエディション | アップグレード先のエディション |
|--|--|
| Windows Server 2008 Standard SP2<p>または<p>Windows Server 2008 Enterprise SP2 | Windows Server 2012 Standard<p>または<p>Windows Server 2012 Datacenter |
| Windows Server 2008 Datacenter SP2 | Windows Server 2012 Datacenter |
| Windows Web Server 2008 | Windows Server 2012 Standard |
| Windows Server 2008 R2 Standard SP1<p>または<p>Windows Server 2008 R2 Enterprise SP1 | Windows Server 2012 Standard<p>または<p>Windows Server 2012 Datacenter |
| Windows Server 2008 R2 Datacenter SP1 | Windows Server 2012 Datacenter |
| Windows Web Server 2008 R2 | Windows Server 2012 Standard |

サポートされるアップグレード パスの詳細については、「 [Windows Server 2012 の評価バージョンとアップグレード オプション](https://go.microsoft.com/fwlink/?LinkId=260917)」を参照してください。 Windows Server 2012 の評価版を実行するドメイン コントローラーを直接製品版に変換することはできません。 代わりに、まず製品版を実行するサーバーに追加のドメイン コントローラーをインストールし、評価版で実行されているドメイン コントローラーから AD DS を削除します。

既知の問題のため、Windows Server 2008 R2 の Server Core インストールを実行しているドメインコントローラーを、Windows Server 2012 の Server Core インストールにアップグレードすることはできません。 アップグレードしようとすると、アップグレード プロセスの終盤でブラック スクリーンになります。 このような DC をリブートすると、boot.ini ファイル内のオプションが前のオペレーティング システム バージョンにロールバックされます。 追加のリブートを行うと、前のオペレーティング システムに自動的にロールバックされます。 ソリューションを使用できるようになるまでは、windows server 2008 R2 の Server Core インストールを実行する既存のドメインコントローラーをインプレースアップグレードするのではなく、Windows Server 2012 の Server Core インストールを実行する新しいドメインコントローラーをインストールすることをお勧めします。 詳細については、サポート技術情報の記事 [2734222](https://support.microsoft.com/kb/2734222)を参照してください。

## <a name="functional-level-features-and-requirements"></a><a name="BKMK_FunctionalLevels"></a>機能レベルの機能と要件

Windows Server 2012 には、Windows Server 2003 フォレストの機能レベルが必要です。 つまり、Windows Server 2012 を実行するドメインコントローラーを既存の Active Directory フォレストに追加するには、フォレストの機能レベルが Windows Server 2003 以上である必要があります。 Windows Server 2008 R2、Windows Server 2008、または Windows Server 2003 を実行するドメイン コントローラーは同じフォレストで動作しますが、Windows 2000 Server を実行するドメイン コントローラーはサポートされていないため、Windows Server 2012 を実行するドメイン コントローラーのインストールをブロックします。 Windows Server 2003 以降を実行するドメイン コントローラーがフォレストに含まれており、フォレストの機能レベルが Windows 2000 のレベルである場合も、インストールがブロックされます。

Windows 2000 のドメイン コントローラーは、フォレストに Windows Server 2012 のドメイン コントローラーを追加する前に削除する必要があります。 この場合、次に示すワークフローを検討してください。

1. Windows Server 2003 以降を実行するドメイン コントローラーをインストールします。 これらのドメイン コントローラーは、Windows Server の評価版に展開できます。 この手順では、前提条件として、オペレーティング システムに応じた [adprep.exe の実行](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd464018(v=ws.10)) も必要です。
2. Windows 2000 ドメイン コントローラーを削除します。 具体的には、Windows Server 2000 ドメイン コントローラーをドメインから正常に降格するか強制的に削除し、Active Directory ユーザーとコンピューターを使用して、削除されたすべてのドメイン コントローラーのドメイン コントローラー アカウントを削除します。
3. フォレストの機能レベルを Windows Server 2003 以上に昇格します。
4. Windows Server 2012 を実行するドメイン コントローラーをインストールします。
5. 以前のバージョンの Windows Server を実行するドメイン コントローラーを削除することはできません。

新しい Windows Server 2012 ドメインの機能レベルでは、1つの新機能が有効になります。 **kdc で信頼性情報、複合認証、および Kerberos 防御をサポート**する kdc 管理用テンプレートポリシーには、Windows Server 2012 ドメインの機能レベルを必要とする2つの設定 (**常に**要求を提供し、**防御認証を要求**します) があります。

Windows Server 2012 フォレストの機能レベルでは新しい機能は提供されませんが、フォレスト内に作成された新しいドメインは、Windows Server 2012 ドメインの機能レベルで自動的に動作するようになります。 Windows Server 2012 ドメインの機能レベルでは、KDC が信頼性情報、複合認証、および Kerberos 防御をサポートする以外に、他の新機能は提供されません。 ただし、ドメイン内のすべてのドメインコントローラーが Windows Server 2012 を実行していることを確認します。 別の機能レベルで使用できる他の機能の詳細については、「 [AD DS の機能レベルとは](../active-directory-functional-levels.md)」を参照してください。

フォレストの機能レベルを特定の値に設定した後で、フォレストの機能レベルをロールバックしたり下げたりすることはできません。ただし、次の例外があります。フォレストの機能レベルを Windows Server 2012 に上げると、Windows Server 2008 R2 に下げることができます。 Active Directory のごみ箱が有効になっていない場合は、フォレストの機能レベルを Windows Server 2012 から Windows server 2008 R2 または windows Server 2008 に下げるか、windows server 2008 R2 から Windows Server 2008 に戻すことができます。 フォレストの機能レベルが Windows Server 2008 R2 に設定されている場合、たとえば Windows Server 2003 にロールバックすることはできません。

ドメインの機能レベルを特定の値に設定した後、ドメインの機能レベルをロールバックしたり下げたりすることはできません。ただし、次の例外があります。ドメインの機能レベルを Windows Server 2008 R2 または Windows Server 2012 に上げると、フォレストの機能レベルが Windows Server 2008 以下である場合、ドメインの機能レベルを Windows Server 2008 または Windows Server 2008 R2 にロールバックすることができます ドメインの機能レベルを下げることができるのは、Windows Server 2012 から windows server 2008 R2 または windows Server 2008、または Windows server 2008 R2 から Windows Server 2008 に限定されます。 ドメインの機能レベルが Windows Server 2008 R2 に設定されている場合、たとえば Windows Server 2003 にロールバックすることはできません。

低い機能レベルで使用できる機能の詳細については、「 [AD DS の機能レベルとは](../active-directory-functional-levels.md)」を参照してください。

Windows Server 2012 を実行するドメインコントローラーは、機能レベル以外にも、以前のバージョンの Windows Server を実行しているドメインコントローラーでは使用できない追加機能を提供します。 たとえば、Windows Server 2012 を実行するドメインコントローラーは仮想ドメインコントローラーの複製に使用できますが、以前のバージョンの Windows Server を実行するドメインコントローラーは使用できません。 ただし、Windows Server 2012 の仮想ドメインコントローラーの複製と仮想ドメインコントローラーの保護には、機能レベルの要件はありません。

> [!NOTE]
> Microsoft Exchange Server 2013 では、フォレストの機能レベルとして Windows server 2003 以上が必要です。

## <a name="ad-ds-interoperability-with-other-server-roles-and-windows-operating-systems"></a><a name="BKMK_ServerRoles"></a>他のサーバー役割および Windows オペレーティング システムとの AD DS の相互運用性

AD DS は、次の Windows オペレーティング システムではサポートされません。

- Windows MultiPoint Server
- Windows Server 2012 Essentials

次のサーバー役割または役割サービスを実行するサーバーに、AD DS をインストールすることはできません。

- Hyper-V Server
- リモート デスクトップ接続ブローカー

## <a name="operations-master-roles"></a><a name="BKMK_OpsMasters"></a>操作マスターの役割

Windows Server 2012 の一部の新機能は、操作マスターの役割に影響します。

- PDC エミュレーターは、仮想ドメインコントローラーの複製をサポートするために、Windows Server 2012 を実行している必要があります。 DC の複製については、追加の前提条件があります。 詳細については、「 [Active Directory ドメイン サービス (AD DS) の仮想化](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd464018(v=ws.10))」を参照してください。
- PDC エミュレーターが Windows Server 2012 を実行すると、新しいセキュリティプリンシパルが作成されます。
- RID マスターには、新しい RID 発行および監視機能があります。 機能強化には、イベント ロギングの向上、適切な制限の向上、緊急時における RID プール割り当て全体の 1 ビット増加などがあります。 詳細については、「[RID 発行の管理](../../ad-ds/manage/Managing-RID-Issuance.md)」を参照してください。

> [!NOTE]
> これらは操作マスターの役割ではありませんが、AD DS インストールにおけるもう1つの変更として、DNS サーバーの役割とグローバルカタログが、Windows Server 2012 を実行するすべてのドメインコントローラーに既定でインストールされます。

## <a name="virtualizing-domain-controllers"></a><a name="BKMK_Virtual"></a>ドメイン コントローラーの仮想化

Windows Server 2012 以降の AD DS の機能強化により、ドメインコントローラーの仮想化がより安全になり、ドメインコントローラーを複製できるようになりました。 同様に、ドメイン コントローラーを複製することで、新しいドメインに追加のドメイン コントローラーを迅速に展開できるなどのメリットがあります。 詳細については、「 [Active Directory Domain Services &#40;AD DS&#41; 仮想化 &#40;レベル 100&#41;の概要」を](../../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md)参照してください。

## <a name="administration-of-windows-server-2012-servers"></a><a name="BKMK_Admin"></a>Windows Server 2012 サーバーの管理

Windows [8 のリモートサーバー管理ツール](https://www.microsoft.com/download/details.aspx?id=28972)を使用して、windows Server 2012 を実行するドメインコントローラーやその他のサーバーを管理します。 Windows 8 を実行しているコンピューターで Windows Server 2012 リモートサーバー管理ツールを実行することができます。

## <a name="application-compatibility"></a><a name="BKMK_AppCompat"></a>アプリケーションの互換性

次の表は、Active Directory が統合されている一般的な Microsoft アプリケーションの一覧です。 アプリケーションをインストールできる Windows Server のバージョンと、Windows Server 2012 DC の導入がアプリケーションの互換性に影響するかどうかが示されています。

|Product|メモ|
|-----------|---------|
|[Microsoft SharePoint 2010](https://support.microsoft.com/kb/2724471)|をインストールして操作するには、SharePoint 2010 Service Pack 2 が必要です。 <br />Windows Server 2012 サーバー上の SharePoint 2010<p>SharePoint 2010 Foundation を Windows Server 2012 サーバーにインストールして操作するには、SharePoint 2010 Foundation Service Pack 2 が必要です。<p>SharePoint Server 2010 (Service Pack なし) を Windows Server 2012 にインストールするプロセスは失敗します。<p>SharePoint Server 2010 の前提条件インストーラー (PrerequisiteInstaller.exe) は、"このプログラムには互換性の問題があります" というエラーが発生して失敗します。 [ヘルプを表示せずにプログラムを実行する] をクリックすると、Windows Server 2012 に sharepoint Server 2010 (service pack がインストールされていない &#124;) をインストールできないことを確認するエラーが表示されます。|
|[Microsoft SharePoint 2013](/SharePoint/install/hardware-and-software-requirements-0)|ファーム内のデータベース サーバーの最小要件:<p>64 ビット エディションの Windows Server 2008 R2 Service Pack 1 (SP1) Standard、Enterprise、または Datacenter、あるいは 64 ビット エディションの Windows Server 2012 Standard または Datacenter<p>組み込みデータベースを持つ単一サーバーの最小要件:<p>64 ビット エディションの Windows Server 2008 R2 Service Pack 1 (SP1) Standard、Enterprise、または Datacenter、あるいは 64 ビット エディションの Windows Server 2012 Standard または Datacenter<p>ファーム内のフロントエンド Web サーバーおよびアプリケーション サーバーの最小要件:<p>64 ビット エディションの Windows Server 2008 R2 Service Pack 1 (SP1) Standard、Enterprise、または Datacenter、あるいは 64 ビット エディションの Windows Server 2012 Standard または Datacenter|
|[Configuration Manager 2012](/SharePoint/install/hardware-and-software-requirements-0)|Configuration Manager 2012 Service Pack 1:<p>Service Pack 1 のリリースで、クライアント サポート マトリックスに次のオペレーティング システムが追加されます。<p>-Windows 8 Pro<br />-Windows 8 Enterprise<br />-Windows Server 2012 Standard<br />-Windows Server 2012 Datacenter<p>サイト サーバーの役割はすべて (サイト サーバー、SMS プロバイダー、管理ポイントを含めて)、次のオペレーティング システム エディションのサーバーに展開できます。<p>-Windows Server 2012 Standard<br />-Windows Server 2012 Datacenter|
|[Microsoft エンドポイント Configuration Manager (現在のブランチ)](/configmgr/core/plan-design/configs/supported-configurations)|[Configuration Manager サイトシステムサーバーでサポートされているオペレーティングシステム](/configmgr/core/plan-design/configs/supported-operating-systems-for-site-system-servers)。|
|[Microsoft Lync Server 2013](/lyncserver/lync-server-2013-server-and-tools-operating-system-support)|Lync Server 2013 には、Windows Server 2008 R2 または Windows Server 2012 が必要です。 Server Core インストールで実行することはできません。 [仮想サーバー](/lyncserver/lync-server-2013-running-lync-server-on-virtual-servers)で実行できます。|
|[Lync Server 2010](https://support.microsoft.com/kb/2777359)|[Lync Server 用の累積的更新プログラム (2012 年 10 月)](https://support.microsoft.com/?kbid=2493736) がインストールされていれば、新しい (アップグレードされていない) Windows Server 2012 のインストールに Lync Server 2010 をインストールすることができます。 Lync Server 2010 の既存インストールのためにオペレーティング システムを Windows Server 2012 にアップグレードすることはできません。 Microsoft Lync Server 2010 グループ チャット サーバーも、Windows Server 2012 ではサポートされていません。|
|[System Center 2012 Endpoint Protection](/SharePoint/install/hardware-and-software-requirements-0)|System Center 2012 Endpoint Protection Service Pack 1 では、クライアント サポート マトリックスが更新され、次のオペレーティング システムが追加されます。<p>-Windows 8 Pro<br />-Windows 8 Enterprise<br />-Windows Server 2012 Standard<br />-Windows Server 2012 Datacenter|
|[System Center 2012 Forefront Endpoint Protection](/SharePoint/install/hardware-and-software-requirements-0)|FEP 2010 更新プログラム ロールアップ 1 では、クライアント サポート マトリックスが更新され、次のオペレーティング システムが追加されます。<p>-Windows 8 Pro<br />-Windows 8 Enterprise<br />-Windows Server 2012 Standard<br />-Windows Server 2012 Datacenter|
|Forefront Threat Management Gateway (TMG)|TMG の実行がサポートされているのは、Windows Server 2008 および Windows Server 2008 R2 のみです。 詳細については、「 [Forefront TMG のシステム要件](/previous-versions/tn-archive/dd896981(v=technet.10))」を参照してください。|
|Windows Server Update Services|このリリースの WSUS では既に、Windows 8 ベースのコンピューターまたは Windows Server 2012 コンピューターがクライアントとしてサポートされています。|
|Windows Server Update Services 3.0|更新プログラムサポート技術情報の記事[2734608](https://support.microsoft.com/kb/2734608)では、WINDOWS SERVER UPDATE SERVICES (wsus) 3.0 SP2 を実行しているサーバーで、windows 8 または windows server 2012 を実行しているコンピューターの更新プログラムを提供します。**注:** スタンドアロンの wsus 3.0 sp2 環境がある場合、または wsus 2007 sp2 を使用する Configuration Manager 3.0 Service Pack 2 環境の場合[は、windows](https://support.microsoft.com/kb/2734608) 8 ベース|
|[Exchange 2013](/Exchange/plan-and-deploy/prerequisites?view=exchserver-2019)|Windows Server 2012 Standard および Datacenter は、次の役割に対してサポートされています: スキーマ マスター、グローバル カタログ サーバー、ドメイン コントローラー、メールボックス サーバー、クライアント アクセス サーバー<p>フォレストの機能レベル:Windows Server 2003 以降<p>ソース:Exchange 2013 のシステム要件|
|Exchange 2010|[ソース:Exchange 2010 Service Pack 3](https://techcommunity.microsoft.com/t5/exchange-team-blog/bg-p/Exchange)<p>Exchange 2010 Service Pack 3 は、Windows Server 2012 メンバー サーバーにインストールできます。<p>[Exchange 2010 のシステム要件](/previous-versions/office/exchange-server-2010/aa996719(v=exchg.141)) には、サポートされている最新のスキーマ マスター、グローバル カタログ、およびドメイン コントローラーとして Windows Server 2008 R2 が記載されています。<p>フォレストの機能レベル:Windows Server 2003 以降|
|SQL Server 2012|ソース:サポート技術情報 [2681562](https://support.microsoft.com/kb/2681562)<p>Windows Server 2012 では SQL Server 2012 RTM がサポートされています。|
|SQL Server 2008 R2|ソース:サポート技術情報 [2681562](https://support.microsoft.com/kb/2681562)<p>Windows Server 2012 にインストールするには、SQL Server 2008 R2 Service Pack 1 以上が必要です。|
|SQL Server 2008|ソース:サポート技術情報 [2681562](https://support.microsoft.com/kb/2681562)<p>Windows Server 2012 にインストールするには、SQL Server 2008 Service Pack 3 以上が必要です。|
|SQL Server 2005|ソース:サポート技術情報 [2681562](https://support.microsoft.com/kb/2681562)<p>Windows Server 2012 へのインストールがサポートされていません。|

## <a name="known-issues"></a><a name="BKMK_KnownIssues"></a>既知の問題

AD DS のインストールに関する既知の問題を次の表に示します。

| サポート技術情報の記事番号とタイトル | 影響を受けるテクノロジ エリア | 問題点/説明 |
|--|--|--|
| [2830145](https://support.microsoft.com/kb/2830145):ドメイン環境の Windows 7 または Windows Server 2008 R2 ベースのコンピューター上で SID S-1-18-1 および SID S-1-18-2 をマップできない | AD DS の管理/アプリケーションの互換性 | Windows Server 2012 の新機能である SID S-1-18-1 および SID S-1-18-2 をマップするアプリケーションは失敗する可能性があります。それらの SID を Windows 7 ベースまたは Windows Server 2008 R2 ベースのコンピューター上で解決できないためです。 この問題を解決するには、ドメイン内の Windows 7 ベースおよび Windows Server 2008 R2 ベースのコンピューターに修正プログラムをインストールしてください。 |
| [2737129](https://support.microsoft.com/kb/2737129):Windows Server 2012 の既存のドメインを自動的に準備した場合、グループ ポリシーの準備が実行されない | AD DS のインストール | Windows Server 2012 を実行するドメイン内の最初の DC をインストールする場合、adprep /domainprep /gpprep は、インストールの一部として自動的には実行されません。 ドメイン内でそれまでに実行したことがない場合は、手動で実行する必要があります。 |
| [2737416](https://support.microsoft.com/kb/2737416):Windows PowerShell ベースのドメイン コントローラーの展開で、警告が繰り返し表示される | AD DS のインストール | 警告は、前提条件の確認時に表示され、インストール中に再度表示されることがあります。 |
| [2737424](https://support.microsoft.com/kb/2737424):ドメイン コントローラーから Active Directory ドメイン サービスを削除しようとすると、"指定されたドメイン名の形式は無効です" エラーが発生する | AD DS のインストール | 事前作成された RODC アカウントがまだ存在する場合にドメイン内で最後の DC を削除しようとすると、このエラーが表示されます。 Windows Server 2012、Windows Server 2008 R2、および Windows Server 2008 に影響します。 |
| [2737463](https://support.microsoft.com/kb/2737463):ドメイン コントローラーが起動しない、c00002e2 エラーが発生する、または "オプションの選択" が表示される | AD DS のインストール | DC が起動しないのは、管理者が Dism.exe、Pkgmgr.exe、または Ocsetup.exe を使用して DirectoryServices-DomainController 役割を削除したためです。 |
| [2737516](https://support.microsoft.com/kb/2737516):Windows Server 2012 サーバー マネージャーでの IFM による検証の制限 | AD DS のインストール | サポート技術情報の記事に記載されているように、IFM による検証には制限があります。 |
| [2737535](https://support.microsoft.com/kb/2737535):Install-AddsDomainController コマンドレットから、RODC のパラメーター セット エラーが返される | AD DS のインストール | 事前作成済みの RODC アカウントに対して指定済みの引数を指定してサーバーを RODC アカウントに関連付けようとすると、エラーが発生することがあります。 |
| [2737560](https://support.microsoft.com/kb/2737560):"交換スキーマ競合チェックを実行できません" エラーが発生し、前提条件のチェックに失敗する | AD DS のインストール | 既存のドメイン内で最初の Windows Server 2012 DC を構成する際に、前提条件のチェックに失敗します。これは、Network Service に対する SeServiceLogonRight が DC にないため、あるいは WMI または DCOM プロトコルがブロックされているためです。 |
| [2737797](https://support.microsoft.com/kb/2737797):AddsDeployment モジュールに -Whatif 引数が指定されている場合に表示される DNS 結果に誤りがある | AD DS のインストール | -WhatIf パラメーターを指定すると、DNS サーバーはインストールされませんが、のように表示されます。 |
| [2737807](https://support.microsoft.com/kb/2737807):[ドメイン コントローラー オプション] ページで [次へ] ボタンを使用できない | AD DS のインストール | [ドメイン コントローラー オプション] ページの [次へ] ボタンが無効になっているのは、ターゲット DC の IP アドレスが既存のサブネットまたはサイトにマップされていないためか、DSRM パスワードの入力と確認が正しく行われていないためです。 |
| [2737935](https://support.microsoft.com/kb/2737935):Active Directory のインストールが "NTDS 設定オブジェクトを作成しています" の段階で動作しなくなる | AD DS のインストール | インストールがハングするのは、ローカルの Administrator パスワードがドメインの Administrator パスワードと一致するためか、ネットワークの問題によって重要なレプリケーションが完了しないためです。 |
| [2738060](https://support.microsoft.com/kb/2738060):Install-AddsDomain を使用してリモートで子ドメインを作成すると、"アクセスが拒否されました" エラー メッセージが表示される | AD DS のインストール | Install-ADDSDomain を Invoke-Command コマンドレットと共に実行した場合に、DNSDelegationCredential に指定されたパスワードに問題があると、エラーが発生します。 |
| [2738697](https://support.microsoft.com/kb/2738697):サーバー マネージャーを使用してサーバーを構成すると、ドメイン コントローラーの構成エラー "サーバーは使用可能ではありません" が発生する | AD DS のインストール | ワークグループ コンピューターに AD DS をインストールしようとすると、このエラーが発生します。これは、NTLM 認証が無効になっているためです。 |
| [2738746](https://support.microsoft.com/kb/2738746):ローカル管理者ドメイン アカウントにログオンした後に、アクセス拒否エラーが発生する | AD DS のインストール | 組み込みの Administrator アカウントではなくローカルの Administrator アカウントを使用してログオンし、新しいドメインを作成した場合、このアカウントは Domain Admins グループに追加されません。 |
| [2743345](https://support.microsoft.com/kb/2743345):adprep /gpprep エラー "指定されたファイルが見つかりません" が表示されるか、ツールがクラッシュする | AD DS のインストール | このエラーは、インフラストラクチャ マスターにより実装されている名前空間が不適切であるために、adprep /gpprep を実行したときに発生します。 |
| [2743367](https://support.microsoft.com/kb/2743367):64 ビット バージョンの Windows Server 2003 で、Adprep に対する "有効な Win32 アプリケーションではありません" エラーが発生する | AD DS のインストール | Windows Server 2012 Adprep は Windows Server 2003 で実行できないために、このエラーが発生します。 |
| [2753560](https://support.microsoft.com/kb/2753560):Windows Server 2012 で ADMT 3.2 と PES 3.1 のインストール エラーが発生する | ADMT | 設計上、ADMT 3.2 は Windows Server 2012 にインストールできません。 |
| [2750857](https://support.microsoft.com/kb/2750857):Internet Explorer 10 で、DFS レプリケーション診断レポートが正しく表示されない | DFS レプリケーション | Internet Explorer 10 での変更のため、DFS レプリケーション診断レポートが正しく表示されません。 |
| [2741537](https://support.microsoft.com/kb/2741537):リモートでのグループ ポリシーの更新がユーザーに対して表示される | グループ ポリシー | この状況は、スケジュールされたタスクが、ログオンしている各ユーザーのコンテキストで実行されることが原因で発生します。 Windows タスク スケジューラの仕様により、このシナリオでは対話的なプロンプトが必要です。 |
| [2741591](https://support.microsoft.com/kb/2741591):GPMC のインフラストラクチャ状態オプションで、SYSVOL に ADM ファイルが存在しない | グループ ポリシー | GPMC インフラストラクチャの状態は、カスタマイズされたフィルター処理規則に従っていないため、GP レプリケーションは "レプリケーションが進行中です" を報告できます。 |
| [2737880](https://support.microsoft.com/kb/2737880):AD DS の構成操作中に "サービスを開始できません" エラーが発生する | 仮想 DC の複製 | このエラーは、DS 役割サーバー サービスが無効になっているために、AD DS のインストール、削除、または複製の実行中に発生します。 |
| [2742836](https://support.microsoft.com/kb/2742836):VDC 複製機能の使用時に、各ドメイン コントローラーに対して DHCP リースが 2 つ作成される | 仮想 DC の複製 | この状況は、複製されたドメイン コントローラーが、複製前にもクローンの完了時にもリースを受け取ることが原因で発生します。 |
| [2742844](https://support.microsoft.com/kb/2742844):Windows Server 2012 で、ドメイン コントローラーの複製に失敗し、サーバーが DSRM で再起動される | 仮想 DC の複製 | 複製された DC が DSRM で再起動されるのは、サポート技術情報の記事に記載されているさまざまな理由のいずれかによって複製に失敗したためです。 |
| [2742874](https://support.microsoft.com/kb/2742874):ドメイン コントローラーの複製で、すべてのサービス プリンシパル名が再作成されない | 仮想 DC の複製 | 複製された DC で 3 部構成の SPN のうち再作成されないものがあるのは、ドメイン名の変更プロセスの制限が原因です。 |
| [2742908](https://support.microsoft.com/kb/2742908):ドメイン コントローラーの複製後に、"使用可能なログオン サーバーがない" というエラーが発生する | 仮想 DC の複製 | このエラーは、仮想 DC の複製後にログオンしようとすると発生します。これは、複製に失敗し、DC が DSRM で起動されたことが原因です。 複製の失敗に対するトラブルシューティングを行うには、.\administrator としてログオンしてください。 |
| [2742916](https://support.microsoft.com/kb/2742916):ドメイン コントローラーの複製に失敗し、dcpromo.log 内にエラー 8610 が出力される | 仮想 DC の複製 | PDC エミュレーターがドメイン パーティションについて入力方向のレプリケーションを実行していない場合、複製が失敗します。原因としては、役割が転送されていないことが考えられます。 |
| [2742927](https://support.microsoft.com/kb/2742927):New-AdDcCloneConfig で "インデックスが範囲外です" エラーが発生する | 仮想 DC の複製 | このエラーは、仮想 DC の複製中、New-ADDCCloneConfigFile コマンドレットの実行後に発生します。コマンドレットが管理者特権のコマンド プロンプトで実行されていないか、アクセス トークンに Administrators グループが含まれていないことが原因です。 |
| [2742959](https://support.microsoft.com/kb/2742959):ドメイン コントローラーの複製に失敗し、エラー 8437 "このレプリケーション操作に対して、無効なパラメーターが指定されました" が発生する | 仮想 DC の複製 | 無効な複製名または重複した NetBIOS 名が指定されたことが原因で、複製に失敗しています。 |
| [2742970](https://support.microsoft.com/kb/2742970):DC の複製に失敗し、DSRM は発生せず、ソース コンピューターと複製コンピューターの重複が発生する | 仮想 DC の複製 | 複製された仮想 DC は、ソース DC の重複名を使用してディレクトリ サービス復元モード (DSRM) で起動されます。これは、DCCloneConfig.xml ファイルが正しい場所に作成されていないか、ソース DC が複製前に再起動されたことが原因です。 |
| [2743278](https://support.microsoft.com/kb/2743278):ドメイン コントローラーの複製エラー 0x80041005 | 仮想 DC の複製 | WINS サーバーが 1 つしか指定されていないために、複製された DC が DSRM で起動されます。 WINS サーバーを指定する場合は、優先 WINS サーバーと代替 WINS サーバーの両方を指定する必要があります。 |
| [2745013](https://support.microsoft.com/kb/2745013):Windows Server 2012 で New-AdDcCloneConfigFile を実行すると、エラー メッセージ "サーバーは使用可能ではありません" が表示される | 仮想 DC の複製 | このエラーは、サーバーがグローバル カタログ サーバーに接続できない場合に、New-ADDCCloneConfigFile コマンドレットの実行後に表示されます。 |
| [2747974](https://support.microsoft.com/kb/2747974):ドメイン コントローラーの複製イベント 2224 で不適切なガイダンスが表示される | 仮想 DC の複製 | イベント ID 2224 で表示される、管理されたサービス アカウントは複製前に削除する必要があるというメッセージは不適切です。 スタンドアロンの MSA は削除する必要がありますが、グループの MSA は複製をブロックしません。 |
| [2748266](https://support.microsoft.com/kb/2748266):Windows 8 へのアップグレード後、BitLocker の暗号化されたドライブのロックを解除できない | BitLocker | Windows 7 からアップグレードされたコンピューターでドライブのロックを解除しようとすると、"アプリケーションが見つかりません" というエラーが表示されます。 |

## <a name="see-also"></a>参照

[Windows Server 2012 評価](https://www.microsoft.com/en-us/evalcenter/)のためのリソース 
[Windows Server 2012 評価ガイド](https://download.microsoft.com/download/5/B/2/5B254183-FA53-4317-B577-7561058CEF42/WS%202012%20Evaluation%20Guide.pdf) 
[Windows Server 2012 をインストールして展開](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831620(v=ws.11))する
