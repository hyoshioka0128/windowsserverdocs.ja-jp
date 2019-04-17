---
ms.assetid: 39c0126d-af5e-4dcb-88c1-aa38f888e973
title: "Active Directory 統合 DNS ゾーン"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 11940ddda320ea36bf8439afed91fcf6803f2fee
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="active-directory-integrated-dns-zones"></a>Active Directory 統合 DNS ゾーン

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ドメイン コント ローラーで実行されているドメイン ネーム システム (DNS) サーバーは、Active Directory ドメイン サービス (AD DS) で、そのゾーンを格納できます。 この方法では、ゾーンのすべてのデータを自動的に Active Directory レプリケーションによりレプリケートされるため、通常の DNS ゾーン転送を使用する別の DNS レプリケーション トポロジを構成する必要はありません。 これにより、DNS の展開プロセスを簡略化し、次の利点を提供します。  
  
-   DNS レプリケーションには、複数のマスターが作成されます。 そのため、DNS サーバー サービスを実行しているドメイン内の任意のドメイン コント ローラーは、Active Directory 統合 DNS ゾーンのためには権限を持つドメイン名を更新プログラムを記述できます。 別の DNS ゾーン転送のトポロジは必要ありません。  
  
-   保護された動的更新がサポートされます。 保護された動的更新を許可すると、管理者がどのようなコンピューターがどのような名前を更新するかを制御し、不正なコンピュータが DNS 内の既存の名前を上書きしないようにします。  
  
Windows Server 2008 で active Directory 統合 DNS は、アプリケーション ディレクトリ パーティションのゾーン データを格納します。 (Active Directory と Windows Server 2003 ベースの DNS の統合の動作の変更はありません) です。AD DS のインストール中には、次の DNS に固有のアプリケーション ディレクトリ パーティションが作成されます。  
  
-   ForestDnsZones と呼ばれる、フォレスト全体のアプリケーション ディレクトリ パーティション  
  
-   ドメイン全体のアプリケーション ディレクトリ パーティション、フォレスト内の各ドメインのという DomainDnsZones  
  
アプリケーション パーティションを AD DS が DNS 情報を保管する方法の詳細については、次を参照してください。、 [DNS のテクニカル リファレンス](https://go.microsoft.com/fwlink/?LinkId=106636)します。  
  
> [!NOTE]  
> Active Directory ドメイン サービス インストール ウィザード (Dcpromo.exe) を実行すると、DNS をインストールすることをお勧めします。 これを行うと、DNS ゾーンの委任が自動的に作成されます。 詳細については、次を参照してください。 [Windows Server 2008 フォレスト ルート ドメインを展開する](https://technet.microsoft.com/library/cc731174.aspx)します。  
  


