---
ms.assetid: f964d056-11bf-4d9b-b5ab-dceaad8bfbc3
title: "Windows Server 2016 の機能レベル"
description: 
author: MicrosoftGuyJFlo
ms.author: joflore
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.custom: it-pro
ms.reviewer: maheshu
ms.technology: identity-adds
ms.openlocfilehash: a39955cf088ce7ce8bef20c70b83d49c6d508497
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="forest-and-domain-functional-levels"></a>フォレストとドメインの機能レベル

>Windows Server の適用対象:

Windows 2003 のライフ サイクルの最後に、Windows 2003 のドメイン コントローラー (Dc) 2012 または 2016、Windows Server 2008 に更新する必要があります。 その結果、Windows Server 2003 を実行している任意のドメイン コントローラーをドメインから削除する必要があります。 ドメインとフォレストの機能レベルは、発生するには、少なくとも、環境に追加されない以前のバージョンの Windows Server を実行するドメイン コントローラーを防ぐために Windows Server 2008 します。

お客様がこの作業の一環として、ドメインの機能レベル (DFL) とフォレストの機能レベル (FFL) を更新、2003 DFL と FFL は推奨されなくなりました Windows Server 2016 であり、将来的にサポートされるは不要になったために解放ことをお勧めします。

について追加の時間、DFL & FFL 2003 からの移行を評価する必要があるお客様、2003 DFL と FFL は、引き続き Windows 10 でサポートされ、ドメインおよびフォレスト内のすべてのドメイン コントローラー上にある Windows Server 2008、2008 r2、Windows Server 2016 が提供される、2012R2、2012 または 2016 します。

