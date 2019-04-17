---
ms.assetid: d254fca3-85a1-424d-ac22-d6687ec3798e
title: "Active Directory ユーザー アクセスを提供する、クレーム対応アプリケーションとサービス"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f6fb37c16c20915c0051e3a24cdb0c147ae92d9c
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="provide-your-active-directory-users-access-to-your-claims-aware-applications-and-services"></a>Active Directory ユーザー アクセスを提供する、クレーム対応アプリケーションとサービス

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

管理者は、Active Directory フェデレーション サービス \(AD FS\) 展開は、アカウント パートナー組織と従業員が企業ネットワークにホストされているリソースへのシングル sign\-に対する \(SSO\) アクセスを提供する展開の目的をいます。  
  
-   企業ネットワーク内の Active Directory フォレストにログオンしている従業員は、SSO を使用して、複数のアプリケーションやサービス、自分の組織で境界ネットワークにアクセスします。 これらのアプリケーションとサービスは、AD FS によって保護されます。  
  
    たとえば、Fabrikam が企業ネットワークの社員へのフェデレーション Fabrikam の境界ネットワークでホストされている Web ベース アプリケーションへのアクセスをします。  
  
-   Active Directory ドメインにログオンしたリモート従業員は、AD FS\ で保護された Web ベース アプリケーションまたはも、組織内に存在するサービスへのフェデレーション アクセスのために、組織内のフェデレーション サーバーから AD FS トークンを取得できます。  
  
-   Active Directory 属性ストア内の情報は、従業員の AD FS トークンに設定できます。  
  
次のコンポーネントは、この展開の目的必要があります。  
  
-   **Active Directory Domain Services \(AD DS\):** AD DS には、AD FS トークンの生成に使用される従業員のユーザー アカウントが含まれています。 グループのメンバーシップや属性などの情報は、グループ要求およびカスタム要求として AD FS トークンに設定されます。  
  
    > [!NOTE]  
    > また、AD FS トークンの生成の ID を格納するため Lightweight Directory Access Protocol \(LDAP\) または構造化照会言語 \(SQL\) を使用することができます。  
  
-   **企業 DNS:**イントラネット クライアントは、アカウント フェデレーション サーバーを見つけられるようにドメイン ネーム システム \(DNS\) のこの実装には、単純なホスト \(A\) リソース レコードが含まれます。 DNS のこの実装では、企業ネットワークに必要なその他の DNS レコードもホスト可能性があります。 詳細については、次を参照してください。[フェデレーション サーバーの名前解決要件](Name-Resolution-Requirements-for-Federation-Servers.md)します。  
  
-   **アカウント パートナーのフェデレーション サーバー:**このフェデレーション サーバーが、アカウント パートナー フォレスト内のドメインに参加しています。 これにより、従業員のユーザー アカウントを認証し、AD FS トークンを生成します。 従業員のクライアント コンピューターは、AD FS トークンを生成するには、このフェデレーション サーバーに対して統合 Windows 認証を実行します。 詳細については、次を参照してください。[アカウント パートナーのフェデレーション サーバーの役割を確認する](Review-the-Role-of-the-Federation-Server-in-the-Account-Partner.md)します。  
  
    アカウント パートナーのフェデレーション サーバーは、次のユーザーを認証できます。  
  
    -   このドメイン内のユーザー アカウントを持つ従業員  
  
    -   このフォレストの任意の場所でユーザー アカウントを持つ従業員  
  
    -   Anywhere いるフォレスト内のユーザー アカウントを持つ従業員がこのフォレストによって信頼されている \ (を通じて two\ 方向の Windows trust\)  
  
-   **従業員:**従業員が Web ベース サービスにアクセス \(through an application\) または Web ベース アプリケーション \ (サポートされている Web browser\) を通じてそのユーザーがログオン中に、企業ネットワークにします。 企業ネットワーク上の従業員のクライアント コンピューターは、認証用のフェデレーション サーバーと直接通信します。  
  
後のリンク先のトピックの情報を確認するには、次の手順に従って、この目標のデプロイを開始できます[チェックリスト: Implementing a Federated Web SSO Design](../../ad-fs/deployment/Checklist--Implementing-a-Federated-Web-SSO-Design.md)します。  
  
次の図は、この AD FS 展開目標に必要なコンポーネントの各を示します。  
  
![要求へのアクセスします。](media/31394ea8-fecb-4372-ac3f-cc3cf566ffc9.gif)  
  
## <a name="see-also"></a>参照してください。
[Windows Server 2012 で AD FS 設計ガイドします。](AD-FS-Design-Guide-in-Windows-Server-2012.md)
