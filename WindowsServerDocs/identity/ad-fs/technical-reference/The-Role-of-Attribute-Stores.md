---
ms.assetid: 4ddb927d-d65e-491d-840a-16049c083d13
title: 属性ストアの役割
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 595f0b3b11172df9bf95d3bb8aab90368bb0e77f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80860195"
---
# <a name="the-role-of-attribute-stores"></a>属性ストアの役割
Active Directory フェデレーションサービス (AD FS) では、"属性ストア" という用語を使用して、ユーザーアカウントとそれらに関連付けられている属性値を格納するために組織が使用するディレクトリまたはデータベースを参照します。 Id プロバイダー組織で構成された後、AD FS は、これらの属性値をストアから取得し、その情報に基づいて要求を作成します。これにより、証明書利用者組織でホストされている Web アプリケーションまたはサービスが、id プロバイダー\) 組織に格納されているユーザー \(、アプリケーションまたはサービスへのアクセスが試行されます。  
  
信頼性情報を生成する方法の詳細については、「 [The Role of Claims](The-Role-of-Claims.md)」を参照してください。  
  
## <a name="how-attribute-stores-fit-in-with-your-ad-fs-deployment-goals"></a>AD FS の展開目標に属性ストアを適合させる方法  
ユーザー属性ストアの場所と、ユーザーの認証元の場所によって、ユーザー id をサポートするための AD FS の設計方法が決まります。 属性ストアが配置されている場所と、ユーザーがイントラネットまたはインターネット\)のアプリケーション \(にアクセスする場所に応じて、次のいずれかの展開目標を使用できます。  
  
-   [Active Directory ユーザーに要求に対応するアプリケーションとサービスへのアクセスを提供する](https://technet.microsoft.com/library/dd807071.aspx)—この目的では、組織内のユーザーは、企業イントラネットの Active Directory にログオンしているときに、独自のアプリケーションまたはサービス、パートナーのアプリケーションまたは\) サービスのいずれか \(AD FS セキュリティで保護されたアプリケーションまたはサービスにアクセスします。  
  
-   [Active Directory ユーザーが他の組織のアプリケーションやサービスにアクセスできるようにする](https://technet.microsoft.com/library/dd807123.aspx)-この目的では、組織のユーザーは、企業イントラネットの属性ストアにログオンしているときと、ユーザーがインターネットからリモートでログオンしたときに、独自のアプリケーションまたはサービス、パートナーのアプリケーションまたはサービス\) \(AD FS セキュリティで保護されたアプリケーションまたはサービスにアクセス  
  
-   [別の組織のユーザーに、要求に対応するアプリケーションとサービスへのアクセスを提供](https://technet.microsoft.com/library/dd807099.aspx)する—この目的では、組織の企業イントラネット上の属性ストアに配置されている別の組織のユーザーアカウントが、組織内の AD FS で保護されたアプリケーションにアクセスする必要があります。 この目標は、組織の境界ネットワーク内の属性ストアに配置されているコンシューマー\-ベースのユーザーアカウントに、組織内の AD FS で保護されたアプリケーションへのアクセスを提供する必要がある場合にも使用できます。  
  
属性ストアの配置と組織のその他の要件によっては、これらの展開目標のいくつかを組み合わせて、AD FS 展開の設計を完了することができます。  
  
## <a name="attribute-stores-that-are-supported-by-ad-fs"></a>AD FS でサポートされている属性ストア  
AD FS は、管理者\-定義された属性値を抽出し、それらの値を使用して要求を設定するために使用できる、さまざまなディレクトリおよびデータベースストアをサポートしています。 AD FS は、次のいずれかのディレクトリまたはデータベースを属性ストアとしてサポートしています。  
  
-   Windows server 2003 で Active Directory、windows server 2008 では AD DS\)、windows Server 2012 および 2012 R2 では AD DS、Windows Server 2016 では Active Directory Domain Services \(ます。 
  
-   Microsoft SQL Server 2005、SQL Server 2008、SQL Server 2012、SQL Server 2014、および SQL Server 2016 のすべてのエディション  
  
-   カスタム属性ストア  
  

