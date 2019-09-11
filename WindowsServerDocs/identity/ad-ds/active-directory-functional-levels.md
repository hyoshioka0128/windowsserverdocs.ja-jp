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
ms.openlocfilehash: c1e2108084b03fabbf7c6a18c2ecbcaf3cbd1dd9
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70868254"
---
# <a name="forest-and-domain-functional-levels"></a>フォレストおよびドメインの機能レベル

>適用先:Windows Server

機能レベルによって、使用可能な Active Directory Domain Services (AD DS) ドメインまたはフォレストの機能が決まります。 また、ドメインまたはフォレスト内のドメインコントローラーで実行できる Windows Server オペレーティングシステムも決定します。 ただし、機能レベルは、ドメインまたはフォレストに参加しているワークステーションやメンバーサーバーで実行できるオペレーティングシステムには影響しません。

AD DS を展開するときに、ドメインおよびフォレストの機能レベルを、環境でサポートできる最高の値に設定します。 これにより、できるだけ多くの AD DS 機能を使用できるようになります。 新しいフォレストを展開するときに、フォレストの機能レベルを設定して、ドメインの機能レベルを設定するように求められます。 ドメインの機能レベルは、フォレストの機能レベルよりも高い値に設定できますが、ドメインの機能レベルを、フォレストの機能レベルよりも低い値に設定することはできません。

Windows 2003 の有効期間が終了すると、windows 2003 ドメインコントローラー (Dc) を Windows Server 2008、2008R2、2012、2012R2、2016、または2019に更新する必要があります。 そのため、Windows Server 2003 を実行するドメインコントローラーをドメインから削除する必要があります。

