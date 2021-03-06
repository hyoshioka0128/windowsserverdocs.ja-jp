---
title: 'AD FS と Web アプリケーション プロキシを使ったワーク フォルダーの展開: 手順 5: クライアントのセットアップ'
ms.prod: windows-server-threshold
ms.technology: storage-work-folders
ms.topic: article
manager: klaasl
ms.author: jeffpatt
author: JeffPatt24
ms.date: 4/5/2017
ms.assetid: f168292b-0dbc-44b9-965f-d480e5134a0c
ms.openlocfilehash: 44e3ab06ac29d770ad47b43db5eba06f0eb08a60
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447788"
---
# <a name="deploy-work-folders-with-ad-fs-and-web-application-proxy-step-5-set-up-clients"></a>AD FS と Web アプリケーション プロキシを使ったワーク フォルダーを展開します。手順 5 では、クライアントのセットアップ

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックでは、Active Directory フェデレーション サービス (AD FS) と Web アプリケーション プロキシを使用して、ワーク フォルダーを展開する 5 番目の手順について説明します。 このプロセスの他の手順は、次のトピックで確認できます。  
  
-   [AD FS と Web アプリケーション プロキシを使ったワーク フォルダーを展開します。概要](deploy-work-folders-adfs-overview.md)  
  
-   [AD FS と Web アプリケーション プロキシを使ったワーク フォルダーを展開します。手順 1、AD FS の設定](deploy-work-folders-adfs-step1.md)  
  
-   [AD FS と Web アプリケーション プロキシを使ったワーク フォルダーを展開します。手順 2 では、AD FS の構成後の作業](deploy-work-folders-adfs-step2.md)  
  
-   [AD FS と Web アプリケーション プロキシを使ったワーク フォルダーを展開します。手順 3 では、ワーク フォルダーの設定](deploy-work-folders-adfs-step3.md)  
  
-   [AD FS と Web アプリケーション プロキシを使ったワーク フォルダーを展開します。手順 4、Web アプリケーション プロキシの設定](deploy-work-folders-adfs-step4.md)  
  
ドメインに参加している Windows クライアントおよびドメインに参加していない Windowsクライアントをセットアップするには、次の手順を使用します。 これらのクライアントを使用して、クライアントのワーク フォルダーの間でファイルが正しく同期されているかどうかをテストすることができます。  
  
## <a name="set-up-a-domain-joined-client"></a>ドメインに参加しているクライアントのセットアップ  
  
### <a name="install-the-ad-fs-and-work-folder-certificates"></a>AD FS とワーク フォルダーの証明書のインストール  
以前に作成した AD FS とワーク フォルダーの証明書を、ドメインに参加しているクライアント コンピューター上のローカル コンピューターの証明書ストアにインストールする必要があります。  
  
信頼されたルート証明機関の証明書ストアの発行元によらない、自己署名証明書をインストールしようとしているため、証明書もそのストアにコピーする必要があります。  
  
証明書をインストールするには、以下の手順を実行します。  
  
1.  **[スタート]** ボタンをクリックして **[ファイル名を指定して実行]** をクリックします。  
  
2.  「**MMC**」と入力します。  
  
3.  **[ファイル]** メニューの **[スナップインの追加と削除]** をクリックします。  
  
4.  **[利用できるスナップイン]** の一覧で、 **[証明書]** 、 **[追加]** の順に選択します。 証明書スナップイン ウィザードが開始されます。  
  
5.  **[コンピューター アカウント]** を選択し、 **[次へ]** をクリックします。  
  
6.  **[ローカル コンピュータ (このコンソールを実行しているコンピュータ)]** を選択し、次に **[完了]** をクリックします。  
  
7.  **[OK]** をクリックします。  
  
8.  [コンソール ルート\証明書 \(ローカル コンピューター)\個人\証明書] フォルダーを展開します。  
  
9. **[証明書]** を右クリックし、 **[すべてのタスク]** 、 **[インポート]** の順にクリックします。  
  
10. AD FS 証明書を含むフォルダーを参照し、ウィザードの指示に従ってファイルをインポートして、証明書ストアに配置します。  
  
11. 手順 9 と 10 を繰り返します。今回はワーク フォルダー証明書を参照して、インポートします。  
  
12. [コンソール ルート\証明書 \(ローカル コンピューター)\信頼されたルート証明機関\証明書] フォルダーを展開します。  
  
13. **[証明書]** を右クリックし、 **[すべてのタスク]** 、 **[インポート]** の順にクリックします。  
  
