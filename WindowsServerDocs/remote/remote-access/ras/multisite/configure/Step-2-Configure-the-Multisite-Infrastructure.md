---
title: 手順 2 は、マルチサイトのインフラストラクチャを構成します。
description: このトピックは、「Windows Server 2016 のマルチサイト展開に複数のリモートアクセスサーバーを展開する」の一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: faec70ac-88c0-4b0a-85c7-f0fe21e28257
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 6f020dc2bf5c0dc11d18e886346a98a4a40f3855
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80314053"
---
# <a name="step-2-configure-the-multisite-infrastructure"></a>手順 2 は、マルチサイトのインフラストラクチャを構成します。

>適用対象: Windows Server 2012 R2、Windows Server 2012

マルチサイト展開を構成するのには、いくつかの手順を含むネットワーク インフラストラクチャの設定を変更する必要があります。 その他の Active Directory を構成するサイトとドメイン コント ローラーで、追加のセキュリティ グループを構成すると、自動的に使用しない場合は、グループ ポリシー オブジェクト (Gpo) を構成する構成 Gpo です。  
  
|タスク|説明|  
|----|--------|  
|2.1. 追加の Active Directory サイトを構成する|展開用に追加の Active Directory サイトを構成します。|  
|2.2. 追加のドメインコントローラーを構成する|必要に応じて、追加の Active Directory ドメインコントローラーを構成します。|  
|2.3. セキュリティ グループを構成する|Windows 7 クライアント コンピューターのセキュリティ グループを構成します。|  
|2.4. GPO を構成する|必要に応じてその他のグループ ポリシー オブジェクトを構成します。|  
  
