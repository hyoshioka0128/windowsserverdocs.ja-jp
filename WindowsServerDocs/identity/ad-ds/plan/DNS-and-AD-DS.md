---
ms.assetid: c32606b4-2ee2-4df3-a704-8ac6723e188f
title: DNS と AD DS
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 82c96ac3f146510c5590aabea75a60ca0f5f90cc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402688"
---
# <a name="dns-and-ad-ds"></a>DNS と AD DS

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

Active Directory Domain Services (AD DS) は、ドメインネームシステム (DNS) の名前解決サービスを使用して、クライアントがドメインコントローラーを特定し、ディレクトリサービスをホストするドメインコントローラーが相互に通信できるようにします。  
  
AD DS により、Active Directory 名前空間を既存の DNS 名前空間に簡単に統合できます。 Active Directory 統合された DNS ゾーンなどの機能を使用すると、セカンダリゾーンを設定する必要がなくなり、ゾーン転送を構成しなくても、DNS を簡単に展開できるようになります。  
  
DNS が AD DS をサポートする方法の詳細については、「 [Active Directory テクニカルリファレンスの Dns サポート](https://go.microsoft.com/fwlink/?LinkID=48147)」セクションを参照してください。  
  
> [!NOTE]  
> AD DS ドメイン名がクライアントが使用するプライマリ DNS サフィックスとは異なる名前空間を実装した場合、DNS との統合 AD DS より複雑になります。 詳細については、「[不整合な名前空間](../../ad-ds/plan/../../ad-ds/plan/Disjoint-Namespace.md)」を参照してください。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
- [ドメイン コントローラーの場所](../../ad-ds/plan/Domain-Controller-Location.md)  
- [Active Directory 統合 DNS ゾーン](../../ad-ds/plan/Active-Directory-Integrated-DNS-Zones.md)  
- [コンピューターの名前付け](../../ad-ds/plan/Computer-Naming.md)  
- [名前空間の不整合](../../ad-ds/plan/../../ad-ds/plan/Disjoint-Namespace.md)  
