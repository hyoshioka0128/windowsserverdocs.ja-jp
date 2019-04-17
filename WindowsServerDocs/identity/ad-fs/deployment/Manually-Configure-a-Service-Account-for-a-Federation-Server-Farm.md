---
ms.assetid: 5a1ae56b-adcb-447e-9e34-c0629d7cb241
title: "フェデレーション サーバー ファームのサービス アカウントを手動で構成します。"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 5b5a8d198f93772903ea9b0a2b4b01075799bf0f
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="manually-configure-a-service-account-for-a-federation-server-farm"></a>フェデレーション サーバー ファームのサービス アカウントを手動で構成します。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Active Directory フェデレーション サービス \(AD FS\) でフェデレーション サーバー ファーム環境を構成する場合は、作成し、ファームを常駐 Active Directory Domain Services \(AD DS\) で専用のサービス アカウントを構成する必要があります。 このアカウントを使用して、ファーム内の各フェデレーション サーバーを構成します。 Windows 統合認証を使用して、AD FS ファーム内のフェデレーション サーバーのいずれかへの認証に企業ネットワーク上のクライアント コンピューターを許可する場合は、組織内、次のタスクを実行する必要があります。  
  
> [!NOTE]  
> この手順で、フェデレーション サーバー ファーム全体について 1 回だけタスクを実行する必要があります。 後で、AD FS フェデレーション サーバー構成ウィザードを使用してフェデレーション サーバーを作成するときにする必要がありますアカウントを指定するこの同じで、**サービス アカウント**ウィザード ページで、ファーム内の各フェデレーション サーバー。  
  
#### <a name="create-a-dedicated-service-account"></a>専用のサービス アカウントを作成します。  
  
1.  Id プロバイダー組織に配置されている Active Directory フォレストに専用のユーザー/サービス アカウントを作成します。 このアカウントは、Kerberos 認証プロトコル、ファーム シナリオで動作して、各フェデレーション サーバーで pass\ を介して認証を許可する必要があります。 このアカウントは、フェデレーション サーバー ファームの目的にのみ使用します。  
  
2.  ユーザー アカウントのプロパティを編集し、選択、**パスワードを無期限**チェック ボックスをオンします。 この操作は、ドメイン パスワードの変更要件の結果として、このサービス アカウントの機能が中断されていないことを確認します。  
  
    > [!NOTE]  
    > この専用アカウントに、Network Service アカウントを使用してエラーが発生ランダム アクセスしようとすると、Windows 統合認証を通じてで検証されない 1 つのサーバー間の Kerberos チケットの結果として。  
  
#### <a name="to-set-the-spn-of-the-service-account"></a>サービス アカウントの SPN を設定するには  
  
1.  AD FS AppPool のアプリケーション プール ID はドメイン ユーザー/サービス アカウントとして実行されている、ために、Setspn.exe コマンド ライン ツールを使用してドメインでそのアカウントのサービス プリンシパル名 \(SPN\) を構成する必要があります。 Setspn.exe は、Windows Server 2008 を実行しているコンピューターでは既定でインストールされます。 ユーザー/サービス アカウントが存在する同じドメインに参加しているコンピューターで、次のコマンドを実行します。  
  
    ```  
    setspn -a host/<server name> <service account>  
    ```  
  
    やなどのシナリオでは、すべてのフェデレーション サーバーで、ドメイン ネーム システム \(DNS\) ホスト名 fs.fabrikam.com クラスター化し、AD FS AppPool に割り当てられているサービス アカウント名を adfs2farm、次のようにコマンドを入力し、Enter キーを押します。  
  
    ```  
    setspn -a host/fs.fabrikam.com adfs2farm  
    ```  
  
    このアカウントに、このタスクを 1 回だけ実行する必要があります。  
  
2.  サービス アカウントに、AD FS AppPool ID が変更されると、AD FS AppPool はポリシー データを読み取ることができるように、この新しいアカウントへの読み取りアクセスを許可するように SQL Server データベースのアクセス制御リスト \(ACLs\) を設定します。  
  

