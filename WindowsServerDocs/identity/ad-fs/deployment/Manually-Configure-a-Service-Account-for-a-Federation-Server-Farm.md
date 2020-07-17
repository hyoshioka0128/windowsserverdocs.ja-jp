---
ms.assetid: 5a1ae56b-adcb-447e-9e34-c0629d7cb241
title: フェデレーション サーバー ファームのサービス アカウントを手動で構成する
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: c30215f5f8e39bb97452fccaaef8d1bb0469dc31
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855345"
---
# <a name="manually-configure-a-service-account-for-a-federation-server-farm"></a>フェデレーション サーバー ファームのサービス アカウントを手動で構成する

Active Directory フェデレーションサービス (AD FS) \(AD FS\)でフェデレーションサーバーファーム環境を構成する場合は、ファームが存在する Active Directory Domain Services \(AD DS\) で専用のサービスアカウントを作成し、構成する必要があります。 次に、このアカウントを使用するために、ファーム内の各フェデレーション サーバーを構成します。 企業ネットワーク上のクライアントコンピューターが Windows 統合認証を使用して AD FS ファーム内のいずれかのフェデレーションサーバーに対して認証を行うことができるようにするには、組織で次のタスクを完了する必要があります。  

> [!IMPORTANT]
> AD FS 3.0 (Windows Server 2012 R2) 以降、AD FS では、グループの管理された[サービスアカウント](https://docs.microsoft.com/windows-server/security/group-managed-service-accounts/group-managed-service-accounts-overview)\(gMSA\) をサービスアカウントとして使用することがサポートされています。  これは、時間の経過と共にサービスアカウントのパスワードを管理する必要がないため、推奨されるオプションです。  このドキュメントでは、従来のサービスアカウントを使用する別のケースについて説明します。たとえば、Windows Server 2008 R2 以前のドメイン機能レベル \(DFL\)を実行しているドメインの場合などです。

> [!NOTE]  
> この手順のタスクは、フェデレーション サーバー ファーム全体で 1 回のみ実行する必要があります。 後になって、AD FS フェデレーション サーバーの構成ウィザードを使ってフェデレーション サーバーを作成する場合、ファーム内のフェデレーション サーバーごとに、 **[サービス アカウント]** ウィザード ページでこれと同じアカウントを指定する必要があります。  
  
#### <a name="create-a-dedicated-service-account"></a>専用のサービス アカウントを作成する  
  
1.  Id プロバイダー組織に配置されている Active Directory フォレストに専用のユーザー\/サービスアカウントを作成します。 このアカウントは、ファームシナリオで Kerberos 認証プロトコルが動作するために必要であり、各フェデレーションサーバーで認証を通じて\-を通過できるようにします。 このアカウントは、フェデレーションサーバーファームの目的でのみ使用してください。  
  
2.  ユーザー アカウント プロパティを編集し、 **[パスワードを無期限にする]** チェック ボックスをオンにします。 このアクションにより、サービス アカウントの機能がドメイン パスワードの変更要件によって妨げられることがなくなります。  
  
    > [!NOTE]  
    > この専用アカウントの Network Service アカウントを使用する場合、Windows 統合認証経由でアクセスを試みると、ランダムに失敗する結果となります。これは、Kerberos チケットがサーバー間で検証されないことが原因です。  
  
#### <a name="to-set-the-spn-of-the-service-account"></a>サービス アカウントの SPN を設定するには  
  
1.  AD FS AppPool のアプリケーションプール id はドメインユーザー\/サービスアカウントとして実行されているので、ドメイン内のそのアカウントの SPN\) \(サービスプリンシパル名を指定する必要があります。これには、Setspn コマンド\-line ツールを使用します。 Setspn は、Windows Server 2008 を実行しているコンピューターに既定でインストールされます。 ユーザー\/サービスアカウントが存在するドメインと同じドメインに参加しているコンピューターで、次のコマンドを実行します。  
  
    ```  
    setspn -a host/<server name> <service account>  
    ```  
  
    たとえば、すべてのフェデレーションサーバーがドメインネーム\) \(システムの下にクラスター化されていて、AD FS AppPool に割り当てられているサービスアカウント名が adfs2farm である場合は、次のようにコマンドを入力して、enter キーを押します。 fs.fabrikam.com  
  
    ```  
    setspn -a host/fs.fabrikam.com adfs2farm  
    ```  
  
    このタスクはこのアカウントについて 1 回だけ実行する必要があります。  
  
2.  AD FS AppPool id がサービスアカウントに変更された後、SQL Server データベースのアクセス制御リスト \(Acl\) を設定して、この新しいアカウントへの読み取りアクセスを許可し、AD FS AppPool がポリシーデータを読み取ることができるようにします。  
  

