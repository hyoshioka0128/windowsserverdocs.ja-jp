---
title: 証明機関をインストールする
description: このトピックでは、802.1 X ワイヤードおよびワイヤレス展開の証明書をサーバーのデプロイ ガイドの一部
manager: brianlic
ms.topic: article
ms.assetid: 4acdc3ad-078e-45cc-b54c-e9456e0c90f5
ms.prod: windows-server
ms.technology: networking
ms.author: lizross
author: eross-msft
ms.openlocfilehash: fffb03a707c48c8dd485c68b5c6bf10783b0e6cf
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80318367"
---
# <a name="install-the-certification-authority"></a>証明機関をインストールする

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

この手順を使用すると、ネットワーク ポリシー サーバー (NPS)、ルーティングとリモート アクセス サービス (RRAS)、またはその両方を実行しているサーバーにサーバー証明書を登録できるように、Active Directory 証明書サービス (AD CS) をインストールします。  
  
> [!IMPORTANT]  
> -   Active Directory Certificate Services をインストールする前に、コンピューターの名前が静的 IP アドレスを持つコンピューターを構成、コンピューターをドメインに参加してください。 これらのタスクを実行する方法の詳細については、Windows Server 2016 を参照してください。 [コア ネットワーク ガイド](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide)します。  
> -   この手順を実行するには、AD CS をインストールするコンピューターを Active Directory ドメイン サービス (AD DS) がインストールされているドメインに参加する必要があります。  
  
メンバーシップの両方、 **Enterprise Admins** とルート ドメインの **Domain Admins** グループは、この手順を実行するために必要な最小値。  
  
> [!NOTE]  
> Windows PowerShell を使用してこの手順を実行するには、Windows PowerShell を開きます次のコマンドを入力し、ENTER キーを押します。   
>   
> `Add-WindowsFeature Adcs-Cert-Authority -IncludeManagementTools`  
>   
> AD CS をインストールした後は、次のコマンドを入力し、ENTER キーを押します。  
>   
> `Install-AdcsCertificationAuthority -CAType EnterpriseRootCA`  
  
### <a name="to-install-active-directory-certificate-services"></a>Active Directory 証明書サービスをインストールするには  

> [!TIP]
> Windows PowerShell を使用して Active Directory 証明書サービスをインストールする場合は、コマンドレットとオプションのパラメーターの[AdcsCertificationAuthority](https://docs.microsoft.com/powershell/module/adcsdeployment/install-adcscertificationauthority?view=win10-ps)を参照してください。
  
1.  Enterprise Admins グループとルート ドメインの Domain Admins グループの両方のメンバーであるアカウントでログオンします。  
  
2.  サーバー マネージャーで、 **[管理]** をクリックし、 **[役割と機能の追加]** をクリックします。 役割と機能の追加ウィザードが起動されます。  
  
3.  **[開始する前に]** で **[次へ]** をクリックします。  
  
    > [!NOTE]  
    > 以前、役割と機能の追加ウィザードの実行時に **[既定でこのページを表示しない]** をクリックした場合、 **[開始する前に]** ページは表示されません。  
  
4.  **[インストールの種類の選択]** で **[役割ベースまたは機能ベースのインストール]** が選択されていることを確認して、 **[次へ]** をクリックします。  
  
5.  **[対象サーバーの選択]** で、 **[サーバー プールからサーバーを選択]** が選択されていることを確認します。 **[サーバー プール]** で、ローカル コンピューターが選択されていることを確認します。 **[次へ]** をクリックします。  
  
6.  **サーバーの役割**, で、 **ロール**,  **Active Directory Certificate Services**します。 必要な機能を追加するメッセージが表示されたら、クリックして **機能の追加**, 、 をクリックし、 **次**します。  
  
7.  **機能の選択**, をクリックして **次**します。  
  
8.  **Active Directory Certificate Services**, 、提供された情報を読み取り、およびクリックして **次**します。  
  
9. **[インストール オプションの確認]** で、 **[インストール]** をクリックします。 インストール プロセス中に、ウィザードを閉じないでください。 インストールが完了したら、クリックして **、移行先サーバーに Active Directory Certificate Services を構成する**です。 AD CS の構成ウィザードが開きます。 資格情報を読み取るし、必要な場合は、Enterprise Admins グループのメンバーであるアカウントの資格情報を指定します。 **[次へ]** をクリックします。  
  
10. **役割サービスの**, 、 をクリックして **証明機関**, 、 をクリックし、 **次**します。  
  
11. **セットアップの種類** いることを確認 ページで、 **エンタープライズ CA** クリックして選択すると、 **次**します。  
  
12. **CA の種類を指定** いることを確認 ページで、 **ルート CA** クリックして選択すると、 **次**します。  
  
13. **秘密キーの種類を指定** いることを確認 ページで、 **新しい秘密キーを作成** クリックして選択すると、 **次**します。  
  
14. **[CA の暗号化]** ページで、CSP (**RSA # Microsoft Software Key Storage Provider**) とハッシュアルゴリズム (**SHA2**) の既定の設定をそのままにして、展開に最適なキー文字の長さを決定します。 大規模なキー文字列の長さが最適なセキュリティを提供します。ただし、サーバーのパフォーマンスに影響を与えることができますが、従来のアプリケーションと互換性がない可能性があります。 2048 の既定の設定を維持することをお勧めします。 **[次へ]** をクリックします。  
  
15. **CA 名** ページで、CA の推奨される共通名を保持するか、必要に応じて名前を変更します。 している AD CS をインストールした後、CA の名前を変更できないために、CA 名は名前付け規則と目的で、互換性のあることを確認します。 **[次へ]** をクリックします。  
  
16. **有効期間** ] ページの [ **有効期間の指定**, 、番号を入力し、時刻の値 (年、月、週、または日) を選択します。 既定の設定値は 5 年間 (推奨) です。 **[次へ]** をクリックします。  
  
17. **CA データベース** ] ページの [ **データベースの場所を指定**, 、証明書データベースと証明書データベース ログのフォルダーの場所を指定します。 既定の場所以外の場所を指定する場合は、指定したフォルダーが、承認されていないユーザーやコンピューターによる CA データベースや CA ログ ファイルへのアクセスを防止するアクセス制御リスト (ACL) によって、セキュリティで保護されていることを確認してください。 **[次へ]** をクリックします。  
  
18. **確認**, 、クリックして **構成** を選択内容を適用し、をクリックして **閉じる**します。  
  


