---
title: ドメイン ネーム システム (DNS)
description: このトピックでは、Windows Server 2016 での DNS の概要
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: 1324ba18-4e28-4b9d-bbe7-75707e6d30ab
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 23851d2d8015fc6ae9e0653e8a0843f8c4295162
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="domain-name-system-dns"></a>ドメイン ネーム システム (DNS)

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

ドメイン ネーム システム (DNS) は業界標準の TCP/IP を構成するプロトコル群の 1 つと、DNS クライアントおよび DNS サーバーを併用してコンピューター名 TO-IP アドレス マッピングの名前解決サービス コンピューターとユーザーにします。  
  
> [!NOTE]  
> このトピックに加え、次の DNS コンテンツは使用できます。  
>   
> -   [DNS クライアントの新機能](What-s-New-in-DNS-Client.md)  
> -   [DNS サーバーの新機能](What-s-New-in-DNS-Server.md)  
> -   [DNS ポリシー シナリオ ガイド](deploy/DNS-Policy-Scenario-Guide.md)  
> -   ビデオ: [Windows Server 2016: IPAM で DNS の管理](https://channel9.msdn.com/Blogs/windowsserver/Windows-Server-2016-DNS-management-in-IPAM)  
  
Windows Server 2016 では、DNS は、サーバー マネージャーまたは Windows PowerShell コマンドを使用して、インストール可能なサーバーの役割です。 新しい Active Directory フォレストとドメインをインストールする場合に自動的に DNS がインストールされていると Active Directory フォレストおよびドメインのグローバル カタログ サーバーとして。  
  
Active Directory ドメイン サービス (AD DS) では、そのドメイン コントローラーの特定手段として DNS を使用します。 プリンシパルの Active Directory 操作のいずれかを実行すると、認証など更新、または検索するには、コンピューター DNS を使用して Active Directory ドメイン コントローラーを検索します。 さらに、ドメイン コントローラーは、互いを見つける DNS を使用します。  
  
DNS クライアント サービスは、Windows オペレーティング システムのすべてのクライアントとサーバーのバージョンでは含まれており、オペレーティング システムのインストール時に既定で実行しています。 DNS サーバーの IP アドレスを持つ、TCP/IP ネットワーク接続を構成するときに、DNS クライアントは、ドメイン コントローラーを検出して、コンピューター名を IP アドレスに解決するのには、DNS サーバーを照会します。 たとえば、Active Directory ユーザー アカウントを使用して、ネットワーク ユーザーが、Active Directory ドメインにログインすると、DNS クライアント サービスは、Active Directory ドメインのドメイン コントローラーを見つけるには DNS サーバーを照会します。 DNS サーバーは、クエリに応答すると、ドメイン コントローラーの IP アドレスをクライアントに提供、クライアントは、ドメイン コントローラーに接続し、認証プロセスが開始します。  
  
Windows Server 2016 の DNS サーバーと DNS クライアント サービスは、TCP/IP プロトコル スイートに含まれている、DNS プロトコルを使用します。 DNS は、次の図に示すように、TCP/IP 参照モデルのアプリケーション層の一部です。  
  
![TCP/IP の DNS](../media/Domain-Name-System--DNS-/dns_in_tcpip.jpg)  
  