14. AD FS 証明書を含むフォルダーを参照し、ウィザードの指示に従ってファイルをインポートして、信頼されたルート証明機関ストアに配置します。  
  
15. 手順 13 と 14 を繰り返します。今回はワーク フォルダー証明書を参照して、インポートします。  
  
### <a name="configure-work-folders-on-the-client"></a>クライアントのワーク フォルダーの構成  
クライアント コンピューター上のワーク フォルダーを構成するには、次の手順に従います。  
  
1. クライアント コンピューターで **[コントロール パネル]** を開き、 **[ワーク フォルダー]** をクリックします。  
  
2. **[ワーク フォルダーのセットアップ]** をクリックします。  
  
3. **職場の電子メール アドレスを入力** ページで、ユーザーの電子メール アドレスを入力します (たとえば、 user@contoso.com) またはワーク フォルダーの URL (テスト例では、https で:\//workfolders.contoso.com)、順にクリックします**次へ**します。  
  
4. ユーザーが企業ネットワークに接続されている場合、Windows 統合認証によって、認証が実行されます。 ユーザーが企業ネットワークに接続されていない場合は、ADFS (OAuth) で認証が実行され、ユーザーは資格情報の入力を求められます。 資格情報を入力して、 **[OK]** をクリックします。  
  
5. 認証が行われると、 **[ワーク フォルダーの導入中]** ページが表示されます。ここではワーク フォルダー ディレクトリの場所を必要に応じて変更できます。 **[次へ]** をクリックします。  
  
6. **[セキュリティ ポリシー]** ページでは、ワーク フォルダーに設定したセキュリティ ポリシーが一覧表示されます。 **[次へ]** をクリックします。  
  
7. ワーク フォルダーがお使いの PC との同期を開始したことを示すメッセージが表示されます。 **[閉じる]** をクリックします。  
  
8. **[ワーク フォルダーの管理]** ページでは、サーバー上で使用可能な空き容量、同期の状態などが示されます。 必要な場合は、ここで資格情報を再入力することができます。 ウィンドウを閉じます。  
  
9. ワーク フォルダーのフォルダーは、自動的に開きます。 このフォルダーにコンテンツを追加すると、デバイス間で同期できます。  
  
    今回のテストのため、このワーク フォルダーのフォルダーにテスト ファイルを追加します。 ドメインに参加していないコンピューターでワーク フォルダーをセットアップした後で、各コンピューターのワーク フォルダー間でファイルを同期することができます。  
  
## <a name="set-up-a-non-domain-joined-client"></a>ドメインに参加していないクライアントのセットアップ  
  
### <a name="install-the-ad-fs-and-work-folder-certificates"></a>AD FS とワーク フォルダーの証明書のインストール  
ドメインに参加しているコンピューターで使用したものと同じ手順を使用して、ドメインに参加していないコンピューターで、AD FS とワーク フォルダーの証明書をインストールします。  
  
### <a name="update-the-hosts-file"></a>Hosts ファイルの更新  
ドメインに参加していないクライアント上の hosts ファイルは、テスト環境用に更新する必要があります。これは、ワーク フォルダーにはパブリック DNS レコードが作成されていないためです。 次のエントリを hosts ファイルに追加します。  
  
-  workfolders.ドメイン  
  
-  AD FS サービス名.ドメイン  
  
-  enterpriseregistration.ドメイン  
  
テストの例では、以下の値を使います。  
  
-  **10.0.0.10 workfolders.contoso.com**  
  
-  **10.0.0.10 blueadfs.contoso.com**  
  
-  **10.0.0.10 enterpriseregistration.contoso.com**  
  
### <a name="configure-work-folders-on-the-client"></a>クライアントのワーク フォルダーの構成  
ドメインに参加しているコンピューターで使用したものと同じ手順を実行して、ドメインに参加していないコンピューター上のワーク フォルダーを構成します。  
  
このクライアントで新しいワーク フォルダーのフォルダーを開くと、ドメインに参加しているコンピューターからのファイルが、ドメインに参加していないコンピューターに、既に同期されていることを確認できます。 このフォルダーにコンテンツを追加すると、デバイス間で同期できます。  
  
Windows Server の UI を使って、ワーク フォルダー、AD FS、Web アプリケーション プロキシを展開する手順は、以上で完了です。  
  
## <a name="see-also"></a>関連項目  
[ワーク フォルダーの概要](Work-Folders-Overview.md)  
  

