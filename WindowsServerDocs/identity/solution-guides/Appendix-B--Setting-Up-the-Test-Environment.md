---
ms.assetid: 82918181-525d-4e93-af96-957dac6aedb6
title: 付録 B テスト環境のセットアップ
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 5f529e6b0176b7ad416a728163b4ae9671040bf8
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861285"
---
# <a name="appendix-b-setting-up-the-test-environment"></a>付録 B:テスト環境のセットアップ

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックでは、ダイナミック アクセス制御をテストする実践的ラボを作成する手順の概要を示します。 依存関係のあるコンポーネントが多数存在するため、手順には順に従ってください。  

## <a name="prerequisites"></a>前提条件  
**ハードウェアとソフトウェアの要件**  

テスト ラボを設定するための要件:  

-   Windows Server 2008 R2 (SP1) および Hyper-V を実行しているホスト サーバー  

-   Windows Server 2012 ISO のコピー  

-   Windows 8 ISO のコピー  

-   Microsoft Office 2010  

-   Microsoft Exchange Server 2003 以降を実行しているサーバー  

ダイナミック アクセス制御のシナリオをテストするには、次の仮想マシンを作成する必要があります。  

-   DC1 (ドメイン コントローラー)  

-   DC2 (ドメイン コントローラー)  

-   FILE1 (ファイル サーバーおよび Active Directory Rights Management サービス)  

-   SRV1 (POP3 および SMTP サーバー)  

-   CLIENT1 (Microsoft Outlook がインストールされたクライアント コンピューター)  

仮想マシンのパスワードは、次のようにする必要があります。  

-   BUILTIN\Administrator: pass@word1  

-   Contoso\Administrator: pass@word1  

-   その他のすべてのアカウント: pass@word1  

## <a name="build-the-test-lab-virtual-machines"></a>テスト ラボ仮想マシンを作成する  

### <a name="install-the-hyper-v-role"></a>Hyper-V の役割をインストールする  
Windows Server 2008 R2 (SP1) を実行しているコンピューターに Hyper-V の役割をインストールする必要があります。  

##### <a name="to-install-the-hyper-v-role"></a>Hyper-V の役割をインストールするには  

1.  **[スタート]** ボタンをクリックして、[サーバー マネージャー] をクリックします。  

2.  サーバー マネージャーのメイン ウィンドウの 役割の概要 エリアにある **役割の追加** をクリックします。  

3.  **[サーバーの役割の選択]** ページで、 **[Hyper-V]** をクリックします。  

4.  **[仮想ネットワークの作成]** ページで、1 つ以上のネットワーク アダプターをクリックします (仮想マシンからそのネットワーク接続を使用可能にする場合)。  

5.  **[インストール オプションの確認]** ページで、 **[インストール]** をクリックします。  

6.  インストールを完了するにはコンピューターを再起動する必要があります。 **[閉じる]** をクリックしてウィザードを終了してから、 **[はい]** をクリックしてコンピューターを再起動します。  

7.  コンピューターを再起動した後に、役割のインストールに使用したのと同じアカウントでサインインします。 構成の再開ウィザードでインストールが完了したら、 **[閉じる]** をクリックしてウィザードを終了します。  

### <a name="create-an-internal-virtual-network"></a>内部仮想ネットワークを作成する  
ここでは、ID_AD_Network という内部仮想ネットワークを作成します。  

##### <a name="to-create-a-virtual-network"></a>仮想ネットワークを作成するには  

1.  Hyper-V マネージャーを開きます。  

2.  **[操作]** メニューで **[仮想ネットワーク マネージャー]** をクリックします。  

3.  **[仮想ネットワークの作成]** で **[内部]** を選択します。  

4.  **[追加]** をクリックします。 **[新しい仮想ネットワーク]** ページが表示されます。  

5.  新規ネットワークの名前として **ID_AD_Network** を入力します。 他のプロパティを確認し、必要に応じて変更します。  

6.  **[OK]** をクリックして仮想ネットワークを作成して仮想ネットワーク マネージャーを閉じるか、 **[適用]** をクリックして仮想ネットワークを作成して仮想ネットワーク マネージャーの使用を続行します。  

### <a name="build-the-domain-controller"></a><a name="BKMK_Build"></a>ドメインコントローラーを構築する  
ドメイン コントローラー (DC1) として使用する仮想マシンを作成します。 Windows Server 2012 ISO を使用して仮想マシンをインストールし、DC1 という名前を指定します。  

##### <a name="to-install-active-directory-domain-services"></a>Active Directory ドメイン サービスをインストールするには  

1. 仮想マシンを ID_AD_Network に接続します。 <strong>pass@word1</strong>パスワードを使用して管理者として DC1 にサインインします。  

2. サーバー マネージャーで、 **[管理]** をクリックし、 **[役割と機能の追加]** をクリックします。  

3. **[開始する前に]** ページで、 **[次へ]** をクリックします。  

4. **[インストールの種類の選択]** ページで **[役割ベースまたは機能ベースのインストール]** をクリックし、 **[次へ]** をクリックします。  

5. **[対象サーバーの選択]** ページで、 **[次へ]** をクリックします。  

6. **[サーバーの役割の選択]** ページで、 **[Active Directory ドメイン サービス]** を選択します。 **[役割と機能の追加ウィザード]** ダイアログ ボックスで、 **[機能の追加]** をクリックし、 **[次へ]** をクリックします。  

7. **[機能の選択]** ページで **[次へ]** をクリックします。  

8. **[Active Directory Domain Services]** ページの情報を確認し、 **[次へ]** をクリックします。  

9. **[インストール オプションの確認]** ページで、 **[インストール]** をクリックします。 [結果] ページの機能のインストールの進行状況バーにより、役割がインストールされていることが示されます。  

10. **[結果]** ページで、インストールが成功したことを確認し、 **[閉じる]** をクリックします。 サーバー マネージャーで、画面の右上隅の **[管理]** の隣にある、感嘆符の付いた警告アイコンをクリックします。 タスク リストで **このサーバーをドメイン コントローラーに昇格する** リンクをクリックします。  

11. **[配置構成]** ページで **[新しいフォレストを追加する]** をクリックし、ルート ドメインの名前 **contoso.com** を入力してから、 **[次へ]** をクリックします。  

12. **[ドメインコントローラーオプション]** ページで、Windows Server 2012 としてドメインおよびフォレストの機能レベルを選択し、DSRM パスワード<strong>pass@word1</strong>を指定して、 **[次へ]** をクリックします。  

13. **[DNS オプション]** ページで、 **[次へ]** をクリックします。  

14. **[追加オプション]** ページで、 **[次へ]** をクリックします。  

