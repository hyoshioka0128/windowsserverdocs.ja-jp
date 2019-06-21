---
title: Configure a Multi-Forest Deployment
description: このトピックでは、Windows Server 2016 でのマルチ フォレスト環境でのリモート アクセスの展開ガイドの一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3c8feff2-cae1-4376-9dfa-21ad3e4d5d99
ms.author: pashort
author: shortpatti
ms.openlocfilehash: bf9222293dfd22b6f32cf00021f34b44c555e340
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67281103"
---
# <a name="configure-a-multi-forest-deployment"></a>Configure a Multi-Forest Deployment

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

このトピックでは、いくつかの可能なシナリオでリモート アクセス マルチフォレスト展開を構成する方法について説明します。 これらのすべてのシナリオでは、DirectAccess が現在 Forest1 という名前の単一のフォレスに展開されていること、および Forest2 という名前の新しいフォレストと連携するように DirectAccess を構成していることを前提にしています。  
  
## <a name="AccessForest2"></a>Forest2 からリソースにアクセス  
このシナリオでは、DirectAccess が Forest1 に既に展開され、クライアントが Forest1 から企業ネットワークにアクセスできるように構成されています。 既定では、DirectAccess 経由で接続されたクライアントは Forest1 内のリソースにのみアクセスでき、Forest2 のどのサーバーにもアクセスできません。  
  
#### <a name="to-enable-directaccess-clients-to-access-resources-from-forest2"></a>DirectAccess クライアントが Forest2 からリソースにアクセスできるようにするには  
  
1.  Forest2 の DNS サフィックスが Forest1 の DNS サフィックスの一部になっていない場合は、Forest2 のドメインのサフィックスに NRPT 規則を追加し、必要に応じて Forest2 のドメインのサフィックスを DNS サフィックス検索一覧に追加します。  
  
2.  IPv6 が内部ネットワークに展開されている場合、Forest2 に関連の内部 IPv6 プレフィックスを追加します。  
  
## <a name="EnableForest2DA"></a>DirectAccess 経由で接続に Forest2 からクライアントを有効にします。  
このシナリオでは、クライアントが Forest2 から企業ネットワークにアクセスできるようにリモート アクセスの展開を構成します。 Forest2 のクライアント コンピューターに必要なセキュリティ グループを作成していることが前提になります。   
  
#### <a name="to-allow-clients-from-forest2-to-access-the-corporate-network"></a>クライアントが Forest2 から企業ネットワークにアクセスできるようにするには  
  
1.  クライアントのセキュリティ グループを Forest2 から追加します。  
  
2.  Forest2 の DNS サフィックスが Forest1 の DNS サフィックスの一部ではない場合は、forest2 の認証では、ドメイン コント ローラーへのアクセスを有効にするクライアントのドメインのサフィックスに NRPT 規則を追加および必要に応じて、DNS suf に Forest2 のドメインのサフィックスを追加検索ボックスの一覧を修正します。 
  
3.  Forest2 に内部 IPv6 プレフィックスを追加して、DirectAccess で認証用のドメイン コントローラーへの IPsec トンネルを作成できるようにします。  
  
4.  管理サーバーの一覧を更新します。  
  
## <a name="AddEPForest2"></a>Forest 2 からエントリ ポイントを追加します。  
このシナリオでは、DirectAccess が Forest1 上のマルチサイト構成に展開されており、DA2 という名前のリモート アクセス サーバーを、既存の DirectAccess マルチサイト展開へのエントリ ポイントとして Forest2 から追加します。  
  
#### <a name="to-add-a-remote-access-server-from-forest2-as-an-entry-point"></a>リモート アクセス サーバーを、エントリ ポイントとして Forest2 から追加するには  
  
1.  リモート アクセス管理者に DA2 のドメインで GPO を書き込む十分なアクセス許可があること、およびリモート アクセス管理者が DA2 のローカル管理者であることを確認します。  
  
2.  DA2 をエントリ ポイントとして追加します。   
  
3.  Forest2 のドメインのサフィックスに NRPT 規則を追加して、認証用のドメイン コントローラーにアクセスできるようにします。また、必要に応じて Forest2 のドメインのサフィックスを DNS サフィックス検索一覧に追加します。  
  
4.  Forest2 に関連の内部 IPv6 プレフィックスを必要に応じて追加し、リモート アクセスで企業リソースへの IPsec トンネルを確立できるようにしたり、NCSI プローブが正しく動作していることを確認したりします。  
  
5.  管理サーバーの一覧を更新します。  
  
