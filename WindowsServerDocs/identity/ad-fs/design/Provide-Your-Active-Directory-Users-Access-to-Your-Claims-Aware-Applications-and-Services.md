---
ms.assetid: d254fca3-85a1-424d-ac22-d6687ec3798e
title: Active Directory ユーザーに要求に対応するアプリケーションとサービスへのアクセスを提供する
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 6fb5779eb655534e97c5291c6b883e2e07851415
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87969719"
---
# <a name="provide-your-active-directory-users-access-to-your-claims-aware-applications-and-services"></a>Active Directory ユーザーに要求に対応するアプリケーションとサービスへのアクセスを提供する

Active の Directory フェデレーション サービスのアカウント パートナー組織の管理者であると \(AD FS\) 展開して、1 つを提供する展開の目的をいる\-記号\-に \(SSO\) 人の従業員が会社のネットワークにホストされているリソースへのアクセス。

-   企業ネットワークの Active Directory フォレストにログオンした従業員は、SSO を使用して、管理者の組織内の境界ネットワークの複数のアプリケーションやサービスにアクセスできます。 これらのアプリケーションとサービスは、AD FS によってセキュリティで保護されています。

    Fabrikam が企業ネットワーク上の社員へのフェデレーション Web へのアクセスにするなど、\-ベースのアプリケーションの Fabrikam の境界ネットワークでホストされています。

-   Active Directory ドメインにログオンしたリモート従業員は、組織内のフェデレーションサーバーから AD FS トークンを取得して、 \- 組織内にあるセキュリティで保護され \- た Web ベースのアプリケーションまたはサービス AD FS へのフェデレーションアクセスを得ることができます。

-   Active Directory 属性ストアの情報を、従業員の AD FS トークンに設定できます。

このような展開目標を達成するには、次のコンポーネントが必要です。

-   **Active Directory Domain Services \(AD DS \) :** AD DS には、AD FS トークンの生成に使用される従業員のユーザーアカウントが含まれています。 グループのメンバーシップや属性などの情報は、グループ要求およびカスタム要求として AD FS トークンに設定されます。

    > [!NOTE]
    > ライトウェイトディレクトリアクセスプロトコル \( LDAP \) または構造化照会言語 SQL を使用して \( \) 、AD FS トークン生成用の id を含めることもできます。

-   **会社の DNS:** ドメイン ネーム システムのこの実装 \(DNS\) シンプルなホストを含む \(A\) リソース レコードのイントラネット クライアントは、アカウント フェデレーション サーバーを検出できるようにします。 DNS のこの実装では、企業ネットワークで必要とされる他の DNS レコードもホストされる可能性があります。 詳細については、「[フェデレーション サーバーの名前解決の要件](Name-Resolution-Requirements-for-Federation-Servers.md)」をご覧ください。

-   **アカウント パートナーのフェデレーション サーバー:** このフェデレーション サーバーが、アカウント パートナー フォレスト内のドメインに参加しています。 従業員のユーザー アカウントを認証し、AD FS トークンを生成します。 従業員のクライアント コンピューターは、AD FS トークンを生成するには、このフェデレーション サーバーに対して Windows 統合認証を実行します。 詳細については、「 [Review the Role of the Federation Server in the Account Partner](Review-the-Role-of-the-Federation-Server-in-the-Account-Partner.md)」を参照してください。

    アカウント パートナーのフェデレーション サーバーは、次のユーザーを認証できます。

    -   このドメインにユーザー アカウントを持つ従業員

    -   このフォレスト内のどこかにユーザー アカウントを持つ従業員

    -   このフォレストによって信頼されているフォレスト内の任意の場所にあるユーザーアカウントを持つ従業員 (双 \( \- 方向の Windows 信頼)\)

-   **従業員:** 従業員は、 \- \( \) \- \( 企業ネットワークにログオンしている間、サポートされている web ブラウザーを介して、アプリケーションまたは web ベースのアプリケーションを介して web ベースのサービスにアクセス \) します。 企業ネットワーク上の従業員のクライアント コンピューターは、認証用のフェデレーション サーバーと直接通信します。

リンク先のトピックの情報を確認した後は、「 [Checklist: Implementing a Federated Web SSO Design](../../ad-fs/deployment/Checklist--Implementing-a-Federated-Web-SSO-Design.md)」の手順に従って、この目標のデプロイを開始できます。

次の図は、この AD FS 展開の目的に必要なコンポーネントの各を示します。

![要求へのアクセスします。](media/31394ea8-fecb-4372-ac3f-cc3cf566ffc9.gif)

## <a name="see-also"></a>参照
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