15. **[パス]** ページで、Active Directory データベース、ログ ファイル、および SYSVOL フォルダーの場所を入力し (または既定の場所を受け入れて)、 **[次へ]** をクリックします。  

16. **[オプションの確認]** ページで、選択を確認し、 **[次へ]** をクリックします。  

17. **[前提条件のチェック]** ページで、前提条件の検証が完了していることを確認し、 **[インストール]** をクリックします。  

18. **[結果]** ページで、サーバーがドメイン コントローラーとして正しく構成されたことを確認してから、 **[閉じる]** をクリックします。  

19. サーバーを再起動して AD DS のインストールを完了します。 (既定では、これは自動的に行われます)。  

Active Directory 管理センターを使用して、次のユーザーを作成します。  

##### <a name="create-users-and-groups-on-dc1"></a>DC1 でユーザーおよびグループを作成する  

1. Administrator として contoso.com にサインインします。 Active Directory 管理センターを起動します。  

2. 次のセキュリティ グループを作成します。  


   |    グループ名    |        メール アドレス         |
   |------------------|------------------------------|
   |   FinanceAdmin   |   financeadmin@contoso.com   |
   | FinanceException | financeexception@contoso.com |


3. 次の組織単位 (OU) を作成します。  


   |   OU 名    | コンピューター |
   |--------------|-----------|
   | FileServerOU |   FILE1   |