Windows Server 2008 とより高いドメイン機能レベルでは、分散ファイル サービス (DFS) レプリケーションを使用してドメイン コントローラー間で SYSVOL フォルダーの内容をレプリケートします。 Windows Server 2008 ドメインの機能レベルが以上に新しいドメインを作成する場合、DFS レプリケーションは自動的に SYSVOL をレプリケートする使用します。 低い機能レベルでドメインを作成した場合は、SYSVOL の DFS レプリケーションに FRS を使用してから移行する必要があります。 移行手順については、いずれかのフォローできます、 [TechNet の「手順](https://technet.microsoft.com/library/dd640019(v=WS.10).aspx)または参照することができます、[一連の記憶域チーム File Cabinet ブログ手順を合理化](http://blogs.technet.com/b/filecab/archive/2014/06/25/streamlined-migration-of-frs-to-dfsr-sysvol.aspx)します。

Windows Server 2003 のドメインとフォレストの機能レベルは引き続きサポートされますが、組織が Windows Server 2008 (または可能であれば、高い) の機能レベルを上げる必要がありますを SYSVOL レプリケーションの互換性を確保し、将来的にサポートします。 さらがあるその他の多くの利点と機能、上位の機能レベルでより高い。 詳細については、次のリソースを参照してください。

## <a name="windows-server-2016"></a>Windows Server 2016

ドメイン コントローラーのオペレーティング システムがサポートされています。

* Windows Server 2016

### <a name="windows-server-2016-forest-functional-level-features"></a>Windows Server 2016 のフォレスト機能レベルの機能

* すべての Windows Server 2012R2 フォレストの機能レベルで使用できる機能と、次の機能を利用できます。
    * [Privileged access management (PAM) Microsoft Identity Manager (MIM) を使用する](https://docs.microsoft.com/windows-server/identity/whats-new-active-directory-domain-services#a-namebkmkpamaprivileged-access-management)

### <a name="windows-server-2016-domain-functional-level-features"></a>Windows Server 2016 ドメイン機能レベルの機能

* 既定の Active Directory 機能をすべて、Windows Server 2012R2 ドメインの機能レベルですべての機能に加えて、次の機能:
    * Dc では、公開キーのみユーザーの NTLM シークレットをロールバックをサポートできます。 
    * Dc は、ユーザーがドメインに参加しているデバイスの特定に制限されているときにすることがネットワーク NTLM をサポートできます。 
    * 鮮度拡張子を持つ認証が成功する Kerberos クライアントでは、新しい公開キー ID SID を取得します。

    詳細については、次を参照してください[Kerberos 認証の新](https://docs.microsoft.com/windows-server/security/kerberos/whats-new-in-kerberos-authentication)と[資格情報の保護の新機能。](https://docs.microsoft.com/windows-server/security/credentials-protection-and-management/whats-new-in-credential-protection)

## <a name="windows-server-2012r2"></a>Windows Server 2012R2

ドメイン コントローラーのオペレーティング システムがサポートされています。

* Windows Server 2016
* Windows Server 2012 R2

### <a name="windows-server-2012r2-forest-functional-level-features"></a>Windows Server 2012R2 フォレスト機能レベルの機能

* すべての機能、Windows Server 2012 で使用可能なフォレストの機能レベルではない追加機能。

### <a name="windows-server-2012r2-domain-functional-level-features"></a>Windows Server 2012R2 ドメイン機能レベルの機能

* 既定の Active Directory 機能をすべて、Windows Server 2012 ドメインの機能レベルのすべての機能に加えて、次の機能:
    * Protected Users に対する DC 側の保護。 保護されているドメインが不要になったことができます、Windows Server 2012 R2 へのユーザーの認証。
        * NTLM 認証を使用します。
        * Kerberos 事前認証で DES または RC4 暗号スイートを使用してください。
        * 制約なし/制約付き委任を使用して委任します。
        * 最初の 4 時間の有効期間を超えるユーザー チケット (Tgt) を更新します。
    * 認証ポリシー
        * 新しいフォレストに基づいた Active Directory ポリシーでホストを管理する Windows Server 2012 R2 のドメインのアカウントに適用できますをアカウントからサインオンできアカウントとして実行されているサービスに認証のアクセス制御条件を適用できます。
    * 認証ポリシー サイロ
        * 新しいフォレストに基づいた Active Directory オブジェクト、ユーザー、管理されたサービスとコンピューター アカウントの認証ポリシーまたは認証の分離のための分類に使用されるアカウントを間の関係を作成することができます。

## <a name="windows-server-2012"></a>Windows Server 2012

ドメイン コントローラーのオペレーティング システムがサポートされています。

* Windows Server 2016
* Windows Server 2012 R2
* Windows Server 2012

### <a name="windows-server-2012-forest-functional-level-features"></a>Windows Server 2012 フォレスト機能レベルの機能

* すべての Windows Server 2008 R2 で利用できる機能はフォレスト機能レベルではない追加機能です。

### <a name="windows-server-2012-domain-functional-level-features"></a>Windows Server 2012 ドメイン機能レベルの機能

* 既定の Active Directory 機能をすべて、Windows Server 2008 r2 のドメインの機能レベルですべての機能に加えて、次の機能:
    * KDC で信頼性情報、複合認証、および Kerberos 防御 KDC 管理用テンプレート ポリシーが 2 つの設定 ([常に信頼性情報を提供および防御されていない認証要求を失敗) を Windows Server 2012 ドメインの機能レベルを必要とするをサポートします。 詳細については、次を参照してください[Kerberos 認証の新。](https://technet.microsoft.com/en-us/library/hh831747.aspx)

## <a name="windows-server-2008r2"></a>Windows Server 2008R2

ドメイン コントローラーのオペレーティング システムがサポートされています。

* Windows Server 2016
* Windows Server 2012 R2
* Windows Server 2012
* Windows Server 2008 R2

### <a name="windows-server-2008r2-forest-functional-level-features"></a>Windows Server 2008 r2 フォレスト機能レベルの機能

* すべての Windows Server 2003 で利用できる機能はフォレストの機能レベルと、次の機能。
    * Active Directory のごみ箱、AD DS の実行中に完全に削除されたオブジェクトを復元する機能を提供します。

### <a name="windows-server-2008r2-domain-functional-level-features"></a>Windows Server 2008 r2 のドメイン機能レベルの機能

* 既定の Active Directory 機能をすべて、Windows Server 2008 ドメインの機能レベルのすべての機能に加えて、次の機能:
    * 認証メカニズム保証を各ユーザーの Kerberos トークン内のドメイン ユーザーを認証に使用されるログオン方法 (スマート カードまたはユーザー名/パスワード) の種類に関する情報をパッケージ化します。 Active Directory フェデレーション サービス (AD FS) などのフェデレーション ID 管理インフラストラクチャを展開しているネットワーク環境でこの機能が有効にすると、ユーザーがユーザーのログオン方法に基づいて承認の判断に展開されている任意の要求対応ではアプリケーションへのアクセスを試みるたびに、トークンの情報は、しを抽出します。
    * 名前または DNS のホスト名、コンピューター アカウントの変更時に、管理されたサービス アカウントのコンテキストで特定のコンピューターで実行されているサービスの SPN の自動管理します。 管理されたサービス アカウントの詳細については、次を参照してください。[サービス アカウント Step-by-Step Guide](https://go.microsoft.com/fwlink/?LinkId=180401)します。

## <a name="windows-server-2008"></a>Windows Server 2008

ドメイン コントローラーのオペレーティング システムがサポートされています。

* Windows Server 2016
* Windows Server 2012 R2
* Windows Server 2012
* Windows Server 2008 R2
* Windows Server 2008

### <a name="windows-server-2008-forest-functional-level-features"></a>Windows Server 2008 フォレスト機能レベルの機能

* その他の機能はありませんが、すべての Windows Server 2003 フォレストの機能レベルで使用できる機能を利用できます。 

### <a name="windows-server-2008-domain-functional-level-features"></a>Windows Server 2008 ドメイン機能レベルの機能

* すべて既定の AD DS の機能、すべての Windows Server 2003 ドメイン機能レベルで機能し、次の機能を利用します。
    * 分散ファイル システム (DFS) レプリケーションのサポートを Windows Server 2003 システム ボリューム (SYSVOL)
        * DFS レプリケーションのサポートは、SYSVOL の内容より堅牢で詳細なレプリケーションを提供します。
        [!NOTE]>
        >Windows Server 2012 R2 以降では、ファイル レプリケーション サービス (FRS) は推奨されなくなりました。 以降を実行しているドメイン コントローラーで作成される新しいドメイン、Windows Server 2008 ドメインの機能レベルを以上、Windows Server 2012 R2 を設定する必要があります。

    * ドメイン ベース DFS 名前空間アクセス ベースの列挙とスケーラビリティの向上のサポートが含まれる Windows Server 2008 モードで実行されています。 Windows Server 2008 モードでドメイン ベース名前空間は、Windows Server 2003 フォレストの機能レベルを使用するフォレストにも必要です。 詳細については、次を参照してください。 [Namespace の種類を選択](https://go.microsoft.com/fwlink/?LinkId=180400)します。
    * Kerberos プロトコルの高度な (AES 128 および 256 の AES) 暗号化標準サポートします。 Tgt AES を使用して発行するためには、ドメインの機能レベルは Windows Server 2008 以上である必要があり、ドメイン パスワードを変更する必要があります。 
        * 詳細については、次を参照してください。 [Kerberos の強化](https://technet.microsoft.com/library/cc749438(ws.10).aspx)します。
        [!NOTE]>
        >認証エラーが発生するドメイン コントローラーを Windows Server 2008 またはそれ以上のドメインの機能レベルが発生した後、ドメイン コントローラーが DFL 変更が既にレプリケートされたが krbtgt パスワードはまだ更新していないかどうか。 ここでは、ドメイン コントローラー上で KDC サービスの再起動は、メモリ内で新しい krbtgt パスワードの更新をトリガし、関連する認証エラーを解決します。

    * [前回の対話型ログオン](https://go.microsoft.com/fwlink/?LinkId=180387)情報には、次の情報が表示されます。
        * Windows Server 2008 ドメインに参加しているサーバーまたは Windows Vista ワークステーションで失敗したログオン試行の合計数
        * Windows Server 2008 サーバーまたは Windows Vista ワークステーションに成功したログオン後に失敗したログオン試行の合計数
        * Windows Server 2008 または Windows Vista ワークステーションで前回の失敗したログオン試行の時刻
        * Windows Server 2008 サーバーまたは Windows Vista ワークステーションで前回成功したログオンの時刻の試行します。
    * 詳細なパスワード ポリシーでは、ドメイン内のユーザーおよびグローバル セキュリティ グループのパスワードとアカウント ロックアウトのポリシーを指定できます。 詳細については、次を参照してください。[細かいパスワードおよびアカウント ロックアウトのポリシー構成のステップ バイ ステップ ガイド](https://go.microsoft.com/fwlink/?LinkID=91477)します。
    * 個人用仮想デスクトップ
        * Windows Server 2008 R2 の Active Directory ユーザーとコンピューターのユーザー アカウントのプロパティ] ダイアログ ボックスで、[個人用仮想デスクトップ] タブで提供される追加の機能を使用する、AD DS スキーマを拡張する必要があります (スキーマ オブジェクト バージョン = 47)。 詳細については、次を参照してください。[を展開する個人用仮想デスクトップを使用して RemoteApp とデスクトップ接続によって Step-by-Step Guide](https://go.microsoft.com/fwlink/?LinkId=183552)します。

## <a name="windows-server-2003"></a>Windows Server 2003

ドメイン コントローラーのオペレーティング システムがサポートされています。

* Windows Server 2012 R2
* Windows Server 2012
* Windows Server 2008 R2
* Windows Server 2008
* Windows Server 2003

### <a name="windows-server-2003-forest-functional-level-features"></a>Windows Server 2003 フォレスト機能レベルの機能

* すべての既定の AD DS の機能と、次の機能を利用できます。
    * フォレストの信頼
    * ドメイン名の変更
    * リンクされた値のレプリケーション
        - リンクされた値のレプリケーションを保存し、値を 1 つの単位としてメンバーシップ全体をレプリケートする代わりに、個々 のメンバーにレプリケートするグループのメンバーシップを変更できます。 保存して、個々 のメンバーの値をレプリケートするより少ないネットワーク帯域幅と、レプリケーション中に少ないプロセッサ サイクルを使用してし、を追加または別のドメイン コントローラーで同時に複数のメンバーを削除する場合は、更新プログラムを失うことができなきます。
    * 読み取り専用ドメイン コントローラー (RODC) を展開する機能
    * 知識整合性チェッカー (KCC) アルゴリズムおよびスケーラビリティの向上
        - サイト間トポロジ ジェネレーター (ISTG) は、AD DS は、Windows 2000 フォレストの機能レベルでサポートできるより多くのサイトを持つフォレストをサポートする拡張強化されたアルゴリズムを使用します。 強化された ISTG 選択アルゴリズムは、Windows 2000 フォレストの機能レベルで ISTG を選ぶためそれほど高過ぎないメカニズムです。
    * という名前の動的な補助型クラスのインスタンスを作成する機能**dynamicObject**ドメイン ディレクトリ パーティション
    * 変換する機能、 **inetOrgPerson**オブジェクトのインスタンスへの**ユーザー**オブジェクトのインスタンスを逆方向に変換を完了します。
    * 役割ベースの承認をサポートするために新しいグループの種類のインスタンスを作成する機能。 
        - これらの種類はアプリケーション基本グループおよび LDAP クエリ グループと呼ばれます。
    * 非アクティブ化と属性およびクラスのスキーマの再定義します。 次の属性を再利用できます: および ldapDisplayName、schemaIdGuid、OID と mapiID します。
    * ドメイン ベース DFS 名前空間アクセス ベースの列挙とスケーラビリティの向上のサポートが含まれる Windows Server 2008 モードで実行されています。 詳細については、次を参照してください。 [Namespace の種類を選択](https://go.microsoft.com/fwlink/?LinkId=180400)します。

### <a name="windows-server-2003-domain-functional-level-features"></a>Windows Server 2003 ドメイン機能レベルの機能

* 既定の AD DS の機能をすべて、Windows 2000 ネイティブ ドメインの機能レベルで使用できるすべての機能と、次の機能を使用できます。
    * ドメインの管理ツール Netdom.exe、ドメイン コントローラーの名前を変更できるようになりますが
    * ログオン タイムスタンプを更新します。
        * **LastLogonTimestamp**属性は、ユーザーまたはコンピューターの最後のログオン時に更新します。 この属性は、ドメイン内でレプリケートされます。
    * 設定する機能、 **userPassword**で有効なパスワードとして属性**inetOrgPerson**とユーザー オブジェクト
    * ユーザーとコンピューターをリダイレクトする機能のコンテナー
        * コンピューターとユーザーのアカウントを格納する既定では、2 つのよく知られているコンテナーが提供されている、cn = コンピューター、<domain root>および cn = Users,<domain root>します。 この機能は、これらのアカウントのよく知られている、新しい場所の定義を使用します。
    * AD DS 内の承認ポリシーを保存する承認マネージャーの機能
    * 制約付き委任
        * 制約付き委任できるようになりますアプリケーションを利用するためにユーザーの資格情報のセキュリティで保護された委任の Kerberos ベースの認証を使用します。
        * 特定の宛先サービスのみへの委任を制限することができます。
    * 認証の選択
        * 認証の選択により、ユーザーおよび信頼する側のフォレスト内のリソース サーバーに対する認証を許可されている信頼されたフォレストからのグループを指定することはなります。

## <a name="windows-2000"></a>Windows 2000

ドメイン コントローラーのオペレーティング システムがサポートされています。

* Windows Server 2008 R2
* Windows Server 2008
* Windows Server 2003
* Windows 2000

### <a name="windows-2000-native-forest-functional-level-features"></a>Windows 2000 ネイティブのフォレスト機能レベルの機能

* すべての既定の AD DS の機能を利用できます。

### <a name="windows-2000-native-domain-functional-level-features"></a>Windows 2000 ネイティブ ドメイン機能レベルの機能

* すべての既定の AD DS の機能と、次のディレクトリ機能が利用可能なを含みます。
    * 両方の配布とセキュリティ グループのユニバーサル グループ。
    * グループの入れ子
    * セキュリティ グループと配布グループ間の変換は、グループの変換
    * セキュリティ識別子 (SID) の履歴

## <a name="next-steps"></a>次の手順

* [ドメインの機能レベルを上げる](https://technet.microsoft.com/library/cc753104.aspx)  
* [フォレストの機能レベルを上げる](https://technet.microsoft.com/library/cc730985.aspx)
