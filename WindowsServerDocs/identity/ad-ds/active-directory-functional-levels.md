---
ms.assetid: f964d056-11bf-4d9b-b5ab-dceaad8bfbc3
title: Windows Server 2016 の機能レベル
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 10/29/2018
ms.topic: article
ms.prod: windows-server
ms.custom: it-pro
ms.reviewer: maheshu
ms.technology: identity-adds
ms.openlocfilehash: 7f16d58eb6c5074c75f49ba7936c4d312a3dbda4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71390979"
---
# <a name="forest-and-domain-functional-levels"></a>フォレストとドメインの機能レベル

>適用先:Windows Server

機能レベルによって、Active Directory ドメイン サービス (AD DS) のドメインまたはフォレストで使用できる機能が決まります。 また、機能レベルにより、ドメインまたはフォレスト内のドメイン コントローラーで実行できる Windows Server オペレーティング システムが決まります。 ただし、機能レベルによって、ドメインやフォレストに参加しているワークステーションやメンバー サーバーで実行できるオペレーティング システムが影響を受けることはありません。

AD DS を展開するときに、ドメインおよびフォレストの機能レベルを、環境でサポートできる最高値に設定します。 こうすることで、可能な限り多くの AD DS 機能を使用できます。 新しいフォレストを展開するときに、フォレストの機能レベルを設定するよう求められ、その次にドメインの機能レベルを設定するよう求められます。 ドメインの機能レベルをフォレストの機能レベルより高い値に設定することはできますが、ドメインの機能レベルをフォレストの機能レベルより低い値に設定することはできません。

Windows 2003 の有効期間が終了したら、Windows 2003 のドメイン コントローラー (DC) を、Windows Server 2008、2008R2、2012、2012R2、2016、または 2019 に更新する必要があります。 その結果として、Windows Server 2003 を実行するすべてのドメイン コントローラーを、ドメインから削除する必要があります。

