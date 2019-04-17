---
title: 証明機関をインストールします。
description: このトピックの「802.1 X ワイヤードおよびワイヤレス展開の証明書をサーバーのデプロイ ガイドの一部である
manager: brianlic
ms.topic: article
ms.assetid: 4acdc3ad-078e-45cc-b54c-e9456e0c90f5
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 17a887ab32570b739d5ca99611ee0d496a966d1b
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="install-the-certification-authority"></a>証明機関をインストールします。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

この手順を使用すると、ネットワーク ポリシー サーバー (NPS)、ルーティングとリモート アクセス サービス (RRAS)、またはその両方を実行しているサーバーにサーバー証明書を登録できるように、Active Directory 証明書サービス (AD CS) をインストールします。  
  
> [!IMPORTANT]  
> -   Active Directory Certificate Services をインストールする前に、コンピューターの名前、静的 IP アドレスを持つコンピューターを構成する、コンピューターをドメインに参加してください。 これらのタスクを実行する方法の詳細については、Windows Server 2016 を参照してください。[コア ネットワーク ガイド](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide)します。  
> -   この手順を実行するには、Active Directory ドメイン サービス (AD DS) がインストールされているドメインに AD CS をインストールするコンピューターを参加する必要があります。  
  
メンバーシップの両方、 **Enterprise Admins**とルート ドメインの**Domain Admins**グループはこの手順を完了するために必要な最小値。  
  
> [!NOTE]  
> Windows PowerShell を使用してこの手順を実行するには、Windows PowerShell を開くし、次のコマンドを入力し、Enter キーを押します。   
>   
> `Add-WindowsFeature Adcs-Cert-Authority -IncludeManagementTools`  
>   
> AD CS がインストールされた後、次のコマンドを入力し、Enter キーを押します。  
>   
> `Install-AdcsCertificationAuthority -CAType EnterpriseRootCA`  
  
### <a name="to-install-active-directory-certificate-services"></a>Active Directory Certificate Services をインストールするには  
  
1.  Enterprise Admins グループとルート ドメインの Domain Admins グループの両方のメンバーとしてログオンします。  
  
2.  サーバー マネージャーで、クリックして**管理**、] をクリックし、**追加の役割と機能**します。 追加の役割と機能のウィザードが開きます。  
  
3.  **開始する前に**、] をクリックして**次**します。  
  
    > [!NOTE]  
    > **開始する前に**以前選択した場合、追加の役割と機能のウィザードのページが表示されない**既定でこのページをスキップ**、追加の役割と機能のウィザードが実行されました。  
  
4.  **[インストールの種類**、いることを確認**役割ベースまたは機能ベースのインストール**をクリックして選択して**次**します。  
  
5.  **対象サーバーの選択**、いることを確認**サーバー プールからサーバーを選択**が選択されています。 **サーバー プール**、ローカル コンピューターが選択されていることを確認します。 をクリックして**次**します。  
  
6.  **サーバーの役割の選択**で、**役割**[ **Active Directory Certificate Services**します。 必要な機能を追加するのにメッセージが表示されたら、] をクリックして**機能の追加**、] をクリックし、**次**します。  
  
7.  **機能の選択**、] をクリックして**次**します。  
  
8.  **Active Directory Certificate Services**、提供された情報を読み取るし、[クリックして**次**します。  
  
9. **インストール オプションの確認**、] をクリックして**インストール**します。 インストール プロセス中に、ウィザードを閉じないでください。 インストールが完了したら、クリックして**、移行先サーバーに Active Directory Certificate Services を構成する**します。 AD CS の構成ウィザードが開きます。 資格情報を読み取るし、必要な場合は、Enterprise Admins グループのメンバーあるアカウントの資格情報を提供します。 をクリックして**次**します。  
  
10. **役割サービス**、] をクリックして**証明機関**、] をクリックし、**次**します。  
  
11. **セットアップの種類**] ページで、いることを確認**エンタープライズ CA**をクリックして選択して**次**します。  
  
12. **CA の種類を指定**いることを確認] ページで、**ルート CA**をクリックして選択して**[次へ]**します。  
  
13. **秘密キーの種類を指定**いることを確認] ページで、**新しい秘密キーを作成する**をクリックして選択して**[次へ]**します。  
  
14. **CA の暗号化**] ページで、CSP の既定の設定を保持 (**RSA #Microsoft Software Key Storage Provider**) とハッシュ アルゴリズム (**SHA1**)、し、展開に最適なキーの文字の長さを決定します。 大規模なキー文字列の長さが最適なセキュリティを提供します。ただし、サーバーのパフォーマンスに影響を与えることができますが、従来のアプリケーションと互換性がない可能性があります。 2048 の既定の設定を保持することをお勧めします。 をクリックして**次**します。  
  
15. **CA 名**ページで、CA の推奨される共通名を保持するか、必要に応じて名前を変更します。 している CA の名前は、AD CS をインストールした後、CA の名前を変更できないため、名前付け規則と目的との互換性のあることを確認します。 をクリックして**次**します。  
  
16. **有効期間**] ページの [**有効期間の指定**、番号を入力し、時間の値 (年、月、週、または日) を選択します。 5 年間の既定の設定をお勧めします。 をクリックして**次**します。  
  
17. **CA データベース**] ページの [**データベースの場所を指定**、証明書データベースおよび証明書データベースのログ フォルダーの場所を指定します。 既定の場所以外の場所を指定する場合は、フォルダーが承認されていないユーザーまたはコンピューターが、CA データベースとログ ファイルにアクセスすることを防ぐアクセス制御リスト (Acl) で保護されていることを確認します。 をクリックして**次**します。  
  
18. **確認**、] をクリックして**構成**、選択内容を適用し、[**閉じる**します。  
  


