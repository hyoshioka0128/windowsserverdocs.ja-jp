---
ms.assetid: 4d002764-58b4-4137-9c86-1e55b02e07ce
title: "パートナー組織の構成"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 5494f3bd8d012bf1ecc240439ff880d1bb52c280
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="configuring-partner-organizations"></a>パートナー組織の構成

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Active Directory フェデレーション サービス \(AD FS\) 内に新しいパートナー組織を展開するには、いずれかのタスクを完了[チェックリスト: Configuring the Resource Partner Organization](Checklist--Configuring-the-Resource-Partner-Organization.md)または[チェックリスト: アカウント パートナー組織の構成](Checklist--Configuring-the-Account-Partner-Organization.md)に応じて、AD FS 設計します。  
  
> [!NOTE]  
> これらのチェックリストのいずれかを使用する場合を強くお勧めアカウント パートナーまたはリソース パートナーの計画のガイダンスへの参照を最初に読むこと、 [Windows Server 2012 で AD FS 設計ガイド](https://technet.microsoft.com/library/dd807036.aspx)新しいパートナー組織を設定するための手順に進む前にします。 次のチェックリストに、この方法では、アカウント パートナーまたはリソース パートナー組織の完全 AD FS 設計と展開ストーリーの理解を深めるため、役立ちます。  
  
## <a name="about-account-partner-organizations"></a>アカウント パートナー組織について  
アカウント パートナーは、物理的にユーザー アカウントを AD FS: サポートされている属性ストアに格納するフェデレーションの信頼関係内の組織です。 アカウント パートナーは収集、ユーザーの資格情報の認証しそのユーザーの信頼性情報を構築、および、信頼性情報のセキュリティ トークンにパッケージ化します。 これらのトークンをリソース パートナー組織に配置されている web ベースのリソースへのアクセスを有効にするフェデレーションの信頼間で提示することです。  
  
つまり、アカウント パートナーは、セキュリティ トークンを発行する account\ 側のフェデレーション サーバーのユーザーが組織を表します。 アカウント パートナー組織内のフェデレーション サーバーは、ローカル ユーザーを認証し、承認の判断で、リソース パートナーを使用するセキュリティ トークンを作成します。  
  
属性ストア、に関して、アカウント パートナーの AD FS では概念的には、単一の Active Directory フォレスト アカウントを持つ別のフォレストに物理的に格納されているリソースへのアクセスを必要と同等です。 外部的信頼またはフォレストの信頼の 2 つのフォレスト間の関係が存在して、承認の適切なアクセス許可を持つリソースのアクセスをユーザーにしようとしていますが設定されている場合にのみ、このフォレストのアカウントには、リソース フォレスト内のリソースにアクセスできます。  
  
## <a name="about-resource-partner-organizations"></a>リソース パートナー組織について  
リソース パートナーは、Web サーバーが配置されている AD FS の展開で組織です。 リソース パートナーは、ユーザーを認証する、アカウント パートナーを信頼します。 そのため、承認の判断させるには、リソース パートナーは、アカウント パートナー内のユーザーから送信されるセキュリティ トークンにパッケージ化する要求を消費します。  
  
つまり、リソース パートナーが Web サーバーが resource\ 側のフェデレーション サーバーによって保護されている組織を表します。 リソース パートナーのフェデレーション サーバーは、リソース パートナーに Web サーバーの承認の判断をアカウント パートナーによって生成されるセキュリティ トークンを使用します。  
  
インストールされている Windows Identity Foundation \(WIF\) を持っているか、AD FS のリソース、リソース パートナー組織内の Web サーバーに機能または Active Directory フェデレーション サービス \(AD FS\) 1.x Claims\ に対応する Web エージェント役割サービスをインストールします。 AD FS リソースとして機能する web サーバーは、web browser\-ベースか、web service \current-ベースのアプリケーションをホストできます。  
