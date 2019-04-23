---
ms.assetid: 5a1ae56b-adcb-447e-9e34-c0629d7cb241
title: フェデレーション サーバー ファームのサービス アカウントを手動で構成する
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 7d215c80c03236df9479aff8046981741dfc83e2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838153"
---
# <a name="manually-configure-a-service-account-for-a-federation-server-farm"></a>フェデレーション サーバー ファームのサービス アカウントを手動で構成する

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

Active Directory フェデレーション サービスでフェデレーション サーバー ファーム環境を構成する場合\(AD FS\)を作成し、Active Directory Domain Services の専用のサービス アカウントを構成する必要があります\(AD DS\) 、ファームが存在します。 次に、このアカウントを使用するために、ファーム内の各フェデレーション サーバーを構成します。 Windows 統合認証を使用して、AD FS ファームにフェデレーション サーバーのいずれかの認証に企業ネットワーク上のクライアント コンピューターをできるようにする場合に、組織内で、次のタスクを行う必要があります。  

> [!IMPORTANT]
> AD FS は AD FS 3.0 (Windows Server 2012 R2) の時点での使用をサポートする[グループ管理サービス アカウント](https://docs.microsoft.com/windows-server/security/group-managed-service-accounts/group-managed-service-accounts-overview) \(gMSA\)サービス アカウントとして。  これは、時間の経過と共に、サービス アカウントのパスワードを管理する必要があることをお勧めのオプションです。  このドキュメントがなど、従来のサービス アカウントを使用して、Windows Server 2008 R2 またはそれ以前のドメイン機能レベルがまだ実行しているドメイン内の別のケースでは\(DFL\)します。

> [!NOTE]  
> この手順のタスクは、フェデレーション サーバー ファーム全体で 1 回のみ実行する必要があります。 後で、AD FS フェデレーション サーバー構成ウィザードを使用してフェデレーション サーバーを作成するときにする必要がありますこの同じアカウントを指定、**サービス アカウント**ウィザード ページで、ファーム内の各フェデレーション サーバー。  
  
#### <a name="create-a-dedicated-service-account"></a>専用のサービス アカウントを作成する  
  
1.  専用のユーザーの作成\/サービスは id プロバイダー組織にある Active Directory フォレスト内のアカウント。 このアカウントは、Kerberos 認証プロトコル、ファーム シナリオで作業して、パスを許可するために必要な\-各フェデレーション サーバーで認証を使用します。 このアカウントは、フェデレーション サーバー ファームの目的にのみ使用します。  
  
2.  ユーザー アカウントのプロパティを編集し、**[パスワードを無期限にする]** チェック ボックスをオンにします。 この操作によって、ドメイン パスワードの変更要件によってサービス アカウントの機能が中断されることはなくなります。  
  
    > [!NOTE]  
    > この専用アカウントの Network Service アカウントを使用する場合、Windows 統合認証経由でアクセスを試みると、ランダムに失敗する結果となります。これは、Kerberos チケットがサーバー間で検証されないことが原因です。  
  
#### <a name="to-set-the-spn-of-the-service-account"></a>サービス アカウントの SPN を設定するには  
  
1.  AD FS の AppPool のアプリケーション プール id がドメイン ユーザーとして実行されているため、\/サービス アカウント、サービス プリンシパル名を構成する必要があります\(SPN\) Setspn.exeコマンドを使用してドメインでそのアカウントの\-ライン ツール。 Setspn.exe は、既定では Windows Server 2008 を実行しているコンピューターにインストールされます。 同じドメインに参加しているコンピューターで次のコマンドを実行する場所、ユーザー\/サービス アカウントが存在します。  
  
    ```  
    setspn -a host/<server name> <service account>  
    ```  
  
    どのすべてのフェデレーション サーバーが、ドメイン ネーム システムでクラスター化シナリオなどで\(DNS\)ホスト名 fs.fabrikam.com と AD FS の AppPool に割り当てられているサービス アカウント名は adfs2farm、コマンドを入力します次し、し、ENTER キーを押すだけで。  
  
    ```  
    setspn -a host/fs.fabrikam.com adfs2farm  
    ```  
  
    このタスクはこのアカウントについて 1 回だけ実行する必要があります。  
  
2.  サービス アカウントに AD FS の AppPool id が変更されると、設定、アクセス制御リスト\(Acl\)できるように、AD FS の AppPool はポリシー データを読み取ることができます、この新しいアカウントへの読み取りアクセスを許可する SQL Server データベース。  
  

