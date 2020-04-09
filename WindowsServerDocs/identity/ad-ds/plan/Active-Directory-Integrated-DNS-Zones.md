---
ms.assetid: 39c0126d-af5e-4dcb-88c1-aa38f888e973
title: Active Directory 統合 DNS ゾーン
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 5e9047fced5c89c1f2c9d5edaf1ff02536c2a709
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80822895"
---
# <a name="active-directory-integrated-dns-zones"></a>Active Directory 統合 DNS ゾーン

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ドメインコントローラー上で実行されているドメインネームシステム (DNS) サーバーは、Active Directory Domain Services (AD DS) にゾーンを格納できます。 この方法では、すべてのゾーンデータが Active Directory レプリケーションによって自動的にレプリケートされるため、通常の DNS ゾーン転送を使用する別の DNS レプリケーショントポロジを構成する必要はありません。 これにより、DNS の展開プロセスが簡略化され、次のような利点があります。  
  
-   DNS レプリケーション用に複数のマスターが作成されます。 そのため、DNS サーバーサービスを実行しているドメイン内のドメインコントローラーは、そのドメインが権限を持っているドメイン名に対して、Active Directory 統合された DNS ゾーンの更新を書き込むことができます。 別の DNS ゾーン転送トポロジは必要ありません。  
  
-   セキュリティで保護された動的更新がサポートされています。 セキュリティで保護された動的更新を使用すると、管理者は、コンピューターの名前を更新したり、許可されていないコンピューターが DNS 内の既存の名前を上書きすることを防ぐ  
  
Windows Server 2008 の Active Directory 統合 DNS では、ゾーンデータがアプリケーションディレクトリパーティションに格納されます。 (Active Directory との Windows Server 2003 ベースの DNS 統合から動作が変更されることはありません)。AD DS のインストール時に、次の DNS 固有のアプリケーションディレクトリパーティションが作成されます。  
  
-   ForestDnsZones と呼ばれるフォレスト全体のアプリケーションディレクトリパーティション  
  
-   ドメイン全体のアプリケーションディレクトリパーティション (DomainDnsZones という名前のフォレスト内の各ドメイン用)  
  
AD DS がアプリケーションパーティションに DNS 情報を格納する方法の詳細については、「 [Dns テクニカルリファレンス](https://go.microsoft.com/fwlink/?LinkId=106636)」を参照してください。  
  
> [!NOTE]  
> Active Directory ドメインサービスインストールウィザード (Dcpromo.exe) を実行する場合は、DNS をインストールすることをお勧めします。 これを行うと、ウィザードによって自動的に DNS ゾーンの委任が作成されます。 詳細については、「 [Windows Server 2008 のフォレストルートドメインの展開](https://technet.microsoft.com/library/cc731174.aspx)」を参照してください。  
  