Windows Server 2008 以上のドメイン機能レベルでは、分散ファイル サービス (DFS) レプリケーションを使用して、ドメイン コントローラー間で SYSVOL フォルダーの内容をレプリケートします。 Windows Server 2008 ドメイン機能レベル以上で新しいドメインを作成した場合、SYSVOL のレプリケートには DFS レプリケーションが自動的に使用されます。 それより低い低い機能レベルでドメイン作成した場合は、SYSVOL のレプリケーションを FRS から DFS に移行する必要があります。 移行手順については、[TechNet の手順](https://technet.microsoft.com/library/dd640019(v=WS.10).aspx)に従うか、[ストレージ チームのファイル キャビネット ブログの合理化された一連の手順](http://blogs.technet.com/b/filecab/archive/2014/06/25/streamlined-migration-of-frs-to-dfsr-sysvol.aspx)を参照してください。

## <a name="windows-server-2019"></a>Windows Server 2019

このリリースでは、フォレストまたはドメインの新しい機能レベルは追加されていません。

Windows Server 2019 ドメイン コントローラーを追加する最小要件は、Windows Server 2008 機能レベルです。 ドメインでは、SYSVOL をレプリケートするためにエンジンとして、DFS-R を使用する必要もあります。

## <a name="windows-server-2016"></a>Windows Server 2016

サポートされるドメイン コントローラーのオペレーティング システム:

* Windows Server 2019
* Windows Server 2016

### <a name="windows-server-2016-forest-functional-level-features"></a>Windows Server 2016 フォレストの機能レベルの機能

* Windows Server 2012R2 フォレストの機能レベルで使用できるすべての機能と以下の機能を使用できます。
   * [Microsoft Identity Manager (MIM) を使用する Privileged access management (PAM)](https://docs.microsoft.com/windows-server/identity/whats-new-active-directory-domain-services#a-namebkmkpamaprivileged-access-management)

### <a name="windows-server-2016-domain-functional-level-features"></a>Windows Server 2016 ドメインの機能レベルの機能

* Active Directory のすべての既定機能、Windows Server 2012R2 ドメイン機能レベルのすべての機能、それに加えて以下の機能:
   * DC を使うと、PKI 認証が必要なように構成されているユーザー アカウントでの、NTLM および他のパスワード ベースのシークレットの自動ローリングをサポートできます。 この構成は、"対話型ログオンにはスマート カードが必要" とも呼ばれます
   * DC を使うと、ユーザーが特定のドメイン参加済みデバイスに制限されているときのネットワーク NTLM の許可をサポートできます。
   * Kerberos クライアントが PKInit Freshness Extension で正常に認証されると、新しい公開キー ID SID を取得します。

    詳細については、「[Kerberos 認証の新機能](https://docs.microsoft.com/windows-server/security/kerberos/whats-new-in-kerberos-authentication)」および「[Credential Protection の新機能](https://docs.microsoft.com/windows-server/security/credentials-protection-and-management/whats-new-in-credential-protection)」を参照してください

## <a name="windows-server-2012r2"></a>Windows Server 2012R2

サポートされるドメイン コントローラーのオペレーティング システム:

* Windows Server 2019
* Windows Server 2016
* Windows Server 2012 R2

### <a name="windows-server-2012r2-forest-functional-level-features"></a>Windows Server 2012R2 フォレストの機能レベルの機能

* Windows Server 2012 フォレストの機能レベルで使用可能な機能がすべて提供されますが、他に追加される機能はありません。

### <a name="windows-server-2012r2-domain-functional-level-features"></a>Windows Server 2012R2 ドメインの機能レベルの機能

* Active Directory のすべての既定機能、Windows Server 2012 ドメイン機能レベルのすべての機能、それに加えて以下の機能:
   * 保護されたユーザーに対する DC 側の保護。 Windows Server 2012 R2 ドメインで認証を行う保護されたユーザーは、次のことをできなくなります。
      * NTLM 認証で認証を行う
      * Kerberos の事前認証で DES または RC4 の暗号スイートを使用する
      * 制約なしの委任または制約付き委任を使用して委任される
      * 最初の 4 時間の有効期間を超えてユーザー チケット (TGT) を更新する
   * Authentication Policies
      * 新しいフォレスト ベースの Active Directory ポリシー。Windows Server 2012 R2 ドメインのアカウントに適用して、アカウントがサインオンできるホストを制御したり、アカウントとして実行されているサービスに認証のアクセス制御条件を適用したりすることができます。
   * Authentication Policy Silos
      * 新しいフォレスト ベースの Active Directory オブジェクト。ユーザー、マネージド サービスとマネージド コンピューター、および認証ポリシーまたは認証分離のためのアカウントの分類に使用されるアカウントの間に、関係を作成できます。

## <a name="windows-server-2012"></a>Windows Server 2012

サポートされるドメイン コントローラーのオペレーティング システム:

* Windows Server 2019
* Windows Server 2016
* Windows Server 2012 R2
* Windows Server 2012

### <a name="windows-server-2012-forest-functional-level-features"></a>Windows Server 2012 フォレストの機能レベルの機能

* Windows Server 2008 R2 フォレストの機能レベルで使用可能な機能がすべて提供されますが、他に追加される機能はありません。

### <a name="windows-server-2012-domain-functional-level-features"></a>Windows Server 2012 ドメインの機能レベルの機能

* Active Directory のすべての既定機能、Windows Server 2008R2 ドメイン機能レベルのすべての機能、それに加えて以下の機能:
   * [KDC で信頼性情報、複合認証、および Kerberos 防御をサポートする] KDC 管理テンプレート ポリシーには、Windows Server 2012 ドメイン機能レベルを必要とする 2 つの設定 ([常に信頼性情報を提供する] および [防御されていない要求を失敗とする]) があります。 詳細については、「[Kerberos 認証の新機能](https://technet.microsoft.com/library/hh831747.aspx)」を参照してください

## <a name="windows-server-2008r2"></a>Windows Server 2008R2

サポートされるドメイン コントローラーのオペレーティング システム:

* Windows Server 2019
* Windows Server 2016
* Windows Server 2012 R2
* Windows Server 2012
* Windows Server 2008 R2

### <a name="windows-server-2008r2-forest-functional-level-features"></a>Windows Server 2008R2 フォレストの機能レベルの機能

* Windows Server 2003 フォレストの機能レベルで使用できる機能がすべて提供されます。加えて、以下の機能も提供されます。
   * Active Directory のごみ箱。AD DS の実行中に、削除されたオブジェクト全体を復元する機能を提供します。

### <a name="windows-server-2008r2-domain-functional-level-features"></a>Windows Server 2008R2 ドメインの機能レベルの機能

* Active Directory のすべての既定機能、Windows Server 2008 ドメイン機能レベルのすべての機能、それに加えて以下の機能:
   * 認証メカニズム保証。各ユーザーの Kerberos トークン内のドメイン ユーザーの認証に使用されるログオン方法の種類 (スマート カードまたはユーザー名/パスワード) に関する情報をパッケージ化します。 Active Directory フェデレーション サービス (AD FS) などのフェデレーション ID 管理インフラストラクチャを導入済みのネットワーク環境でこの認証メカニズム保証が有効になっている場合、ユーザーが要求対応型アプリケーション (ユーザーのログオン方法に基づいて承認の可否を判定するアプリケーション) へのアクセスを試みるたびに、Kerberos トークン内の情報が抽出されます。
   * コンピューター アカウントの名前または DNS ホスト名が変更されたときの、マネージド サービス アカウントのコンテキストで特定のコンピューターで実行されているサービスに対する自動 SPN 管理。 マネージド サービス アカウントについて詳しくは、「[サービス アカウントのステップ バイ ステップ ガイド](https://go.microsoft.com/fwlink/?LinkId=180401)」を参照してください。

## <a name="windows-server-2008"></a>Windows Server 2008

サポートされるドメイン コントローラーのオペレーティング システム:

* Windows Server 2019
* Windows Server 2016
* Windows Server 2012 R2
* Windows Server 2012
* Windows Server 2008 R2
* Windows Server 2008

### <a name="windows-server-2008-forest-functional-level-features"></a>Windows Server 2008 フォレストの機能レベルの機能

* Windows Server 2003 フォレストの機能レベルで使用可能な機能がすべて提供されますが、追加機能は使用できません。 

### <a name="windows-server-2008-domain-functional-level-features"></a>Windows Server 2008 ドメインの機能レベルの機能

* AD DS のすべての既定機能、Windows Server 2003 ドメイン機能レベルのすべての機能、および以下の機能を使用できます。
  * Windows Server 2003 システム ボリューム (SYSVOL) に対する分散ファイル システム (DFS) レプリケーションのサポート
    * DFS レプリケーションを使うと、SYSVOL の内容の、より強力で詳細なレプリケーションが提供されます。

      > [!NOTE]
      > Windows Server 2012 R2 以降、ファイル レプリケーション サービス (FRS) は非推奨になります。 Windows Server 2012 R2 以降を実行するドメイン コントローラー上に作成される新しいドメインは、Windows Server 2008 ドメイン機能レベル以上に設定する必要があります。

  * Windows Server 2008 モードで実行されているドメイン ベースの DFS 名前空間。これには、アクセスベースの列挙とスケーラビリティの向上のサポートが含まれます。 Windows Server 2008 モードでのドメイン ベースの名前空間を使うと、フォレストで Windows Server 2003 フォレスト機能レベルを使用する必要もあります。 詳しくは、「[名前空間の種類を選択する](https://go.microsoft.com/fwlink/?LinkId=180400)」をご覧ください。
  * Kerberos プロトコルに対する Advanced Encryption Standard (AES 128 および AES 256) のサポート。 AES を使用して TGT を発行するには、ドメイン機能レベルを Windows Server 2008 以上にし、ドメイン パスワードを変更する必要があります。 
    * 詳しくは、「[Kerberos の強化](https://technet.microsoft.com/library/cc749438(ws.10).aspx)」をご覧ください。

      > [!NOTE]
      >ドメイン コントローラーで DFL の変更が既にレプリケートされていても、まだ krbtgt パスワードが更新されていない場合、ドメインの機能レベルを Windows Server 2008 以上に上げた後、ドメイン コントローラーで認証エラーが発生することがあります。 この場合、ドメイン コントローラーで KDC サービスを再起動すると、新しい krbtgt パスワードのメモリ内更新がトリガーされ、関連する認証エラーが解決されます。

  * [前回の対話型ログオン](https://go.microsoft.com/fwlink/?LinkId=180387)に関する情報では、次の情報が表示されます。
     * ドメイン参加済み Windows Server 2008 サーバーまたは Windows Vista ワークステーションでのログオン試行失敗の合計回数
     * Windows Server 2008 サーバーまたは Windows Vista ワークステーションに正常にログオンした後で失敗したログオン試行の合計回数
     * Windows Server 2008 または Windows Vista ワークステーションでのログオン試行が最後に失敗した時刻
     * Windows Server 2008 サーバーまたは Windows Vista ワークステーションでのログオン試行が最後に成功した時刻
  * 詳細なパスワード ポリシーにより、ドメイン内のユーザーおよびグローバル セキュリティ グループに対して、パスワードおよびアカウント ロックアウト ポリシーを指定することが可能になります。 詳細については、[細かい設定が可能なパスワードおよびアカウント ロックアウトのポリシー構成についての手順ガイド](https://go.microsoft.com/fwlink/?LinkID=91477)に関するページを参照してください。
  * 個人用仮想デスクトップ
     * [Active Directory ユーザーとコンピューター] の [ユーザー アカウントのプロパティ] ダイアログ ボックスの [個人用仮想デスクトップ] タブにある機能を使用するには、AD DS スキーマを Windows Server 2008 R2 用に拡張する必要があります (スキーマ オブジェクト バージョン = 47)。 詳しくは、「[RemoteApp とデスクトップ接続を使用した個人用仮想デスクトップの展開のステップバイステップ ガイド](https://go.microsoft.com/fwlink/?LinkId=183552)」をご覧ください。

## <a name="windows-server-2003"></a>Windows Server 2003

サポートされるドメイン コントローラーのオペレーティング システム:

* Windows Server 2012 R2
* Windows Server 2012
* Windows Server 2008 R2
* Windows Server 2008
* Windows Server 2003

### <a name="windows-server-2003-forest-functional-level-features"></a>Windows Server 2003 フォレストの機能レベルの機能

* すべての既定の AD DS 機能と、次の機能を使用できます。
   * フォレストの信頼
   * ドメイン名の変更。
   * リンクされた値のレプリケーション
      - リンクされた値のレプリケーションを使うと、メンバーシップ全体を 1 つの単位としてレプリケートするのではなく、個々のメンバーの値が保存およびレプリケートされるように、グループ メンバーシップを変更できるようになります。 個々のメンバーの値を格納およびレプリケートすると、レプリケーション中に使用されるネットワーク帯域幅とプロセッサ サイクルが少なくなるため、複数のメンバーを異なるドメイン コントローラーで同時に追加または削除したときに、更新が失われるのを防ぐことができます。
   * 読み取り専用ドメイン コントローラー (RODC) を展開する機能
   * 知識整合性チェッカー (KCC) の強化されたアルゴリズムとスケーラビリティ
      - サイト間トポロジ ジェネレーター (ISTG) では、強化されたアルゴリズムが使用されます。スケーラビリティの向上により、Windows 2000 フォレストの機能レベルで AD DS がサポートできるサイト数より多くのサイトを含むフォレストがサポート可能になります。 向上した ISTG 選択アルゴリズムは、Windows 2000 フォレストの機能レベルで ISTG を選択するための、より影響の少ないメカニズムです。
   * **dynamicObject** と呼ばれる動的な補助型クラスのインスタンスをドメイン ディレクトリ パーティションに作成する機能
   * **inetOrgPerson** オブジェクト インスタンスから **User** オブジェクト インスタンスへの変換、および逆方向の変換を行う機能
   * ロールベースの承認をサポートするために新しいグループの種類のインスタンスを作成する機能。 
      - これらの種類は、アプリケーション基本グループおよび LDAP クエリ グループと呼ばれます。
   * スキーマの属性およびクラスの非アクティブ化と再定義。 ldapDisplayName、schemaIdGuid、OID、mapiID の各属性を再利用できます。
   * Windows Server 2008 モードで実行されているドメイン ベースの DFS 名前空間。これには、アクセスベースの列挙とスケーラビリティの向上のサポートが含まれます。 詳しくは、「[名前空間の種類を選択する](https://go.microsoft.com/fwlink/?LinkId=180400)」をご覧ください。

### <a name="windows-server-2003-domain-functional-level-features"></a>Windows Server 2003 ドメインの機能レベルの機能

* AD DS のすべての既定機能、Windows 2000 ネイティブ ドメイン機能レベルで使用可能なすべての機能、および以下の機能を使用できます。
   * ドメイン管理ツール Netdom.exe。ドメイン コントローラーの名前を変更できるようになります
   * ログオン タイムスタンプの更新
      * **lastLogonTimestamp** 属性は、ユーザーまたはコンピューターの最後のログオン日時で更新されます。 この属性は、ドメイン内でレプリケートされます。
   * **inetOrgPerson** オブジェクトやユーザー オブジェクトでの有効なパスワードとして **userPassword** 属性を設定する機能
   * Users および Computers コンテナーをリダイレクトする機能
      * 既定では、コンピューター カウントとユーザー アカウントを格納するために、既知の 2 つのコンテナー cn=Computers,<domain root> および cn=Users,<domain root> が提供されます。 この機能を使用すると、これらのアカウントに対して新しい既知の場所を定義することができます。
   * 承認マネージャーが AD DS に承認ポリシーを保存する機能
   * 制約付き委任
      * 制約付き委任を使うと、アプリケーションで、Kerberos ベースの認証によるユーザー資格情報の安全な委任を利用することができます。
      * 特定の宛先サービスのみに委任を制限できます。
   * 選択的な認証
      * 選択的な認証を使うと、信頼する側のフォレストのリソース サーバーで認証を行うことができる、信頼される側のフォレストのユーザーおよびグループを指定できます。

## <a name="windows-2000"></a>Windows 2000

サポートされるドメイン コントローラーのオペレーティング システム:

* Windows Server 2008 R2
* Windows Server 2008
* Windows Server 2003
* Windows 2000

### <a name="windows-2000-native-forest-functional-level-features"></a>Windows 2000 ネイティブ フォレストの機能レベルの機能

* AD DS の既定の機能をすべて使用できます。

### <a name="windows-2000-native-domain-functional-level-features"></a>Windows 2000 ネイティブ ドメインの機能レベルの機能

* すべての既定の AD DS 機能と、次のディレクトリ機能を使用できます。
   * 配布グループとセキュリティ グループ両方のユニバーサル グループ。
   * グループの入れ子
   * グループの変換。セキュリティ グループと配布グループ間の変換が可能になります
   * セキュリティ識別子 (SID) の履歴

## <a name="next-steps"></a>次のステップ

* [ドメインの機能レベルを上げる](https://technet.microsoft.com/library/cc753104.aspx)  
* [フォレストの機能レベルを上げる](https://technet.microsoft.com/library/cc730985.aspx)