## <a name="OTPMultiForest"></a>マルチ フォレスト展開で OTP を構成します。  
マルチフォレスト展開で OTP を構成する場合は次の用語に注意してください。  
  
-   ルート CA をフォレスト メインの PKI ツリー CA です。  
  
-   すべてのエンタープライズ CA の他の Ca。  
  
-   リソース フォレストのフォレストでは、ルート CA を含み、'管理フォレスト \ ドメイン' と見なされます。  
  
-   すべてのアカウント フォレスト トポロジ内の他のフォレスト。  
  
この手順には、PowerShell スクリプトの PKISync.ps1 が必要です。 参照してください[AD CS:フォレスト間証明書の登録のための PKISync.ps1 スクリプト](https://technet.microsoft.com/library/ff961506.aspx)します。  
  
> [!NOTE]  
> このトピックでは、サンプル Windows PowerShell コマンドレットを紹介します。ここで説明する手順の一部はこのコマンドレットで自動化できます。 詳しくは、 [コマンドレットの使用に関するページ](https://go.microsoft.com/fwlink/p/?linkid=230693)をご覧ください。  
  
### <a name="BKMK_CertPub"></a>証明書の発行元として Ca を構成します。  
  
1.  管理者特権でのコマンド プロンプトで次のコマンドを実行して、すべてのフォレストのすべてのエンタープライズ CA で LDAP 紹介サポートを有効にします。  
  
    ```  
    certutil -setreg Policy\EditFlags +EDITF_ENABLELDAPREFERRALS  
    ```  
  
2.  すべてのエンタープライズ CA コンピューター アカウントを、各アカウント フォレストの Active Directory Cert Publishers セキュリティ グループに追加します。  
  
3.  管理者特権でのコマンド プロンプトで次のコマンドを実行して、すべてのフォレストのすべての CA コンピューターですべての certsvc サービスを再開します。  
  
    ```  
    net stop certsvc && net start certsvc  
    ```  
  
4.  管理者特権でのコマンド プロンプトで次のコマンドを実行して、ルート CA 証明書を抽出します。  
  
    ```  
    certutil -config <Computer-Name>\<Root-CA-Name> -ca.cert <root-ca-cert-filename.cer>  
    ```  
  
    (ルート CA でコマンドを実行する場合は、接続情報-config < Computer-name > を省略できます\\< ルート CA 名 >)  
  
    1.  管理者特権でのコマンド プロンプトで次のコマンドを実行して、アカウント フォレスト CA で前の手順のルート CA 証明書をインポートします。  
  
        ```  
        certutil -dspublish -f <root-ca-cert-filename.cer> RootCA  
        ```  
  
    2.  Grant リソース フォレストの証明書テンプレートの読み取り/書き込み権限を\<アカウント フォレスト\>\\< 管理者アカウント\>します。  
  
    3.  管理者特権でのコマンド プロンプトで次のコマンドを実行して、すべてのリソース フォレストのエンタープライズ CA 証明書を抽出します。  
  
        ```  
        certutil -config <Computer-Name>\<Enterprise-CA-Name> -ca.cert <enterprise-ca-cert-filename.cer>  
        ```  
  
        (ルート CA でコマンドを実行する場合は、接続情報-config < Computer-name > を省略できます\\< ルート CA 名 >)  
  
    4.  管理者特権でのコマンド プロンプトで次のコマンドを実行して、アカウント フォレスト CA で前の手順のエンタープライズ CA 証明書をインポートします。  
  
        ```  
        certutil -dspublish -f <enterprise-ca-cert-filename.cer> NTAuthCA  
        certutil -dspublish -f <enterprise-ca-cert-filename.cer> SubCA  
        ```  
  
    5.  発行された証明書テンプレートの一覧からアカウント フォレストの OTP 証明書テンプレートを削除します。  
  
### <a name="BKMK_DelImp"></a>削除し、OTP 証明書テンプレートのインポート  
  
1.  OTP 証明書テンプレートをアカウント フォレスト Forest2 から削除します。  
  
2.  次の PowerShell コマンドを使用して、証明書テンプレートおよび Oid オブジェクトをリソース フォレストから各アカウント フォレストにコピーします。  
  
    ```  
    .\PKISync.ps1 -sourceforest <resource forest DNS> -targetforest <account forest DNS> -type Template -cn <DA OTP registration authority template common name>.  
    .\PKISync.ps1 -sourceforest <resource forest DNS> -targetforest <account forest DNS> -type Template -cn <Secure DA OTP logon certificate template common name>.  
    .\PKISync.ps1 -sourceforest <resource forest DNS> -targetforest <account forest DNS> -type Oid -f  
    ```  
  
### <a name="BKMK_Publish"></a>OTP 証明書テンプレートを発行します。  
  
-   すべてのアカウント フォレスト CA で新しくインポートされた証明書テンプレートを発行します。  
  
### <a name="BKMK_Extract"></a>抽出し、CA を同期化  
  
1.  管理者特権でのコマンド プロンプトで次のコマンドを実行して、アカウント フォレストからすべてのエンタープライズ CA 証明書を抽出します。  
  
    ```  
    certutil -config <Computer-Name>\<Enterprise-CA-Name> -ca.cert <enterprise-ca-cert-filename.cer>  
    ```  
  
2.  次の PowerShell コマンドを使用して、アカウント フォレストからリソース フォレストへのフォレスト間で CA を同期化します。  
  
    ```  
    .\PKISync.ps1 -sourceforest <account forest DNS> -targetforest <resource forest DNS> -type CA -cn <enterprise CA sanitized name> -f  
    ```  
  
3.  次の PowerShell コマンドを使用して、リソース フォレストからアカウント フォレストへのフォレスト間で CA を同期化します。  
  
    ```  
    .\PKISync.ps1 -sourceforest <resource forest DNS> -targetforest <account forest DNS> -type CA -cn <enterprise CA sanitized name> -f  
    ```  
  
## <a name="configuration-procedures"></a>構成手順  
ここでは、上記のシナリオ展開の構成手順を説明します。 手順が完了した後に、シナリオに戻り続行します。  
  
### <a name="NRPT_DNSSearchSuffix"></a>NRPT 規則と DNS サフィックスを追加します。  
DirectAccess 経由で企業ネットワークに接続するクライアントは、名前解決ポリシー テーブル (NRPT) を使用して、さまざまなリソースのアドレスの解決に使用する DNS サーバーを決定します。 これにより、クライアントは企業リソースのアドレスを解決し、DirectAccess の稼働を維持するために必要な社内/社外の分類を維持できます。 DirectAccess 構成ツールでは、Forest1 のルート DNS サフィックスを自動的に検出し、NRPT テーブルに追加します。 ただし、Forest2 の FQDN サフィックスは NRPT テーブルに自動的に追加されないため、リモート アクセス管理者はそれらを手動で追加する必要があります。  
  
DNS サフィックス検索一覧では、クライアントは FQDN ではなく短いラベル名を使用できます。 リモート アクセス構成ツールでは、Forest1 のすべてのドメインを DNS サフィックス検索一覧に自動的に追加します。 クライアントで Forest2 のリソースに短いラベル名を使用できるようにする場合は、それらのラベル名を手動で追加する必要があります。  
  
##### <a name="to-add-a-dns-suffix-to-the-nrpt-table-and-domain-suffixes-to-the-dns-suffix-search-list"></a>DNS サフィックスを NRPT テーブルに追加し、ドメイン サフィックスを DNS サフィックス検索一覧に追加するには  
  
1.  リモート アクセス管理コンソールの中央ウィンドウの **[手順 3 インフラストラクチャ サーバー]** 領域で、 **[編集]** をクリックします。  
  
2.  **[ネットワーク ロケーション サーバー]** ページで、 **[次へ]** をクリックします。  
  
3.  **[DNS]** ページのテーブルで、Forest2 の企業ネットワークの一部である追加の名前サフィックスを入力します。 **[DNS サーバー アドレス]** に、DNS サーバー アドレスを手動または **[検出]** をクリックして入力します。 アドレスを入力しない場合は、新しいエントリが NRPT 除外として適用されます。 **[次へ]** をクリックします。  
  
4.  省略可能: **[DNS サフィックス検索一覧]** ページで、 **[新しいサフィックス]** ボックスにサフィックスを入力し、 **[追加]** をクリックして、DNS サフィックスを追加します。 **[次へ]** をクリックします。  
  
5.  **[管理]** ページで、 **[完了]** をクリックします。  
  
6.  リモート アクセス管理コンソールの中央ウィンドウで、 **[完了]** をクリックします。  
  
7.  **[リモート アクセスの確認]** ダイアログ ボックスで、 **[適用]** をクリックします。  
  
8.  **[リモートアクセス セットアップ ウィザードの設定を適用しています]** ダイアログ ボックスで、 **[閉じる]** をクリックします。  
  
### <a name="IPv6Prefix"></a>内部 IPv6 プレフィックスを追加します。  
  
> [!NOTE]  
> 内部 IPv6 プレフィックスの追加は、IPv6 が内部ネットワークに展開されている場合にのみ関連します。  
  
リモート アクセスでは、企業リソースの IPv6 プレフィックスの一覧が管理されます。 これらの IPv6 プレフィックスを含むリソースにのみ、DirectAccess 経由で接続されているクライアントからアクセスできます。 自動的に、リモート アクセス管理コンソールと Windows PowerShell コマンドは、Forest1 の IPv6 プレフィックスを追加し、他のフォレストのプレフィックスは追加されない可能性があります、ため、見つからない Forest2 のプレフィックスを手動で追加する必要があります。  
  
##### <a name="to-add-an-ipv6-prefix"></a>IPv6 プレフィックスを追加するには  
  
1.  リモート アクセス管理コンソールの中央ウィンドウの **[手順 2 リモート アクセス サーバー]** 領域で、 **[編集]** をクリックします。  
  
2.  リモート アクセス サーバーのセットアップ ウィザードで、 **[プレフィックスの構成]** をクリックします。  
  
3.  **[プレフィックスの構成]** ページの **[内部ネットワークの IPv6 プレフィックス]** で、2001:db8:1::/64;2001:db8:2::/64 のようにセミコロンで区切られた追加の IPv6 プレフィックスを追加します。 **[次へ]** をクリックします。  
  
4.  **[認証]** ページで、 **[完了]** をクリックします。  
  
5.  リモート アクセス管理コンソールの中央ウィンドウで、 **[完了]** をクリックします。  
  
6.  **[リモート アクセスの確認]** ダイアログ ボックスで、 **[適用]** をクリックします。  
  
7.  **[リモートアクセス セットアップ ウィザードの設定を適用しています]** ダイアログ ボックスで、 **[閉じる]** をクリックします。  
  
### <a name="SGs"></a>クライアント セキュリティ グループを追加します。  
DirectAccess を介してリソースにアクセスする Forest2 から Windows 8 クライアント コンピューターを有効にするのには、リモート アクセス展開に Forest2 からセキュリティ グループを追加する必要があります。  
  
##### <a name="to-add-windows-8-client-security-groups"></a>Windows 8 クライアント セキュリティ グループを追加するには  
  
1.  リモート アクセス管理コンソールの中央ウィンドウの **[手順 1: リモート クライアント]** 領域で、 **[編集]** をクリックします。  
  
2.  DirectAccess クライアントのセットアップ ウィザードで **[グループの選択]** をクリックし、 **[グループの選択]** ページで **[追加]** をクリックします。  
  
3.  **[グループの選択]** ダイアログ ボックスで、DirectAccess クライアント コンピューターを含むセキュリティ グループを選択します。 **[次へ]** をクリックします。  
  
4.  **[Network Connectivity Assistant]** ページで、 **[完了]** をクリックします。  
  
5.  リモート アクセス管理コンソールの中央ウィンドウで、 **[完了]** をクリックします。  
  
6.  **[リモート アクセスの確認]** ダイアログ ボックスで、 **[適用]** をクリックします。  
  
7.  **[リモートアクセス セットアップ ウィザードの設定を適用しています]** ダイアログ ボックスで、 **[閉じる]** をクリックします。  
  
クライアント コンピューターが Forest2 から DirectAccess マルチサイトとを通してリソースにアクセスが有効になっている Windows 7 を有効にするには、各エントリ ポイントのリモート アクセス展開に Forest2 からセキュリティ グループを追加する必要があります。 Windows 7 のセキュリティ グループに追加する方法の詳細については、の説明を参照して、**クライアント サポート**3.6 でのページ。 マルチサイト展開を有効にします。  
  
### <a name="RefreshMgmtServers"></a>管理サーバーの一覧を更新します。  
リモート アクセスでは、DirectAccess 構成 GPO を含むすべてのフォレストのインフラストラクチャ サーバーを自動的に検出します。 DirectAccess が Forest1 からサーバーに展開された場合、サーバーの GPO は Forest1 のそのドメインに書き込まれます。 Forest2 からクライアントの DirectAccess へのアクセスを有効にした場合、クライアントの GPO が Forest2 のドメインに書き込まれます。  
  
DirectAccess を通じてドメイン コントローラーおよび System Center Configuration Manager にアクセスできるようにするには、インフラストラクチャ サーバーの自動検出プロセスが必要です。 検出プロセスを手動で開始する必要があります。  
  
##### <a name="to-refresh-the-management-servers-list"></a>管理サーバーの一覧を更新するには  
  
1.  リモート アクセス管理コンソールで **[構成]** をクリックし、 **[タスク]** ウィンドウで **[管理サーバーの更新]** をクリックします。  
  
2.  **[管理サーバーを更新しています]** ダイアログ ボックスで、 **[閉じる]** をクリックします。  
  


