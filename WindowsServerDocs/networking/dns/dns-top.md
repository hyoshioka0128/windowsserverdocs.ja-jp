---
title: ドメイン ネーム システム (DNS)
description: このトピックでは、Windows Server 2016 での DNS の概要を提供します。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: 1324ba18-4e28-4b9d-bbe7-75707e6d30ab
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 3d4ec63e904dd899a3ddc53a59274ad607136edd
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870823"
---
# <a name="domain-name-system-dns"></a>ドメイン ネーム システム (DNS)

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

ドメイン ネーム システム (DNS) は、業界標準の TCP/IP を構成するプロトコル群のいずれかと、まとめて DNS クライアントおよび DNS サーバー コンピューターとユーザーにコンピューター名と IP アドレスのマッピング名前解決サービスを提供します。  
  
> [!NOTE]  
> このトピックに加え、次の DNS コンテンツは使用できます。  
>   
> -   [DNS クライアントの新機能新機能](What-s-New-in-DNS-Client.md)  
> -   [DNS サーバーの新機能新機能](What-s-New-in-DNS-Server.md)  
> -   [DNS ポリシー シナリオ ガイド](deploy/DNS-Policy-Scenario-Guide.md)  
> -   ビデオ:[Windows Server 2016:IPAM の DNS の管理](https://channel9.msdn.com/Blogs/windowsserver/Windows-Server-2016-DNS-management-in-IPAM)  
  
Windows Server 2016 では、DNS とは、サーバー マネージャーまたは Windows PowerShell コマンドを使用して、インストール可能なサーバーの役割です。 新しい Active Directory フォレストおよびドメインをインストールする場合に自動的に DNS がインストールされていると Active Directory フォレストおよびドメインのグローバル カタログ サーバーとして。  
  
Active Directory Domain Services (AD DS) では、そのドメイン コント ローラーの場所のメカニズムとして DNS を使用します。 プリンシパルの Active Directory 操作のいずれかが実行されると、認証など、更新、または検索するには、コンピューター DNS を使用して Active Directory ドメイン コント ローラーを特定します。 さらに、ドメイン コント ローラーは、お互いを検索するのに DNS を使用します。  
  
DNS クライアント サービスは、Windows オペレーティング システムのすべてのクライアントとサーバー バージョンが用意されており、オペレーティング システムのインストール時に既定で実行しています。 DNS サーバーの IP アドレスで、TCP/IP ネットワーク接続を構成するときに、DNS クライアントは、ドメイン コント ローラーを検出して、コンピューター名を IP アドレスに解決するのには、DNS サーバーを照会します。 たとえば、Active Directory ユーザー アカウントを持つネットワーク ユーザーが Active Directory ドメインにログインすると、DNS クライアント サービスは、Active Directory ドメインのドメイン コント ローラーに DNS サーバーを照会します。 DNS サーバーは、クエリに応答すると、ドメイン コント ローラーの IP アドレスをクライアントに提供する、クライアントは、ドメイン コント ローラーに接続し、認証プロセスを開始できます。  
  
Windows Server 2016 の DNS サーバーと DNS クライアント サービスは、TCP/IP プロトコル スイートに含まれている、DNS プロトコルを使用します。 次の図に示すように、DNS は、TCP/IP 参照モデルのアプリケーション層の一部です。  
  
![TCP/IP の DNS](../media/Domain-Name-System--DNS-/dns_in_tcpip.jpg)  
  

