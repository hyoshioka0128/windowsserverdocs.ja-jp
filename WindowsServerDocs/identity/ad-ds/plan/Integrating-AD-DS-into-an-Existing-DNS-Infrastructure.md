---
ms.assetid: 4981b32f-741e-4afc-8734-26a8533ac530
title: "AD DS を既存の DNS インフラストラクチャに統合します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: ab8d92a237a6d1fb623d9f4bb7dcc88561edf742
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="integrating-ad-ds-into-an-existing-dns-infrastructure"></a>AD DS を既存の DNS インフラストラクチャに統合します。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

既に、組織に既存のドメイン ネーム システム (DNS) サーバー サービスがある場合は、Active Directory ドメイン サービス (AD DS) の所有者に DNS を AD DS を既存のインフラストラクチャに統合する組織の DNS の所有者は必要があります。 これは、DNS サーバーと DNS クライアントの構成を作成する必要があります。  
  
## <a name="creating-a-dns-server-configuration"></a>DNS サーバーの構成を作成します。  
既存の DNS 名前空間と AD DS を統合することで、次を実行することお勧めします。  
  
-   フォレスト内のすべてのドメイン コントローラー上の DNS サーバー サービスをインストールします。 これにより、DNS サーバーのいずれかが利用できない場合、フォールト トレランスが実現できます。 これにより、ドメイン コントローラーは名前解決のためには、他の DNS サーバーに依存する必要はありません。 管理環境は、すべてのドメイン コントローラーがある一貫した構成のためこれも合理化されます。  
  
-   Active Directory フォレストの DNS ゾーンをホストする Active Directory フォレストのルート ドメイン コントローラーを構成します。  
  
-   Active Directory ドメインに対応する DNS ゾーンをホストする各地域ドメインのドメイン コントローラーを構成します。  
  
-   Active Directory フォレスト全体のロケーター レコードを含むゾーンの構成 (つまり、_msdcs*。forestname*ゾーン) フォレスト全体の DNS アプリケーション ディレクトリ パーティションを使用して、フォレスト内のすべての DNS サーバーにレプリケートします。  
  
    > [!NOTE]  
    > DNS サーバー サービスが、Active Directory ドメイン サービス インストール ウィザード (ことをお勧めは、このオプション) にインストールされている、以前のすべてのタスクが自動的に実行されます。 詳細については、次を参照してください。 [Windows Server 2008 フォレスト ルート ドメインを展開する](https://technet.microsoft.com/library/cc731174.aspx)します。  
  
    > [!NOTE]  
    > AD DS では、フォレスト全体のロケーター レコードを使用して、互いを見つけると、クライアントをグローバル カタログ サーバーを検索するには、レプリケーション パートナーを有効にします。 AD DS では、フォレスト全体のロケーター レコードを _msdcs に格納します。*forestname*ゾーンです。 ゾーン内の情報は広く利用可能でなければならないので、このゾーンがフォレスト全体の DNS アプリケーション ディレクトリ パーティションを使用して、フォレスト内のすべての DNS サーバーにレプリケートされます。  
  
既存の DNS の構造はそのまま維持します。 任意のサーバーまたはゾーンを移動する必要はありません。 単に、既存の DNS 階層から、Active Directory 統合 DNS ゾーンの委任を作成する必要があります。  
  
## <a name="creating-the-dns-client-configuration"></a>DNS クライアントの構成を作成します。  
DNS クライアント コンピューターを構成、AD DS の所有者に DNS がスキームと、クライアントが DNS サーバーを検索する方法の名前を付け、コンピューターを指定してください。 次の表は、これらの設計要素で、推奨される構成を示します。  
  
|デザイン要素|構成|  
|------------------|-----------------|  
|コンピューターの名前付け|既定の名前付けを使用します。 Windows 2000、Windows XP、Windows Server 2003、Windows Server 2008、または Windows Vista ベースのコンピューターがドメインに参加、コンピューターを割り当てます自体のコンピューターのホスト名を構成する完全修飾ドメイン名 (FQDN) と Active Directory ドメインの名前。|  
|クライアントの競合回避モジュールの構成|ネットワーク上の任意の DNS サーバー] をポイントするクライアント コンピューターを構成します。|  
  
> [!NOTE]  
> Active Directory クライアントとドメイン コントローラー動的に登録できます DNS 名の名前に対して権限のある DNS サーバーにポイントしない場合でもします。  
  
組織以前は、静的に登録されている場合、コンピューターを DNS または組織が以前動的ホスト構成プロトコル (DHCP) の統合ソリューションを展開されているかどうか、コンピューターは、別の既存の DNS 名があります。 クライアント コンピューターでは登録済み DNS 名では、既にあるが参加しているドメインが Windows Server 2008 AD DS にアップグレードされると、次の 2 つの異なる名前を必要があります。  
  
-   既存の DNS 名  
  
-   新しい完全修飾ドメイン名 (FQDN)  
  
クライアントは、いずれかの名前で引き続き存在します。 すべての既存の DNS、DHCP、または DNS と DHCP の統合ソリューションはそのままです。 新しいプライマリ名が自動的に作成され、動的更新を使用して更新します。 これらは自動的にクリーンアップ清掃によってします。  
  
Windows 2000、Windows Server 2003、または Windows Server 2008 を実行するサーバーに接続するときに、Kerberos 認証を利用する場合は、クライアントがプライマリ名を使用してサーバーに接続を確認する必要があります。  
  


