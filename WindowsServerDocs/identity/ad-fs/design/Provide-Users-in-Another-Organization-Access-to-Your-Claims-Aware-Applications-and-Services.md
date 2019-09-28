---
ms.assetid: de7e1e4a-f96d-4b59-ac9b-f65f5d37a96f
title: 要求に対応するアプリケーションやサービスへのアクセスを別の組織のユーザーに提供する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: a0b2429599036f2893f23df7921a11c8232d9f67
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359070"
---
# <a name="provide-users-in-another-organization-access-to-your-claims-aware-applications-and-services"></a>要求に対応するアプリケーションやサービスへのアクセスを別の組織のユーザーに提供する


Active Directory フェデレーションサービス (AD FS) @no__t のリソースパートナー組織の管理者である場合に、別の @no__t 組織のユーザーにフェデレーションアクセスを提供するための展開目標がある場合は、アカウントパートナー組織 @ no__t-3 を要求 @ no__t-4aware アプリケーション、または組織内にある Web @ no__t ベースのサービスに、リソースパートナー組織 @ no__t-7 を @no__t します。  
  
-   組織内のフェデレーションユーザーと組織のフェデレーション信頼を構成している組織 \(account パートナー組織 @ no__t は、組織でホストされている AD FS セキュリティで保護されたアプリケーションまたはサービスにアクセスできます。 詳細については、次を参照してください。 [フェデレーション Web SSO デザイン](Federated-Web-SSO-Design.md)します。  
  
    たとえば、Fabrikam が、Contoso でホストされている Web サービスへのフェデレーション アクセスを、企業ネットワークの従業員に提供するような場合です。  
  
-   信頼された組織に直接関連付けられていないフェデレーションユーザー @no__t。たとえば、境界ネットワークでホストされている属性ストアにログオンしている個々の顧客 @ no__t-1 は、複数の AD FS @ no__t-2secured で保護されたアプリケーションにアクセスできます。また、インターネット上にあるクライアントコンピューターから1回ログオンすることで、境界ネットワークでホストされています。 つまり、あなたが顧客アカウントをホストして、境界ネットワークへのアクセスを有効にした場合、属性ストアでホストされた顧客は 1 回ログオンするだけで、境界ネットワーク内の 1 つ以上のアプリケーションやサービスにアクセスできるようになります。 詳細については、次を参照してください。 [Web SSO デザイン](Web-SSO-Design.md)します。  
  
    たとえば、Fabrikam たいお客様は、1 つ\-記号\-に \(SSO\) 複数のアプリケーションまたはその境界ネットワークでホストされるサービスにアクセスします。  
  
このような展開目標を達成するには、次のコンポーネントが必要です。  
  
-   **Active Directory Domain Services \( AD DS @ no__t:** リソースパートナーのフェデレーションサーバーは、Active Directory ドメインに参加している必要があります。  
  
-   **境界 DNS:** ドメインネームシステム \(DNS @ no__t には、クライアントコンピューターがリソースパートナーのフェデレーションサーバーと Web サーバーを特定できるように、単純なホスト \(A @ no__t リソースレコードが含まれている必要があります。 DNS サーバーでは、境界ネットワークにも必要なその他の DNS レコードがホストされる場合があります。 詳細については、「[フェデレーション サーバーの名前解決の要件](Name-Resolution-Requirements-for-Federation-Servers.md)」をご覧ください。  
  
-   **リソースパートナーのフェデレーションサーバー:** リソースパートナーフェデレーションサーバーは、アカウントパートナーが送信する AD FS トークンを検証します。 アカウント パートナーの検出は、このフェデレーション サーバーによって行われます。 詳細については、次を参照してください。 [アカウント パートナーのフェデレーション サーバーの役割を検討](Review-the-Role-of-the-Federation-Server-in-the-Resource-Partner.md)します。  
  
-   **Web サーバー:** Web サーバーは、Web アプリケーションか Web サービスのいずれかをホストできます。 Web サーバーは、保護された Web アプリケーションや Web サービスへのアクセスを許可する前に、フェデレーション ユーザーから有効な AD FS トークンを受信したかどうかを確認します。  
  
    Windows Identity Foundation を使用して、 \(WIF\), Web アプリケーションを開発する、またはその it を受け入れるようにサービスがユーザー名とパスワードなどの任意の標準のログオン メソッドを使用して作成されるユーザー ログオン要求をフェデレーションします。  
  
リンク先のトピックの情報を確認した後、@no__t のチェックリストの手順に従って、この目標の展開を開始できます。フェデレーション Web SSO 設計の実装 @ no__t-0 と @no__t チェックリスト:Web SSO デザイン @ no__t を実装します。  
  
次の図は、この AD FS 展開の目的に必要なコンポーネントの各を示します。  
  
![要求へのアクセスします。](media/75358b16-2a6f-4e16-9cc4-b0e614480305.gif)  
  
## <a name="see-also"></a>関連項目
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
