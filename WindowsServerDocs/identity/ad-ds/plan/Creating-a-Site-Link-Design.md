---
ms.assetid: 206b8072-1d0c-4a0b-ba8a-35a868d67b4c
title: サイト リンク設計の作成
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 4e0607cf66d41e1747b108a3ecc10562120d9174
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861933"
---
# <a name="creating-a-site-link-design"></a>サイト リンク設計の作成

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

サイト リンクを含む、サイトを接続するサイト リンク設計を作成します。 サイト リンクでは、サイト間接続とレプリケーションのトラフィックを転送に使用する方法を反映します。 サイトごとのドメイン コント ローラーは、Active Directory の変更をレプリケートできるように、サイト リンクにサイトを接続する必要があります。  
  
## <a name="connecting-sites-with-site-links"></a>サイトとサイト リンクの接続

サイト リンクにサイトを接続するには、サイト リンクで接続、それぞれのサイト間トランスポート コンテナー サイト リンク オブジェクトを作成し、名前をサイト リンクにするメンバーのサイトを特定します。 サイト リンクを作成した後、サイト リンクのプロパティを設定することができます。  
  
サイト リンクを作成するときは、すべてのサイトがサイト リンクに含まれることを確認します。 さらに、すべてのサイトが接続されている相互に他のサイト リンクから、変更は、任意のサイト内のドメイン コント ローラーから他のすべてのサイトにレプリケートできるようにを確認します。 これに失敗した場合、ディレクトリ サービス ログにイベント ビューアーでは、サイトのトポロジが接続されていないことを示すエラー メッセージが生成されます。  
  
新しく作成されたサイト リンクにサイトを追加するたびに追加するサイトがその他のサイト リンクのメンバーであるかどうかし、必要な場合は、サイトのサイト リンクのメンバーシップを変更します。 などを行う場合、サイト既定の最初のサイトのリンクのメンバー、サイトを最初に作成するは、新しいサイト リンクにサイトを追加した後、既定の最初のサイトのリンクからサイトを削除することを確認します。 既定の最初のサイトのリンクからサイトを削除しないと、知識整合性チェッカー (KCC) が両方のサイト リンク ルーティングの間違いになる可能性がありますのメンバーシップに基づくルーティングの決定になります。  
  
サイト リンクで接続するメンバーのサイトを識別するには、場所と「地理的な場所との通信リンク」(DSSTOPO_1.doc) ワークシートに記録したリンクの場所の一覧を使用します。 複数のサイトが同じ接続と相互に可用性がある場合は、同じサイト リンクを使用して接続できます。  
  
サイト間トランスポート コンテナーは、サイト リンクをリンクを使用するトランスポートにマップするための手段を提供します。 IP トランスポート経由でリモート プロシージャ コール (RPC) とサイト リンクを関連付けます、IP コンテナーまたは SMTP サイト リンクに関連付けます簡易メール転送プロトコル (SMTP) のコンテナーのいずれかで作成するときに、サイト リンク オブジェクトを作成します。トランスポート。  
  
> [!NOTE]  
> SMTP レプリケーションは、Active Directory Domain Services (AD DS); の将来のバージョンではサポートされません。そのため、SMTP のコンテナーにサイト リンク オブジェクトを作成しないでください。  
  
それぞれのサイト間トランスポート コンテナーには、サイト リンク オブジェクトを作成するときに AD DS は、ドメイン コント ローラー間でサイト間とサイト内の両方のレプリケーションを転送するのに IP 経由で RPC を使用します。 転送中にデータをセキュリティで保護されたままには、レプリケーションの IP を経由した RPC は、Kerberos 認証プロトコルとデータ暗号化の両方を使用します。  
  
直接 IP 接続が利用できない場合は、SMTP を使用してサイト間レプリケーションを構成できます。 ただし、SMTP レプリケーションの機能は制限され、エンタープライズ証明機関 (CA) が必要です。 SMTP では、構成、スキーマ、およびアプリケーション ディレクトリ パーティションにのみレプリケートでき、ドメイン ディレクトリ パーティションのレプリケーションをサポートしていません。  
  
サイト リンクの名前、name_of_site1 name_of_site2 などの一貫性のある名前付けスキームを使用します。 サイト、サイトのリンク、およびワークシート内でこれらのサイトを接続するサイト リンクの名前の一覧を記録します。 サイト名と関連付けられているサイト リンク名を記録するためのワークシートを参照してください[ジョブ エイドの Windows Server 2003 展開キット](https://go.microsoft.com/fwlink/?LinkID=102558)、Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip をダウンロードし、。「サイトと関連付けられているサイト リンク」を開きます (DSSTOPO_5.doc)。  
  
## <a name="in-this-guide"></a>このガイドについて

[サイト リンクのプロパティの設定](Setting-Site-Link-Properties.md)  
