---
ms.assetid: f964d056-11bf-4d9b-b5ab-dceaad8bfbc3
title: Windows Server 2016 の機能レベル
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 10/29/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.custom: it-pro
ms.reviewer: maheshu
ms.technology: identity-adds
ms.openlocfilehash: ea56c718394d145a36145d32e5769661a62efd56
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841003"
---
# <a name="forest-and-domain-functional-levels"></a>フォレストおよびドメイン機能レベル

>適用先:Windows Server

機能レベルでは、使用可能な Active Directory Domain Services (AD DS) ドメインまたはフォレストの機能を決定します。 また、ドメインまたはフォレストのドメイン コント ローラーで実行できる Windows Server オペレーティング システムを決定します。 ただし、機能レベルは、どのワークステーションで実行できるオペレーティング システムとドメインまたはフォレストに参加しているメンバー サーバーには影響しません。

AD DS を展開するときに、お客様の環境をサポートできる最大値に、ドメインおよびフォレスト機能レベルを設定します。 これにより、できるだけ多くの AD DS の機能を使用できます。 新しいフォレストを展開するときに、フォレストの機能レベルを設定して、ドメインの機能レベルを設定するように求められます。 フォレストの機能レベルよりも高い値に、ドメインの機能レベルを設定できますが、フォレストの機能レベルよりも小さい値に、ドメインの機能レベルを設定することはできません。

Windows 2003 のドメイン コント ローラー (Dc) を Windows 2003 の有効期間の終了時に、2012、Windows server 2008、2008R2、更新する必要があります 2012R2、2016、または 2019 します。 その結果、Windows Server 2003 を実行している任意のドメイン コント ローラーをドメインから削除する必要があります。

