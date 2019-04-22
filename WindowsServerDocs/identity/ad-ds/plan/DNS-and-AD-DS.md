---
ms.assetid: c32606b4-2ee2-4df3-a704-8ac6723e188f
title: DNS と AD DS
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: f6d75a78119d76a0f8380967292b1d0abc720597
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813143"
---
# <a name="dns-and-ad-ds"></a>DNS と AD DS

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

Active Directory Domain Services (AD DS) は、互いに通信するのにディレクトリ サービスをホストする、クライアントがドメイン コント ローラーを特定してのに、ドメイン コント ローラーのできるようにするにドメイン ネーム システム (DNS) 名前解決サービスを使用します。  
  
AD DS では、Active Directory 名前空間の既存の DNS 名前空間に簡単に統合できるようにします。 機能など、Active Directory 統合 DNS ゾーン、セカンダリ ゾーンを設定する必要がなくなるため、DNS の展開が容易し、ゾーン転送を構成します。  
  
DNS は AD DS をサポートする方法については、セクションをご覧ください。 [Active Directory に関するテクニカル リファレンス用に DNS サポート](https://go.microsoft.com/fwlink/?LinkID=48147)します。  
  
> [!NOTE]  
> クライアントが使用するプライマリ DNS サフィックスから AD DS のドメイン名とは異なる不整合な名前空間を実装する場合、DNS と AD DS の統合は複雑です。 詳細については、次を参照してください。[不整合のある Namespace](../../ad-ds/plan/../../ad-ds/plan/Disjoint-Namespace.md)します。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
- [ドメイン コント ローラーの場所](../../ad-ds/plan/Domain-Controller-Location.md)  
- [Active Directory 統合 DNS ゾーン](../../ad-ds/plan/Active-Directory-Integrated-DNS-Zones.md)  
- [コンピューターの名前付け](../../ad-ds/plan/Computer-Naming.md)  
- [不整合のある Namespace](../../ad-ds/plan/../../ad-ds/plan/Disjoint-Namespace.md)  
