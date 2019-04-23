---
ms.assetid: 39c0126d-af5e-4dcb-88c1-aa38f888e973
title: Active Directory 統合 DNS ゾーン
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 5e0830944ec5d91dace52db337e89211ee362b98
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873253"
---
# <a name="active-directory-integrated-dns-zones"></a>Active Directory 統合 DNS ゾーン

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

ドメイン コント ローラーで実行されているドメイン ネーム システム (DNS) サーバーは、そのゾーンを Active Directory Domain Services (AD DS) に格納できます。 この方法では、Active Directory のレプリケーションを使用してすべてのゾーン データが自動的にレプリケートされるため、通常の DNS ゾーン転送を使用する別の DNS レプリケーション トポロジを構成する必要はありません。 これは、DNS の展開プロセスを簡略化し、次の利点を提供します。  
  
-   DNS レプリケーションには、複数のマスターが作成されます。 そのため、DNS サーバー サービスを実行しているドメイン内の任意のドメイン コント ローラーは、権限のあるドメイン名の Active Directory 統合 DNS ゾーンに更新プログラムを記述できます。 別の DNS ゾーン転送のトポロジは必要ありません。  
  
-   安全な動的更新がサポートされています。 安全な動的更新を許可すると、管理者がどのようなコンピューターがどのような名前を更新するかを制御し、承認されていないコンピューターが DNS 内の既存の名前を上書きしないようにします。  
  
Windows Server 2008 の active Directory 統合 DNS は、アプリケーション ディレクトリ パーティションにゾーン データを格納します。 (Active Directory と Windows Server 2003 ベースの DNS の統合からの動作の変更はありません) です。次の特定の DNS アプリケーション ディレクトリ パーティションは、AD DS のインストール中に作成されます。  
  
-   フォレスト全体のアプリケーション ディレクトリ パーティション、ForestDnsZones と呼ばれる  
  
-   ドメイン全体のアプリケーション ディレクトリ パーティション、フォレスト内の各ドメインのという DomainDnsZones  
  
AD DS がアプリケーション パーティションの DNS 情報を格納する方法の詳細については、次を参照してください。、 [DNS テクニカル リファレンス](https://go.microsoft.com/fwlink/?LinkId=106636)します。  
  
> [!NOTE]  
> Active Directory ドメイン サービス インストール ウィザード (Dcpromo.exe) を実行すると、DNS をインストールすることをお勧めします。 これを行うと、DNS ゾーンの委任が自動的に作成されます。 詳細については、次を参照してください。 [Windows Server 2008 フォレスト ルート ドメインを展開する](https://technet.microsoft.com/library/cc731174.aspx)します。  
  


