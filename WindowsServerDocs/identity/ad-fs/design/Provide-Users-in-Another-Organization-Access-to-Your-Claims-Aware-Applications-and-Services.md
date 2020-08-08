---
ms.assetid: de7e1e4a-f96d-4b59-ac9b-f65f5d37a96f
title: 信頼性情報に対応したアプリケーションやサービスへのアクセスを別の組織のユーザーに提供する
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 03b9e4142d522ce8a455bb9cb18dbae48a89f302
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87969739"
---
# <a name="provide-users-in-another-organization-access-to-your-claims-aware-applications-and-services"></a>信頼性情報に対応したアプリケーションやサービスへのアクセスを別の組織のユーザーに提供する


Active Directory フェデレーション サービスでリソース パートナー組織の管理者であると \(AD FS\) 別の組織のユーザーのフェデレーション アクセスを提供する展開の目的を使用して \(アカウント パートナー組織\) を請求情報に\-対応のアプリケーションまたは Web\-ベースの組織に配置されているサービス \(リソース パートナー組織\):

-   ユーザーの組織への信頼の組織と組織のフェデレーションを構成、ユーザーの両方をフェデレーション \(アカウント パートナー組織\) AD FS がアプリケーションや、組織でホストされているサービスをセキュリティ保護にアクセスできます。 詳細については、次を参照してください。 [フェデレーション Web SSO デザイン](Federated-Web-SSO-Design.md)します。

    たとえば、Fabrikam が、Contoso でホストされている Web サービスへのフェデレーション アクセスを、企業ネットワークの従業員に提供するような場合です。

-   フェデレーションの信頼された組織との直接の関連付けを持たないユーザー \(などの個人顧客\), 、複数の AD FS にアクセスできる、境界ネットワークでホストされている属性ストアにログオンしている\-、インターネット上にあるクライアント コンピューターから 1 回のログオンで、境界ネットワークでホストされているアプリケーションをセキュリティで保護します。 つまり、あなたが顧客アカウントをホストして、境界ネットワークへのアクセスを有効にした場合、属性ストアでホストされた顧客は 1 回ログオンするだけで、境界ネットワーク内の 1 つ以上のアプリケーションやサービスにアクセスできるようになります。 詳細については、次を参照してください。 [Web SSO デザイン](Web-SSO-Design.md)します。

    たとえば、Fabrikam たいお客様は、1 つ\-記号\-に \(SSO\) 複数のアプリケーションまたはその境界ネットワークでホストされるサービスにアクセスします。

このような展開目標を達成するには、次のコンポーネントが必要です。

-   **Active Directory ドメイン サービス \(AD DS\):** リソース パートナーのフェデレーション サーバーは、Active Directory ドメインに参加する必要があります。

-   **境界の DNS:** ドメイン ネーム システム \(DNS\) シンプルなホストを含める必要があります \(A\) リソース レコードのクライアント コンピューターは、リソース パートナーのフェデレーション サーバーと Web サーバーを検出できるようにします。 DNS サーバーでは、境界ネットワークにも必要なその他の DNS レコードがホストされる場合があります。 詳細については、「[フェデレーション サーバーの名前解決の要件](Name-Resolution-Requirements-for-Federation-Servers.md)」をご覧ください。

-   **リソース パートナーのフェデレーション サーバー:** リソース パートナーのフェデレーション サーバーは、アカウント パートナーに送信される AD FS トークンを検証します。 アカウント パートナーの検出は、このフェデレーション サーバーによって行われます。 詳細については、次を参照してください。 [リソース パートナーのフェデレーション サーバーの役割を検討](Review-the-Role-of-the-Federation-Server-in-the-Resource-Partner.md)します。

-   **Web サーバー:** Web サーバーは、Web アプリケーションと Web サービスのいずれかをホストできます。 Web サーバーは、保護された Web アプリケーションや Web サービスへのアクセスを許可する前に、フェデレーション ユーザーから有効な AD FS トークンを受信したかどうかを確認します。

    Windows Identity Foundation を使用して、 \(WIF\), Web アプリケーションを開発する、またはその it を受け入れるようにサービスがユーザー名とパスワードなどの任意の標準のログオン メソッドを使用して作成されるユーザー ログオン要求をフェデレーションします。

リンク先のトピックの情報を確認して、次の手順に従って、この目標の展開を開始できます [チェックリスト: フェデレーション Web SSO 設計の実装](../../ad-fs/deployment/Checklist--Implementing-a-Federated-Web-SSO-Design.md) と [チェックリスト: Web SSO 設計の実装](../../ad-fs/deployment/Checklist--Implementing-a-Web-SSO-Design.md)します。

次の図は、この AD FS 展開の目的に必要なコンポーネントの各を示します。

![要求へのアクセスします。](media/75358b16-2a6f-4e16-9cc4-b0e614480305.gif)

## <a name="see-also"></a>参照
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
