---
ms.assetid: 4ddb927d-d65e-491d-840a-16049c083d13
title: 属性ストアの役割
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 0a1543f2c935c2ef76ea014567b18bfc778c7401
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407384"
---
# <a name="the-role-of-attribute-stores"></a>属性ストアの役割
Active Directory フェデレーションサービス (AD FS) では、"属性ストア" という用語を使用して、ユーザーアカウントとそれらに関連付けられている属性値を格納するために組織が使用するディレクトリまたはデータベースを参照します。 Id プロバイダーの組織で構成された後、AD FS は、これらの属性値をストアから取得し、その情報に基づいて要求を作成します。これにより、証明書利用者組織でホストされている Web アプリケーションまたはサービスが適切にアクセスできるようになります。id プロバイダー組織\)にアカウントが\(格納されているユーザーがフェデレーションユーザーによってアプリケーションまたはサービスにアクセスしようとするたびに、承認の決定。  
  
信頼性情報を生成する方法の詳細については、「 [The Role of Claims](The-Role-of-Claims.md)」を参照してください。  
  
## <a name="how-attribute-stores-fit-in-with-your-ad-fs-deployment-goals"></a>AD FS の展開目標に属性ストアを適合させる方法  
ユーザー属性ストアの場所と、ユーザーの認証元の場所によって、ユーザー id をサポートするための AD FS の設計方法が決まります。 属性ストアの場所と、ユーザーがイントラネットまたはインターネット\(\)でアプリケーションにアクセスする場所に応じて、次のいずれかの展開目標を使用できます。  
  
-   [Active Directory ユーザーが要求に対応するアプリケーションとサービスにアクセスできるよう](https://technet.microsoft.com/library/dd807071.aspx)にします。この目的では、組織内のユーザーは、AD FS \(で保護されたアプリケーションまたはサービスにアクセスし、独自のアプリケーションやサービス、またはパートナーのユーザーが企業\)イントラネットの Active Directory にログオンしているときのアプリケーションまたはサービス。  
  
-   [Active Directory ユーザーが他の組織のアプリケーションやサービスにアクセスできるようにする](https://technet.microsoft.com/library/dd807123.aspx)-この目的では、組織のユーザーは、AD FS で保護\(されたアプリケーションまたはサービスにアクセスして、独自のアプリケーションやサービスにアクセスするか、ユーザーが企業イントラネット内\)の属性ストアにログオンしている場合や、インターネットからリモートでログオンした場合のパートナーのアプリケーションまたはサービス。  
  
-   [別の組織のユーザーに、要求に対応するアプリケーションとサービスへのアクセスを提供](https://technet.microsoft.com/library/dd807099.aspx)する—この目的では、その組織の企業イントラネット上の属性ストアに配置されている別の組織内のユーザーアカウントは、AD FS にアクセスする必要があります。組織内のセキュリティで保護されたアプリケーション。 この目標は、組織の\-境界ネットワーク内の属性ストアに格納されているコンシューマーベースのユーザーアカウントに、組織内の AD FS で保護されたアプリケーションへのアクセスを提供する必要がある場合にも使用できます。  
  
属性ストアの配置と組織のその他の要件によっては、これらの展開目標のいくつかを組み合わせて、AD FS 展開の設計を完了することができます。  
  
## <a name="attribute-stores-that-are-supported-by-ad-fs"></a>AD FS でサポートされている属性ストア  
AD FS では、管理者\-が定義した属性値を抽出し、それらの値を使用して要求を設定するために使用できる、さまざまなディレクトリおよびデータベースストアがサポートされています。 AD FS は、次のいずれかのディレクトリまたはデータベースを属性ストアとしてサポートしています。  
  
-   Windows server 2003 の Active Directory は、 \(windows\) server 2008 の Active Directory Domain Services AD DS、windows server 2012 および 2012 R2 での AD DS、および windows server 2016 です。 
  
-   Microsoft SQL Server 2005、SQL Server 2008、SQL Server 2012、SQL Server 2014、および SQL Server 2016 のすべてのエディション  
  
-   カスタム属性ストア  
  