Windows Server 2008 以上のドメイン機能レベルでは、分散ファイル システム (DFS) レプリケーションを使用して、ドメイン コント ローラー間の SYSVOL フォルダーの内容をレプリケートします。 以降、Windows Server 2008 のドメイン機能レベルで新しいドメインを作成すると、SYSVOL をレプリケートする DFS レプリケーションが自動的に使用します。 低い機能レベル ドメインを作成した場合は、SYSVOL の DFS レプリケーションに FRS を使用してから移行する必要があります。 移行手順については、いずれかに従ってできます、 [technet プロシージャ](https://technet.microsoft.com/library/dd640019(v=WS.10).aspx)または参照できる、[ストレージ チームのファイル キャビネット ブログでの手順のセットを簡素化](http://blogs.technet.com/b/filecab/archive/2014/06/25/streamlined-migration-of-frs-to-dfsr-sysvol.aspx)。

## <a name="windows-server-2019"></a>Windows Server 2019

新しいフォレストやこのリリースで追加のドメイン機能レベルはありません。

Windows Server 2019 ドメイン コント ローラーを追加する最小要件では、Windows Server 2008 r2 の機能レベルです。

## <a name="windows-server-2016"></a>Windows Server 2016

ドメイン コント ローラーのオペレーティング システムがサポートされています。

* Windows Server 2019
* Windows Server 2016

### <a name="windows-server-2016-forest-functional-level-features"></a>Windows Server 2016 フォレスト機能レベルの機能

* すべての Windows Server 2012R2 のフォレストの機能レベルで利用できる機能と、次の機能を使用できます。
   * [Microsoft Identity Manager (MIM) を使用して特権アクセス管理 (PAM)](https://docs.microsoft.com/windows-server/identity/whats-new-active-directory-domain-services#a-namebkmkpamaprivileged-access-management)

### <a name="windows-server-2016-domain-functional-level-features"></a>Windows Server 2016 ドメイン機能レベルの機能

* 既定の Active Directory 機能をすべて、Windows Server 2012R2 ドメインの機能レベルで機能をすべて。 加えて、次の機能です。
   * NTLM の自動ローリングの Dc をサポートし、PKI 認証を要求するように構成されているその他のユーザー アカウントにパスワード ベースのシークレット。 この構成は、「スマート カードの対話型ログオンに必要な」とも呼ばれます
   * Dc は、ユーザーがドメインに参加しているデバイスの特定の場所に制限されている場合に許可するネットワーク NTLM をサポートできます。
   * PKInit 鮮度の拡張機能で正常に認証、Kerberos クライアントは新しいパブリック キー id の SID を取得します。

    詳細については、次を参照してください[Kerberos 認証で新](https://docs.microsoft.com/windows-server/security/kerberos/whats-new-in-kerberos-authentication)と[新機能については資格情報の保護。](https://docs.microsoft.com/windows-server/security/credentials-protection-and-management/whats-new-in-credential-protection)

## <a name="windows-server-2012r2"></a>Windows Server 2012R2

ドメイン コント ローラーのオペレーティング システムがサポートされています。

* Windows Server 2019
* Windows Server 2016
* Windows Server 2012 R2

### <a name="windows-server-2012r2-forest-functional-level-features"></a>Windows Server 2012R2 フォレスト機能レベルの機能

* フォレスト機能レベルですが他の機能のすべては、Windows Server 2012 で使用できる機能。

### <a name="windows-server-2012r2-domain-functional-level-features"></a>Windows Server 2012R2 ドメイン機能レベルの機能

* 既定の Active Directory 機能をすべて、Windows Server 2012 のドメイン機能レベルで機能をすべて。 加えて、次の機能です。
   * Protected Users に対する DC 側の保護。 ドメインが不要になったことができます、Windows Server 2012 R2 へのユーザーの認証を保護するには。
      * NTLM 認証を使用します。
      * Kerberos 事前認証で DES または RC4 暗号スイートを使用します。
      * 委任を使用して制約なし/制約付き委任
      * 最初の 4 時間以内の有効期間を超えてユーザー チケット (Tgt) を更新します。
   * Authentication Policies
      * 新しいフォレストに基づいた Active Directory ポリシーのうちでホストを管理する Windows Server 2012 R2 のドメインのアカウントに適用できるアカウントできますからシングル サインオンとアカウントとして実行されているサービスに認証のアクセス制御条件を適用します。
   * Authentication Policy Silos
      * 新しいフォレストに基づいた Active Directory オブジェクト、ユーザー、管理されたサービスとコンピューター アカウントの認証ポリシーまたは認証を分離するための分類に使用するアカウント間のリレーションシップを作成することができます。

## <a name="windows-server-2012"></a>Windows Server 2012

ドメイン コント ローラーのオペレーティング システムがサポートされています。

* Windows Server 2019
* Windows Server 2016
* Windows Server 2012 R2
* Windows Server 2012

### <a name="windows-server-2012-forest-functional-level-features"></a>Windows Server 2012 フォレスト機能レベルの機能

* すべての Windows Server 2008 R2 で利用できる機能はフォレスト機能レベルですが他の機能です。

### <a name="windows-server-2012-domain-functional-level-features"></a>Windows Server 2012 ドメイン機能レベルの機能

* 既定の Active Directory 機能をすべて、Windows Server 2008 r2 ドメインの機能レベルで機能をすべて。 加えて、次の機能です。
   * KDC は、信頼性情報、複合認証、および Kerberos 防 KDC 管理用テンプレート ポリシーが 2 つの設定 (常に信頼性情報を提供および防御されていない認証要求を失敗) を Windows Server 2012 ドメインの機能レベルを必要とするサポートします。 詳細については、次を参照してください[Kerberos 認証では新機能。](https://technet.microsoft.com/library/hh831747.aspx)

## <a name="windows-server-2008r2"></a>Windows Server 2008R2

ドメイン コント ローラーのオペレーティング システムがサポートされています。

* Windows Server 2019
* Windows Server 2016
* Windows Server 2012 R2
* Windows Server 2012
* Windows Server 2008 R2

### <a name="windows-server-2008r2-forest-functional-level-features"></a>Windows Server 2008 r2 フォレスト機能レベルの機能

* Windows Server 2003 フォレストの機能レベルで使用できる機能がすべて提供されます。加えて、以下の機能も提供されます。
   * Active Directory のごみ箱。AD DS の実行中に、削除されたオブジェクト全体を復元する機能を提供します。

### <a name="windows-server-2008r2-domain-functional-level-features"></a>Windows Server 2008 r2 ドメイン機能レベルの機能

* 既定の Active Directory 機能をすべて、Windows Server 2008 のドメイン機能レベルで機能をすべて。 加えて、次の機能です。
   * 認証メカニズム保証。各ユーザーの Kerberos トークン内のドメイン ユーザーの認証に使用されるログオン方法の種類 (スマート カードまたはユーザー名/パスワード) に関する情報をパッケージ化します。 Active Directory フェデレーション サービス (AD FS) などのフェデレーション id 管理インフラストラクチャが展開されているネットワーク環境でこの機能が有効にすると、トークン内の情報を抽出できますユーザーがアクセスを試みるたびにユーザーのログオン方法に基づいて承認の判断に開発された要求対応アプリケーション。
   * 名前または DNS のホストにマシン アカウントの変更の名前と、管理されたサービス アカウントのコンテキストで特定のコンピューターで実行されているサービスの SPN の自動管理します。 管理されたサービス アカウントの詳細については、次を参照してください。[サービス アカウントのステップ バイ ステップ ガイド](https://go.microsoft.com/fwlink/?LinkId=180401)します。

## <a name="windows-server-2008"></a>Windows Server 2008

ドメイン コント ローラーのオペレーティング システムがサポートされています。

* Windows Server 2019
* Windows Server 2016
* Windows Server 2012 R2
* Windows Server 2012
* Windows Server 2008 R2
* Windows Server 2008

### <a name="windows-server-2008-forest-functional-level-features"></a>Windows Server 2008 フォレスト機能レベルの機能

* 追加の機能ではありませんが、すべての Windows Server 2003 フォレストの機能レベルで使用できる機能を利用できます。 

### <a name="windows-server-2008-domain-functional-level-features"></a>Windows Server 2008 ドメイン機能レベルの機能

* すべて既定の AD DS の機能、すべての Windows Server 2003 ドメイン機能レベルで機能し、次の機能を利用します。
   * 分散ファイル システム (DFS) レプリケーションのサポートの Windows Server 2003 システム ボリューム (SYSVOL)
      * DFS レプリケーションのサポートは、SYSVOL の内容のより堅牢で詳細なレプリケーションを提供します。
        [!NOTE]>
        >Windows Server 2012 R2 以降では、ファイル レプリケーション サービス (FRS) は非推奨とされます。 実行しているドメイン コント ローラー上に作成された新しいドメイン、Windows Server 2008 のドメイン機能レベルを以上には、Windows Server 2012 R2 を設定する必要があります。

   * ドメイン ベース DFS 名前空間アクセス ベースの列挙とスケーラビリティの向上をサポートする Windows Server 2008 モードで実行されています。 Windows Server 2008 モードでのドメイン ベース名前空間には、Windows Server 2003 フォレストの機能レベルを使用するフォレストも必要です。 詳細については、次を参照してください。 [Namespace の種類を選択](https://go.microsoft.com/fwlink/?LinkId=180400)します。
   * Kerberos プロトコルの高度な (AES 128、AES 256) 暗号化標準サポートします。 Tgt を AES を使用して発行するためには、ドメインの機能レベルが Windows Server 2008 またはそれ以降にする必要があり、ドメインのパスワードを変更する必要があります。 
      * 詳細については、次を参照してください。 [Kerberos の強化](https://technet.microsoft.com/library/cc749438(ws.10).aspx)します。
        [!NOTE]>
        >認証エラーが発生するドメイン コント ローラーで Windows Server 2008 以降のドメイン機能レベルが発生した後、ドメイン コント ローラーが DFL 変更が既にレプリケートされたが、krbtgt のパスワードをまだ更新されていないかどうか。 この場合、ドメイン コント ローラー上で KDC サービスの再起動は、krbtgt の新しいパスワードのメモリ内の更新をトリガーし、関連する認証エラーを解決します。

   * [最後の対話型ログオン](https://go.microsoft.com/fwlink/?LinkId=180387)情報には、次の情報が表示されます。
      * Windows Server 2008 をドメインに参加しているサーバーまたは Windows Vista ワークステーションで失敗したログオン試行の合計数
      * Windows Server 2008 サーバーまたは Windows Vista ワークステーションにログオンに成功、失敗したログオン試行の合計数
      * Windows Server 2008 または Windows Vista ワークステーションで失敗したログオン試行が最後の時刻
      * 最後のログオンに成功した時間が、Windows Server 2008 サーバーまたは Windows Vista ワークステーションで試行します。
   * 詳細なパスワード ポリシーでは、ドメインのユーザーおよびグローバル セキュリティ グループのパスワードとアカウント ロックアウトのポリシーを指定できます。 詳細については、次を参照してください。[細かいパスワードおよびアカウント ロックアウトのポリシー構成のステップ バイ ステップ ガイド](https://go.microsoft.com/fwlink/?LinkID=91477)します。
   * 個人用仮想デスクトップ
      * Active Directory ユーザーとコンピューター でユーザー アカウントのプロパティ ダイアログ ボックスで、個人用仮想デスクトップ タブで提供される追加機能を使用するには、Windows Server 2008 R2 の AD DS スキーマを拡張 (スキーマ オブジェクトのバージョン = 47)。 詳細については、次を参照してください。[を展開する個人用仮想デスクトップを使用して RemoteApp とデスクトップ接続のステップ バイ ステップ ガイドで](https://go.microsoft.com/fwlink/?LinkId=183552)します。

## <a name="windows-server-2003"></a>Windows Server 2003

ドメイン コント ローラーのオペレーティング システムがサポートされています。

* Windows Server 2012 R2
* Windows Server 2012
* Windows Server 2008 R2
* Windows Server 2008
* Windows Server 2003

### <a name="windows-server-2003-forest-functional-level-features"></a>Windows Server 2003 フォレスト機能レベルの機能

* すべての既定の AD DS の機能と、次の機能を使用できます。
   * フォレストの信頼
   * ドメイン名の変更。
   * リンクされている値のレプリケーション
      - リンクされている値のレプリケーションでは、格納し、1 つの単位としてメンバーシップ全体をレプリケートするのではなく個々 のメンバーの値をレプリケート グループ メンバーシップを変更することが可能です。 格納して、個々 のメンバーの値をレプリケートするネットワーク帯域幅とレプリケーション中に、以下のプロセッサ サイクルを使用および追加または別のドメイン コント ローラーで同時に複数のメンバーを削除するときに更新プログラムの損失を防ぎます。
   * 読み取り専用ドメイン コント ローラー (RODC) をデプロイする機能
   * 知識整合性チェッカー (KCC) のアルゴリズムおよびスケーラビリティの向上
      - サイト間トポロジ ジェネレーター (ISTG) は、AD DS は、Windows 2000 フォレストの機能レベルでサポートできるよりも多くのサイトでフォレストをサポートする拡張強化されたアルゴリズムを使用します。 向上 ISTG 選択アルゴリズムは、Windows 2000 フォレストの機能レベルで ISTG を選択するためあまり侵入メカニズムです。
   * という名前の動的な補助型クラスのインスタンスを作成する機能**dynamicObject**をドメイン ディレクトリ パーティション
   * 変換する機能、 **inetOrgPerson**オブジェクトのインスタンスに、**ユーザー**オブジェクトのインスタンスと方向が逆に変換が完了するには
   * ロール ベースの承認をサポートするために、新しい種類のグループのインスタンスを作成する機能。 
      - これらの型には、アプリケーションの基本グループおよび LDAP クエリ グループは呼び出されます。
   * スキーマの属性およびクラスの非アクティブ化と再定義。 次の属性を再利用できます: ldapDisplayName、schemaIdGuid、OID、および mapiID します。
   * ドメイン ベース DFS 名前空間アクセス ベースの列挙とスケーラビリティの向上をサポートする Windows Server 2008 モードで実行されています。 詳細については、次を参照してください。 [Namespace の種類を選択](https://go.microsoft.com/fwlink/?LinkId=180400)します。

### <a name="windows-server-2003-domain-functional-level-features"></a>Windows Server 2003 ドメイン機能レベルの機能

* 既定の AD DS の機能をすべて、Windows 2000 ネイティブ ドメインの機能レベルで利用できるすべての機能と、次の機能を使用できます。
   * ドメインの管理ツール Netdom.exe、ドメイン コント ローラーの名前を変更することができます。
   * ログオン タイムスタンプを更新します。
      * **lastLogonTimestamp** 属性は、ユーザーまたはコンピューターの最後のログオン日時で更新されます。 この属性は、ドメイン内でレプリケートされます。
   * 設定する機能、 **userPassword**で有効なパスワードとして属性**inetOrgPerson**とユーザー オブジェクト
   * ユーザーとコンピューターをリダイレクトする機能のコンテナー
      * 既定では、2 つのよく知られているコンテナーを提供して、コンピューターとユーザーのアカウントが格納具体的には、cn = コンピューター、<domain root>および cn = ユーザー、<domain root>します。 この機能は、これらのアカウントのよく知られている、新しい場所の定義を使用できます。
   * AD DS にその承認ポリシーを格納する承認マネージャーの機能
   * 制約付き委任
      * 制約付き委任は、アプリケーションが Kerberos ベースの認証を使用してユーザーの資格情報のセキュリティで保護された委任の利用可能にします。
      * 特定の宛先サービスのみへの委任を制限することができます。
   * 認証の選択
      * 選択的認証を使用するユーザーと信頼する側のフォレスト内のリソース サーバーに対する認証を許可されている信頼されたフォレストからのグループを指定することが可能になります。

## <a name="windows-2000"></a>Windows 2000

ドメイン コント ローラーのオペレーティング システムがサポートされています。

* Windows Server 2008 R2
* Windows Server 2008
* Windows Server 2003
* Windows 2000

### <a name="windows-2000-native-forest-functional-level-features"></a>Windows 2000 ネイティブ フォレスト機能レベルの機能

* すべての既定の AD DS の機能を利用できます。

### <a name="windows-2000-native-domain-functional-level-features"></a>Windows 2000 ネイティブ ドメイン機能レベルの機能

* すべての既定の AD DS の機能と、次のディレクトリ機能が利用できます。
   * ユニバーサル グループの配布とセキュリティの両方のグループ。
   * グループの入れ子
   * セキュリティおよび配布グループ間の変換は、グループの変換
   * セキュリティ識別子 (SID) の履歴

## <a name="next-steps"></a>次の手順

* [ドメイン機能レベルを上げる](https://technet.microsoft.com/library/cc753104.aspx)  
* [フォレストの機能レベルを上げる](https://technet.microsoft.com/library/cc730985.aspx)
