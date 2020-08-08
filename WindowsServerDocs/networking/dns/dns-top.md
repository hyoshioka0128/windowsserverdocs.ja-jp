---
title: ドメイン ネーム システム (DNS)
description: このトピックでは、Windows Server 2016 の DNS の概要について説明します。
manager: brianlic
ms.topic: article
ms.assetid: 1324ba18-4e28-4b9d-bbe7-75707e6d30ab
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 1117e523e23bfc5415754484385d290eb2375d91
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954098"
---
# <a name="domain-name-system-dns"></a>ドメイン ネーム システム (DNS)

>適用先:Windows Server (半期チャネル)、Windows Server 2016

ドメインネームシステム (DNS) は、TCP/IP を構成する業界標準のプロトコルスイートの1つであり、DNS クライアントと DNS サーバーの組み合わせにより、コンピューター名から IP アドレスへのマッピング名前解決サービスがコンピューターとユーザーに提供されます。

> [!NOTE]
> このトピックに加えて、次の DNS コンテンツを利用できます。
>
> -   [DNS クライアントの新機能](What-s-New-in-DNS-Client.md)
> -   [DNS サーバーの新機能](What-s-New-in-DNS-Server.md)
> -   [DNS ポリシー シナリオ ガイド](deploy/DNS-Policy-Scenario-Guide.md)
> -   ビデオ: [Windows Server 2016: IPAM での DNS 管理](https://channel9.msdn.com/Blogs/windowsserver/Windows-Server-2016-DNS-management-in-IPAM)

Windows Server 2016 では、DNS はサーバーの役割であり、サーバーマネージャーまたは Windows PowerShell コマンドを使用してインストールできます。 新しい Active Directory フォレストとドメインをインストールする場合は、フォレストとドメインのグローバルカタログサーバーとして Active Directory と共に DNS が自動的にインストールされます。

Active Directory Domain Services (AD DS) は、ドメインコントローラーの場所のメカニズムとして DNS を使用します。 認証、更新、検索などのプリンシパル Active Directory 操作が実行されると、コンピューターは DNS を使用して Active Directory ドメインコントローラーを検索します。 さらに、ドメインコントローラーは、DNS を使用して互いを検索します。

DNS クライアントサービスは、Windows オペレーティングシステムのすべてのクライアントバージョンとサーバーバージョンに含まれており、オペレーティングシステムのインストール時に既定で実行されます。 Dns サーバーの IP アドレスを使用して TCP/IP ネットワーク接続を構成すると、dns クライアントは dns サーバーに対してクエリを行い、ドメインコントローラーを検出し、コンピューター名を IP アドレスに解決します。 たとえば、Active Directory ユーザーアカウントを持つネットワークユーザーが Active Directory ドメインにログインすると、DNS クライアントサービスは DNS サーバーに対してクエリを行い、Active Directory ドメインのドメインコントローラーを検索します。 DNS サーバーがクエリに応答し、ドメインコントローラーの IP アドレスをクライアントに提供すると、クライアントはドメインコントローラーに接続し、認証プロセスを開始できます。

Windows Server 2016 の DNS サーバーと DNS クライアントサービスは、TCP/IP プロトコルスイートに含まれている DNS プロトコルを使用します。 DNS は、次の図に示すように、TCP/IP 参照モデルのアプリケーション層の一部です。

![TCP/IP の DNS](../media/Domain-Name-System--DNS-/dns_in_tcpip.jpg)


