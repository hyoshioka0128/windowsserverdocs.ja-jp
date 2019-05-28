---
ms.assetid: 4ddb927d-d65e-491d-840a-16049c083d13
title: 属性ストアの役割
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: bec3ebf1bd12b260dbbb245a6a905277ff0d749f
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66188540"
---
# <a name="the-role-of-attribute-stores"></a>属性ストアの役割
Active Directory フェデレーション サービスは、「属性ストア」という用語を使用すると、ディレクトリや組織がそのユーザー アカウントとその関連付けられた属性値の格納に使用するデータベースを参照してください。 AD FS がストアからこれらの属性値を取得できる Web アプリケーションまたはサービス証明書利用者のパーティ組織でホストされているように、適切な情報に基づくクレームを作成と、id プロバイダー組織で構成が完了後承認決定されるたびに、フェデレーション ユーザー \(id プロバイダー組織にアカウントが格納されているユーザー\)アプリケーションまたはサービスにアクセスしようとしています。  
  
信頼性情報を生成する方法の詳細については、「 [The Role of Claims](The-Role-of-Claims.md)」を参照してください。  
  
## <a name="how-attribute-stores-fit-in-with-your-ad-fs-deployment-goals"></a>AD FS の展開目標に属性ストアを適合させる方法  
ユーザーが認証場所とユーザーの属性ストアの場所は、ユーザー id をサポートするために AD FS の設計方法を決定します。 属性ストアが配置されていると、ユーザーがアプリケーションにアクセスする場所に応じて\(イントラネットまたはインターネット上\)、次の展開の目標の 1 つを使用することができます。  
  
-   [クレーム対応アプリケーションとサービスに、Active Directory ユーザーへのアクセスを提供](https://technet.microsoft.com/library/dd807071.aspx)— この目標を組織のユーザーのアクセスの AD FS で保護されたアプリケーションまたはサービス\(独自のアプリケーションまたはサービス、またはパートナーのアプリケーションまたはサービス\)ときに、ユーザー ログオンしている Active Directory に企業のイントラネット内。  
  
-   [アプリケーションとその他の組織のサービスに、Active Directory ユーザーへのアクセスを提供](https://technet.microsoft.com/library/dd807123.aspx)-AD FS で保護されたアプリケーションまたはサービスでこの目標を組織のユーザーがアクセス\(独自のアプリケーションまたはサービス、またはパートナーのアプリケーションまたはサービス\)ユーザーが企業のイントラネット内を使用して、インターネットからリモートでログオン属性ストアにログオンするとします。  
  
-   [クレーム対応アプリケーションとサービスをユーザーに別の組織のアクセスを提供する](https://technet.microsoft.com/library/dd807099.aspx)— この目標は、その組織の企業イントラネット上の属性ストアに格納されている別の組織のユーザー アカウントにアクセスする必要があります、AD FS:組織のセキュリティで保護されたアプリケーション。 この目標にも動作ときにコンシューマー\-AD 組織内の FS で保護されたアプリケーションにアクセス権を持つ、組織の境界ネットワーク内の属性ストアに格納されているベースのユーザー アカウントを指定する必要があります。  
  
属性ストアの場所と、組織の他の要件に応じて、AD FS 展開の設計を完了するには、これらの展開目標のいくつかを組み合わせることができます。  
  
## <a name="attribute-stores-that-are-supported-by-ad-fs"></a>AD FS でサポートされている属性ストア  
AD FS は、さまざまなディレクトリをサポートし、管理者の展開で使用できるデータベースに格納されます\-属性値を定義し、それらの値を持つ信頼性情報を設定します。 AD FS は、属性ストアとして、次のディレクトリやデータベースのいずれかのようにサポートされています。  
  
-   Windows Server 2003 では、Active Directory Domain Services での active Directory \(AD DS\)で Windows Server 2012 および 2012 R2、Windows Server 2008 では、AD DS と Windows Server 2016 でします。 
  
-   Microsoft SQL Server 2005、SQL Server 2008、SQL Server 2012、SQL Server 2014 および SQL Server 2016 のすべてのエディション  
  
-   カスタム属性ストア  
  

