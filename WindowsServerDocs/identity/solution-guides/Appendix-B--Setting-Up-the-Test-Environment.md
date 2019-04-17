---
ms.assetid: 82918181-525d-4e93-af96-957dac6aedb6
title: "付録 B テスト環境のセットアップ"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: deb08b0663e5f349df7cce51ddabd4aae7f624c5
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="appendix-b-setting-up-the-test-environment"></a>付録 b: テスト環境のセットアップ

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックでは、ダイナミック アクセス制御をテストする実践的ラボを作成する手順について説明します。 」の手順は、コンポーネントが多数存在依存関係があるために順番に従うものです。  
  
## <a name="prerequisites"></a>前提条件  
**ハードウェアおよびソフトウェア要件**  
  
テスト ラボを設定するための要件:  
  
-   SP1 と HYPER-V を Windows Server 2008 R2 を実行しているホスト サーバー  
  
-   Windows Server 2012 ISO のコピー  
  
-   Windows 8 ISO のコピー  
  
-   Microsoft Office 2010  
  
-   Microsoft Exchange Server 2003 以降を実行しているサーバー  
  
ダイナミック アクセス制御シナリオをテストするのには、次のバーチャル マシンを作成する必要があります。  
  
-   DC1 (ドメイン コント ローラー)  
  
-   DC2 (ドメイン コント ローラー)  
  
-   FILE1 (ファイル サーバーおよび Active Directory Rights Management サービス)  
  
-   SRV1 (POP3 および SMTP サーバー)  
  
-   CLIENT1 (Microsoft Outlook でクライアント コンピューター)  
  
仮想マシン用のパスワードは、次のようにする必要があります。  
  
-   BUILTIN\Administrator:pass@word1  
  
-   Contoso \administrator:pass@word1  
  
-   その他のすべてのアカウント:pass@word1  
  
## <a name="build-the-test-lab-virtual-machines"></a>テスト ラボ仮想マシンの作成します。  
  
### <a name="install-the-hyper-v-role"></a>HYPER-V の役割をインストールします。  
Sp1 では Windows Server 2008 R2 を実行するコンピューターで HYPER-V の役割をインストールする必要があります。  
  
##### <a name="to-install-the-hyper-v-role"></a>HYPER-V の役割をインストールするには  
  
1.  をクリックして**開始**、し、[サーバー マネージャー] をクリックします。  
  
2.  サーバー マネージャーのメイン ウィンドウの [役割の概要] をクリックして**役割の追加**します。  
  
3.  **サーバーの役割の選択**] ページで [ **HYPER-V**します。  
  
4.  **仮想ネットワークの作成**] ページで、ネットワーク接続を仮想マシンを利用できるようにする場合は、1 つまたは複数のネットワーク アダプターをクリックします。  
  
5.  **インストール オプションの確認**] ページで [**インストール**します。  
  
6.  インストールを完了するには、コンピューターを再起動する必要があります。 をクリックして**閉じる**ウィザードを終了し、[**はい**コンピューターを再起動します。  
  
7.  コンピューターを再起動した後にの役割をインストールするために使用する同じアカウントでサインインします。 構成の再開ウィザードでは、インストールが完了したら、クリックして**閉じる**ウィザードを完了します。  
  
### <a name="create-an-internal-virtual-network"></a>内部仮想ネットワークを作成します。  
今すぐ ID_AD_Network という内部仮想ネットワークを作成します。  
  
##### <a name="to-create-a-virtual-network"></a>仮想ネットワークを作成するには  
  
1.  HYPER-V マネージャーを開きます。  
  
2.  **アクション**] メニューのをクリックして**仮想ネットワーク マネージャー**します。  
  
3.  **仮想ネットワークの作成**を選択、**内部**します。  
  
4.  をクリックして**追加**します。 **新しい仮想ネットワーク**ページが表示されます。  
  
5.  種類**ID_AD_Network**として新しいネットワークの名前。 その他のプロパティを確認し、必要に応じて変更します。  
  
6.  をクリックして**OK**仮想ネットワークを作成する仮想ネットワーク マネージャーを閉じるか] をクリックする**適用**を仮想ネットワークを作成し、仮想ネットワーク マネージャーの使用を続行します。  
  
### <a name="BKMK_Build"></a>ドメイン コント ローラーをビルドします。  
ドメイン コント ローラー (DC1) として使用する仮想マシンを作成します。 Windows Server 2012 の ISO を使用して仮想マシンをインストールし、その名前を DC1 します。  
  
##### <a name="to-install-active-directory-domain-services"></a>Active Directory ドメイン サービスをインストールするには  
  
1.  仮想マシンを ID_AD_Network に接続します。 管理者としてパスワードを使用して、DC1 にサインインします。 ** pass@word1**します。  
  
2.  サーバー マネージャーで、クリックして**管理**、] をクリックし、**追加の役割と機能**します。  
  
3.  **開始する前に**] ページで [**次**します。  
  
4.  **インストールの種類の選択**] ページで [**役割ベースまたは機能ベースのインストール**、] をクリックし、 **[次へ]**します。  
  
5.  **対象サーバーの選択**] ページで [**次**します。  
  
6.  **サーバーの役割の選択**] ページで [ **Active Directory Domain Services**します。 **追加の役割と機能のウィザード**ダイアログ ボックスで、をクリックして**機能の追加**、] をクリックし、 **[次へ]**します。  
  
7.  **機能の選択**] ページで [**次**します。  
  
8.  **Active Directory Domain Services** ] ページで、情報を確認してをクリックして**次**します。  
  
9. **インストール オプションの確認**] ページで [**インストール**します。 [結果] ページで、機能のインストールの進行状況バーは、役割がインストールされることを示します。  
  
10. **結果**] ページで、インストールが成功したことを確認] をクリックして**閉じる**します。 サーバー マネージャーで、をクリックして、画面の右上隅に感嘆符の付いた警告アイコン] の横に**管理**します。 タスクの一覧でクリックして、**このサーバーのドメイン コント ローラーを昇格**リンクします。  
  
11. **展開構成**] ページで [**新しいフォレストを追加**、ルート ドメインの名前を入力**contoso.com**、] をクリックし、 **[次へ]**します。  
  
12. **ドメイン コント ローラー オプション**ページ、Windows Server 2012 としてドメインとフォレストの機能レベルを選択し、DSRM パスワードを指定** pass@word1 **、] をクリックし、**次**します。  
  
