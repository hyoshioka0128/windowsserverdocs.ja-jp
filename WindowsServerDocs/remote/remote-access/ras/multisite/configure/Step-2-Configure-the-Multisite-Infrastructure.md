---
title: 手順 2 は、マルチサイトのインフラストラクチャを構成します。
description: このトピックは、ガイドの一部複数リモート アクセス サーバーの展開で Windows Server 2016 の Multisite 展開します。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: faec70ac-88c0-4b0a-85c7-f0fe21e28257
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 2d8d5fbe427f25e9e26eac96d89dc5fae17e197b
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67281052"
---
# <a name="step-2-configure-the-multisite-infrastructure"></a>手順 2 は、マルチサイトのインフラストラクチャを構成します。

>適用先:Windows Server 2012 R2、Windows Server 2012

マルチサイト展開を構成するのには、いくつかの手順を含むネットワーク インフラストラクチャの設定を変更する必要があります。 その他の Active Directory を構成するサイトとドメイン コント ローラーで、追加のセキュリティ グループを構成すると、自動的に使用しない場合は、グループ ポリシー オブジェクト (Gpo) を構成する構成 Gpo です。  
  
|タスク|説明|  
|----|--------|  
|2.1. 追加の Active Directory サイトを構成します。|展開の追加の Active Directory サイトを構成します。|  
|2.2. 追加のドメイン コント ローラーを構成します。|必要に応じて追加の Active Directory ドメイン コント ローラーを構成します。|  
|2.3. セキュリティ グループを構成する|Windows 7 クライアント コンピューターのセキュリティ グループを構成します。|  
|2.4. GPO を構成する|必要に応じてその他のグループ ポリシー オブジェクトを構成します。|  
  
