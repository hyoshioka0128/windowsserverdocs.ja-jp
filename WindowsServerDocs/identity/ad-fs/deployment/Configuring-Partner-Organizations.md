---
ms.assetid: 4d002764-58b4-4137-9c86-1e55b02e07ce
title: パートナー組織の構成
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 5494f3bd8d012bf1ecc240439ff880d1bb52c280
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59875183"
---
# <a name="configuring-partner-organizations"></a>パートナー組織の構成

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

Active Directory フェデレーション サービスで新しい取引先組織をデプロイする\(AD FS\)、いずれかでタスクを完了[チェックリスト。Configuring the Resource Partner Organization](Checklist--Configuring-the-Resource-Partner-Organization.md)または[チェックリスト。アカウント パートナー組織の構成](Checklist--Configuring-the-Account-Partner-Organization.md)、AD FS 設計によって異なります。  
  
> [!NOTE]  
> これらのチェックリストのいずれかを使用する場合を強くお勧めアカウント パートナーまたはリソース パートナーの計画のガイダンスへの参照を最初に読むこと、 [Windows Server 2012 で AD FS 設計ガイド](https://technet.microsoft.com/library/dd807036.aspx)を続行する前に、新しい取引先組織の設定の手順。 次のチェックリストには、この方法と、アカウント パートナーまたはリソース パートナー組織の完全な AD FS の設計と展開ストーリーの理解を深めるために役立ちます。  
  
## <a name="about-account-partner-organizations"></a>アカウント パートナー組織について  
アカウント パートナーは、組織で AD FS でサポートされる属性ストアでユーザー アカウントを物理的に格納するフェデレーションの信頼関係です。 アカウント パートナーは、収集、ユーザーの資格情報の認証し、そのユーザーの要求の作成、およびセキュリティ トークンに要求をパッケージ化します。 Web へのアクセスを有効にするフェデレーションの信頼の間でこれらのトークンを提示することができますし、\-ベースのリソース パートナー組織に配置されているリソース。  
  
つまり、アカウント パートナー組織を表します。 ユーザー アカウント\-側フェデレーション サーバーがセキュリティ トークンを発行します。 アカウント パートナー組織のフェデレーション サーバーでは、ローカル ユーザーを認証し、承認決定を行うことで、リソース パートナーが使用するセキュリティ トークンを作成します。  
  
属性ストア、に関しては、AD FS におけるアカウント パートナーは、概念的には、1 つの Active Directory フォレスト アカウントを持つ別のフォレストに物理的に格納されているリソースにアクセスする必要と同じです。 このフォレストのアカウントには、外部的信頼またはフォレストの信頼の 2 つのフォレスト間にリレーションシップが存在して、適切な承認とアクセスするユーザーにしようとしているリソースが設定されている場合にのみ、リソース フォレスト内のリソースにアクセスできます。アクセス許可。  
  
## <a name="about-resource-partner-organizations"></a>リソース パートナー組織について  
リソース パートナーは、Web サーバーが配置される AD FS の展開で組織です。 リソース パートナーは、ユーザーを認証するアカウント パートナーを信頼します。 そのため、リソース パートナーは、承認決定を行うにはアカウント パートナー内のユーザーから取得したセキュリティ トークンにパッケージ化要求を消費します。  
  
リソース パートナーの Web サーバーが、リソースによって保護されている組織を表します。 つまり、\-側フェデレーション サーバー。 リソース パートナーのフェデレーション サーバーでは、承認決定を行う Web サーバーのリソース パートナーのアカウント パートナーによって作成されたセキュリティ トークンを使用します。  
  
AD FS リソースとして機能するため、リソース パートナー組織内の Web サーバーか、必要があります Windows Identity Foundation \(WIF\) Active の Directory フェデレーション サービスまたはインストールされている\(AD FS\) 1.xクレーム\-対応する Web エージェント役割サービスをインストールします。 Web サーバーを AD FS リソースは、いずれかの Web をホストできるように機能する\-ブラウザー\-ベースまたは Web\-サービス\-ベースのアプリケーション。  