13. **DNS オプション**] ページで [**次**します。  
  
14. **追加オプション**ページで、[**次**します。  
  
15. **パス**ページ、Active Directory データベース、ログ ファイル、および SYSVOL フォルダーの場所を入力 (既定の場所を受け入れて)、] をクリックし、**次**します。  
  
16. **オプションの確認**] ページで、選択内容を確認してをクリックして**次**します。  
  
17. **前提条件のチェック**] ページで、前提条件の検証が完了したら、ことを確認し、をクリックして**インストール**します。  
  
18. **結果**] ページで、サーバーが、ドメイン コント ローラーとして正しく構成されたことを確認してをクリックして**閉じる**します。  
  
19. AD DS のインストールを完了するには、サーバーを再起動します。 (既定では、この自動的に行われます。)  
  
次のユーザーを作成するには、Active Directory 管理センターを使用します。  
  
##### <a name="create-users-and-groups-on-dc1"></a>DC1 でユーザーとグループを作成します。  
  
1.  管理者として contoso.com にサインインします。 Active Directory 管理センターを起動します。  
  
2.  次のセキュリティ グループを作成します。  
  
    |グループ名|電子メール アドレス|  
    |--------------|-----------------|  
    |FinanceAdmin|financeadmin@contoso.com|  
    |FinanceException|financeexception@contoso.com|  
  
3.  次の組織単位 (OU) を作成します。  
  
    |OU 名|コンピューター|  
    |-----------|-------------|  
    |FileServerOU|FILE1|  
  
4.  示されている属性では、次のユーザーを作成します。  
  
    |ユーザー|ユーザー名|電子メール アドレス|部門|グループ|国/地域|  
    |--------|------------|-----------------|--------------|---------|-------------------|  
    |Myriam Delesalle|MDelesalle|MDelesalle@contoso.com|Finance||マイクロソフト|  
    |Miles Reid|MReid|MReid@contoso.com|Finance|FinanceAdmin|マイクロソフト|  
    |Esther Valle|EValle|EValle@contoso.com|操作|FinanceException|マイクロソフト|  
    |Maira Wenzel|MWenzel|MWenzel@contoso.com|人事部||マイクロソフト|  
    |Jeff Low|JLow|JLow@contoso.com|人事部||マイクロソフト|  
    |RMS サーバー|rms|rms@contoso.com||||  
  
    For more information about creating security groups, see [Create a New Group](https://technet.microsoft.com/library/dd861305.aspx) on the Windows Server website.  
  
##### <a name="to-create-a-group-policy-object"></a>グループ ポリシー オブジェクトを作成するには  
  
1.  画面の右上隅にカーソルを置き、検索アイコンをクリックします。 検索ボックスに次のように入力します。**グループ ポリシー管理**、] をクリック**グループ ポリシーの管理**します。  
  
2.  展開**フォレスト: contoso.com**、し、展開**ドメイン**に移動**contoso.com**、展開**(contoso.com)**、し、[ **FileServerOU**します。 右クリック**このドメインに GPO を作成し、次のとおりにリンクします。**
  
3.  など、GPO のわかりやすい名前を入力**FlexibleAccessGPO**、] をクリックし、 **OK**します。  
  
##### <a name="to-enable-dynamic-access-control-for-contosocom"></a>Contoso.com のダイナミック アクセス制御を有効にするには  
  
1.  グループ ポリシー管理コンソールを開き、[ **contoso.com**、順にダブルクリック**ドメイン コント ローラー**します。  
  
2.  右クリック**既定のドメイン コント ローラー ポリシー**、] を選択して**編集**します。  
  
3.  グループ ポリシー管理エディター] ウィンドウでダブルクリック**コンピューターの構成**、] をダブルクリック**ポリシー**、] をダブルクリック**管理用テンプレート**、] をダブルクリック**システム**、順にダブルクリック**KDC**します。  
  
4.  ダブルクリック**KDC で信頼性情報、複合認証、および Kerberos 防御をサポート**オプションを選択する] の横に**有効**します。 集約型アクセス ポリシーを使用するには、この設定を有効にする必要があります。  
  
5.  管理者特権のコマンド プロンプトを開き、次のコマンドを実行します。  
  
    ```  
    gpupdate /force  
    ```  
  
### <a name="BKMK_FS1"></a>ファイル サーバーおよび AD RMS サーバー (FILE1) を構築します。  
  
1.  Windows Server 2012 ISO から file1 という名前の仮想マシンを作成します。  
  
2.  仮想マシンを ID_AD_Network に接続します。  
  
3.  仮想マシンを contoso.com ドメインに参加させるし、パスワードを使用して contoso \administrator として FILE1 にサインイン** pass@word1**します。  
  
#### <a name="install-file-services-resource-manager"></a>ファイル サービス リソース マネージャーをインストールします。  
  
###### <a name="to-install-the-file-services-role-and-the-file-server-resource-manager"></a>ファイル サービスの役割とファイル サーバー リソース マネージャーをインストールするには  
  
1.  サーバー マネージャーで、クリックして**追加の役割と機能**します。  
  
2.  **開始する前に**] ページで [**次**します。  
  
3.  **インストールの種類の選択**ページで、[**次**します。  
  
4.  **対象サーバーの選択**] ページで [**次**します。  
  
5.  **サーバーの役割の選択**] ページで、展開**ファイル サービスおよび記憶域サービス**、横にチェック ボックスを選択**ファイル サービスおよび iSCSI サービス**、展開、および選択**ファイル サーバー リソース マネージャー**します。  
  
    追加の役割と機能のウィザードで、をクリックして**機能の追加**、] をクリックし、 **[次へ]**します。  
  
