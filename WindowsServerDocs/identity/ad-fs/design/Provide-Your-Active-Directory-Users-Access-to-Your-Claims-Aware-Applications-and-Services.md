---
ms.assetid: d254fca3-85a1-424d-ac22-d6687ec3798e
title: Active Directory ユーザーに要求に対応するアプリケーションとサービスへのアクセスを提供する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f6fb37c16c20915c0051e3a24cdb0c147ae92d9c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835873"
---
# <a name="provide-your-active-directory-users-access-to-your-claims-aware-applications-and-services"></a>Active Directory ユーザーに要求に対応するアプリケーションとサービスへのアクセスを提供する

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

Active の Directory フェデレーション サービスのアカウント パートナー組織の管理者が\(AD FS\)展開して、1 つを提供する展開の目的をいる\-サインオン\-で\(SSO\)人の従業員が企業ネットワークにホストされているリソースにアクセスします。  
  
-   企業ネットワークの Active Directory フォレストにログオンした従業員は、SSO を使用して、管理者の組織内の境界ネットワークの複数のアプリケーションやサービスにアクセスできます。 これらのアプリケーションとサービスは、AD FS によってセキュリティで保護されています。  
  
    Fabrikam が企業ネットワーク上の社員へのフェデレーション Web へのアクセスにするなど、\-ベースのアプリケーションの Fabrikam の境界ネットワークでホストされています。  
  
-   AD FS にフェデレーション アクセスのために、組織内のフェデレーション サーバーから AD FS トークンを取得できますが、Active Directory ドメインにログオンしたリモート従業員は\-Web をセキュリティで保護された\-ベースのアプリケーションまたはサービスにも存在します。お客様の組織。  
  
-   Active Directory 属性ストアの情報を、従業員の AD FS トークンに設定できます。  
  
このような展開目標を達成するには、次のコンポーネントが必要です。  
  
-   **Active Directory Domain Services \(AD DS\):** AD DS には、AD FS トークンの生成に使用される従業員のユーザー アカウントが含まれます。 グループのメンバーシップや属性などの情報は、グループ要求およびカスタム要求として AD FS トークンに設定されます。  
  
    > [!NOTE]  
    > ライトウェイト ディレクトリ アクセス プロトコルを使用することもできます。 \(LDAP\)または構造化照会言語\(SQL\)を格納するには、AD FS トークンを生成します。  
  
-   **企業 DNS:** ドメイン ネーム システムのこの実装\(DNS\)単純なホストを含む\(A\)リソース レコードのイントラネット クライアントは、アカウント フェデレーション サーバーを特定できるようにします。 DNS のこの実装では、企業ネットワークで必要とされる他の DNS レコードもホストされる可能性があります。 詳細については、「[フェデレーション サーバーの名前解決の要件](Name-Resolution-Requirements-for-Federation-Servers.md)」をご覧ください。  
  
-   **アカウント パートナーのフェデレーション サーバー:** このフェデレーション サーバーは、アカウント パートナー フォレスト内のドメインに参加しています。 従業員のユーザー アカウントを認証し、AD FS トークンを生成します。 従業員のクライアント コンピューターでは、AD FS トークンを生成するには、このフェデレーション サーバーに対して Windows 統合認証を実行します。 詳細については、次を参照してください。 [アカウント パートナーのフェデレーション サーバーの役割を検討](Review-the-Role-of-the-Federation-Server-in-the-Account-Partner.md)します。  
  
    アカウント パートナーのフェデレーション サーバーは、次のユーザーを認証できます。  
  
    -   このドメインにユーザー アカウントを持つ従業員  
  
    -   このフォレスト内のどこかにユーザー アカウントを持つ従業員  
  
    -   任意の場所にフォレストのユーザー アカウントを持つ従業員がこのフォレストによって信頼されている\(2 を通じて\-Windows 信頼の方法\)  
  
-   **従業員:** 従業員が Web にアクセスする\-ベースのサービス\(アプリケーションを通じて\)または Web\-ベースのアプリケーション\(サポートされている Web ブラウザーを介して\)中に、そのユーザーがログオンして、企業のネットワーク。 企業ネットワーク上の従業員のクライアント コンピューターは、認証用のフェデレーション サーバーと直接通信します。  
  
リンク先のトピックの情報を確認した後には、次の手順に従って、この目標の展開を開始できます[チェックリスト。フェデレーション Web SSO 設計を実装する](../../ad-fs/deployment/Checklist--Implementing-a-Federated-Web-SSO-Design.md)します。  
  
次の図は、この AD FS 展開の目的に必要なコンポーネントの各を示します。  
  
![要求へのアクセスします。](media/31394ea8-fecb-4372-ac3f-cc3cf566ffc9.gif)  
  
## <a name="see-also"></a>関連項目
[Windows Server 2012 で AD FS 設計ガイドします。](AD-FS-Design-Guide-in-Windows-Server-2012.md)
