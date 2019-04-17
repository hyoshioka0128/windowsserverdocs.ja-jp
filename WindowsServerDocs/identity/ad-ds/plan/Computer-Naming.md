---
ms.assetid: f7002265-60fa-40b8-9dd7-4bf131d9320a
title: "コンピューターの名前付け"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: d0dbe2da76a1cf3d1a4dd74183b5dd7106ef17b9
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="computer-naming"></a>コンピューターの名前付け

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Windows 2000、Windows XP、Windows Server 2003、Windows Server 2008、または Windows Vista オペレーティング システムを実行しているコンピューターを参加させるときに、ドメイン、コンピューターの既定で名前を割り当てます自体。 自体に割り当てます名には、コンピューター (つまり、システムのプロパティでコンピューター名) のホスト名と、コンピューターが参加している Active Directory ドメインのドメイン ネーム システム (DNS) 名が構成されています (つまり、プライマリ DNS サフィックス システムのプロパティで)。 ホスト名とドメインの DNS 名を連結したものは、完全修飾ドメイン名 (FQDN) と呼ばれます。 たとえば、Server1 のホスト名を持つコンピューターに corp.contoso.com ドメインに参加している場合、コンピューターの FQDN は server1.corp.contoso.com です。  
  
コンピューターは、静的に DNS ゾーンに挿入または統合の DNS/動的ホスト構成プロトコル (DHCP) サーバー サービスによって登録されたさまざまな DNS ドメイン名を既に持っている場合、コンピューターの FQDN とは異なりますが、以前に登録された名前。 コンピューターは、いずれかの名前で参照できます。  
  
Active Directory ドメイン サービス (AD DS) 内の命名規則に関する詳細については、コンピューター、ドメイン、サイト、および組織単位の Active Directory 内の名前付け規則を参照してください ([https://go.microsoft.com/fwlink/?LinkID=106629](https://go.microsoft.com/fwlink/?LinkID=106629))。  
  


