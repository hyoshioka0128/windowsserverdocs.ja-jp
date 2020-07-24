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
ms.openlocfilehash: 10cd66a3346c6312474fa1a96b41b53c49a0f36d
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86961194"
---
# <a name="the-role-of-attribute-stores"></a>属性ストアの役割
Active Directory フェデレーションサービス (AD FS) では、"属性ストア" という用語を使用して、ユーザーアカウントとそれらに関連付けられている属性値を格納するために組織が使用するディレクトリまたはデータベースを参照します。 Id プロバイダー組織で構成された後、AD FS は、これらの属性値をストアから取得し、その情報に基づいて要求を作成します。これにより、証明書利用者組織でホストされている Web アプリケーションまたはサービスが、 \( id プロバイダー組織に格納されているユーザーが \) アプリケーションまたはサービスにアクセスしようとしたときに、その  
  
信頼性情報を生成する方法の詳細については、「 [The Role of Claims](The-Role-of-Claims.md)」を参照してください。  
  
## <a name="how-attribute-stores-fit-in-with-your-ad-fs-deployment-goals"></a>AD FS の展開目標に属性ストアを適合させる方法  
ユーザー属性ストアの場所と、ユーザーの認証元の場所によって、ユーザー id をサポートするための AD FS の設計方法が決まります。 属性ストアの場所と、ユーザーがイントラネットまたはインターネットでアプリケーションにアクセスする場所に応じて、 \( \) 次のいずれかの展開目標を使用できます。  
  
-   [Active Directory ユーザーが要求に対応するアプリケーションとサービスにアクセスできるよう](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807071(v=ws.11))にします。この目的では、組織内のユーザーは、 \( \) 企業イントラネット内の Active Directory にログオンしたときに、AD FS で保護されたアプリケーションまたはサービス、またはパートナーのアプリケーションやサービスのいずれかにアクセスできます。  
  
-   [Active Directory ユーザーが他の組織のアプリケーションやサービスにアクセスできるようにする](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807123(v=ws.11))-この目的では、組織のユーザーは、 \( \) 企業イントラネットの属性ストアにログオンしているときと、ユーザーがインターネットからリモートでログオンしたときに、AD FS で保護されたアプリケーションまたはサービスにアクセスするか、パートナーのアプリケーションやサービスにアクセスします。  
  
-   [別の組織のユーザーに、要求に対応するアプリケーションとサービスへのアクセスを提供](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807099(v=ws.11))する—この目的では、組織の企業イントラネット上の属性ストアに配置されている別の組織のユーザーアカウントが、組織内の AD FS で保護されたアプリケーションにアクセスする必要があります。 この目標は、組織 \- の境界ネットワーク内の属性ストアに格納されているコンシューマーベースのユーザーアカウントに、組織内の AD FS で保護されたアプリケーションへのアクセスを提供する必要がある場合にも使用できます。  
  
属性ストアの配置と組織のその他の要件によっては、これらの展開目標のいくつかを組み合わせて、AD FS 展開の設計を完了することができます。  
  
## <a name="attribute-stores-that-are-supported-by-ad-fs"></a>AD FS でサポートされている属性ストア  
AD FS では、管理者が定義した \- 属性値を抽出し、それらの値を使用して要求を設定するために使用できる、さまざまなディレクトリおよびデータベースストアがサポートされています。 AD FS は、次のいずれかのディレクトリまたはデータベースを属性ストアとしてサポートしています。  
  
-   Windows server 2003 の Active Directory は、windows server 2008 の Active Directory Domain Services \( AD DS、 \) windows server 2012 および 2012 R2 での AD DS、および windows server 2016 です。 
  
-   Microsoft SQL Server 2005、SQL Server 2008、SQL Server 2012、SQL Server 2014、および SQL Server 2016 のすべてのエディション  
  
-   カスタム属性ストア  
  