Windows Server 2008 以上のドメイン機能レベルでは、分散ファイルサービス (DFS) レプリケーションを使用して、ドメインコントローラー間で SYSVOL フォルダーのコンテンツをレプリケートします。 Windows Server 2008 ドメインの機能レベル以上で新しいドメインを作成した場合、SYSVOL のレプリケートには DFS レプリケーションが自動的に使用されます。 ドメインを低い機能レベルで作成した場合は、FRS から SYSVOL へのレプリケーションを使用するように移行する必要があります。 移行手順については、 [TechNet の手順](https://technet.microsoft.com/library/dd640019(v=WS.10).aspx)に従うか、[ストレージチームのファイルキャビネットのブログで合理化](http://blogs.technet.com/b/filecab/archive/2014/06/25/streamlined-migration-of-frs-to-dfsr-sysvol.aspx)された一連の手順を参照することができます。

## <a name="windows-server-2019"></a>Windows Server 2019

このリリースでは、新しいフォレストまたはドメインの機能レベルは追加されていません。

Windows Server 2019 ドメインコントローラーを追加する最小要件は、Windows Server 2008 の機能レベルです。 ドメインでは、SYSVOL をレプリケートするために、エンジンとして DFS-R を使用する必要もあります。

## <a name="windows-server-2016"></a>Windows Server 2016

サポートされているドメインコントローラーのオペレーティングシステム:

* Windows Server 2019
* Windows Server 2016

### <a name="windows-server-2016-forest-functional-level-features"></a>Windows Server 2016 フォレストの機能レベル機能

* Windows Server 2012R2 フォレストの機能レベルで使用可能なすべての機能と、次の機能を使用できます。
   * [Microsoft Identity Manager (MIM) を使用した Privileged access management (PAM)](https://docs.microsoft.com/windows-server/identity/whats-new-active-directory-domain-services#a-namebkmkpamaprivileged-access-management)

### <a name="windows-server-2016-domain-functional-level-features"></a>Windows Server 2016 ドメインの機能レベルの機能

* すべての既定の Active Directory 機能、Windows Server 2012R2 ドメインの機能レベルのすべての機能に加え、次の機能があります。
   * Dc は、PKI 認証を要求するように構成されたユーザーアカウントで、NTLM とその他のパスワードベースのシークレットの自動的なローリングをサポートできます。 この構成は、"対話型ログオンに必要なスマートカード" とも呼ばれます。
   * Dc は、ユーザーが特定のドメインに参加しているデバイスに制限されている場合に、ネットワーク NTLM の許可をサポートできます。
   * Kerberos クライアントが PKInit 鮮度拡張機能を使用して正常に認証されると、新しい公開キー id SID が取得されます。

    詳細については、「 [Kerberos 認証の新機能](https://docs.microsoft.com/windows-server/security/kerberos/whats-new-in-kerberos-authentication)」と「[資格情報の保護の新機能](https://docs.microsoft.com/windows-server/security/credentials-protection-and-management/whats-new-in-credential-protection)」を参照してください。

## <a name="windows-server-2012r2"></a>Windows Server 2012R2

サポートされているドメインコントローラーのオペレーティングシステム:

* Windows Server 2019
* Windows Server 2016
* Windows Server 2012 R2

### <a name="windows-server-2012r2-forest-functional-level-features"></a>Windows Server 2012R2 フォレストの機能レベル機能

* Windows Server 2012 フォレストの機能レベルで使用できるすべての機能。ただし、その他の機能はありません。

### <a name="windows-server-2012r2-domain-functional-level-features"></a>Windows Server 2012R2 のドメイン機能レベル機能

* すべての既定 Active Directory 機能、Windows Server 2012 ドメインの機能レベルのすべての機能に加え、次の機能があります。
   * 保護されたユーザーの DC 側の保護。 保護されたユーザーが Windows Server 2012 R2 ドメインに対する認証を行うことができなくなります。
      * NTLM 認証を使用した認証
      * Kerberos 事前認証で DES または RC4 暗号スイートを使用する
      * 制約なしの委任または制約付き委任を使用して委任する
      * 最初の4時間の有効期間を超えてユーザーチケット (Tgt) を更新する
   * Authentication Policies
      * 新しいフォレストベースの Active Directory ポリシーでは、Windows Server 2012 R2 ドメインのアカウントに適用して、アカウントがサインオンできるホストを制御したり、アカウントとして実行されているサービスに認証のアクセス制御条件を適用したりすることができます。
   * Authentication Policy Silos
      * 新しいフォレストベースの Active Directory オブジェクト。ユーザー、管理されたサービスとコンピューターの間の関係を作成したり、認証ポリシーまたは認証の分離のためにアカウントを分類するために使用されるアカウントです。

## <a name="windows-server-2012"></a>Windows Server 2012

サポートされているドメインコントローラーのオペレーティングシステム:

* Windows Server 2019
* Windows Server 2016
* Windows Server 2012 R2
* Windows Server 2012

### <a name="windows-server-2012-forest-functional-level-features"></a>Windows Server 2012 フォレストの機能レベル機能

* Windows Server 2008 R2 フォレストの機能レベルで使用できるすべての機能。ただし、その他の機能はありません。

### <a name="windows-server-2012-domain-functional-level-features"></a>Windows Server 2012 ドメインの機能レベルの機能

* すべての既定 Active Directory 機能、Windows Server 2008R2 ドメインの機能レベルのすべての機能に加え、次の機能があります。
   * KDC の信頼性情報、複合認証、および Kerberos 防御の管理用テンプレートポリシーには、Windows Server 2012 ドメインの機能レベルを必要とする2つの設定があります (常に要求を提供し、防御認証要求を送信します)。 詳細については、「 [Kerberos 認証の新機能](https://technet.microsoft.com/library/hh831747.aspx)」を参照してください。

## <a name="windows-server-2008r2"></a>Windows Server 2008R2

サポートされているドメインコントローラーのオペレーティングシステム:

* Windows Server 2019
* Windows Server 2016
* Windows Server 2012 R2
* Windows Server 2012
* Windows Server 2008 R2

### <a name="windows-server-2008r2-forest-functional-level-features"></a>Windows Server 2008R2 フォレストの機能レベル機能

* Windows Server 2003 フォレストの機能レベルで使用できる機能がすべて提供されます。加えて、以下の機能も提供されます。
   * Active Directory のごみ箱。AD DS の実行中に、削除されたオブジェクト全体を復元する機能を提供します。

### <a name="windows-server-2008r2-domain-functional-level-features"></a>Windows Server 2008R2 のドメイン機能レベル機能

* すべての既定 Active Directory 機能、Windows Server 2008 ドメインの機能レベルのすべての機能に加え、次の機能があります。
   * 認証メカニズムの保証。各ユーザーの Kerberos トークン内のドメインユーザーを認証するために使用されるログオン方法の種類 (スマートカードまたはユーザー名/パスワード) に関する情報をパッケージ化します。 Active Directory フェデレーションサービス (AD FS) (AD FS) などのフェデレーション id 管理インフラストラクチャを展開したネットワーク環境でこの機能を有効にすると、ユーザーが任意のユーザーにアクセスしようとするたびに、トークン内の情報を抽出できます。ユーザーのログオン方法に基づいて承認を決定するために開発された要求に対応するアプリケーション。
   * コンピューターアカウントの名前または DNS ホスト名が変更された場合に、管理されたサービスアカウントのコンテキストで特定のコンピューターで実行されるサービスの自動 SPN 管理。 管理されたサービスアカウントの詳細については、「[サービスアカウントのステップバイステップガイド](https://go.microsoft.com/fwlink/?LinkId=180401)」を参照してください。

## <a name="windows-server-2008"></a>Windows Server 2008

サポートされているドメインコントローラーのオペレーティングシステム:

* Windows Server 2019
* Windows Server 2016
* Windows Server 2012 R2
* Windows Server 2012
* Windows Server 2008 R2
* Windows Server 2008

### <a name="windows-server-2008-forest-functional-level-features"></a>Windows Server 2008 フォレストの機能レベル機能

* Windows Server 2003 フォレストの機能レベルで使用できる機能はすべてありますが、追加機能はありません。 

### <a name="windows-server-2008-domain-functional-level-features"></a>Windows Server 2008 ドメインの機能レベルの機能

* すべての既定の AD DS 機能、Windows Server 2003 ドメインの機能レベルのすべての機能、および次の機能を使用できます。
  * Windows Server 2003 システムボリューム (SYSVOL) の分散ファイルシステム (DFS) レプリケーションのサポート
    * DFS レプリケーションサポートは、SYSVOL コンテンツのより堅牢で詳細なレプリケーションを提供します。

      > [!NOTE]
      > Windows Server 2012 R2 以降では、ファイルレプリケーションサービス (FRS) は非推奨とされます。 Windows Server 2012 R2 以降を実行するドメインコントローラー上に作成された新しいドメインは、Windows Server 2008 ドメインの機能レベル以上に設定する必要があります。

  * Windows Server 2008 モードで実行されるドメインベースの DFS 名前空間。アクセスベースの列挙とスケーラビリティの向上がサポートされています。 Windows Server 2008 モードのドメインベースの名前空間では、フォレストで Windows Server 2003 フォレストの機能レベルを使用する必要もあります。 詳細については、「[名前空間の種類を選択する](https://go.microsoft.com/fwlink/?LinkId=180400)」を参照してください。
  * Advanced Encryption Standard (AES 128 および AES 256) は、Kerberos プロトコルのサポートをサポートしています。 AES を使用して Tgt を発行するには、ドメインの機能レベルが Windows Server 2008 以降で、ドメインパスワードを変更する必要があります。 
    * 詳細については、「 [Kerberos の機能強化](https://technet.microsoft.com/library/cc749438(ws.10).aspx)」を参照してください。

      > [!NOTE]
      >ドメインコントローラーで DFL の変更が既にレプリケートされていても、まだ krbtgt パスワードが更新されていない場合、ドメインの機能レベルが Windows Server 2008 以降に発行された後、ドメインコントローラーで認証エラーが発生することがあります。 この場合、ドメインコントローラーで KDC サービスを再起動すると、新しい krbtgt パスワードのメモリ内更新がトリガーされ、関連する認証エラーが解決されます。

  * [前回の対話型ログオン](https://go.microsoft.com/fwlink/?LinkId=180387)情報には、次の情報が表示されます。
     * ドメインに参加している Windows Server 2008 サーバーまたは Windows Vista ワークステーションでログオンに失敗した回数の合計
     * Windows Server 2008 サーバーまたは Windows Vista ワークステーションへのログオンに成功した後に失敗したログオン試行回数の合計
     * Windows Server 2008 または Windows Vista ワークステーションでのログオン試行が最後に失敗した時刻
     * Windows Server 2008 サーバーまたは Windows Vista ワークステーションでログオンが最後に成功した時刻
  * 細かい設定が可能なパスワードポリシーを使用すると、ドメイン内のユーザーおよびグローバルセキュリティグループにパスワードとアカウントロックアウトのポリシーを指定できます。 詳細については、「[細かい設定が可能なパスワードとアカウントロックアウトのポリシー構成のステップバイステップガイド](https://go.microsoft.com/fwlink/?LinkID=91477)」を参照してください。
  * 個人用仮想デスクトップ
     * Active Directory ユーザーとコンピューターの [ユーザーアカウントのプロパティ] ダイアログボックスの [個人用仮想デスクトップ] タブに用意されている機能を使用するには、AD DS スキーマを Windows Server 2008 R2 用に拡張する必要があります (スキーマオブジェクトバージョン = 47)。 詳細については、「[ステップバイステップガイド: RemoteApp とデスクトップ接続使用した個人用仮想デスクトップの展開](https://go.microsoft.com/fwlink/?LinkId=183552)」を参照してください。

## <a name="windows-server-2003"></a>Windows Server 2003

サポートされているドメインコントローラーのオペレーティングシステム:

* Windows Server 2012 R2
* Windows Server 2012
* Windows Server 2008 R2
* Windows Server 2008
* Windows Server 2003

### <a name="windows-server-2003-forest-functional-level-features"></a>Windows Server 2003 フォレストの機能レベル機能

* 既定の AD DS 機能と、次の機能のすべてを使用できます。
   * フォレストの信頼
   * ドメイン名の変更。
   * リンクされた値のレプリケーション
      - リンクされた値のレプリケーションを使用すると、メンバーシップ全体を1つの単位としてレプリケートするのではなく、個々のメンバーの値を格納およびレプリケートするようにグループメンバーシップを変更できます。 個々のメンバーの値を格納およびレプリケートすると、レプリケーション中に使用されるネットワーク帯域幅とプロセッササイクルが少なくなるため、複数のメンバーを異なるドメインコントローラーで同時に追加または削除した場合に、更新プログラムが失われるのを防ぐことができます。
   * 読み取り専用ドメインコントローラー (RODC) を展開する機能
   * 改良された知識整合性チェッカー (KCC) のアルゴリズムとスケーラビリティ
      - サイト間トポロジジェネレーター (ISTG) では、強化されたアルゴリズムを使用して、Windows 2000 フォレストの機能レベルでサポートできるより AD DS も多くのサイトを持つフォレストをサポートするように拡張できます。 強化された ISTG 選択アルゴリズムは、Windows 2000 フォレストの機能レベルで ISTG を選択するための、より影響の少ないメカニズムです。
   * 動的な補助クラスのインスタンスを、 **Dynamicobject**という名前のドメインディレクトリパーティションに作成する機能
   * **InetOrgPerson**オブジェクトインスタンスを**ユーザー**オブジェクトインスタンスに変換し、逆方向の変換を完了する機能。
   * 新しいグループの種類のインスタンスを作成して、ロールベースの承認をサポートする機能。 
      - これらの型は、アプリケーションの基本グループと LDAP クエリグループと呼ばれます。
   * スキーマの属性およびクラスの非アクティブ化と再定義。 LdapDisplayName、schemaIdGuid、OID、mapiID の各属性を再利用できます。
   * Windows Server 2008 モードで実行されるドメインベースの DFS 名前空間。アクセスベースの列挙とスケーラビリティの向上がサポートされています。 詳細については、「[名前空間の種類を選択する](https://go.microsoft.com/fwlink/?LinkId=180400)」を参照してください。

### <a name="windows-server-2003-domain-functional-level-features"></a>Windows Server 2003 ドメインの機能レベルの機能

* すべての既定の AD DS 機能。 Windows 2000 ネイティブドメインの機能レベルで使用可能なすべての機能と、次の機能を使用できます。
   * ドメイン管理ツール (Netdom.exe) により、ドメインコントローラーの名前を変更できるようになります。
   * ログオンタイムスタンプの更新
      * **lastLogonTimestamp** 属性は、ユーザーまたはコンピューターの最後のログオン日時で更新されます。 この属性は、ドメイン内でレプリケートされます。
   * **InetOrgPerson**および user オブジェクトの有効なパスワードとして**userPassword**属性を設定する機能
   * ユーザーとコンピューターのコンテナーをリダイレクトする機能
      * 既定では、コンピューターアカウントとユーザーアカウント (cn = Computers、<domain root> cn = Users)<domain root>に対して、既知の2つのコンテナーが用意されています。 この機能を使用すると、これらのアカウントの新しい既知の場所を定義できます。
   * 承認マネージャーが承認ポリシーを AD DS に格納する機能
   * 制約付き委任
      * 制約付き委任を使用すると、Kerberos ベースの認証を使用して、アプリケーションがユーザー資格情報のセキュリティで保護された委任を利用できるようになります。
      * 特定の宛先サービスのみに委任を制限できます。
   * 認証の選択
      * 選択的認証を使用すると、信頼する側のフォレストのリソースサーバーに対して認証を受けることができる信頼されたフォレストのユーザーとグループを指定できます。

## <a name="windows-2000"></a>Windows 2000

サポートされているドメインコントローラーのオペレーティングシステム:

* Windows Server 2008 R2
* Windows Server 2008
* Windows Server 2003
* Windows 2000

### <a name="windows-2000-native-forest-functional-level-features"></a>Windows 2000 ネイティブフォレストの機能レベル機能

* 既定の AD DS のすべての機能を使用できます。

### <a name="windows-2000-native-domain-functional-level-features"></a>Windows 2000 ネイティブドメインの機能レベル機能

* 既定の AD DS 機能と次のディレクトリ機能のすべてを使用できます。
   * 配布グループとセキュリティグループの両方のユニバーサルグループ。
   * グループの入れ子
   * グループの変換。セキュリティグループと配布グループ間の変換を可能にします。
   * セキュリティ識別子 (SID) の履歴

## <a name="next-steps"></a>次の手順

* [ドメインの機能レベルを上げる](https://technet.microsoft.com/library/cc753104.aspx)  
* [フォレストの機能レベルを上げる](https://technet.microsoft.com/library/cc730985.aspx)
