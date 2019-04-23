---
ms.assetid: 4981b32f-741e-4afc-8734-26a8533ac530
title: AD DS を既存の DNS インフラストラクチャに統合する
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 62405ea9ee38bb3fa457b7731e26fbffb2594797
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59891043"
---
# <a name="integrating-ad-ds-into-an-existing-dns-infrastructure"></a>AD DS を既存の DNS インフラストラクチャに統合する

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

既に組織に既存のドメイン ネーム システム (DNS) サーバー サービスがある場合は、Active Directory Domain Services (AD DS) の所有者の DNS を既存のインフラストラクチャに AD DS に統合する、組織の DNS の所有者は必要があります。 これは、DNS サーバーおよび DNS クライアントの構成を作成する必要があります。  
  
## <a name="creating-a-dns-server-configuration"></a>DNS サーバーの構成を作成します。  
既存の DNS 名前空間と AD DS の統合には、次を行うことお勧めします。  
  
-   フォレスト内のすべてのドメイン コント ローラー上の DNS サーバー サービスをインストールします。 これにより、DNS サーバーのいずれかが利用できない場合、フォールト トレランスを提供します。 これにより、ドメイン コント ローラーは他の DNS サーバーの名前解決に依存する必要はありません。 すべてのドメイン コント ローラーが一貫した構成があるため、これも、管理環境が合理化されます。  
  
-   Active Directory フォレストの DNS ゾーンをホストする Active Directory フォレストのルート ドメイン コント ローラーを構成します。  
  
-   Active Directory ドメインに対応する DNS ゾーンをホストする各地域ドメインのドメイン コント ローラーを構成します。  
  
-   Active Directory フォレスト全体のロケーター レコードを含むゾーンの構成 (_msdcs つまり *。forestname*ゾーン) フォレスト全体の DNS アプリケーション ディレクトリ パーティションを使用して、フォレスト内のすべての DNS サーバーにレプリケートします。  
  
    > [!NOTE]  
    > DNS サーバー サービスは、Active Directory ドメイン サービス インストール ウィザード (このオプションを推奨) にインストールされている、以前のすべてのタスクが自動的に実行されます。 詳細については、次を参照してください。 [Windows Server 2008 フォレスト ルート ドメインを展開する](https://technet.microsoft.com/library/cc731174.aspx)します。  
  
    > [!NOTE]  
    > AD DS では、フォレスト全体のロケーター レコードを使用して、互いに検出し、クライアントがグローバル カタログ サーバーを検索するを有効にするレプリケーション パートナーを有効にします。 AD DS では、フォレスト全体のロケーター レコードが、_msdcs に格納します。*forestname*ゾーン。 ゾーンの情報は、広く普及している必要があります、ため、このゾーンは、フォレスト全体の DNS アプリケーション ディレクトリ パーティションを使用して、フォレスト内のすべての DNS サーバーにレプリケートされます。  
  
既存の DNS の構造は変わりません。 任意のサーバーまたはゾーンに移動する必要はありません。 単に、既存の DNS 階層から、Active Directory 統合 DNS ゾーンの委任を作成する必要があります。  
  
## <a name="creating-the-dns-client-configuration"></a>DNS クライアントの構成を作成します。  
クライアント コンピューターで DNS を構成、AD DS の所有者の DNS が、コンピューターの名前付けスキームと、クライアントが DNS サーバーを検索する方法を指定してください。 次の表では、これらのデザイン要素で、推奨される構成を示します。  
  
|デザイン要素|構成|  
|------------------|-----------------|  
|コンピューターの名前付け|既定の名前付けを使用します。 Windows 2000、Windows XP、Windows Server 2003、Windows Server 2008、または Windows Vista ベースのコンピューターがドメインに参加、コンピューターのホスト名で構成される完全修飾ドメイン名 (FQDN) とのアクティブな名前そのものコンピューター割り当てますディレクトリのドメイン。|  
|クライアントの競合回避モジュールの構成|ネットワーク上の任意の DNS サーバー をポイントするクライアント コンピューターを構成します。|  
  
> [!NOTE]  
> Active Directory クライアントとドメイン コント ローラーできますを動的に登録が DNS 名の名前に対して権限のある DNS サーバーをポイントしない場合でもです。  
  
コンピューターは、組織以前は、静的に登録されている場合、コンピューターの DNS または組織が動的ホスト構成プロトコル (DHCP) の統合ソリューションを以前展開されているかどうか、別の既存の DNS 名にすることがあります。 場合は、クライアント コンピューターでは登録済みの DNS 名では、既にあるが参加しているドメインを Windows Server 2008 AD DS にアップグレードすると、これら 2 つの異なる名前になります。  
  
-   既存の DNS 名  
  
-   新しい完全修飾ドメイン名 (FQDN)  
  
クライアントは、いずれかの名前でも配置できます。 任意の既存の DNS、DHCP または DNS と DHCP の統合ソリューションはそのまま残っています。 新しいプライマリ名は自動的に作成され、動的更新を使用して更新します。 これらは自動的にクリーンアップ清掃を使用しています。  
  
Windows 2000、Windows Server 2003、または Windows Server 2008 を実行するサーバーに接続するときに、Kerberos 認証を利用する場合は、クライアントがプライマリの名前を使用してサーバーに接続を確認する必要があります。  
  