> [!NOTE]  
> このトピックには、説明する手順の一部を自動化するために使用できるサンプルの Windows PowerShell コマンドレットが含まれます。 詳しくは、 [コマンドレットの使用に関するページ](https://go.microsoft.com/fwlink/p/?linkid=230693)をご覧ください。  
  
## <a name="21-configure-additional-active-directory-sites"></a><a name="BKMK_ConfigAD"></a>2.1。 追加の Active Directory サイトを構成する  
すべてのエントリ ポイントは、単一の Active Directory サイトに配置できます。 したがって、マルチサイト構成でリモートアクセスサーバーを実装するには、少なくとも1つの Active Directory サイトが必要です。 最初の Active Directory サイトを作成する必要がある場合、またはマルチサイト展開に追加の Active Directory サイトを使用する場合は、この手順を使用します。 Active Directory サイトを使用して、サービス スナップインを使用して、組織の"s network に新しいサイトの作成します。  

メンバーシップ、 **Enterprise Admins** グループ、または **Domain Admins** 、フォレスト ルート ドメインには、少なくともそれと同等のグループがこの手順を実行するために必要なです。 適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。  

詳細については、次を参照してください。 [フォレストにサイトを追加する](https://technet.microsoft.com/library/cc732761.aspx)です。  

### <a name="to-configure-additional-active-directory-sites"></a>追加の Active Directory サイトを構成するには  
  
1.  プライマリ ドメイン コント ローラーで、次のようにクリックします。 **開始**, 、クリックして **Active Directory サイトとサービス**します。  
  
2.  コンソール ツリーで、Active Directory サイトとサービス コンソールで、右クリック **サイト**, 、クリックして **新しいサイト**します。  
  
3.  **新しいオブジェクト - サイト** ダイアログ ボックスで、 **名前** ボックスで、新しいサイトの名前を入力します。  
  
4.  **リンク名**, をサイト リンク オブジェクトをクリックして、クリックして **OK** 2 回クリックします。  
  
5.  コンソール ツリーで  **サイト**, を右クリックして **サブネット**, 、クリックして **新しいサブネット**します。  
  
6.  **新しいオブジェクト - サブネット** ダイアログ ボックスで、 **プレフィックス**, 、IPv4 または IPv6 サブネットのプレフィックスを入力、 **このプレフィックスのサイト オブジェクトを選択して**  をクリックして、このサブネットに関連付けるサイトをクリックして **ok**します。  
  
7.  デプロイに必要なすべてのサブネットを作成するまで、手順 5. と 6. を繰り返します。  
  
8.  Active Directory サイトとサービスを閉じます。  
  
windows PowerShell の ![](../../../../media/Step-2-Configure-the-Multisite-Infrastructure/PowerShellLogoSmall.gif)***<em>windows powershell の同等のコマンド</em>***  
  
次の Windows PowerShell コマンドレットは、前の手順と同じ機能を実行します。 書式上の制約のため、複数行にわたって折り返される場合でも、各コマンドレットは 1 行に入力してください。  
  
Windows の「Windows PowerShell 用 Active Directory モジュール」機能をインストールするには。  
  
```  
Install-WindowsFeature "Name RSAT-AD-PowerShell  
```  
  
または、「Active Directory PowerShell スナップイン」OptionalFeatures を使用して追加します。  
  
Windows 7"、または Windows Server 2008 R2 では、次のコマンドレットを実行している、Active Directory PowerShell モジュールをインポートする必要があります。  
  
```  
Import-Module ActiveDirectory  
```  
  
Active Directory サイトを構成するには、"秒-"を使用してサイト組み込み DEFAULTIPSITELINK という名前。  
  
```  
New-ADReplicationSite -Name "Second-Site"  
Set-ADReplicationSiteLink -Identity "DEFAULTIPSITELINK" -sitesIncluded @{Add="Second-Site"}  
```  
  
2番目のサイトに IPv4 と IPv6 のサブネットを構成するには、次のようにします。  
  
```  
New-ADReplicationSubnet -Name "10.2.0.0/24" -Site "Second-Site"  
New-ADReplicationSubnet -Name "2001:db8:2::/64" -Site "Second-Site"  
```  
  
## <a name="22-configure-additional-domain-controllers"></a><a name="BKMK_AddDC"></a>2.2。 追加のドメインコントローラーを構成する  
1つのドメインにマルチサイト展開を構成するには、デプロイ内の各サイトに対して1つ以上の書き込み可能なドメインコントローラーを使用することをお勧めします。  
  
この手順を実行するには、少なくとも、ドメインコントローラーがインストールされているドメインの Domain Admins グループのメンバーである必要があります。  
  
詳細については、次を参照してください。 [追加のドメイン コント ローラーをインストールする](https://technet.microsoft.com/library/cc733027.aspx)です。
  
### <a name="to-configure-additional-domain-controllers"></a>追加のドメインコントローラーを構成するには  
  
1.  ドメイン コント ローラーとして機能するサーバーで **サーバー マネージャー**, の **ダッシュ ボード**, 、 をクリックして **役割と機能の追加**します。  
  
2.  クリックして **次** サーバーの役割の選択画面に 3 回  
  
3.  **[サーバーの役割** ] ページで選択 **Active Directory ドメイン サービス**します。 クリックして **機能の追加**  し、順にクリックして **次** 3 回です。  
  
4.  **[確認]** ページで **[インストール]** をクリックします。  
  
5.  インストールが正常に完了すると、クリックして **このサーバーをドメイン コント ローラーを昇格**します。  
  
6.  Active Directory ドメイン サービス構成ウィザード、、 **展開構成**  ページで  **ドメイン コント ローラーを既存のドメインに追加**します。  
  
7.  **ドメイン**, 、ドメインを入力する名前。 たとえば、corp.contoso.com です。  
  
8.  **この操作を実行する資格情報を提供**, をクリックして **変更**します。 **Windows セキュリティ**  ダイアログ ボックスで、追加のドメイン コント ローラーをインストールできるアカウントのユーザー名とパスワードを入力します。 追加のドメイン コントローラーをインストールするには、Enterprise Admins グループまたは Domain Admins グループのメンバーである必要があります。 資格情報の入力が完了したら、クリックして **次**します。  
  
9. **ドメイン コント ローラー オプション**  ページで、次の操作します。  
  
    1.  次の選択を行います。  
  
        -   **ドメイン ネーム システム (DNS) サーバー**"は、このオプションは、ドメイン コント ローラーがドメイン ネーム システム (DNS) サーバーとして機能できるようにに既定で選択されます。 ドメイン コントローラーを DNS サーバーとして使用しない場合はオフにします。  
  
            フォレストルートドメインのプライマリドメインコントローラー (PDC) エミュレーターに DNS サーバーの役割がインストールされていない場合は、追加のドメインコントローラーに DNS サーバーをインストールするオプションは使用できません。 この状況では、回避策としては、AD DS のインストールの前後に DNS サーバーの役割をインストールできます。  
  
            > [!NOTE]  
            > DNS サーバーをインストールするオプションを選択すると、dns サーバーの DNS 委任を作成できなかったことを示すメッセージが表示される場合があります。また、信頼できる名前解決を行うには、dns サーバーに対して dns 委任を手動で作成する必要があります。 追加のドメインコントローラーをフォレストルートドメインまたはツリールートドメインのいずれかにインストールする場合は、DNS 委任を作成する必要はありません。 この場合は、クリックして **はい** と、メッセージは無視します。  
  
        -   **グローバル カタログ (GC)** "既定ではこのオプションを選択します。 これにより、グローバル カタログ、読み取り専用ディレクトリ パーティションがドメイン コントローラーに追加され、グローバル カタログ検索機能が有効になります。  
  
        -   **読み取り専用ドメイン コント ローラー (RODC)** "既定では、このオプションが選択されていません。 追加のドメインコントローラーが読み取り専用になります。つまり、ドメインコントローラーは RODC になります。  
  
    2.  **サイト名**, 、一覧からサイトを選択します。  
  
    3.  **ディレクトリ サービス復元モード (DSRM) パスワードを入力して**, で、 **パスワード** と **パスワードの確認入力**, 2 回、強力なパスワードを入力し、クリックして **次**します。 このパスワードは、AD DS を DSRM でオフライン実行しなければならないタスクの開始に使用する必要があります。  
  
10. **DNS オプション** ] ページで、[、 **DNS 委任** チェック ボックスをクリックして、役割のインストール中に DNS 委任を更新する場合 **次**します。  
  
11. **追加のオプション** ページで入力するか、データベース ファイル、ディレクトリ サービスのログ ファイルとシステム ボリューム (SYSVOL) ファイルのボリュームとフォルダーの場所に移動します。 必要に応じて、レプリケーションのオプションを指定し、クリックして **次**します。  
  
12. **オプションの確認** ページで、インストール オプションを確認し、をクリックして **次**します。  
  
13. **前提条件の確認** ページで、前提条件が検証されたら、をクリックして **インストール**します。  
  
14. クリックして、ウィザードには、構成が完了するまで待機 **閉じる**します。  
  
15. コンピューターを自動的に再起動しない場合は、再起動します。  
  
## <a name="23-configure-security-groups"></a><a name="BKMK_ConfigSG"></a>2.3。 セキュリティ グループを構成する  
マルチサイト展開では、Windows 7 クライアント コンピューターへのアクセスを許可する展開の各エントリ ポイントの Windows 7 クライアント コンピューターの追加のセキュリティ グループが必要です。 Windows 7 クライアント コンピューターを含む複数のドメインがある場合は同じエントリ ポイントの各ドメインのセキュリティ グループを作成する必要があます。 また、両方のドメインのクライアントコンピューターを含む1つのユニバーサルセキュリティグループを使用することもできます。 たとえば、2 つのドメインがある環境でエントリではなく 1 と 3 でのエントリ ポイントでは、Windows 7 クライアント コンピューターへのアクセスを許可したい場合ポイント 2 でし、各ドメイン内の各エントリ ポイントの Windows 7 クライアント コンピューターを含む 2 つの新しいセキュリティ グループを作成します。  
  
### <a name="to-configure-additional-security-groups"></a>追加のセキュリティグループを構成するには  
  
1.  プライマリ ドメイン コント ローラーで、次のようにクリックします。 **開始**, 、クリックして **Active Directory ユーザーとコンピューター**します。  
  
2.  コンソールツリーで、新しいグループを追加するフォルダー (たとえば、corp.contoso.com/Users) を右クリックします。 **[新規作成]** をポイントし、 **[グループ]** をクリックします。  
  
3.  **新しいオブジェクト - グループ** ダイアログ ボックスで、 **グループ名**, 、Win7_Clients_Entrypoint1 など、新しいグループの名前を入力します。  
  
4.  [ **グループのスコープ**, 、] をクリックして **ユニバーサル**, [ **グループの種類**, 、] をクリックして **セキュリティ**, 、順にクリック **OK**します。  
  
5.  新しいセキュリティ グループにコンピューターを追加するには、セキュリティ グループをダブルクリックし、[、 **< Group_Name > プロパティ** ダイアログ ボックスで、をクリックして、 **メンバー** ] タブをクリックします。  
  
6.  **[メンバー]** タブで **[追加]** をクリックします。  
  
7.  このセキュリティ グループに追加し、クリックするには、Windows 7 コンピューターを選択して **OK**します。  
  
8.  必要に応じて、すべてのエントリポイントのセキュリティグループを作成するには、この手順を繰り返します。  
  
windows PowerShell の ![](../../../../media/Step-2-Configure-the-Multisite-Infrastructure/PowerShellLogoSmall.gif)***<em>windows powershell の同等のコマンド</em>***  
  
次の Windows PowerShell コマンドレットは、前の手順と同じ機能を実行します。 書式上の制約のため、複数行にわたって折り返される場合でも、各コマンドレットは 1 行に入力してください。  
  
Windows の「Windows PowerShell 用 Active Directory モジュール」機能をインストールするには。  
  
```  
Install-WindowsFeature "Name RSAT-AD-PowerShell  
```  
  
または、「Active Directory PowerShell スナップイン」OptionalFeatures を使用して追加します。  
  
Windows 7"、または Windows Server 2008 R2 では、次のコマンドレットを実行している、Active Directory PowerShell モジュールをインポートする必要があります。  
  
```  
Import-Module ActiveDirectory  
```  
  
Win7_Clients_Entrypoint1 という名前のセキュリティグループを構成し、次のようなクライアントコンピューターを追加するには:  
  
```  
New-ADGroup -GroupScope universal -Name Win7_Clients_Entrypoint1  
Add-ADGroupMember -Identity Win7_Clients_Entrypoint1 -Members CLIENT2$  
```  
  
## <a name="24-configure-gpos"></a><a name="ConfigGPOs"></a>2.4。 GPO を構成する  
リモート アクセスのマルチサイト展開では、次のグループ ポリシー オブジェクトが必要です。  
  
-   リモートアクセスサーバーのすべてのエントリポイントの GPO。  
  
-   ドメインごとに、Windows 8 クライアント コンピューター用の GPO です。  
  
-   エントリ ポイントごとの Windows 7 クライアント コンピューターを含む各ドメインで GPO サポート Windows 7 に、クライアントが構成されています。  
  
    > [!NOTE]  
    > Windows 7 クライアント コンピューターがあるない場合、コンピューターの Windows 7 用の Gpo を作成する必要はありません。  
  
リモート アクセスを構成するときに自動的に作成、必要なグループ ポリシー オブジェクト"t が存在ない場合します。 グループ ポリシー オブジェクトの作成に必要なアクセス許可がない場合、は、リモート アクセスを構成する前に作成する必要があります。 DirectAccess 管理者は、Gpo に対する完全なアクセス許可を持っている必要があります (Edit + modify security + delete)。  
  
> [!IMPORTANT]  
> リモートアクセス用の Gpo を手動で作成した後、リモートアクセスサーバーに関連付けられている Active Directory サイト内のドメインコントローラーに Active Directory と DFS レプリケーションを実行するのに十分な時間を確保する必要があります。 リモート アクセスが自動的にグループ ポリシー オブジェクトを作成する場合は、待機時間もする必要はありません。  
  
グループ ポリシー オブジェクトを作成するを参照してください。 [を作成し、グループ ポリシー オブジェクトを編集](https://technet.microsoft.com/library/cc754740.aspx)します。  
  
### <a name="domain-controller-maintenance-and-downtime"></a><a name="DCMaintandDowntime"></a>ドメインコントローラーの保守とダウンタイム  
PDC エミュレーターとして実行されているドメインコントローラー、またはサーバー Gpo を管理しているドメインコントローラーでダウンタイムが発生した場合、リモートアクセス構成を読み込んだり変更したりすることはできません。 他のドメインコントローラーが使用可能な場合、クライアント接続には影響しません。  
  
リモートアクセス構成を読み込んだり変更したりするには、クライアントまたはアプリケーションサーバー Gpo の別のドメインコントローラーに PDC エミュレーターの役割を転送します。サーバー Gpo の場合は、サーバー Gpo を管理するドメインコントローラーを変更します。  
  
> [!IMPORTANT]  
> この操作は、ドメイン管理者のみが実行できます。 プライマリドメインコントローラーの変更による影響は、リモートアクセスに限定されません。そのため、PDC エミュレーターの役割を転送するときは注意が必要です。  
  
> [!NOTE]  
> ドメインコントローラーの関連付けを変更する前に、リモートアクセスの展開に含まれるすべての Gpo がドメイン内のすべてのドメインコントローラーにレプリケートされていることを確認してください。 GPO が同期されていない場合は、ドメインコントローラーの関連付けを変更した後に、最近の構成の変更が失われる可能性があります。そのため、構成が壊れている可能性があります。 GPO の同期を確認するを参照してください。 [グループ ポリシー インフラストラクチャの状態を確認](https://technet.microsoft.com/library/jj134176.aspx)します。  
  
#### <a name="to-transfer-the-pdc-emulator-role"></a><a name="TransferPDC"></a>PDC エミュレーターの役割を転送するには  
  
1.  **開始** 画面で「**dsa.msc**, 、ENTER キーを押します。  
  
2.  Active Directory ユーザーとコンピューター コンソールの左側のウィンドウで右クリック **Active Directory ユーザーとコンピューター**, 、クリックして **ドメイン コント ローラーの変更**します。 ディレクトリ サーバーの変更 ダイアログ ボックスで、をクリックして **このドメイン コント ローラーまたは AD LDS インスタンス**, で、一覧には、新しい役割の所有者とする をクリックし、ドメイン コント ローラーが をクリックして **OK**します。  
  
    > [!NOTE]  
    > この手順は、役割の転送先となるドメインコントローラーにない場合に実行する必要があります。 役割の転送先となるドメインコントローラーに既に接続している場合は、この手順を実行しないでください。  
  
3.  コンソール ツリーで、右クリック **Active Directory ユーザーとコンピューター**, 、 をポイント **すべてのタスク**, 、クリックして **操作マスター**します。  
  
4.  [操作マスター] ダイアログ ボックスをクリックして、 **PDC** タブをクリックし、をクリックし、 **変更**します。  
  
5.  をクリックして **はい** クリックして、役割を転送することを確認する **閉じる**します。  
  
#### <a name="to-change-the-domain-controller-that-manages-server-gpos"></a><a name="ChangeDC"></a>サーバー Gpo を管理するドメインコントローラーを変更するには  
  
-   Windows PowerShell コマンドレットを実行  `HYPERLINK "https://technet.microsoft.com/library/hh918412.aspx" Set-DAEntryPointDC` リモート アクセス サーバーに到達できないドメイン コント ローラー名を指定し、 *ExistingDC* パラメーター。 このコマンドは、ドメインコントローラーによって現在管理されているエントリポイントのサーバー Gpo に対するドメインコントローラーの関連付けを変更します。  
  
    -   "Dc1.corp.contoso.com"到達できないドメイン コント ローラーをドメイン コント ローラー"dc2.corp.contoso.com"で置き換えるには、次の操作を行います。  
  
        ```  
        Set-DAEntryPointDC "ExistingDC 'dc1.corp.contoso.com' "NewDC 'dc2.corp.contoso.com' "ErrorAction Inquire  
        ```  
  
    -   到達できないドメイン コント ローラー"dc1.corp.contoso.com"を"DA1.corp.contoso.com"のリモート アクセス サーバーに最も近い Active Directory サイト内のドメイン コント ローラーで置き換えるには、次の操作を行います。  
  
        ```  
        Set-DAEntryPointDC "ExistingDC 'dc1.corp.contoso.com' "ComputerName 'DA1.corp.contoso.com' "ErrorAction Inquire  
        ```  
  
### <a name="change-two-or-more-domain-controllers-that-manage-server-gpos"></a><a name="ChangeTwoDCs"></a>サーバー Gpo を管理する2つ以上のドメインコントローラーを変更する  
サーバー Gpo を管理する2つ以上のドメインコントローラーを使用できない場合は、最小数のケースで使用できません。 この問題が発生した場合、サーバー Gpo のドメインコントローラーの関連付けを変更するには、さらに手順が必要になります。  
  
ドメインコントローラーの関連付け情報は、リモートアクセスサーバーのレジストリとすべてのサーバー Gpo の両方に格納されます。 次の例では、リモート アクセス サーバーを 2 つ、"DA1"の 2 つのエントリ ポイントにある"内のエントリ ポイント 1" と"DA2"「エントリ ポイントの 2」です。 サーバーの GPO の中にドメイン コント ローラー"DC1"で「エントリ ポイント 1」のサーバーの GPO を管理する"エントリ ポイント 2"、"DC2"ドメイン コント ローラーで管理します。 "DC1"と"DC2"の両方は使用できません。 3 番目のドメイン コント ローラーは、まだ使用できるがドメインに"DC3"と"DC1"と"DC2"からのデータが既にレプリケートされている"DC3"にします。  
  
![マルチサイトのインフラストラクチャを構成します。](../../../../media/Step-2-Configure-the-Multisite-Infrastructure/DCAssoc1.png)  
  
##### <a name="to-change-two-or-more-domain-controllers-that-manage-server-gpos"></a>サーバー Gpo を管理する2つ以上のドメインコントローラーを変更するには  
  
1.  "DC2"使用不能なドメイン コント ローラーをドメイン コント ローラー"DC3"で置き換えるには、次のコマンドを実行します。  
  
    ```  
    Set-DAEntryPointDC "ExistingDC 'DC2' "NewDC 'DC3' "ComputerName 'DA2' "ErrorAction Continue  
    ```  
  
    このコマンドは、「エントリ ポイント 2」サーバーのレジストリに GPO のドメイン コント ローラー アソシエーション DA2 のおよび「エントリ ポイント 2 の」サーバー自体の GPO を更新します。ただしは更新されません「エントリ ポイント 1 の」サーバーの GPO によって管理されるドメイン コント ローラーが使用できないためです。  
  
    > [!TIP]  
    > このコマンドの続行値を使用して、 *ErrorAction* パラメーターで、「エントリ ポイント 1 の」サーバー GPO の更新の失敗に関係なく、「エントリ ポイント 2」サーバーの GPO を更新します。  
  
    結果の構成を次の図に示します。  
  
    ![Windows PowerShell](../../../../media/Step-2-Configure-the-Multisite-Infrastructure/DCAssoc2.png)  
  
2.  "DC1"使用不能なドメイン コント ローラーをドメイン コント ローラー"DC3"で置き換えるには、次のコマンドを実行します。  
  
    ```  
    Set-DAEntryPointDC "ExistingDC 'DC1' "NewDC 'DC3' "ComputerName 'DA2' "ErrorAction Continue  
    ```  
  
    このコマンドは、「エントリ ポイント 1」のサーバー GPO や、「エントリ ポイント 1」、「エントリ ポイント 2 の」DA1 のレジストリでサーバーの Gpo のドメイン コント ローラーの関連付けを更新します。 結果の構成を次の図に示します。  
  
    ![Windows PowerShell](../../../../media/Step-2-Configure-the-Multisite-Infrastructure/DCAssoc3.png)  
  
3.  「エントリ ポイント 1 の」サーバー"DC3"と"DC2"を置換し、サーバーが GPO は同期されていません。 ここでは、リモート アクセス サーバーを指定するコマンドを実行している GPO 内の"エントリ ポイント 2"サーバー GPO のドメイン コント ローラーの関連付けを同期する"DA1"用、 *ComputerName* パラメーター。  
  
    ```  
    Set-DAEntryPointDC "ExistingDC 'DC2' "NewDC 'DC3' "ComputerName 'DA1' "ErrorAction Continue  
    ```  
  
    最終的な構成を次の図に示します。  
  
    ![Windows PowerShell](../../../../media/Step-2-Configure-the-Multisite-Infrastructure/DCAssocFinal.png)  
  
### <a name="optimization-of-configuration-distribution"></a><a name="ConfigDistOptimization"></a>構成配布の最適化  
構成を変更すると、サーバー Gpo がリモートアクセスサーバーに伝達された後にのみ、変更が適用されます。 構成の配布時間を短縮するために、リモートアクセスは、サーバー GPO を作成するときに、リモートアクセスサーバーに最も近いハイパーリンク "<https://technet.microsoft.com/library/cc978016.aspx>" である書き込み可能なドメインコントローラーを自動的に選択します。  
  
場合によっては、構成配布時間を最適化するために、サーバー GPO を管理するドメインコントローラーを手動で変更しなければならないことがあります。  
  
-   リモートアクセスサーバーをエントリポイントとして追加するときに、そのサーバーの Active Directory サイトに書き込み可能なドメインコントローラーがありませんでした。 書き込み可能なドメインコントローラーがリモートアクセスサーバーの Active Directory サイトに追加されるようになりました。  
  
-   IP アドレスの変更、または Active Directory サイトとサブネットの変更により、リモートアクセスサーバーが別の Active Directory サイトに移動された可能性があります。  
  
-   エントリポイントに対するドメインコントローラーの関連付けは、ドメインコントローラーでのメンテナンス作業のために手動で変更されましたが、ドメインコントローラーはオンラインに戻りました。  
  
これらのシナリオでは、PowerShell コマンドレットを実行 `Set-DAEntryPointDC` リモート アクセス サーバーで、パラメーターを使用して最適化するために必要なエントリ ポイントの名前を指定して *EntryPointName*します。 この操作は、サーバー GPO を現在格納しているドメインコントローラーの GPO データが、目的の新しいドメインコントローラーに既に完全にレプリケートされている場合にのみ実行してください。  
  
> [!NOTE]  
> ドメインコントローラーの関連付けを変更する前に、リモートアクセスの展開に含まれるすべての Gpo がドメイン内のすべてのドメインコントローラーにレプリケートされていることを確認してください。 GPO が同期されていない場合は、ドメインコントローラーの関連付けを変更した後に、最近の構成の変更が失われる可能性があります。そのため、構成が壊れている可能性があります。 GPO の同期を確認するを参照してください。 [グループ ポリシー インフラストラクチャの状態を確認](https://technet.microsoft.com/library/jj134176.aspx)します。  
  
構成配布時間を最適化するには、次のいずれかの操作を行います。  
  
-   サーバーを管理するには、エントリの GPO ポイント「エントリ ポイント 1 の」最も近い Active Directory サイト内のドメイン コント ローラーを次のコマンドを実行するリモート アクセス サーバー"DA1.corp.contoso.com"。  
  
    ```  
    Set-DAEntryPointDC "EntryPointName 'Entry point 1' "ComputerName 'DA1.corp.contoso.com' "ErrorAction Inquire  
    ```  
  
-   サーバーを管理するには、エントリの GPO ポイント「エントリ ポイント 1」、ドメイン コント ローラー"dc2.corp.contoso.com"、次のコマンドを実行します。  
  
    ```  
    Set-DAEntryPointDC "EntryPointName 'Entry point 1' "NewDC 'dc2.corp.contoso.com' "ComputerName 'DA1.corp.contoso.com' "ErrorAction Inquire  
    ```  
  
    > [!NOTE]  
    > 特定のエントリ ポイントに関連付けられているドメイン コント ローラーを変更する際の場合は、そのエントリ ポイントのメンバーであるリモート アクセス サーバーを指定する必要があります、 *ComputerName* パラメーター。  
  
## <a name="see-also"></a><a name="BKMK_Links"></a>関連項目  
  
-   [手順 3: マルチサイト展開を構成する](Step-3-Configure-the-Multisite-Deployment.md)  
-   [手順 1: 単一サーバーのリモートアクセスの展開を実装する](Step-1-Implement-a-Single-Server-Remote-Access-Deployment.md)  

