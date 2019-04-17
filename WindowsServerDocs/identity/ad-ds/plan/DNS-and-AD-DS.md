---
ms.assetid: c32606b4-2ee2-4df3-a704-8ac6723e188f
title: "DNS と AD DS"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 8e7ee494c157396a7d58e9fd1b4b80060c4d99fc
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="dns-and-ad-ds"></a>DNS と AD DS

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Active Directory ドメイン サービス (AD DS) の可能にするクライアントをドメイン コントローラーを検索し、ドメイン コントローラー、ドメイン ネーム システム (DNS) 名前解決サービスが相互に通信するためにディレクトリ サービスは、そのホストで使用します。  
  
AD DS は、Active Directory 名前空間の既存の DNS 名前空間に簡単に統合を有効にします。 機能など、Active Directory 統合 DNS ゾーンのセカンダリ ゾーンを設定する必要がなくなるため、DNS を展開しやすくし、ゾーン転送を構成します。  
  
DNS が AD DS をサポートする方法の詳細については、Active Directory のテクニカル リファレンスの DNS のサポートを参照してください。([https://go.microsoft.com/fwlink/?LinkID=48147](https://go.microsoft.com/fwlink/?LinkID=48147))。  
  
> [!NOTE]  
> クライアントが使用するプライマリ DNS サフィックスから AD DS ドメイン名とは異なる不整合な名前空間を実装する場合、DNS と AD DS の統合は、複雑です。 詳細については、次を参照してください。[不整合 Namespace](../../ad-ds/plan/../../ad-ds/plan/Disjoint-Namespace.md)します。  
  
## <a name="in-this-section"></a>このセクションで  
  
-   [ドメイン コントローラーの場所](../../ad-ds/plan/Domain-Controller-Location.md)  
  
-   [Active Directory 統合 DNS ゾーン](../../ad-ds/plan/Active-Directory-Integrated-DNS-Zones.md)  
  
-   [コンピューターの名前付け](../../ad-ds/plan/Computer-Naming.md)  
  
-   [不整合のある Namespace](../../ad-ds/plan/../../ad-ds/plan/Disjoint-Namespace.md)  
  


