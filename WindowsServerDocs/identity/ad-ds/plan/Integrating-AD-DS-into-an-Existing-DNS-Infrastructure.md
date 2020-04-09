---
ms.assetid: 4981b32f-741e-4afc-8734-26a8533ac530
title: AD DS を既存の DNS インフラストラクチャに統合する
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: cf069102f409247832204546f3e1c15de7238bd3
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80822275"
---
# <a name="integrating-ad-ds-into-an-existing-dns-infrastructure"></a>AD DS を既存の DNS インフラストラクチャに統合する

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

組織に既存の DNS (ドメインネームシステム) サーバーサービスが既に存在する場合、AD DS を既存のインフラストラクチャに統合するには、Active Directory Domain Services (AD DS) 所有者が組織の DNS 所有者と連携している必要があります。 これには、DNS サーバーと DNS クライアント構成の作成が含まれます。  
  
## <a name="creating-a-dns-server-configuration"></a>DNS サーバー構成の作成  
既存の DNS 名前空間と AD DS を統合する場合は、次の手順を実行することをお勧めします。  
  
-   フォレスト内のすべてのドメインコントローラーに DNS サーバーサービスをインストールします。 これにより、いずれかの DNS サーバーが使用できなくなるとフォールトトレランスが提供されます。 このようにして、ドメインコントローラーは、名前解決のために他の DNS サーバーに依存する必要がありません。 これにより、すべてのドメインコントローラーの構成が統一されるため、管理環境も簡素化されます。  
  
-   Active Directory フォレストの DNS ゾーンをホストするように Active Directory フォレストルートドメインコントローラーを構成します。  
  
-   各地域ドメインのドメインコントローラーが、Active Directory ドメインに対応する DNS ゾーンをホストするように構成します。  
  
-   Active Directory フォレスト全体のロケーターレコードを含むゾーン (つまり、_msdcs を構成します。*forestname*ゾーン)。フォレスト全体の dns アプリケーションディレクトリパーティションを使用して、フォレスト内のすべての dns サーバーにレプリケートします。  
  
    > [!NOTE]  
    > DNS サーバーサービスが Active Directory ドメインサービスインストールウィザードと共にインストールされると (このオプションをお勧めします)、前のすべてのタスクが自動的に実行されます。 詳細については、「 [Windows Server 2008 のフォレストルートドメインの展開](https://technet.microsoft.com/library/cc731174.aspx)」を参照してください。  
  
    > [!NOTE]  
    > AD DS は、フォレスト全体のロケーターレコードを使用して、レプリケーションパートナーが互いを検索し、クライアントがグローバルカタログサーバーを検索できるようにします。 AD DS では、フォレスト全体のロケーターレコードが _msdcs に格納されます。*forestname*ゾーン。 ゾーン内の情報は広く使用可能である必要があるため、フォレスト全体の DNS アプリケーションディレクトリパーティションによって、このゾーンはフォレスト内のすべての DNS サーバーにレプリケートされます。  
  
既存の DNS 構造はそのまま残ります。 サーバーやゾーンを移動する必要はありません。 Active Directory 統合された DNS ゾーンの委任を既存の DNS 階層から作成するだけで済みます。  
  
## <a name="creating-the-dns-client-configuration"></a>DNS クライアント構成を作成する  
クライアントコンピューターで DNS を構成するには、AD DS 所有者の DNS で、コンピューターの名前付けスキームと、クライアントが DNS サーバーを検索する方法を指定する必要があります。 次の表は、これらのデザイン要素で推奨される構成を示しています。  
  
|デザイン要素|構成|  
|------------------|-----------------|  
|コンピューターの名前付け|既定の名前付けを使用します。 Windows 2000、Windows XP、Windows Server 2003、Windows Server 2008、または Windows Vista ベースのコンピューターがドメインに参加している場合、コンピューターは、コンピューターのホスト名と Active Directory ドメインの名前で構成される完全修飾ドメイン名 (FQDN) を割り当てます。|  
|クライアントリゾルバーの構成|ネットワーク上の任意の DNS サーバーをポイントするようにクライアントコンピューターを構成します。|  
  
> [!NOTE]  
> Active Directory クライアントとドメインコントローラーは、名前に対して権限のある DNS サーバーを指していない場合でも、DNS 名を動的に登録できます。  
  
以前に組織が DNS にコンピューターを静的に登録した場合、または組織が事前に統合された動的ホスト構成プロトコル (DHCP) ソリューションを展開した場合は、コンピューターに既存の DNS 名が異なる可能性があります。 クライアントコンピューターに既に登録済みの DNS 名がある場合、参加しているドメインが Windows Server 2008 AD DS にアップグレードされると、2つの異なる名前が使用されます。  
  
-   既存の DNS 名  
  
-   新しい完全修飾ドメイン名 (FQDN)  
  
クライアントは、どちらの名前でも配置できます。 既存の DNS、DHCP、または統合された DNS/DHCP ソリューションは、そのまま残ります。 新しいプライマリ名は、動的更新によって自動的に作成され、更新されます。 これらは清掃によって自動的にクリーンアップされます。  
  
Windows 2000、Windows Server 2003、または Windows Server 2008 を実行しているサーバーに接続するときに Kerberos 認証を利用する場合は、クライアントがプライマリ名を使用してサーバーに接続していることを確認する必要があります。  
  