4. 示されている属性を使用して次のユーザーを作成します。  


   |       ユーザー       |  Username  |     メール アドレス      | 部署 |      グループ       | 国/地域 |
   |------------------|------------|------------------------|------------|------------------|----------------|
   | Myriam Delesalle | MDelesalle | MDelesalle@contoso.com |  Finance   |                  |       US       |
   |    Miles Reid    |   MReid    |   MReid@contoso.com    |  Finance   |   FinanceAdmin   |       US       |
   |   Esther Valle   |   EValle   |   EValle@contoso.com   | 運用 | FinanceException |       US       |
   |   Maira Wenzel   |  MWenzel   |  MWenzel@contoso.com   |     HR     |                  |       US       |
   |     Jeff Low     |    JLow    |    JLow@contoso.com    |     HR     |                  |       US       |
   |    RMS Server    |    rms     |    rms@contoso.com     |            |                  |                |

   セキュリティ グループの作成について詳しくは、Windows Server Web サイトにある「 [新しいグループを作成する](https://technet.microsoft.com/library/dd861305.aspx) 」を参照してください。  

##### <a name="to-create-a-group-policy-object"></a>グループ ポリシー オブジェクトを作成するには  

1.  画面の右上隅にカーソルを移動し、検索アイコンをクリックします。 検索ボックスに「**group policy management**」と入力し、 **[グループ ポリシーの管理]** をクリックします。  

2.  **[フォレスト: contoso.com]** を展開してから、 **[ドメイン]** を展開し、**contoso.com** に移動して、 **(contoso.com)** を展開し、 **[FileServerOU]** を選択します。 **[このドメインに GPO を作成し、ここにリンクします]** を右クリックします。

3.  GPO の記述名 (**FlexibleAccessGPO** など) を入力してから、 **[OK]** をクリックします。  

##### <a name="to-enable-dynamic-access-control-for-contosocom"></a>contoso.com でダイナミック アクセス制御を有効にするには  

1.  グループ ポリシー管理コンソールを開き、**contoso.com** をクリックしてから、 **[ドメイン コントローラー]** をダブルクリックします。  

2.  **[既定のドメイン コントローラー ポリシー]** を右クリックし、 **[編集]** を選択します。  

3.  グループ ポリシー管理エディター ウィンドウで **コンピューターの構成** をダブルクリックし、**ポリシー** をダブルクリックし、**管理用テンプレート** をダブルクリックし、**システム** をダブルクリックしてから、**KDC** をダブルクリックします。  

4.  **[KDC で信頼性情報、複合認証、および Kerberos 防御をサポートする]** をダブルクリックし、 **[有効]** の隣にあるオプションを選択します。 集約型アクセス ポリシーを使用するには、この設定を有効にする必要があります。  

5.  管理者特権のコマンド プロンプトを開き、次のコマンドを実行します。  

    ```  
    gpupdate /force  
    ```  

### <a name="build-the-file-server-and-ad-rms-server-file1"></a><a name="BKMK_FS1"></a>ファイルサーバーと AD RMS サーバー (FILE1) をビルドする  

1. Windows Server 2012 ISO から FILE1 という名前の仮想マシンを作成します。  

2. 仮想マシンを ID_AD_Network に接続します。  

3. 仮想マシンを contoso.com ドメインに参加させ、パスワード<strong>pass@word1</strong>を使用して contoso\administrator として FILE1 にサインインします。  

#### <a name="install-file-services-resource-manager"></a>ファイル サービス リソース マネージャーをインストールする  

###### <a name="to-install-the-file-services-role-and-the-file-server-resource-manager"></a>ファイル サービスの役割およびファイル サーバー リソース マネージャーをインストールするには  

1.  サーバー マネージャーで **[役割と機能の追加]** をクリックします。  

2.  **[開始する前に]** ページで、 **[次へ]** をクリックします。  

3.  **[インストールの種類の選択]** ページで、 **[次へ]** をクリックします。  

4.  **[対象サーバーの選択]** ページで、 **[次へ]** をクリックします。  

5.  **[サーバーの役割の選択]** ページで **[ファイル サービスおよび記憶域サービス]** を展開し、 **[ファイル サービスおよび iSCSI サービス]** の横にあるチェック ボックスを選択し、展開し、 **[ファイル サーバー リソース マネージャー]** を選択します。  

    役割と機能の追加ウィザードで、 **[機能の追加]** をクリックし、 **[次へ]** をクリックします。  

6.  **[機能の選択]** ページで **[次へ]** をクリックします。  

7.  **[インストール オプションの確認]** ページで、 **[インストール]** をクリックします。  

8.  **[インストールの進行状況]** ページで **[閉じる]** をクリックします。  

#### <a name="install-the-microsoft-office-filter-packs-on-the-file-server"></a>ファイル サーバーで Microsoft Office Filter Packs をインストールします。  
Windows Server 2012 に Microsoft Office フィルタパックをインストールして、既定で提供されているよりも大規模な Office ファイルの IFilters を有効にする必要があります。  Windows Server 2012 には Microsoft Office ファイル用の IFilters が既定でインストールされておらず、ファイル分類インフラストラクチャは IFilters を使用してコンテンツ分析を実行します。  

IFilters をダウンロードしてインストールするには、「 [Microsoft Office 2010 フィルタ パック](https://go.microsoft.com/fwlink/?LinkID=234122)」を参照してください。  

#### <a name="configure-email-notifications-on-file1"></a>FILE1 で電子メールによる通知を構成する  
クォータおよびファイル スクリーンを作成した場合、ユーザーのクォータ制限が近づいているとき、またはユーザーがファイルを保存しようとしたがブロックされた後に、電子メール通知をユーザーに送信することができます。 クォータおよびファイル スクリーンのイベントを特定の管理者に定期的に通知する場合、1 つ以上の既定の受信者を構成できます。 このような通知を送信するには、電子メール メッセージを転送するために使用する SMTP サーバーを指定する必要があります。  

###### <a name="to-configure-email-options-in-file-server-resource-manager"></a>ファイル サーバー リソース マネージャーで電子メール オプションを構成するには  

1. ファイル サーバー リソース マネージャーを開きます。 ファイル サーバー リソース マネージャーを開くには、 **[スタート]** をクリックし、「**ファイル サーバー リソース マネージャー**」と入力してから、 **[ファイル サーバー リソース マネージャー]** をクリックします。  

2. ファイル サーバー リソース マネージャー インターフェイスで、 **[ファイル サーバー リソース マネージャー]** を右クリックし、 **[オプションの構成]** をクリックします。 **[ファイル サーバー リソース マネージャーのオプション]** ダイアログ ボックスが開きます。  

3. **電子メールの通知** タブの SMTP サーバー名または IP アドレス  に、電子メールによる通知を転送する SMTP サーバーのホスト名または IP アドレスを入力します。  

4. クォータまたはファイルスクリーンのイベントを特定の管理者に定期的に通知する場合は、[**既定の管理**者の受信者] の下に、各電子メールアドレス (fileadmin@contoso.comなど) を入力します。 account@domainの形式を使用し、複数のアカウントを区切るにはセミコロンを使用します。  

#### <a name="create-groups-on-file1"></a>FILE1 でグループを作成する  

###### <a name="to-create-security-groups-on-file1"></a>FILE1 でセキュリティ グループを作成するには  

1. Contoso\administrator として FILE1 にサインインし、パスワード: <strong>pass@word1</strong>を使用します。  

2. NT AUTHORITY\Authenticated Users を **WinRMRemoteWMIUsers__** グループに追加します。  

#### <a name="create-files-and-folders-on-file1"></a>FILE1 でファイルおよびフォルダーを作成する  

1.  FILE1 で新規 NTFS ボリュームを作成してから、次のフォルダーを作成します。D:\Finance Documents。  

2.  詳細を指定した次のファイルを作成します。  

    -   **Finance Memo.docx**:ドキュメントに金融関連のテキストを追加します。 たとえば、「finance ドキュメントにアクセスできるユーザーに関するビジネスルールが変更されました。 金融ドキュメントにアクセスできるのは、FinanceExpert グループのメンバーのみになりました。 他の部門やグループはアクセスできません。 ' この変更を環境に実装する前にその影響を評価する必要があります。 このドキュメントの各ページのフッターには、「CONTOSO CONFIDENTIAL」と記載してください。  

    -   **Request for Approval to Hire.docx**:このドキュメントでは、応募者情報を収集するフォームを作成します。 ドキュメント内には次のフィールドが含まれている必要があります。 **応募者名、社会保障番号、職名、提案した給料、開始日、上司名、部門**。 このドキュメントでは、**上司署名、承認された給料、オファー確認**、および**オファー状態**用のフォームが含まれたセクションを追加します。   
        ドキュメント Rights Management は有効にします。  

    -   **Word Document1.docx**:このドキュメントには、テスト内容を追加します。  

    -   **Word Document2.docx**:このドキュメントには、テスト内容を追加します。  

    -   **Workbook1**  

    -   **Workbook2**  

    -   「Regular Expressions」というフォルダーをデスクトップに作成します。 このフォルダー内に **RegEx-SSN** というテキスト ドキュメントを作成します。 ファイル内に次の内容を入力してから、ファイルを保存して閉じます。   
        ^(?!000)([0-7]\d{4}|7([0-7]\d|7[012]))([ -]?)(?!00)\d\d\3(?!0000)\d{4}$  

3.  フォルダー D:\Finance Documents を「Finance Documents」として共有し、この共有に対する読み取りアクセスと書き込みアクセスを全員に許可します。  

> [!NOTE]  
> 既定では、システムまたはブート ボリューム C: では、集約型アクセス ポリシーは有効になっていません。  

#### <a name="install-active-directory-rights-management-services"></a><a name="BKMK_CS1"></a>Active Directory Rights Management サービスのインストール  
サーバー マネージャーを使用して、Active Directory Rights Management サービス (AD RMS) およびすべての必要な機能を追加します。 すべての規定値を選択します。  

###### <a name="to-install-active-directory-rights-management-services"></a>Active Directory Rights Management サービスをインストールするには  

1. CONTOSO\Administrator として、または Domain Admins グループのメンバーとして FILE1 にサインインします。  

   > [!IMPORTANT]  
   > AD RMS サーバーの役割をインストールするために、AD RMS をインストールするサーバー コンピューター上のローカル管理者グループのメンバーシップと、Active Directory 内の Enterprise Admins グループのメンバーシップをインストーラー アカウント (この場合、CONTOSO\Administrator) に付与する必要があります。  

2. サーバー マネージャーで **[役割と機能の追加]** をクリックします。 役割と機能の追加ウィザードが表示されます。  

3. **[開始する前に]** 画面で、 **[次へ]** をクリックします。  

4. **[インストールの種類の選択]** 画面で **[役割ベースまたは機能ベースのインストール]** をクリックし、 **[次へ]** をクリックします。  

5. **[サーバー ターゲットの選択]** 画面で、 **[次へ]** をクリックします。  

6. **[サーバーの役割の選択]** 画面で、 **[Active Directory Rights Management サービス]** の横にあるボックスを選択し、 **[次へ]** をクリックします。  

7. **[Active Directory Rights Management サービスに必要な機能を追加しますか?]** ダイアログ ボックスで、 **[機能の追加]** をクリックします。  

8. **[サーバーの役割の選択]** 画面で、 **[次へ]** をクリックします。  

9. **[インストールする機能の選択]** 画面で、 **[次へ]** をクリックします。  

10. **Active Directory Rights Management サービス** 画面で、次へ をクリックします。  

11. **[役割サービスの選択]** 画面で、 **[次へ]** をクリックします。  

12. **[Web Server Role (IIS)]** (Web サーバーの役割 (IIS)) 画面で、 **[次へ]** をクリックします。  

13. **[役割サービスの選択]** 画面で、 **[次へ]** をクリックします。  

14. **[インストール オプションの確認]** 画面で、 **[インストール]** をクリックします。  

15. インストールが完了した後に、 **[インストールの進行状況]** 画面で **[追加の構成を行います]** をクリックします。 AD RMS 構成ウィザードが表示されます。  

16. **[AD RMS]** 画面で **[次へ]** をクリックします。  

17. **[AD RMS クラスター]** 画面で **[新しい AD RMS ルート クラスターを作成する]** を選択してから、 **[次へ]** をクリックします。  

18. **[構成データベース]** 画面で **[このサーバーの Windows Internal Database を使用する]** をクリックしてから、 **[次へ]** をクリックします。  

    > [!NOTE]  
    > Windows Internal Database では、AD RMS クラスター内の複数のサーバーがサポートされないため、テスト環境のみで使用することをお勧めします。 運用展開では、別個のデータベース サーバーを使用する必要があります。  

19. **[サービスアカウント]** 画面の **[ドメインユーザーアカウント]** で **[指定**] をクリックし、ユーザー名 (**contoso\rms**) とパスワード (<strong>pass@word1</strong>) を指定して、 **[OK]** をクリックし、 **[次へ]** をクリックします。  

20. **[暗号化モード]** 画面で **[暗号化モード 2]** をクリックします。  

21. **[クラスター キーの格納]** 画面で、 **[次へ]** をクリックします。  

22. **[クラスターキーパスワード]** 画面で、 **[パスワード]** ボックスと **[パスワードの確認]** 入力 ボックスに「 <strong>pass@word1</strong>」と入力し、 **[次へ]** をクリックします。  

23. **[クラスター Web サイト]** 画面で、 **[既定の Web サイト]** が選択されていることを確認してから、 **[次へ]** をクリックします。  

24. **[クラスター アドレス]** 画面で **[暗号化されない接続を使用する]** オプションを選択し、 **[完全修飾ドメイン名]** ボックスに **FILE1.contoso.com** と入力してから、 **[次へ]** をクリックします。  

25. **[ライセンサー証明書名]** 画面で、テキスト ボックス内の既定の名前 (**FILE1**) を受け入れ、 **[次へ]** をクリックします。  

26. **[SCP の登録]** 画面で **[SCP をすぐに登録する]** を選択してから、 **[次へ]** をクリックします。  

27. **[確認]** 画面で **[インストール]** をクリックします。  

28. **[結果]** 画面で **[閉じる]** をクリックしてから、 **[インストールの進行状況]** 画面の **[閉じる]** をクリックします。 完了したら、ログオフし、指定されたパスワード (<strong>pass@word1</strong>) を使用して contoso\rms としてログオンします。  

29. AD RMS コンソールを起動し、 **[権利ポリシー テンプレート]** に移動します。  

    AD RMS コンソールを開くには、サーバー マネージャーで、コンソール ツリーの **[ローカル サーバー]** をクリックし、 **[ツール]** をクリックして、 **[Active Directory Rights Management サービス]** をクリックします。  

30. 右側のパネルにある **[配布権利ポリシー テンプレートの作成]** テンプレートをクリックし、 **[追加]** をクリックし、次の情報を選択します。  

    -   言語:英語 (米国)  

    -   名前:Contoso Finance Admin のみ  

    -   説明:Contoso Finance Admin のみ  

    **[追加]** をクリックし、 **[次へ]** をクリックします。  

31. ユーザーと権限 セクションで、**ユーザーと権限** をクリックし、**追加** をクリックして<strong>financeadmin@contoso.com</strong>を入力し、 **OK**をクリックします。  

32. **[フル コントロール]** をセンタユーケーし、 **[所有者 (作成者) に無期限のフル コントロールの権利を付与する]** を選択されたままにします。  

33. 残りのタブを変更せずにクリックして完了してから、 **[完了]** をクリックします。 CONTOSO\Administrator としてサインインします。  

34. フォルダーを参照し、C:\inetpub\wwwroot\\_wmcs 証明書を選択して、サーバー証明 .asmx ファイルを選択し、認証されたユーザーを追加して、ファイルに対する読み取りと書き込みのアクセス許可を付与します。  

35. Windows PowerShell を開き、 `Get-FsrmRmsTemplate`を実行します。 このコマンドを使用して、この手順のこれより前の手順で作成した RMS テンプレートを表示できることを確認します。  

> [!IMPORTANT]  
> ファイル サーバーを即時に変更してテストできるようにするには、次の操作を実行する必要があります。  
>   
> 1.  ファイル サーバー FILE1 で、管理者特権でのコマンド プロンプトを開き、次のコマンドを実行します。  
>   
>     -   gpupdate /force。  
>     -   NLTEST /SC_RESET:contoso.com  
> 2.  ドメイン コントローラー (DC1) で、Active Directory をレプリケートします。  
>   
>     Active Directory のレプリケーションを強制する手順について詳しくは、「 [Active Directory Replication](https://technet.microsoft.com/library/cc794809(WS.10).aspx)」を参照してください。  

必要に応じて、サーバー マネージャーの役割と機能の追加ウィザードを使用する代わりに、次の手順に示すように、Windows PowerShell を使用して、AD RMS サーバーの役割をインストールして構成することができます。  

###### <a name="to-install-and-configure-an-ad-rms-cluster-in-windows-server-2012-using-windows-powershell"></a>Windows Server 2012 で Windows PowerShell を使用して AD RMS クラスターをインストールして構成するには  

1. <strong>pass@word1</strong>パスワードを使用して CONTOSO\Administrator としてログオンします。  

   > [!IMPORTANT]  
   > AD RMS サーバーの役割をインストールするために、AD RMS をインストールするサーバー コンピューター上のローカル管理者グループのメンバーシップと、Active Directory 内の Enterprise Admins グループのメンバーシップをインストーラー アカウント (この場合、CONTOSO\Administrator) に付与する必要があります。  

2. サーバーのデスクトップで、タスク バーの Windows PowerShell アイコンを右クリックし、 **[管理者として実行]** を選択して、管理特権で Windows PowerShell プロンプトを開きます。  

3. サーバー マネージャーのコマンドレットを使用して、AD RMS サーバーの役割をインストールするには、次のコマンドを入力します。  

   ```  
   Add-WindowsFeature ADRMS '"IncludeAllSubFeature '"IncludeManagementTools  
   ```  

4. Windows PowerShell ドライブを作成して、インストールする AD RMS サーバーを表します。  

   たとえば、RC という Windows PowerShell ドライブを作成して AD RMS ルート クラスター内の最初のサーバーをインストールして構成する場合は、次のコマンドを入力します。  

   ```  
   Import-Module ADRMS  
   New-PSDrive -PSProvider ADRMSInstall -Name RC -Root RootCluster  
   ```  

5. 必要な構成設定を表すドライブ名前空間のオブジェクトでプロパティを設定します。  

   例えば、AD RMS サービス アカウントを設定する場合は、Windows PowerShell コマンド プロンプトで次のコマンドを入力します。  

   ```  
   $svcacct = Get-Credential  
   ```  

   Windows セキュリティ ダイアログ ボックスが表示されたら、AD RMS サービス アカウント ドメイン ユーザー名 CONTOSO\RMS および割り当てられているパスワードを入力します。  

   次に、AD RMS サービス アカウントを AD RMS クラスター設定に割り当てるために、次のコマンドを入力します。  

   ```  
   Set-ItemProperty -Path RC:\ -Name ServiceAccount -Value $svcacct  
   ```  

   次に、Windows Internal Database を使用するように AD RMS サーバーを設定するために、Windows PowerShell コマンド プロンプトで次のコマンドを入力します。  

   ```  
   Set-ItemProperty -Path RC:\ClusterDatabase -Name UseWindowsInternalDatabase -Value $true  
   ```  

   次に、変数にクラスター キー パスワードをセキュアに格納するために、Windows PowerShell コマンド プロンプトで次のコマンドを入力します。  

   ```  
   $password = Read-Host -AsSecureString -Prompt "Password:"  
   ```  

   クラスター キー パスワードを入力してから、Enter キーを押します。  

   次に、パスワードを AD RMS インストールに割り当てるために、Windows PowerShell コマンド プロンプトで次のコマンドを入力します。  

   ```  
   Set-ItemProperty -Path RC:\ClusterKey -Name CentrallyManagedPassword -Value $password  
   ```  

   次に、AD RMS クラスター アドレスを設定するために、Windows PowerShell コマンド プロンプトで次のコマンドを入力します。  

   ```  
   Set-ItemProperty -Path RC:\ -Name ClusterURL -Value "http://file1.contoso.com:80"  
   ```  

   次に、AD RMS インストールの SLC 名を割り当てるために、Windows PowerShell コマンド プロンプトで次のコマンドを入力します。  

   ```  
   Set-ItemProperty -Path RC:\ -Name SLCName -Value "FILE1"  
   ```  

   次に、AD RMS クラスターのサービス接続ポイント (SCP) を設定するために、Windows PowerShell コマンド プロンプトで次のコマンドを入力します。  

   ```  
   Set-ItemProperty -Path RC:\ -Name RegisterSCP -Value $true  
   ```  

6. **Install-ADRMS** コマンドレットを実行します。 このコマンドレットは、AD RMS サーバーの役割をインストールしてサーバーを構成する以外に、必要に応じて、AD RMS に必要な他の機能もインストールします。  

   例えば、RC という Windows PowerShell ドライブに変更し、AD RMS をインストールして構成する場合は、以下のコマンドを入力します。  

   ```  
   Set-Location RC:\  
   Install-ADRMS -Path.  
   ```  

   コマンドレットでインストールを開始するかを確認するプロンプトが出されたら、「Y」と入力します。  

7. CONTOSO\Administrator としてログアウトし、指定されたパスワード ("pass@word1") を使用して CONTOSO\RMS としてログオンします。  

   > [!IMPORTANT]  
   > AD RMS サーバーを管理するために、ログオンしていて、サーバーの管理に使用するアカウント (この場合、CONTOSO\RMS) には、AD RMS サーバー コンピューター上のローカル管理者グループのメンバーシップと、Active Directory の Enterprise Admins グループのメンバーシップが付与されている必要があります。  

8. サーバーのデスクトップで、タスク バーの Windows PowerShell アイコンを右クリックし、 **[管理者として実行]** を選択して、管理特権で Windows PowerShell プロンプトを開きます。  

9. Windows PowerShell ドライブを作成して、構成する AD RMS サーバーを表します。  

    たとえば、RC という Windows PowerShell ドライブを作成して AD RMS ルート クラスターを構成する場合は、次のコマンドを入力します。  

    ```  
    Import-Module ADRMSAdmin `  
    New-PSDrive -PSProvider ADRMSAdmin -Name RC -Root http://localhost -Force -Scope Global  
    ```  

10. Contoso 金融管理者に新規権利テンプレートを作成して、AR RMS インストールでフル コントロールを備えたユーザー権利を割り当てるために、Windows PowerShell コマンド プロンプトで次のコマンドを入力します。  

    ```  
    New-Item -Path RC:\RightsPolicyTemplate '"LocaleName en-us -DisplayName "Contoso Finance Admin Only" -Description "Contoso Finance Admin Only" -UserGroup financeadmin@contoso.com  -Right ('FullControl')  
    ```  

11. Contoso 金融管理者の新規権利テンプレートを表示できるかを確認するために、Windows PowerShell コマンド プロンプトで次のようにします。  

    ```  
    Get-FsrmRmsTemplate  
    ```  

    このコマンドレットの出力を確認して、前のステップで作成した RMS テンプレートが存在することを確認します。  

### <a name="build-the-mail-server-srv1"></a>メール サーバー (SRV1) を作成する  
SRV1 は SMTP/POP3 メール サーバーです。 アクセス拒否アシスタンスのシナリオの一環として、電子メールによる通知を送信できるようにこれを設定する必要があります。  

このコンピューターで Microsoft Exchange Server を構成します。 詳細については、「 [How to Install Exchange Server (Exchange Server のインストール方法)](https://go.microsoft.com/fwlink/?prd=12364)」を参照してください。  

### <a name="build-the-client-virtual-machine-client1"></a>クライアント仮想マシン (CLIENT1) を作成する  

##### <a name="to-build-the-client-virtual-machine"></a>クライアント仮想マシンを作成するには  

1. CLIENT1 を ID_AD_Network に接続します。  

2. Microsoft Office 2010 をインストールします。  

3. Contoso\Administrator としてサインインし、次の情報を使用して Microsoft Outlook を構成します。  

   - 名前:File Administrator  

   - 電子メールアドレス: fileadmin@contoso.com  

   - アカウントの種類:POP3  

   - 受信メール サーバー:SRV1 の静的 IP アドレス  

   - 送信 メール サーバー:SRV1 の静的 IP アドレス  

   - ユーザー名: fileadmin@contoso.com  

   - パスワードを保存する:選択  

4. contoso\administrator のデスクトップに Outlook へのショートカットを作成する  

5. Outlook を開き、' 初回起動時 ' メッセージすべてに対処します。  

6. 生成されたすべてのテスト メッセージを削除します。  

7. クライアント仮想マシン上のすべてのユーザーに対して、\\\FILE1\Finance ドキュメントを指す新しいショートカットをデスクトップに作成します。  

8. 必要に応じて、再起動します。  

##### <a name="enable-access-denied-assistance-on-the-client-virtual-machine"></a>クライアント仮想マシンでアクセス拒否アシスタンスを有効にする  

1.  レジストリ エディターを開き、**HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\Explorer** に移動します。  

    -   **EnableShellExecuteFileStreamCheck** を **1** に設定します。  

    -   値:DWORD  

## <a name="lab-setup-for-deploying-claims-across-forests-scenario"></a><a name="BKMK_CF"></a>フォレスト間で信頼性情報を展開するためのラボのセットアップ  

### <a name="build-a-virtual-machine-for-dc2"></a><a name="BKMK_2.1"></a>DC2 用の仮想マシンの構築  

-   Windows Server 2012 ISO から仮想マシンを構築します。  

-   DC2 という名前で仮想マシンを作成します。  

-   仮想マシンを ID_AD_Network に接続します。  

> [!IMPORTANT]  
> 仮想マシンをドメインに参加させ、フォレスト全体で信頼性情報の種類を展開するには、仮想マシンは、関連ドメインの FQDN を解決できなければなりません。 これを実現するには、仮想マシンで DNS 設定を手動で構成する必要が生じることがあります。 詳細については、「 [Configuring a virtual network (仮想ネットワークの構成)](https://technet.microsoft.com/library/cc732470%28v=ws.10%29.aspx)」を参照してください。  
>   
> 静的 IP バージョン 4 (IPv4) アドレスおよびドメイン ネーム システム (DNS) クライアント設定を使用するように、すべての仮想マシン イメージ (サーバーとクライアント) を再構成する必要があります。 詳細については、「 [静的 IP アドレスの DNS クライアントを構成する](https://go.microsoft.com/fwlink/?LinkId=150952)」を参照してください。  

### <a name="set-up-a-new-forest-called-adatumcom"></a><a name="BKMK_2.2"></a>Adatum.com という名前の新しいフォレストを設定します。  

##### <a name="to-install-active-directory-domain-services"></a>Active Directory ドメイン サービスをインストールするには  

1. 仮想マシンを ID_AD_Network に接続します。 パスワード<strong>Pass@word1</strong>を使用して、管理者として DC2 にサインインします。  

2. サーバー マネージャーで、 **[管理]** をクリックし、 **[役割と機能の追加]** をクリックします。  

3. **[開始する前に]** ページで、 **[次へ]** をクリックします。  

4. **[インストールの種類の選択]** ページで **[役割ベースまたは機能ベースのインストール]** をクリックし、 **[次へ]** をクリックします。  

5. **[対象サーバーの選択]** ページで **[サーバー プールからサーバーを選択]** をクリックし、Active Directory ドメイン サービス (AD DS) をインストールするサーバーの名前をクリックしてから、 **[次へ]** をクリックします。  

6. **[サーバーの役割の選択]** ページで、 **[Active Directory Domain Services]** を選択します。 **[役割と機能の追加ウィザード]** ダイアログ ボックスで、 **[機能の追加]** をクリックし、 **[次へ]** をクリックします。  

7. **[機能の選択]** ページで **[次へ]** をクリックします。  

8. **[AD DS]** ページで情報を確認してから、 **[次へ]** をクリックします。  

9. **[確認]** ページで **[インストール]** をクリックします。 [結果] ページの機能のインストールの進行状況バーにより、役割がインストールされていることが示されます。  

10. **[結果]** ページで、インストールが成功したことを確認してから、画面の右上隅の **[管理]** の横にある感嘆符付きの警告アイコンをクリックします。 タスク リストで **このサーバーをドメイン コントローラーに昇格する** リンクをクリックします。  

    > [!IMPORTANT]  
    > **[このサーバーをドメイン コントローラーに昇格する]** をクリックせずに、この時点でインストール ウィザードを閉じた場合、サーバー マネージャーで **[タスク]** をクリックすることで、AD DS インストールを続行できます。  

11. **[配置構成]** ページで **[新しいフォレストを追加する]** をクリックし、ルート ドメインの名前 **adatum.com** を入力してから、 **[次へ]** をクリックします。  

12. **[ドメインコントローラーオプション]** ページで、Windows Server 2012 としてドメインおよびフォレストの機能レベルを選択し、DSRM パスワード<strong>pass@word1</strong>を指定して、 **[次へ]** をクリックします。  

13. **[DNS オプション]** ページで、 **[次へ]** をクリックします。  

14. **[追加オプション]** ページで、 **[次へ]** をクリックします。  

15. **[パス]** ページで、Active Directory データベース、ログ ファイル、および SYSVOL フォルダーの場所を入力し (または既定の場所を受け入れて)、 **[次へ]** をクリックします。  

16. **[オプションの確認]** ページで、選択を確認し、 **[次へ]** をクリックします。  

17. **[前提条件のチェック]** ページで、前提条件の検証が完了していることを確認し、 **[インストール]** をクリックします。  

18. **[結果]** ページで、サーバーがドメイン コントローラーとして正しく構成されたことを確認してから、 **[閉じる]** をクリックします。  

19. サーバーを再起動して AD DS のインストールを完了します。 (既定では、これは自動的に行われます)。  

> [!IMPORTANT]  
> ネットワークが正しく構成されていることを確認するために、両方のフォレストを設定した後に、次の操作を実行する必要があります。  
>   
> -   adatum\administrator として adatum.com にサインインします。 コマンド プロンプト ウィンドウを開き、**nslookup contoso.com** と入力してから、Enter キーを押します。  
> -   contoso\administrator として contoso.com にサインインします。 コマンド プロンプト ウィンドウを開き、**nslookup adatum.com** と入力してから、Enter キーを押します。  
>   
> これらのコマンドがエラーなしで実行された場合、フォレストは相互に通信できます。 nslookup のエラーについて詳しくは、トピック「 [NSlookup.exe の使用方法](https://support.microsoft.com/kb/200525)」のトラブルシューティングのセクションを参照してください。  

### <a name="set-contosocom-as-a-trusting-forest-to-adatumcom"></a><a name="BKMK_2.22"></a>Contoso.com を adatum.com に信頼する側のフォレストとして設定します。  
この手順では、Adatum Corporation サイトと Contoso, Ltd. サイト間に信頼関係を作成します。  

##### <a name="to-set-contoso-as-a-trusting-forest-to-adatum"></a>Adatum に信頼する側のフォレストとして Contoso を設定するには  

1.  管理者として DC2 にサインインします。 **[スタート]** 画面で domain.msc と入力します。  

2.  コンソール ツリーで、adatum.com を右クリックし、[プロパティ] をクリックします。  

3.  **[信頼]** タブで、 **[新しい信頼]** をクリックし、 **[次へ]** をクリックします。  

4.  **信頼の名前** ページの ドメイン ネーム システム (DNS) 名 フィールドに **contoso.com** と入力してから、**次へ** をクリックします。  

5.  **[信頼の種類]** ページで、 **[フォレストの信頼]** をクリックし、 **[次へ]** をクリックします。  

6.  **[信頼の方向]** ページで **[双方向]** をクリックします。  

7.  **[信頼の方向]** ページで **[このドメインと指定されたドメインの両方]** をクリックしてから、 **[次へ]** をクリックします。  

8.  引き続き、ウィザードの手順に従います。  

### <a name="create-additional-users-in-the-adatum-forest"></a><a name="BKMK_2.4"></a>Adatum フォレストに追加のユーザーを作成する  
パスワード<strong>pass@word1</strong>を使用してユーザー Jeff Low を作成し、値**Adatum**で company 属性を割り当てます。  

##### <a name="to-create-a-user-with-the-company-attribute"></a>Company 属性を指定してユーザーを作成するには  

1.  Windows PowerShell で管理者特権でのコマンド プロンプトを開き、次のコードを貼り付けます。  

    ```  
    New-ADUser `  
    -SamAccountName jlow `  
    -Name "Jeff Low" `  
    -UserPrincipalName jlow@adatum.com `  
    -AccountPassword (ConvertTo-SecureString `  
    -AsPlainText "pass@word1" -Force) `  
    -Enabled $true `  
    -PasswordNeverExpires $true `  
    -Path 'CN=Users,DC=adatum,DC=com' `  
    -Company Adatum`  

    ```  

### <a name="create-the-company-claim-type-on-adataumcom"></a><a name="BKMK_2.5"></a>Adataum.com で会社の要求の種類を作成する  

##### <a name="to-create-a-claim-type-by-using-windows-powershell"></a>Windows PowerShell を使用して信頼性情報の種類を作成するには  

1.  管理者として adatum.com にサインインします。  

2.  Windows PowerShell で管理者特権でのコマンド プロンプトを開き、次のコードを入力します。  

    ```  
    New-ADClaimType `  
    -AppliesToClasses:@('user') `  
    -Description:"Company" `  
    -DisplayName:"Company" `  
    -ID:"ad://ext/Company:ContosoAdatum" `  
    -IsSingleValued:$true `  
    -Server:"adatum.com" `  
    -SourceAttribute:Company `  
    -SuggestedValues:@((New-Object Microsoft.ActiveDirectory.Management.ADSuggestedValueEntry("Contoso", "Contoso", "")), (New-Object Microsoft.ActiveDirectory.Management.ADSuggestedValueEntry("Adatum", "Adatum", ""))) `  

    ```  

### <a name="enable-the-company-resource-property-on-contosocom"></a><a name="BKMK_2.55"></a>Contoso.com で Company リソースプロパティを有効にする  

##### <a name="to-enable-the-company-resource-property-on-contosocom"></a>contoso.com で Company リソース プロパティを有効にするには  

1.  管理者として contoso.com にサインインします。  

2.  サーバー マネージャーで **[ツール]** をクリックしてから、 **[Active Directory 管理センター]** をクリックします。  

3.  Active Directory 管理センターの左側のウィンドウで、 **[ツリー ビュー]** をクリックします。 左側のウィンドウで、 **[ダイナミック アクセス制御]** をクリックしてから、 **[リソース プロパティ]** をダブルクリックします。  

4.  **[リソース プロパティ]** リストから **[Company]** を選択し、右クリックして **[プロパティ]** を選択します。 **[提案された値]** セクションで **[追加]** をクリックして次の提案された値を追加します。Contoso および Adatum。次に、 **[OK]** を 2 回クリックします。  

5.  **[リソース プロパティ]** リストから **[Company]** を選択し、右クリックして **[有効にする]** を選択します。  

### <a name="enable-dynamic-access-control-on-adatumcom"></a><a name="BKMK_2.6"></a>Adatum.com での動的 Access Control の有効化  

##### <a name="to-enable-dynamic-access-control-for-adatumcom"></a>adatum.com でダイナミック アクセス制御を有効にするには  

1.  管理者として adatum.com にサインインします。  

2.  グループ ポリシー管理コンソールを開き、**adatum.com** をクリックしてから、 **[ドメイン コントローラー]** をダブルクリックします。  

3.  **[既定のドメイン コントローラー ポリシー]** を右クリックし、 **[編集]** を選択します。  

4.  グループ ポリシー管理エディター ウィンドウで **コンピューターの構成** をダブルクリックし、**ポリシー** をダブルクリックし、**管理用テンプレート** をダブルクリックし、**システム** をダブルクリックしてから、**KDC** をダブルクリックします。  

5.  **[KDC で信頼性情報、複合認証、および Kerberos 防御をサポートする]** をダブルクリックし、 **[有効]** の隣にあるオプションを選択します。 集約型アクセス ポリシーを使用するには、この設定を有効にする必要があります。  

6.  管理者特権のコマンド プロンプトを開き、次のコマンドを実行します。  

    ```  
    gpupdate /force  
    ```  

### <a name="create-the-company-claim-type-on-contosocom"></a><a name="BKMK_2.8"></a>Contoso.com で会社の要求の種類を作成する  

##### <a name="to-create-a-claim-type-by-using-windows-powershell"></a>Windows PowerShell を使用して信頼性情報の種類を作成するには  

1.  管理者として contoso.com にサインインします。  

2.  Windows PowerShell で管理者特権でのコマンド プロンプトを開き、次のコードを入力します。  

    ```  
    New-ADClaimType '"SourceTransformPolicy `  
    '"DisplayName 'Company' `  
    '"ID 'ad://ext/Company:ContosoAdatum' `  
    '"IsSingleValued $true `  
    '"ValueType 'string' `  

    ```  

### <a name="create-the-central-access-rule"></a><a name="BKMK_2.9"></a>集約型アクセス規則を作成する  

##### <a name="to-create-a-central-access-rule"></a>集約型アクセス規則を作成するには  

1. Active Directory 管理センターの左側のウィンドウで、 **[ツリー ビュー]** をクリックします。 左側のウィンドウで、 **[ダイナミック アクセス制御]** をクリックしてから、 **[集約型アクセス規則]** をクリックします。  

2. **[集約型アクセス規則]** を右クリックし、 **[新規作成]** をクリックしてから、 **[集約型アクセス規則]** をクリックします。  

3. **[名前]** フィールドに **AdatumEmployeeAccessRule** と入力します。  

4. **[アクセス許可]** セクションで **[次のアクセス許可を現在のアクセス許可として使用する]** オプションを選択し、 **[編集]** をクリックしてから、 **[追加]** をクリックします。 **[プリンシパルの選択]** リンクをクリックし、 **[Authenticated Users]** と入力してから、 **[OK]** をクリックします。  

5. **[アクセス許可のアクセス許可エントリ]** ダイアログ ボックスで **[条件の追加]** をクリックし、次の条件を入力します。 **[User]** **[Company]** **[Equals]** **[Value]** **[Adatum]** 。 アクセス許可は、 **[変更]、[読み取りと実行]、[読み取り]、[書き込み]** にする必要があります。  

6. **[OK]** をクリックすると、  

7. **[OK]** を 3 回クリックして終了し、Active Directory 管理センターに戻ります。  

   ![ソリューションガイド](media/Appendix-B--Setting-Up-the-Test-Environment/PowerShellLogoSmall.gif)***<em>Windows PowerShell の同等のコマンド</em>***  

   次の Windows PowerShell コマンドレットは、前の手順と同じ機能を実行します。 書式上の制約のため、複数行にわたって折り返される場合でも、各コマンドレットは 1 行に入力してください。  

   ```  
   New-ADCentralAccessRule `  
   -CurrentAcl:"O:SYG:SYD:AR(A;;FA;;;OW)(A;;FA;;;BA)(A;;FA;;;SY)(XA;;0x1301bf;;;AU;(@USER.ad://ext/Company:ContosoAdatum == `"Adatum`"))" `  
   -Name:"AdatumEmployeeAccessRule" `  
   -ProposedAcl:$null `  
   -ProtectedFromAccidentalDeletion:$true `  
   -Server:"contoso.com" `  
   ```  

### <a name="create-the-central-access-policy"></a><a name="BKMK_2.10"></a>集約型アクセスポリシーを作成する  

##### <a name="to-create-a-central-access-policy"></a>集約型アクセスポリシーを作成するには  

1.  管理者として contoso.com にサインインします。  

2.  Windows PowerShell で管理者特権でのコマンド プロンプトを開き、次のコードを貼り付けます。  

    ```  
    New-ADCentralAccessPolicy "Adatum Only Access Policy"   
    Add-ADCentralAccessPolicyMember "Adatum Only Access Policy" `  
    -Member "AdatumEmployeeAccessRule" `  
    ```  

### <a name="publish-the-new-policy-through-group-policy"></a><a name="BKMK_2.11"></a>グループポリシーを使用して新しいポリシーを発行する  

##### <a name="to-apply-the-central-access-policy-across-file-servers-through-group-policy"></a>グループ ポリシーを使用してファイル サーバー全体で集約型アクセス ポリシーを適用するには  

1.  **スタート**画面で、「**管理ツール**」と入力して、 **[検索]** バーで **[設定]** をクリックします。 **[設定]** の結果で、 **[管理ツール]** をクリックします。 **[管理ツール]** フォルダーからグループ ポリシー管理コンソールを開きます。  

    > [!TIP]  
    > **管理ツールを表示** の設定が無効になっていると、管理ツール フォルダーとその内容は **設定** の結果に表示されません。  

2.  Contoso.com ドメインを右クリックし、[**このドメインに GPO を作成し、ここにリンク**します] をクリックします。  

3.  GPO の記述名 (**AdatumAccessGPO** など) を入力してから、 **[OK]** をクリックします。  

##### <a name="to-apply-the-central-access-policy-to-the-file-server-through-group-policy"></a>グループ ポリシーを使用してファイル サーバーに集約型アクセス ポリシーを適用するには  

1.  **[スタート]** 画面の **[検索]** ボックスに「**グループ ポリシーの管理**」と入力します。 管理ツール フォルダーから **グループ ポリシーの管理** を開きます。  

    > [!TIP]  
    > **管理ツールを表示** の設定が無効になっていると、管理ツール フォルダーとその内容は 設定 の結果に表示されません。  

2.  次のように、Contoso に移動して選択します。グループ ポリシーの管理\フォレスト: contoso.com\ドメイン\contoso.com.  

3.  **[AdatumAccessGPO]** ポリシーを右クリックし、 **[編集]** を選択します。  

4.  グループ ポリシー管理エディターで、 **[コンピューターの構成]** をクリックし、 **[ポリシー]** を展開し、 **[Windows の設定]** を展開し、 **[セキュリティの設定]** をクリックします。  

5.  **[ファイル システム]** を展開し、 **[集約型アクセス ポリシー]** を右クリックしてから、 **[集約型アクセス ポリシーの管理]** をクリックします。  

6.  **[集約型アクセス ポリシー構成]** ダイアログ ボックスで **[追加]** をクリックし、 **[Adatum 専用アクセス ポリシー]** を選択してから、 **[OK]** をクリックします。  

7.  グループ ポリシー管理エディターを閉じます。 これで、集約型アクセス ポリシーがグループ ポリシーに追加されました。  

### <a name="create-the-earnings-folder-on-the-file-server"></a><a name="BKMK_2.12"></a>ファイルサーバーでの [所得] フォルダーの作成  
FILE1 で新規 NTFS ボリュームを作成し、次のフォルダーを作成します。D:\Earnings。  

> [!NOTE]  
> 既定では、システムまたはブート ボリューム C: では、集約型アクセス ポリシーは有効になっていません。  

### <a name="set-classification-and-apply-the-central-access-policy-on-the-earnings-folder"></a><a name="BKMK_2.13"></a>分類を設定し、[所得] フォルダーに集約型アクセスポリシーを適用します。  

##### <a name="to-assign-the-central-access-policy-on-the-file-server"></a>ファイル サーバーで集約型アクセス ポリシーを割り当てるには  

1. Hyper-V マネージャーでサーバー FILE1 に接続します。 Contoso\Administrator を使用して、パスワード<strong>pass@word1</strong>でサーバーにサインインします。  

2. 管理者特権でのコマンド プロンプトを開き、コマンド **gpupdate /force** を入力します。 これにより、グループ ポリシーの変更がサーバーで有効になります。  

3. Active Directory からグローバル リソース プロパティーを更新する必要もあります。 Windows PowerShell を開き、「 `Update-FSRMClassificationpropertyDefinition`」と入力して、Enter キーを押します。 Windows PowerShell を閉じます。  

4. エクスプローラーを開き、D:\EARNINGS に移動します。 **[Earnings]** フォルダーを右クリックし、 **[プロパティ]** をクリックします。  

5. **[分類]** タブをクリックします。 **[会社]** を選択し、 **[値]** フィールドで **[Adatum]** を選択します。  

6. **[変更]** をクリックし、ドロップダウン メニューから **[Adatum Only Access Policy]** を選択してから、 **[適用]** をクリックします。  

7. **[セキュリティ]** タブをクリックし、 **[詳細設定]** をクリックして、 **[集約型ポリシー]** タブをクリックします。**Adatumemployeeaccessrule が**が表示されます。 この項目を展開して、Active Directory の規則を作成したときに設定したすべてのアクセス許可を表示できます。  

8. **[OK]** をクリックしてエクスプローラーに戻ります。  



