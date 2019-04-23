---
ms.assetid: f7002265-60fa-40b8-9dd7-4bf131d9320a
title: コンピューターの名前付け
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: ae2483571d67b4cdb32c2a547b924b1315573da0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842163"
---
# <a name="computer-naming"></a>コンピューターの名前付け

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

Windows 2000、Windows XP、Windows Server 2003、Windows Server 2008、または Windows Vista オペレーティング システムを実行しているコンピューターを参加させるときに、ドメインでは、既定では、コンピューター自体名を割り当てます。 コンピューター (システムのプロパティでは、コンピューター名) のホスト名と、コンピューターが参加している Active Directory ドメインのドメイン ネーム システム (DNS) 名自体を割り当てます名で構成されます (つまり、プライマリ DNS サフィックスでシステムのプロパティ)。 ホスト名とドメインの DNS 名の連結は、完全修飾ドメイン名 (FQDN) と呼ばれます。 たとえば、Server1 結合 corp.contoso.com というドメイン ホストを使用しているコンピューターの名前、コンピューターの FQDN は server1.corp.contoso.com が。  
  
コンピューターの FQDN は登録された名前の異なるコンピューターに既に静的に DNS ゾーンに入力または統合の DNS/動的ホスト構成プロトコル (DHCP) サーバー サービスによって登録された別の DNS ドメイン名が、先に。 コンピューターは、いずれかの名前で参照できます。  
  
Active Directory Domain Services (AD DS) の名前付け規則の詳細については、コンピューター、ドメイン、サイト、および組織単位の Active Directory 内の名前付け規則を参照してください ([https://go.microsoft.com/fwlink/?LinkID=106629](https://go.microsoft.com/fwlink/?LinkID=106629))。  
  