6.  **機能の選択**] ページで [**次**します。  
  
7.  **インストール オプションの確認**] ページで [**インストール**します。  
  
8.  **インストールの進行状況**] ページで [**閉じる**します。  
  
#### <a name="install-the-microsoft-office-filter-packs-on-the-file-server"></a>ファイル サーバーに Microsoft Office Filter Packs をインストールします。  
幅広い Office ファイルを既定で提供されるよりも用に IFilters を有効にする Windows Server 2012 では、Microsoft Office Filter Packs をインストールする必要があります。  Windows Server 2012 は、既定では、インストールされた Microsoft Office ファイルに対して IFilters をありませんし、ファイル分類インフラストラクチャは IFilters を使用してコンテンツの解析を実行します。  
  
To download and install the IFilters, see [Microsoft Office 2010 Filter Packs](https://go.microsoft.com/fwlink/?LinkID=234122).  
  
#### <a name="configure-email-notifications-on-file1"></a>FILE1 で電子メール通知を構成します。  
クォータおよびファイル スクリーンを作成するときに、そのクォータ制限が近づいているときに、またはブロックされているファイルを保存しようとした後、ユーザーに電子メール通知を送信するオプションがあります。 クォータおよびファイル スクリーンのイベントの特定の管理者に定期的に通知する場合は、1 つまたは複数の既定の受信者を構成することができます。 これらの通知を送信するには、電子メール メッセージの転送に使用する SMTP サーバーを指定する必要があります。  
  
###### <a name="to-configure-email-options-in-file-server-resource-manager"></a>ファイル サーバー リソース マネージャーの電子メールのオプションを構成するには  
  
1.  ファイル サーバー リソース マネージャーを開きます。 ファイル サーバー リソース マネージャーを開くにはクリックして**開始**、種類**ファイル サーバー リソース マネージャー**、] をクリックし、**ファイル サーバー リソース マネージャー**します。  
  
2.  右クリックし、ファイル サーバー リソース マネージャー インターフェイスで**ファイル サーバー リソース マネージャー**、] をクリックし、**オプションを構成する**します。 **ファイル サーバー リソース マネージャーのオプション**] ダイアログ ボックスが開きます。  
  
