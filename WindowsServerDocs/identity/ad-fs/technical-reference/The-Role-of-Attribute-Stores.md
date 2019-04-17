---
ms.assetid: 4ddb927d-d65e-491d-840a-16049c083d13
title: "属性ストアのロール"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 730411ed7efbb9cf0db3d7e94a486cec4c363849
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
 >適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

# <a name="the-role-of-attribute-stores"></a>属性ストアのロール
Active Directory フェデレーション サービスは、「属性ストア」という用語を使用するディレクトリやデータベースの組織を使用してそのユーザー アカウントとその関連付けられた属性値を格納することを参照してください。 Id プロバイダー組織で構成されている AD FS、ストアからこれらの属性値を取得され、Web アプリケーションまたはサービス証明書利用者のパーティ組織でホストされているできるように、適切な承認決定されるたびにフェデレーション ユーザーは、その情報に基づいて信頼性情報が作成 \ (の ID プロバイダー organization\ でアカウントを持つが格納されているユーザー) は、アプリケーションまたはサービスにアクセスしようとしています。  
  
信頼性情報を生成する方法の詳細については、次を参照してください。[The Role of Claims](The-Role-of-Claims.md)します。  
  
## <a name="how-attribute-stores-fit-in-with-your-ad-fs-deployment-goals"></a>AD FS 展開目標を適合属性を格納する方法  
ユーザーの属性ストアの場所とユーザーを認証する元の場所は、ユーザーの ID をサポートするために AD FS を設計する方法を決定します。 属性ストアがあると、ユーザーがアプリケーションにアクセスする場所に応じて \ ([イントラネットまたはとは限らない)、展開の目標を次のいずれかを使用できます。  
  
-   [Your Claims-aware Applications and Services に Your Active Directory ユーザーのアクセスを提供](https://technet.microsoft.com/library/dd807071.aspx)— この目標を組織内のユーザーのアクセスの AD FS で保護されたアプリケーションまたはサービス \ (独自アプリケーションまたはサービスまたはパートナーのアプリケーションまたは service \current) ログオンする際、ユーザーは Active Directory に、企業イントラネット内です。  
  
-   [アプリケーションやサービスの他の組織に Your Active Directory ユーザーのアクセスを提供](https://technet.microsoft.com/library/dd807123.aspx)-AD FS で保護されたアプリケーションまたはサービスに、組織内のユーザーがアクセスこの目標を \ (独自アプリケーションまたはサービスまたはパートナーのアプリケーションまたは service \current) 場合、ユーザーがログオンとリモートのインターネットからログオンしたときに、企業イントラネット内の属性ストアにします。  
  
-   [Your Claims-aware Applications and Services をユーザーに他の組織がアクセスを提供する](https://technet.microsoft.com/library/dd807099.aspx)— この目標をその組織の企業イントラネット上の属性ストアに格納されている別の組織でユーザー アカウントは、AD FS で保護されたアプリケーションにアクセスする必要があります。 この目標は、AD FS で保護されたのアプリケーション、組織内にアクセス権を持つ組織の境界ネットワーク内の属性ストアに格納されている consumer\ ベースのユーザー アカウントを提供する必要があるときにも機能します。  
  
属性ストアの場所と、組織の他の要件に応じて、AD FS 展開の設計を完了するには、これらの展開目標のいくつかを組み合わせることができます。  
  
## <a name="attribute-stores-that-are-supported-by-ad-fs"></a>AD FS でサポートされている属性ストア  
AD FS で、さまざまなディレクトリをサポートし、administrator\ 定義属性の値を抽出し、それらの値を持つ信頼性情報を設定するを使用するデータベースに格納します。 AD FS では、属性ストアとして次のディレクトリやデータベースのいずれかをサポートします。  
  
-   Windows Server 2003 の active Directory は、Active Directory ドメイン サービスの Windows Server 2008、Windows Server 2012 および 2012 R2 での AD DS と Windows Server 2016 で \(AD DS\) します。 
  
-   Microsoft SQL Server 2005、SQL Server 2008、SQL Server 2012、SQL Server 2014、および SQL Server 2016 のすべてのエディション  
  
-   カスタム属性ストア  
  