> [!NOTE]  
> このトピックでは、サンプル Windows PowerShell コマンドレットを紹介します。ここで説明する手順の一部はこのコマンドレットで自動化できます。 詳しくは、 [コマンドレットの使用に関するページ](https://go.microsoft.com/fwlink/p/?linkid=230693)をご覧ください。  
  
## <a name="BKMK_ConfigAD"></a>2.1. 追加の Active Directory サイトを構成します。  
すべてのエントリ ポイントは、単一の Active Directory サイトに配置できます。 そのため、少なくとも 1 つの Active Directory サイトがマルチサイト構成のリモート アクセス サーバーの実装に必要です。 最初の Active Directory サイトを作成する必要がある場合、またはマルチサイト展開に追加の Active Directory サイトを使用したい場合は、この手順を使用します。 Active Directory サイトを使用して、サービス スナップインを使用して、組織の"s network に新しいサイトの作成します。  

メンバーシップ、 **Enterprise Admins** グループ、または **Domain Admins** 、フォレスト ルート ドメインには、少なくともそれと同等のグループがこの手順を実行するために必要なです。 適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。  

詳細については、次を参照してください。 [フォレストにサイトを追加する](https://technet.microsoft.com/library/cc732761.aspx)です。  

### <a name="to-configure-additional-active-directory-sites"></a>追加の Active Directory サイトを構成するには  
  
1.  プライマリ ドメイン コント ローラーで、次のようにクリックします。 **開始**, 、クリックして **Active Directory サイトとサービス**します。  
  
2.  コンソール ツリーで、Active Directory サイトとサービス コンソールで、右クリック **サイト**, 、クリックして **新しいサイト**します。  
  
3.  **新しいオブジェクト - サイト** ダイアログ ボックスで、 **名前** ボックスで、新しいサイトの名前を入力します。  
  
4.  **リンク名**, をサイト リンク オブジェクトをクリックして、クリックして **OK** 2 回クリックします。  
  
5.  コンソール ツリーで  **サイト**, を右クリックして **サブネット**, 、クリックして **新しいサブネット**します。  
  
6.  **新しいオブジェクト - サブネット** ダイアログ ボックスで、 **プレフィックス**, 、IPv4 または IPv6 サブネットのプレフィックスを入力、 **このプレフィックスのサイト オブジェクトを選択して**  をクリックして、このサブネットに関連付けるサイトをクリックして **ok**します。  
  
7.  展開に必要なすべてのサブネットを作成するまで、手順 5. と 6. を繰り返します。  
  
8.  Active Directory サイトとサービスを閉じます。  
  
![Windows PowerShell](../../../../media/Step-2-Configure-the-Multisite-Infrastructure/PowerShellLogoSmall.gif)***<em>Windows PowerShell の同等のコマンド</em>***  
  
以下の Windows PowerShell コマンドレットは、前述の手順と同じ機能を実行します。 ここでは書式上の制約のために、折り返されて複数の行にわたって表示される場合もありますが、各コマンドレットは 1 行に入力します。  
  
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
  
IPv4 および IPv6 サブネットの 2 つ目のサイトを構成するには  
  
```  
New-ADReplicationSubnet -Name "10.2.0.0/24" -Site "Second-Site"  
New-ADReplicationSubnet -Name "2001:db8:2::/64" -Site "Second-Site"  
```  
  
## <a name="BKMK_AddDC"></a>2.2. 追加のドメイン コント ローラーを構成します。  
単一ドメインでは、マルチサイト展開を構成するには、展開で各サイト用に少なくとも 1 つの書き込み可能なドメイン コント ローラーがあることをお勧めします。  
  
ドメイン コント ローラーをインストールするドメインの Domain Admins グループのメンバーである必要がある、少なくとも、この手順を実行します。  
  
詳細については、次を参照してください。 [追加のドメイン コント ローラーをインストールする](https://technet.microsoft.com/library/cc733027.aspx)です。
  
### <a name="to-configure-additional-domain-controllers"></a>追加のドメイン コント ローラーを構成するには  
  
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
  
            フォレスト ルート ドメインのプライマリ ドメイン コント ローラー (PDC) エミュレーターの DNS サーバーの役割がインストールされていない場合、追加のドメイン コント ローラーに DNS サーバーをインストールするオプションは使用できません。 この状況では、回避策としては、AD DS のインストールの前後に DNS サーバーの役割をインストールできます。  
  
            > [!NOTE]  
            > DNS サーバーをインストールするオプションを選択した場合に、DNS サーバーの DNS 委任を作成できませんでしたし、信頼性の高い名前解決できるように DNS サーバーに DNS 委任を手動で作成する必要がありますを示すメッセージが表示される可能性があります。 フォレスト ルート ドメインまたはツリーのルート ドメインのいずれかで、追加のドメイン コント ローラーをインストールする場合、DNS 委任を作成することはありません。 この場合は、クリックして **はい** と、メッセージは無視します。  
  
        -   **グローバル カタログ (GC)** "既定ではこのオプションを選択します。 これにより、グローバル カタログ、読み取り専用ディレクトリ パーティションがドメイン コントローラーに追加され、グローバル カタログ検索機能が有効になります。  
  
        -   **読み取り専用ドメイン コント ローラー (RODC)** "既定では、このオプションが選択されていません。 読み取り専用です。 追加のドメイン コント ローラーになりますつまり、RODC のドメイン コント ローラー アプリケーションはします。  
  
    2.  **サイト名**, 、一覧からサイトを選択します。  
  
    3.  **ディレクトリ サービス復元モード (DSRM) パスワードを入力して**, で、 **パスワード** と **パスワードの確認入力**, 2 回、強力なパスワードを入力し、クリックして **次**します。 このパスワードは、AD DS を DSRM でオフライン実行しなければならないタスクの開始に使用する必要があります。  
  
10. **DNS オプション** ] ページで、[、 **DNS 委任** チェック ボックスをクリックして、役割のインストール中に DNS 委任を更新する場合 **次**します。  
  
11. **追加のオプション** ページで入力するか、データベース ファイル、ディレクトリ サービスのログ ファイルとシステム ボリューム (SYSVOL) ファイルのボリュームとフォルダーの場所に移動します。 必要に応じて、レプリケーションのオプションを指定し、クリックして **次**します。  
  
12. **オプションの確認** ページで、インストール オプションを確認し、をクリックして **次**します。  
  
13. **前提条件の確認** ページで、前提条件が検証されたら、をクリックして **インストール**します。  
  
14. クリックして、ウィザードには、構成が完了するまで待機 **閉じる**します。  
  
15. 自動的に再起動しなかった場合は、コンピューターを再起動します。  
  
## <a name="BKMK_ConfigSG"></a>2.3. セキュリティ グループを構成する  
マルチサイト展開では、Windows 7 クライアント コンピューターへのアクセスを許可する展開の各エントリ ポイントの Windows 7 クライアント コンピューターの追加のセキュリティ グループが必要です。 Windows 7 クライアント コンピューターを含む複数のドメインがある場合は同じエントリ ポイントの各ドメインのセキュリティ グループを作成する必要があます。 または、両方のドメインからクライアント コンピューターを含む 1 つのユニバーサル セキュリティ グループを使用できます。 たとえば、2 つのドメインがある環境でエントリではなく 1 と 3 でのエントリ ポイントでは、Windows 7 クライアント コンピューターへのアクセスを許可したい場合ポイント 2 でし、各ドメイン内の各エントリ ポイントの Windows 7 クライアント コンピューターを含む 2 つの新しいセキュリティ グループを作成します。  
  
### <a name="to-configure-additional-security-groups"></a>追加のセキュリティ グループを構成するには  
  
1.  プライマリ ドメイン コント ローラーで、次のようにクリックします。 **開始**, 、クリックして **Active Directory ユーザーとコンピューター**します。  
  
2.  コンソール ツリーで、corp.contoso.com/Users など、新しいグループを追加するフォルダーを右クリックします。 をポイント **新規**, 、クリックして **グループ**します。  
  
3.  **新しいオブジェクト - グループ** ダイアログ ボックスで、 **グループ名**, 、Win7_Clients_Entrypoint1 など、新しいグループの名前を入力します。  
  
4.  [ **グループのスコープ**, 、] をクリックして **ユニバーサル**, [ **グループの種類**, 、] をクリックして **セキュリティ**, 、順にクリック **OK**します。  
  
5.  新しいセキュリティ グループにコンピューターを追加するには、セキュリティ グループをダブルクリックし、[、 **< Group_Name > プロパティ** ダイアログ ボックスで、をクリックして、 **メンバー** ] タブをクリックします。  
  
6.  **[メンバー]** タブで **[追加]** をクリックします。  
  
7.  このセキュリティ グループに追加し、クリックするには、Windows 7 コンピューターを選択して **OK**します。  
  
8.  必要に応じてすべてのエントリ ポイントのセキュリティ グループを作成するには、この手順を繰り返します。  
  
![Windows PowerShell](../../../../media/Step-2-Configure-the-Multisite-Infrastructure/PowerShellLogoSmall.gif)***<em>Windows PowerShell の同等のコマンド</em>***  
  
以下の Windows PowerShell コマンドレットは、前述の手順と同じ機能を実行します。 ここでは書式上の制約のために、折り返されて複数の行にわたって表示される場合もありますが、各コマンドレットは 1 行に入力します。  
  
Windows の「Windows PowerShell 用 Active Directory モジュール」機能をインストールするには。  
  
```  
Install-WindowsFeature "Name RSAT-AD-PowerShell  
```  
  
または、「Active Directory PowerShell スナップイン」OptionalFeatures を使用して追加します。  
  
Windows 7"、または Windows Server 2008 R2 では、次のコマンドレットを実行している、Active Directory PowerShell モジュールをインポートする必要があります。  
  
```  
Import-Module ActiveDirectory  
```  
  
Win7_Clients_Entrypoint1 というセキュリティ グループを構成し、CLIENT2 をという名前のクライアント コンピューターを追加するには。  
  
```  
New-ADGroup -GroupScope universal -Name Win7_Clients_Entrypoint1  
Add-ADGroupMember -Identity Win7_Clients_Entrypoint1 -Members CLIENT2$  
```  
  
## <a name="ConfigGPOs"></a>2.4. GPO を構成する  
リモート アクセスのマルチサイト展開では、次のグループ ポリシー オブジェクトが必要です。  
  
-   リモート アクセス サーバーのすべてのエントリ ポイントの GPO です。  
  
-   ドメインごとに、Windows 8 クライアント コンピューター用の GPO です。  
  
-   エントリ ポイントごとの Windows 7 クライアント コンピューターを含む各ドメインで GPO サポート Windows 7 に、クライアントが構成されています。  
  
    > [!NOTE]  
    > Windows 7 クライアント コンピューターがあるない場合、コンピューターの Windows 7 用の Gpo を作成する必要はありません。  
  
リモート アクセスを構成するときに自動的に作成、必要なグループ ポリシー オブジェクト"t が存在ない場合します。 グループ ポリシー オブジェクトの作成に必要なアクセス許可がない場合、は、リモート アクセスを構成する前に作成する必要があります。 DirectAccess 管理者には、Gpo の完全なアクセス許可が必要です (編集、セキュリティの変更 + + の削除) します。  
  
> [!IMPORTANT]  
> リモート アクセス Gpo を手動で作成した後は Active Directory とリモート アクセス サーバーに関連付けられている Active Directory サイト内のドメイン コント ローラーの DFS レプリケーションの十分な時間を許可する必要があります。 リモート アクセスが自動的にグループ ポリシー オブジェクトを作成する場合は、待機時間もする必要はありません。  
  
グループ ポリシー オブジェクトを作成するを参照してください。 [を作成し、グループ ポリシー オブジェクトを編集](https://technet.microsoft.com/library/cc754740.aspx)します。  
  
### <a name="DCMaintandDowntime"></a>ドメイン コント ローラーの保守およびダウンタイム  
ダウンタイムが発生、PDC エミュレーターとして実行されているドメイン コント ローラーまたはドメイン コント ローラーのサーバーの Gpo を管理するときに読み込むか、リモート アクセスの構成を変更することはできません。 他のドメイン コント ローラーが使用可能な場合、これはクライアント接続に影響しません。  
  
クライアントまたはアプリケーション サーバー Gpo; の別のドメイン コント ローラーに PDC エミュレーターの役割を転送する読み込みや、リモート アクセスの構成の変更サーバー Gpo の場合、サーバーの Gpo を管理するドメイン コント ローラーを変更します。  
  
> [!IMPORTANT]  
> この操作は、ドメイン管理者によってのみ実行できます。 リモート アクセスには、プライマリ ドメイン コント ローラーの変更の影響は限定されていませんそのため、PDC エミュレーターの役割を転送するときに、注意を使用します。  
  
> [!NOTE]  
> ドメイン コント ローラーの関連付けを変更する前に、すべてのドメインのドメイン コント ローラーにレプリケートされているすべてのリモート アクセス展開で Gpo を確認します。 GPO が同期されていない場合は、最新の構成変更が構成が破損する可能性がありますドメイン コント ローラーの関連付けを変更した後に失われます。 GPO の同期を確認するを参照してください。 [グループ ポリシー インフラストラクチャの状態を確認](https://technet.microsoft.com/library/jj134176.aspx)します。  
  
#### <a name="TransferPDC"></a>PDC エミュレーターの役割を転送するには  
  
1.  **開始** 画面で「**dsa.msc**, 、ENTER キーを押します。  
  
2.  Active Directory ユーザーとコンピューター コンソールの左側のウィンドウで右クリック **Active Directory ユーザーとコンピューター**, 、クリックして **ドメイン コント ローラーの変更**します。 ディレクトリ サーバーの変更 ダイアログ ボックスで、をクリックして **このドメイン コント ローラーまたは AD LDS インスタンス**, で、一覧には、新しい役割の所有者とする をクリックし、ドメイン コント ローラーが をクリックして **OK**します。  
  
    > [!NOTE]  
    > 役割を転送するドメイン コント ローラーでない場合は、この手順を実行する必要があります。 既に役割を転送するドメイン コント ローラーに接続している場合は、この手順を実行しないでください。  
  
3.  コンソール ツリーで、右クリック **Active Directory ユーザーとコンピューター**, 、 をポイント **すべてのタスク**, 、クリックして **操作マスター**します。  
  
4.  [操作マスター] ダイアログ ボックスをクリックして、 **PDC** タブをクリックし、をクリックし、 **変更**します。  
  
5.  をクリックして **はい** クリックして、役割を転送することを確認する **閉じる**します。  
  
#### <a name="ChangeDC"></a>サーバーの Gpo を管理するドメイン コント ローラーを変更するには  
  
-   Windows PowerShell コマンドレットを実行  `HYPERLINK "https://technet.microsoft.com/library/hh918412.aspx" Set-DAEntryPointDC` リモート アクセス サーバーに到達できないドメイン コント ローラー名を指定し、 *ExistingDC* パラメーター。 このコマンドは、そのドメイン コント ローラーによって現在管理されているエントリ ポイントのサーバー Gpo のドメイン コント ローラーの関連付けを変更します。  
  
    -   "Dc1.corp.contoso.com"到達できないドメイン コント ローラーをドメイン コント ローラー"dc2.corp.contoso.com"で置き換えるには、次の操作を行います。  
  
        ```  
        Set-DAEntryPointDC "ExistingDC 'dc1.corp.contoso.com' "NewDC 'dc2.corp.contoso.com' "ErrorAction Inquire  
        ```  
  
    -   到達できないドメイン コント ローラー"dc1.corp.contoso.com"を"DA1.corp.contoso.com"のリモート アクセス サーバーに最も近い Active Directory サイト内のドメイン コント ローラーで置き換えるには、次の操作を行います。  
  
        ```  
        Set-DAEntryPointDC "ExistingDC 'dc1.corp.contoso.com' "ComputerName 'DA1.corp.contoso.com' "ErrorAction Inquire  
        ```  
  
### <a name="ChangeTwoDCs"></a>サーバーの Gpo を管理する 2 つ以上のドメイン コント ローラーを変更します。  
ケースの数を最小限のサーバーの Gpo を管理する 2 つ以上のドメイン コント ローラーは使用できません。 このような場合は、サーバーの Gpo のドメイン コント ローラーの関連付けを変更する複数の手順が必要です。  
  
ドメイン コント ローラーの関連付け情報は、リモート アクセス サーバーのレジストリとすべてのサーバー Gpo の両方に格納されます。 次の例では、リモート アクセス サーバーを 2 つ、"DA1"の 2 つのエントリ ポイントにある"内のエントリ ポイント 1" と"DA2"「エントリ ポイントの 2」です。 サーバーの GPO の中にドメイン コント ローラー"DC1"で「エントリ ポイント 1」のサーバーの GPO を管理する"エントリ ポイント 2"、"DC2"ドメイン コント ローラーで管理します。 "DC1"と"DC2"の両方は使用できません。 3 番目のドメイン コント ローラーは、まだ使用できるがドメインに"DC3"と"DC1"と"DC2"からのデータが既にレプリケートされている"DC3"にします。  
  
![マルチサイトのインフラストラクチャを構成します。](../../../../media/Step-2-Configure-the-Multisite-Infrastructure/DCAssoc1.png)  
  
##### <a name="to-change-two-or-more-domain-controllers-that-manage-server-gpos"></a>サーバーの Gpo を管理する 2 つ以上のドメイン コント ローラーを変更するには  
  
1.  "DC2"使用不能なドメイン コント ローラーをドメイン コント ローラー"DC3"で置き換えるには、次のコマンドを実行します。  
  
    ```  
    Set-DAEntryPointDC "ExistingDC 'DC2' "NewDC 'DC3' "ComputerName 'DA2' "ErrorAction Continue  
    ```  
  
    このコマンドは、「エントリ ポイント 2」サーバーのレジストリに GPO のドメイン コント ローラー アソシエーション DA2 のおよび「エントリ ポイント 2 の」サーバー自体の GPO を更新します。ただしは更新されません「エントリ ポイント 1 の」サーバーの GPO によって管理されるドメイン コント ローラーが使用できないためです。  
  
    > [!TIP]  
    > このコマンドの続行値を使用して、 *ErrorAction* パラメーターで、「エントリ ポイント 1 の」サーバー GPO の更新の失敗に関係なく、「エントリ ポイント 2」サーバーの GPO を更新します。  
  
    結果の構成は、次の図に示されています。  
  
    ![Windows PowerShell](../../../../media/Step-2-Configure-the-Multisite-Infrastructure/DCAssoc2.png)  
  
2.  "DC1"使用不能なドメイン コント ローラーをドメイン コント ローラー"DC3"で置き換えるには、次のコマンドを実行します。  
  
    ```  
    Set-DAEntryPointDC "ExistingDC 'DC1' "NewDC 'DC3' "ComputerName 'DA2' "ErrorAction Continue  
    ```  
  
    このコマンドは、「エントリ ポイント 1」のサーバー GPO や、「エントリ ポイント 1」、「エントリ ポイント 2 の」DA1 のレジストリでサーバーの Gpo のドメイン コント ローラーの関連付けを更新します。 結果の構成は、次の図に示されています。  
  
    ![Windows PowerShell](../../../../media/Step-2-Configure-the-Multisite-Infrastructure/DCAssoc3.png)  
  
3.  「エントリ ポイント 1 の」サーバー"DC3"と"DC2"を置換し、サーバーが GPO は同期されていません。 ここでは、リモート アクセス サーバーを指定するコマンドを実行している GPO 内の"エントリ ポイント 2"サーバー GPO のドメイン コント ローラーの関連付けを同期する"DA1"用、 *ComputerName* パラメーター。  
  
    ```  
    Set-DAEntryPointDC "ExistingDC 'DC2' "NewDC 'DC3' "ComputerName 'DA1' "ErrorAction Continue  
    ```  
  
    最終的な構成は、次の図に表示されます。  
  
    ![Windows PowerShell](../../../../media/Step-2-Configure-the-Multisite-Infrastructure/DCAssocFinal.png)  
  
### <a name="ConfigDistOptimization"></a>構成の配布の最適化  
構成の変更を行うときに、変更は、サーバーの Gpo はリモート アクセス サーバーに伝達した後にのみ適用されます。 構成配布の時間を減らすためには、リモート アクセスを自動的に選択ハイパーリンクである書き込み可能なドメイン コント ローラー"<https://technet.microsoft.com/library/cc978016.aspx>"リモート アクセス サーバーのサーバーの GPO を作成するときに最も近い。  
  
一部のシナリオでは、構成の配布にかかる時間を最適化するために、サーバーの GPO を管理するドメイン コント ローラーを手動で変更が必要があります。  
  
-   書き込み可能なドメイン コント ローラーになかったリモート アクセス サーバーの Active Directory サイトのエントリ ポイントとして追加することにします。 書き込み可能なドメイン コント ローラーは、リモート アクセス サーバーの Active Directory サイトに追加されるようになりましたが。  
  
-   IP アドレスの変更、または Active Directory サイトとサブネットの変更、可能性がありますと、リモート アクセス サーバーが別の Active Directory サイトに移動されました。  
  
-   ドメイン コント ローラーで、メンテナンス作業により、このエントリ ポイントのドメイン コント ローラーの関連付けを手動で変更して、ドメイン コント ローラーがオンラインに戻るようになりました。  
  
これらのシナリオでは、PowerShell コマンドレットを実行 `Set-DAEntryPointDC` リモート アクセス サーバーで、パラメーターを使用して最適化するために必要なエントリ ポイントの名前を指定して *EntryPointName*します。 この設定は、現在既に完全には GPO が目的の新しいドメイン コント ローラーにレプリケートするサーバーを格納するドメイン コント ローラーから GPO のデータの後にのみ行う必要があります。  
  
> [!NOTE]  
> ドメイン コント ローラーの関連付けを変更する前に、すべてのドメインのドメイン コント ローラーにレプリケートされているすべてのリモート アクセス展開で Gpo を確認します。 GPO が同期されていない場合は、最新の構成変更が構成が破損する可能性がありますドメイン コント ローラーの関連付けを変更した後に失われます。 GPO の同期を確認するを参照してください。 [グループ ポリシー インフラストラクチャの状態を確認](https://technet.microsoft.com/library/jj134176.aspx)します。  
  
構成配布の時間を最適化するには、次のいずれかの操作を行います。  
  
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
  
## <a name="BKMK_Links"></a>参照してください。  
  
-   [手順 3:マルチサイト展開を構成します。](Step-3-Configure-the-Multisite-Deployment.md)  
-   [ステップ 1: 単一サーバーのリモート アクセスの展開を実装します。](Step-1-Implement-a-Single-Server-Remote-Access-Deployment.md)  