3.  **電子メール通知**] タブの [SMTP サーバー名または IP アドレス、ホスト名または転送する SMTP サーバーの IP アドレスを入力する通知を電子メールで送信します。  
  
4.  If you want to routinely notify certain administrators of quota or file screening events, under **Default administrator recipients**, type each email address such as fileadmin@contoso.com. Use the format account@domain, and use semicolons to separate multiple accounts.  
  
#### <a name="create-groups-on-file1"></a>FILE1 でグループを作成します。  
  
###### <a name="to-create-security-groups-on-file1"></a>FILE1 でセキュリティ グループを作成するには  
  
1.  パスワードを使用して contoso \administrator として FILE1 にサインインします。 ** pass@word1**します。  
  
2.  NT authority \authenticated Users を追加、 **winrmremotewmiusers _ _**グループ。  
  
#### <a name="create-files-and-folders-on-file1"></a>FILE1 でファイルとフォルダーを作成します。  
  
1.  FILE1 で新規 NTFS ボリュームを作成し、次のフォルダーを作成します。 D:\Finance Documents。  
  
2.  指定された詳細情報を次のファイルを作成します。  
  
    -   **金融 Memo.docx**: 金融ドキュメント内の関連のテキストを追加します。 たとえば、' 金融ドキュメントにアクセスできるユーザーに関するビジネス規則が変更されています。 金融ドキュメントは、FinanceExpert グループのメンバーによってのみアクセスできるようになりました。 その他の部門やグループがあるないアクセスします '。 環境に実装する前にこの変更の影響を評価する必要があります。 このドキュメントにはすべてのページのフッターとして CONTOSO CONFIDENTIAL ことを確認します。  
  
    -   **For Approval to Hire.docx 要求**: 応募者情報を収集するこのドキュメントでフォームを作成します。 ドキュメント内の次のフィールドをする必要があります:**応募者名、社会保障番号、職名、提案した給料、開始日、上司名、部門**します。 用のフォームのあるドキュメントのセクションを追加**上司署名、承認された給料、確認オファー**、および**オファー状態**します。   
        有効になっているドキュメント rights management を確認します。  
  
    -   **Word Document1.docx**: このドキュメントにテスト内容を追加します。  
  
    -   **Word Document2.docx**: 追加するのには、このドキュメントのコンテンツをテストします。  
  
    -   **Workbook1.xlsx**  
  
    -   **Workbook2.xlsx**  
  
    -   Regular Expressions」というデスクトップ上のフォルダーを作成します。 という名前のフォルダーの下にあるテキスト ファイルを作成**REGEX-SSN**します。 ファイルに、次の内容を入力し、保存して閉じてファイル。   
        ^(?!000)([0-7]\d{2}|7([0-7]\d|7[012])) ([-]?)(?!00) \d\d\3 (?0000) \d {4} $  
  
3.  金融ドキュメントとして D:\Finance Documents フォルダーを共有し、すべてのユーザーが読んだおよび、共有への書き込みアクセスを許可します。  
  
> [!NOTE]  
> 集約型アクセス ポリシーは、システムでは既定で無効になってまたはブート ボリューム c: します。  
  
#### <a name="BKMK_CS1"></a>Active Directory Rights Management サービスをインストールします。  
Active Directory Rights Management サービス (AD RMS) とサーバー マネージャーを使ってすべての必要な機能を追加します。 すべての既定値を選択します。  
  
###### <a name="to-install-active-directory-rights-management-services"></a>Active Directory Rights Management サービスをインストールするには  
  
1.  Contoso \administrator としてまたは Domain Admins グループのメンバーとして FILE1 にサインインします。  
  
    > [!IMPORTANT]  
    > AD RMS サーバーの役割をインストーラーをインストールするためには、(この場合、contoso \administrator) でアカウントを両方のローカル管理者グループのメンバーシップ AD RMS がインストールされるサーバー コンピューターおよび Active Directory の Enterprise Admins グループのメンバーシップを付与する必要があります。  
  
2.  サーバー マネージャーで、クリックして**追加の役割と機能**します。 追加の役割と機能のウィザードが表示されます。  
  
3.  **開始する前に**画面で、[**次**します。  
  
4.  **[インストールの種類**画面で、[**役割または機能ベースのインストール**、] をクリックし、 **[次へ]**します。  
  
5.  **サーバー ターゲットの選択**画面で、[**次**します。  
  
6.  **サーバーの役割の選択**画面で、次に、ボックスをオン**Active Directory Rights Management サービス**、] をクリックし、**次**します。  
  
7.  **Active Directory Rights Management サービスに必要な機能を追加しますか?**ダイアログ ボックスで、をクリックして**機能の追加**します。  
  
8.  **サーバーの役割の選択**画面で、[**次**します。  
  
9. **インストールする機能の選択**画面で、[**次**します。  
  
10. **Active Directory Rights Management サービス**画面で、[次へ] をクリックします。  
  
11. **役割サービスの選択**画面で、[**次**します。  
  
12. **Web サーバーの役割 (IIS)**画面で、[**次**します。  
  
13. **役割サービスの選択**画面で、[**次**します。  
  
14. **インストール オプションの確認**画面で、[**インストール**します。  
  
15. 後で、インストールが完了したら、**インストールの進行状況**画面で、[**追加の構成を行います**します。 AD RMS 構成ウィザードが表示されます。  
  
16. **AD RMS**画面で、[**次**します。  
  
17. **AD RMS クラスター**画面で、**新しい AD RMS ルート クラスターを作成**] をクリックし、**次**します。  
  
18. **構成データベース**画面で、[**このサーバー上で使用して Windows Internal Database**、] をクリックし、 **[次へ]**します。  
  
    > [!NOTE]  
    > テスト環境の AD RMS クラスター内の複数のサーバーはサポートされないためにのみは、Windows Internal Database を使用してをお勧めします。 運用展開では、別のデータベース サーバーを使用する必要があります。  
  
19. **サービス アカウント**画面で、**ドメイン ユーザー アカウント**、] をクリックして**を指定する**し、ユーザー名を指定 (**contoso \rms**)、およびパスワード (**pass@word1**)] をクリック**[ok]**、] をクリックし、 **[次へ]**します。  
  
20. **暗号化モード**画面で、[**暗号化モード 2**します。  
  
21. **クラスター キーの格納**画面で、[**次**します。  
  
22. **クラスター キー パスワード**画面で、**パスワード**と**パスワードの確認入力**ボックスで、「 ** pass@word1 **] をクリックし、 **[次へ]**します。  
  
23. **クラスター Web サイト**画面で、ことを確認して**Default Web Site**をクリックして選択して**[次へ]**します。  
  
24. **クラスター アドレス**画面で、**暗号化されていない接続を使用して**オプションを**完全修飾ドメイン名**ボックスに、入力**FILE1.contoso.com**、] をクリックし、 **[次へ]**します。  
  
25. **ライセンサー証明書名**画面で、既定の名前 (**FILE1**)、テキスト ボックスに**次**します。  
  
26. **SCP の登録**画面で、 **SCP を登録できるようになりました**、] をクリックし、**次**します。  
  
27. **確認**画面で、[**インストール**します。  
  
28. **結果**画面で、[**閉じる**、] をクリックし、**閉じる**で**インストールの進行状況**画面です。 完了したら、ログオフして提供されたパスワードを使用して contoso \rms としてログオン (**pass@word1**)。  
  
29. AD RMS コンソールを起動してに移動**権利ポリシー テンプレート**します。  
  
    サーバー マネージャーで、AD RMS コンソールを開くにはクリックして**ローカル サーバー**コンソール ツリーで、をクリックして**ツール**、] をクリックし、 **Active Directory Rights Management サービス**します。  
  
30. をクリックして、**配布権利ポリシーの作成**テンプレートは、右側のパネルにある] をクリックして**追加**、次の情報を選択します。  
  
    -   言語: 英語 (米国)  
  
    -   [名前]: Contoso Finance Admin のみ  
  
    -   説明: Contoso Finance Admin のみ  
  
    をクリックして**追加**、] をクリックし、**次**します。  
  
31. ユーザーおよび権利] セクションで、をクリックして**ユーザーおよび権利**、] をクリックして**追加**、種類** financeadmin@contoso.com **、] をクリック**OK**します。  
  
32. 選択**フル コントロール**をそのまま使用し、**期限なしの権利の許可の所有者 (作成者) フル コントロール**選択します。  
  
33. ただし変更せずに、残りのタブをクリックし、クリックして**完了**します。 Contoso \administrator としてサインインします。  
  
34. C:\inetpub\wwwroot\\_wmcs\certification、フォルダーの選択を ServerCertification.asmx ファイルを参照し、読み取りが、ファイルに対する書き込みアクセス許可を Authenticated Users を追加します。  
  
35. Windows PowerShell を開き、実行`Get-FsrmRmsTemplate`します。 次のコマンドでは、この手順では、前の手順で作成した RMS テンプレートが表示できることを確認します。  
  
> [!IMPORTANT]  
> ファイル サーバーをすぐに変更してテストできるようにする場合は、次の操作が必要です。  
>   
> 1.  ファイル サーバー FILE1 で、管理者特権のコマンド プロンプトを開き、次のコマンドを実行します。  
>   
>     -   gpupdate/force します。  
>     -   NLTEST/SC_RESET:contoso.com  
> 2.  ドメイン コント ローラー (DC1) で、Active Directory をレプリケートします。  
>   
>     For more information about steps to force the replication of Active Directory, see [Active Directory Replication](https://technet.microsoft.com/library/cc794809(WS.10).aspx)  
  
必要に応じてを使用して、追加の役割と機能のウィザードでサーバー マネージャーではなく、インストールして、次の手順で示すように、AD RMS サーバーの役割を構成する Windows PowerShell を使用できます。  
  
###### <a name="to-install-and-configure-an-ad-rms-cluster-in-windows-server-2012-using-windows-powershell"></a>インストールして Windows PowerShell を使用して Windows Server 2012 で AD RMS クラスターを構成するには  
  
1.  パスワードを使用して contoso \administrator としてログオン: ** pass@word1**します。  
  
    > [!IMPORTANT]  
    > AD RMS サーバーの役割をインストーラーをインストールするためには、(この場合、contoso \administrator) でアカウントを両方のローカル管理者グループのメンバーシップ AD RMS がインストールされるサーバー コンピューターおよび Active Directory の Enterprise Admins グループのメンバーシップを付与する必要があります。  
  
2.  サーバーのデスクトップ タスク バーを選択、Windows PowerShell アイコンを右クリックして**管理者として実行**に管理者特権で Windows PowerShell プロンプトを開きます。  
  
3.  AD RMS サーバーの役割をインストールするサーバー マネージャー コマンドレットを使用して、次のように入力します。  
  
    ```  
    Add-WindowsFeature ADRMS '"IncludeAllSubFeature '"IncludeManagementTools  
    ```  
  
4.  インストールする AD RMS サーバーを表す Windows PowerShell ドライブを作成します。  
  
    たとえばをインストールして AD RMS ルート クラスター内の最初のサーバーを構成する RC という Windows PowerShell ドライブを作成するには、次のように入力します。  
  
    ```  
    Import-Module ADRMS  
    New-PSDrive -PSProvider ADRMSInstall -Name RC -Root RootCluster  
    ```  
  
5.  必要な構成設定を表すドライブ名前空間内のオブジェクトのプロパティを設定します。  
  
    たとえば、Windows PowerShell コマンド プロンプトで、AD RMS サービス アカウントを設定するに次のように入力します。  
  
    ```  
    $svcacct = Get-Credential  
    ```  
  
    Windows セキュリティ] ダイアログ ボックスが表示されたら、AD RMS サービス アカウント ドメイン ユーザー名 contoso \rms と割り当てられたパスワードを入力します。  
  
    次に、AD RMS サービス アカウントを AD RMS クラスター設定に割り当てるには、次のように入力します。  
  
    ```  
    Set-ItemProperty -Path RC:\ -Name ServiceAccount -Value $svcacct  
    ```  
  
    次に、Windows PowerShell のコマンド プロンプトで、Windows Internal Database を使用する AD RMS サーバーを設定する次のように入力します。  
  
    ```  
    Set-ItemProperty -Path RC:\ClusterDatabase -Name UseWindowsInternalDatabase -Value $true  
    ```  
  
    次に、Windows PowerShell のコマンド プロンプトで、変数にクラスター キー パスワードを安全に格納する次のように入力します。  
  
    ```  
    $password = Read-Host -AsSecureString -Prompt "Password:"  
    ```  
  
    クラスター キー パスワードを入力し、ENTER キーを押します。  
  
    次に、Windows PowerShell のコマンド プロンプトで、AD RMS のインストールにパスワードを割り当てるに次のように入力します。  
  
    ```  
    Set-ItemProperty -Path RC:\ClusterKey -Name CentrallyManagedPassword -Value $password  
    ```  
  
    次に、Windows PowerShell コマンド プロンプトで、AD RMS クラスター アドレスを設定するに次のように入力します。  
  
    ```  
    Set-ItemProperty -Path RC:\ -Name ClusterURL -Value "http://file1.contoso.com:80"  
    ```  
  
    次に、次のように入力すると、Windows PowerShell のコマンド プロンプトで、AD RMS のインストールの SLC 名を割り当てます。  
  
    ```  
    Set-ItemProperty -Path RC:\ -Name SLCName -Value "FILE1"  
    ```  
  
    次に、Windows PowerShell コマンド プロンプトで、AD RMS クラスターのサービス接続ポイント (SCP) を設定するに次のように入力します。  
  
    ```  
    Set-ItemProperty -Path RC:\ -Name RegisterSCP -Value $true  
    ```  
  
6.  実行、 **INSTALL-ADRMS**コマンドレット。 AD RMS サーバーの役割をインストールし、サーバーの構成に加え、このコマンドレットは、必要に応じて、AD RMS に必要なその他の機能をインストールします。  
  
    たとえば、RC という Windows PowerShell ドライブに変更してインストールし、AD RMS の構成、次のように入力します。  
  
    ```  
    Set-Location RC:\  
    Install-ADRMS -Path.  
    ```  
  
    型"Y"することを確認するプロンプトが表示されたら、コマンドレットは、インストールを開始します。  
  
7.  提供されているパスワードを使用して contoso \rms として contoso \administrator とログとしてログアウトします。 ("pass@word1")。  
  
    > [!IMPORTANT]  
    > AD RMS サーバーを管理するためには、上にログに記録され、サーバー (この場合、contoso \rms) の管理に使用するアカウントは、AD RMS サーバー コンピューターと Active Directory の Enterprise Admins グループのメンバーシップの両方、ローカル管理者グループのメンバーシップを指定する必要があります。  
  
8.  サーバーのデスクトップ タスク バーを選択、Windows PowerShell アイコンを右クリックして**管理者として実行**に管理者特権で Windows PowerShell プロンプトを開きます。  
  
9. 構成して、AD RMS サーバーを表す Windows PowerShell ドライブを作成します。  
  
    たとえば、AD RMS ルート クラスターを構成する RC という Windows PowerShell ドライブを作成するには、次のように入力します。  
  
    ```  
    Import-Module ADRMSAdmin `  
    New-PSDrive -PSProvider ADRMSAdmin -Name RC -Root http://localhost -Force -Scope Global  
    ```  
  
10. Contoso 金融管理者に新規権利テンプレートを作成し、Windows PowerShell コマンド プロンプトで、AD RMS のインストールでフル コントロールを備えたユーザー権利を割り当てる次のように入力します。  
  
    ```  
    New-Item -Path RC:\RightsPolicyTemplate '"LocaleName en-us -DisplayName "Contoso Finance Admin Only" -Description "Contoso Finance Admin Only" -UserGroup financeadmin@contoso.com  -Right ('FullControl')  
    ```  
  
11. Windows PowerShell コマンド プロンプトで、Contoso 金融管理者の新規権利テンプレートを表示できることを確認します。  
  
    ```  
    Get-FsrmRmsTemplate  
    ```  
  
    前の手順で作成した RMS テンプレートを確認するには、このコマンドレットの出力を確認が存在します。  
  
### <a name="build-the-mail-server-srv1"></a>メール サーバー (SRV1) を構築します。  
SRV1 は smtp/pop3 メール サーバーです。 アクセス拒否アシスタンスのシナリオの一部として、電子メール通知を送信できるようにを設定する必要があります。  
  
このコンピューターで Microsoft Exchange Server を構成します。 For more information, see [How to Install Exchange Server](https://go.microsoft.com/fwlink/?prd=12364).  
  
### <a name="build-the-client-virtual-machine-client1"></a>クライアント仮想マシン (CLIENT1) を構築します。  
  
##### <a name="to-build-the-client-virtual-machine"></a>クライアント仮想マシンを作成するには  
  
1.  CLIENT1 を ID_AD_Network に接続します。  
  
2.  Microsoft Office 2010 をインストールします。  
  
3.  Contoso \administrator としてサインインし、Microsoft Outlook を構成する、次の情報を使用します。  
  
    -   自分の名前: File Administrator  
  
    -   電子メール アドレス:fileadmin@contoso.com  
  
    -   アカウントの種類: POP3  
  
    -   受信メール サーバー::srv1 の静的 IP アドレス  
  
    -   送信メール サーバー::srv1 の静的 IP アドレス  
  
    -   ユーザー名:fileadmin@contoso.com  
  
    -   パスワードを保存する: オン  
  
4.  Contoso \administrator のデスクトップに Outlook へのショートカットを作成します。  
  
5.  Outlook を開き、'初回起動' のメッセージを送信します。  
  
6.  生成されたすべてのテスト メッセージを削除します。  
  
7.  \\\FILE1\Finance ドキュメントを指すクライアント仮想マシン上のすべてのユーザーのデスクトップ上の新しいショートカットを作成します。  
  
8.  必要に応じて再起動します。  
  
##### <a name="enable-access-denied-assistance-on-the-client-virtual-machine"></a>クライアント仮想マシンでアクセス拒否アシスタンスを有効にします。  
  
1.  レジストリ エディターを開きに移動**hkey_local_machine \software\policies\microsoft\windows\explorer**します。  
  
    -   設定**EnableShellExecuteFileStreamCheck**に**1**します。  
  
    -   値: DWORD  
  
## <a name="BKMK_CF"></a>フォレスト シナリオ全体で信頼性情報の展開用のラボのセットアップ  
  
### <a name="BKMK_2.1"></a>DC2 の仮想マシンを作成します。  
  
-   Windows Server 2012 ISO から仮想マシンを作成します。  
  
-   DC2 として仮想マシンの名前を作成します。  
  
-   仮想マシンを ID_AD_Network に接続します。  
  
> [!IMPORTANT]  
> 仮想マシンをドメインに参加させると、フォレスト間にわたる要求の種類の展開は、仮想マシンが、関連するドメインの Fqdn を解決できることが必要です。 これを実行する仮想マシン上で、DNS の設定を手動で構成する必要があります。 For more information, see [Configuring a virtual network](https://technet.microsoft.com/library/cc732470%28v=ws.10%29.aspx).  
>   
> すべての仮想マシン イメージ (サーバーとクライアント) は、静的 IP バージョン 4 (IPv4) を使用するように再構成する必要がありますアドレスおよびドメイン ネーム システム (DNS) のクライアント設定します。 For more information, see [Configure a DNS Client for Static IP Address](https://go.microsoft.com/fwlink/?LinkId=150952).  
  
### <a name="BKMK_2.2"></a>Adatum.com という新規フォレストを設定します。  
  
##### <a name="to-install-active-directory-domain-services"></a>Active Directory ドメイン サービスをインストールするには  
  
1.  仮想マシンを ID_AD_Network に接続します。 管理者としてパスワードを使用して、DC2 にサインインします。 ** Pass@word1**します。  
  
2.  サーバー マネージャーで、クリックして**管理**、] をクリックし、**追加の役割と機能**します。  
  
3.  **開始する前に**] ページで [**次**します。  
  
4.  **[インストールの種類**] ページで [**役割ベースまたは機能ベースのインストール**、] をクリックし、 **[次へ]**します。  
  
5.  **対象サーバーの選択**] ページで [**サーバー プールからサーバーを選択**、Active Directory ドメイン サービス (AD DS) をインストールし、をクリックするサーバーの名前をクリックして**[次へ]**します。  
  
6.  **サーバーの役割の選択**] ページで [ **Active Directory Domain Services**します。 **追加の役割と機能のウィザード**ダイアログ ボックスで、をクリックして**機能の追加**、] をクリックし、 **[次へ]**します。  
  
7.  **機能の選択**] ページで [**次**します。  
  
8.  **AD DS** ] ページで、情報を確認してをクリックして**次**します。  
  
9. **確認**] ページで [**インストール**します。 [結果] ページで、機能のインストールの進行状況バーは、役割がインストールされることを示します。  
  
10. **結果**] ページで、インストールが成功したことを確認] の横に、画面の右上隅に感嘆符の付いた警告アイコンをクリックし、**管理**します。 タスクの一覧でクリックして、**このサーバーのドメイン コント ローラーを昇格**リンクします。  
  
    > [!IMPORTANT]  
    > なくする場合この時点で、インストール ウィザードを閉じる] をクリックして**このサーバーのドメイン コント ローラーを昇格**、] をクリックして、AD DS のインストールを続行する**タスク**サーバー マネージャーでします。  
  
11. **展開構成**] ページで [**新しいフォレストを追加**、ルート ドメインの名前を入力**adatum.com**、] をクリックし、 **[次へ]**します。  
  
12. **ドメイン コント ローラー オプション**ページ、Windows Server 2012 としてドメインとフォレストの機能レベルを選択し、DSRM パスワードを指定** pass@word1 **、] をクリックし、**次**します。  
  
13. **DNS オプション**] ページで [**次**します。  
  
14. **追加オプション**ページで、[**次**します。  
  
15. **パス**ページ、Active Directory データベース、ログ ファイル、および SYSVOL フォルダーの場所を入力 (既定の場所を受け入れて)、] をクリックし、**次**します。  
  
16. **オプションの確認**] ページで、選択内容を確認してをクリックして**次**します。  
  
17. **前提条件のチェック**] ページで、前提条件の検証が完了したら、ことを確認し、をクリックして**インストール**します。  
  
18. **結果**] ページで、サーバーが、ドメイン コント ローラーとして正しく構成されたことを確認してをクリックして**閉じる**します。  
  
19. AD DS のインストールを完了するには、サーバーを再起動します。 (既定では、この自動的に行われます。)  
  
> [!IMPORTANT]  
> ネットワークが、両方のフォレストをセットアップした後、正しく構成されていることを確認するには、次の操作を行う必要があります。  
>   
> -   Adatum \administrator として adatum.com にサインインします。 開き、コマンド プロンプト ウィンドウに「 **nslookup contoso.com**し、ENTER キーを押します。  
> -   Contoso \administrator として contoso.com にサインインします。 開き、コマンド プロンプト ウィンドウに「 **nslookup adatum.com**し、ENTER キーを押します。  
>   
> これらのコマンドは、エラーなしで実行する場合、は、フォレストが相互に通信できます。 For more information on nslookup errors, see the troubleshooting section in the topic [Using NSlookup.exe](https://support.microsoft.com/kb/200525)  
  
### <a name="BKMK_2.22"></a>Adatum.com に信頼する側のフォレストとして contoso.com を設定します。  
In this step, you create a trust relationship between the Adatum Corporation site and the Contoso, Ltd. site.  
  
##### <a name="to-set-contoso-as-a-trusting-forest-to-adatum"></a>Adatum に信頼する側のフォレストとして Contoso を設定するには  
  
1.  管理者として DC2 にサインインします。 **開始**画面で domain.msc と入力します。  
  
2.  コンソール ツリーで、adatum.com を右クリックし、[のプロパティ] をクリックします。  
  
3.  **信頼**] タブ、[**新しい信頼**、] をクリックし、 **[次へ]**します。  
  
4.  **信頼の名前**] ページで、入力**contoso.com**、ドメイン ネーム システム (DNS) の名前] フィールドに、およびクリックして**[次へ]**します。  
  
5.  **信頼の種類**] ページで [**フォレストの信頼**、] をクリックし、 **[次へ]**します。  
  
6.  **信頼の方向**] ページで [**双方向**します。  
  
7.  **信頼の方向**ページで、[**両方このドメインおよび指定されたドメイン**、] をクリックし、 **[次へ]**します。  
  
8.  続行すると、ウィザードの指示に従ってください。  
  
### <a name="BKMK_2.4"></a>Adatum フォレストで追加のユーザーを作成します。  
パスワードを使用してユーザー Jeff Low を作成する** pass@word1 **、company 属性値を割り当てると**Adatum**します。  
  
##### <a name="to-create-a-user-with-the-company-attribute"></a>会社の属性を持つユーザーを作成するには  
  
1.  Windows PowerShell で管理者特権のコマンド プロンプトを開きし、次のコードを貼り付けます。  
  
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
  
### <a name="BKMK_2.5"></a>Adataum.com で会社の要求の種類を作成します。  
  
##### <a name="to-create-a-claim-type-by-using-windows-powershell"></a>Windows PowerShell を使用して、要求の種類を作成するには  
  
1.  管理者として adatum.com にサインインします。  
  
2.  Windows PowerShell で、管理者特権のコマンド プロンプトを開き、次のコードを入力します。  
  
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
  
### <a name="BKMK_2.55"></a>Contoso.com で Company リソース プロパティを有効にします。  
  
##### <a name="to-enable-the-company-resource-property-on-contosocom"></a>Contoso.com で Company リソース プロパティを有効にするには  
  
1.  管理者として contoso.com にサインインします。  
  
2.  サーバー マネージャーで、クリックして**ツール**、] をクリックし、 **Active Directory 管理センター**します。  
  
3.  Active Directory 管理センターの左側のウィンドウでをクリックして**ツリー ビュー**します。 左側のウィンドウで [**ダイナミック アクセス制御**、順にダブルクリック**リソース プロパティ**します。  
  
4.  選択**会社**から、**リソース プロパティ**リストを右クリックして選択**プロパティ**します。 **提案された値**セクションで、をクリックして**追加**提案された値を追加する: Contoso および Adatum、] をクリックし、 **OK** 2 回クリックします。  
  
5.  選択**会社**から、**リソース プロパティ**リストを右クリックして選択**を有効にする**します。  
  
### <a name="BKMK_2.6"></a>Adatum.com でダイナミック アクセス制御を有効にします。  
  
##### <a name="to-enable-dynamic-access-control-for-adatumcom"></a>Adatum.com をダイナミック アクセス制御を有効にするには  
  
1.  管理者として adatum.com にサインインします。  
  
2.  グループ ポリシー管理コンソールを開き、[ **adatum.com**、順にダブルクリック**ドメイン コント ローラー**します。  
  
3.  右クリック**既定のドメイン コント ローラー ポリシー**、] を選択して**編集**します。  
  
4.  グループ ポリシー管理エディター] ウィンドウでダブルクリック**コンピューターの構成**、] をダブルクリック**ポリシー**、] をダブルクリック**管理用テンプレート**、] をダブルクリック**システム**、順にダブルクリック**KDC**します。  
  
5.  ダブルクリック**KDC で信頼性情報、複合認証、および Kerberos 防御をサポート**オプションを選択する] の横に**有効**します。 集約型アクセス ポリシーを使用するには、この設定を有効にする必要があります。  
  
6.  管理者特権のコマンド プロンプトを開き、次のコマンドを実行します。  
  
    ```  
    gpupdate /force  
    ```  
  
### <a name="BKMK_2.8"></a>Contoso.com で会社の要求の種類を作成します。  
  
##### <a name="to-create-a-claim-type-by-using-windows-powershell"></a>Windows PowerShell を使用して、要求の種類を作成するには  
  
1.  管理者として contoso.com にサインインします。  
  
2.  開いている Windows PowerShell で、管理者特権のコマンド プロンプトし、次のコードを入力します。  
  
    ```  
    New-ADClaimType '"SourceTransformPolicy `  
    '"DisplayName 'Company' `  
    '"ID 'ad://ext/Company:ContosoAdatum' `  
    '"IsSingleValued $true `  
    '"ValueType 'string' `  
  
    ```  
  
### <a name="BKMK_2.9"></a>集約型アクセス規則を作成します。  
  
##### <a name="to-create-a-central-access-rule"></a>集約型アクセス規則を作成するには  
  
1.  Active Directory 管理センターの左側のウィンドウでをクリックして**ツリー ビュー**します。 左側のウィンドウで [**ダイナミック アクセス制御**、] をクリックし、**集約型アクセス規則**します。  
  
2.  右クリック**集約型アクセス規則**、] をクリックして**新規**、し、**集約型アクセス規則**します。  
  
3.  **名**フィールドを入力**AdatumEmployeeAccessRule**します。  
  
4.  **アクセス許可**] セクションで、選択、**次のアクセス権を使用して現在のアクセス許可として**オプション] をクリックして**編集**、] をクリックし、**追加**します。 をクリックして、**プリンシパルの選択**リンク、入力**Authenticated Users**、] をクリックし、 **OK**します。  
  
5.  **アクセス許可のアクセス許可エントリ**ダイアログ ボックスで、] をクリックして**条件を追加**、し、次の条件を入力します。 [**ユーザー**] [**会社**] [**等しい**] [**値**] [**Adatum**] します。 アクセス許可をする必要があります**変更、読み取りと実行、読み取り、書き込み**します。  
  
6.  をクリックして**OK**します。  
  
7.  をクリックして**OK** 3 回を完了し、Active Directory 管理センターに戻ります。  
  
    ![ソリューション ガイド](media/Appendix-B--Setting-Up-the-Test-Environment/PowerShellLogoSmall.gif)Windows PowerShell と同等のコマンド * * *  
  
    次の Windows PowerShell コマンドレットまたはコマンドレットは、前の手順と同じ機能を実行します。 表示される場合でも可能性があります複数行に改行書式上の制約のためには、各コマンドレットを 1 つの行を入力します。  
  
    ```  
    New-ADCentralAccessRule `  
    -CurrentAcl:"O:SYG:SYD:AR(A;;FA;;;OW)(A;;FA;;;BA)(A;;FA;;;SY)(XA;;0x1301bf;;;AU;(@USER.ad://ext/Company:ContosoAdatum == `"Adatum`"))" `  
    -Name:"AdatumEmployeeAccessRule" `  
    -ProposedAcl:$null `  
    -ProtectedFromAccidentalDeletion:$true `  
    -Server:"contoso.com" `  
    ```  
  
### <a name="BKMK_2.10"></a>集約型アクセス ポリシーを作成します。  
  
##### <a name="to-create-a-central-access-policy"></a>集約型アクセス ポリシーを作成するには  
  
1.  管理者として contoso.com にサインインします。  
  
2.  、Windows PowerShell で管理者特権でコマンド プロンプトを開き、次のコードを貼り付けます。  
  
    ```  
    New-ADCentralAccessPolicy "Adatum Only Access Policy"   
    Add-ADCentralAccessPolicyMember "Adatum Only Access Policy" `  
    -Member "AdatumEmployeeAccessRule" `  
    ```  
  
### <a name="BKMK_2.11"></a>グループ ポリシーによって新しいポリシーを公開します  
  
##### <a name="to-apply-the-central-access-policy-across-file-servers-through-group-policy"></a>グループ ポリシーを介してファイル サーバー全体で集約型アクセス ポリシーを適用するには  
  
1.  **開始**画面で「**管理ツール**し [、**検索**バー、] をクリックして**設定**します。 **設定**結果、] をクリックして**管理ツール**します。 グループ ポリシー管理コンソールを開き、**管理ツール**フォルダー。  
  
    > [!TIP]  
    > 場合、**管理ツールを表示**設定が無効になっている、管理ツール] フォルダーとその内容には表示されません、**設定**結果。  
  
2.  Contoso.com ドメインを右クリックし、をクリックして**このドメインに GPO を作成し、次のとおりにリンクします。**  
  
3.  など、GPO のわかりやすい名前を入力**AdatumAccessGPO**、] をクリックし、 **OK**します。  
  
##### <a name="to-apply-the-central-access-policy-to-the-file-server-through-group-policy"></a>グループ ポリシー経由でファイル サーバーに集約型アクセス ポリシーを適用するには  
  
1.  **開始**画面で「**グループ ポリシーの管理**で、、**検索**ボックス。 開いている**グループ ポリシーの管理**管理ツール] フォルダーからです。  
  
    > [!TIP]  
    > 場合、**管理ツールを表示**設定が無効になっている、管理ツール] フォルダーとその内容は、設定の結果に表示されません。  
  
2.  移動し、次のように Contoso を選択します。 グループ ポリシーの管理 \ フォレスト: contoso.com\Domains\contoso.com します。  
  
3.  右クリックし、 **AdatumAccessGPO**ポリシー、および選択**編集**します。  
  
4.  グループ ポリシー管理エディター] をクリックして**コンピューターの構成**、展開**ポリシー**、展開**Windows 設定**、] をクリックし、**セキュリティ設定**します。  
  
5.  展開**ファイル システム**、右クリックして**集約型アクセス ポリシー**、] をクリックし、**管理集約型アクセス ポリシー**します。  
  
6.  **集約型アクセス ポリシー構成**ダイアログ ボックスで、] をクリックして**追加**を選択**Adatum Only Access Policy**、] をクリックし、 **OK**します。  
  
7.  グループ ポリシー管理エディターを閉じます。 グループ ポリシーに集約型アクセス ポリシーが追加されました。  
  
### <a name="BKMK_2.12"></a>ファイル サーバーで Earnings フォルダーを作成します。  
FILE1 で新規 NTFS ボリュームを作成し、次のフォルダーを作成します。 D:\Earnings。  
  
> [!NOTE]  
> 集約型アクセス ポリシーは、システムでは既定で無効になってまたはブート ボリューム c: します。  
  
### <a name="BKMK_2.13"></a>分類を設定し、Earnings フォルダーで集約型アクセス ポリシーを適用  
  
##### <a name="to-assign-the-central-access-policy-on-the-file-server"></a>ファイル サーバー上の集約型アクセス ポリシーを割り当てる  
  
1.  HYPER-V マネージャーでサーバー FILE1 に接続します。 パスワードを使用して contoso \administrator を使用して、サーバーにサインイン** pass@word1**します。  
  
2.  管理者特権でコマンド プロンプトを開き: **gpupdate/force**します。 これにより、グループ ポリシーの変更が反映されるサーバー上にします。  
  
3.  また、Active Directory からグローバル リソース プロパティーを更新する必要があります。 Windows PowerShell を開き、「`Update-FSRMClassificationpropertyDefinition`し、ENTER キーを押します。 Windows PowerShell を閉じます。  
  
4.  Windows エクスプ ローラーを開き、D:\EARNINGS に移動します。 右クリックし、 **Earnings**フォルダー、およびクリック**プロパティ**します。  
  
5.  Click the **Classification** tab. Select **Company**, and then select **Adatum** in the **Value** field.  
  
6.  をクリックして**変更**[ **Adatum Only Access Policy**クリックして、ドロップダウン メニューから**適用**します。  
  
7.  Click the **Security** tab, click **Advanced**, and then click the **Central Policy** tab. You should see the **AdatumEmployeeAccessRule** listed. すべての Active Directory 内の規則を作成するときに設定したアクセス許可を表示する項目を展開することができます。  
  
8.  をクリックして**OK** Windows エクスプ ローラーに戻ります。  
  


