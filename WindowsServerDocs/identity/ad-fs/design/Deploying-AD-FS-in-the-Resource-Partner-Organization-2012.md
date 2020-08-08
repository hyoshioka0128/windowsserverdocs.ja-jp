---
ms.assetid: 39acccd9-0402-49ca-8ce1-b239e1e7e455
title: リソース パートナー組織での AD FS のデプロイ
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: ae43da6a8aa2968cc5123c9bc707c44c77fa6ea2
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87942917"
---
# <a name="deploying-ad-fs-in-the-resource-partner-organization"></a>リソース パートナー組織での AD FS のデプロイ

Active Directory フェデレーションサービス (AD FS) AD FS のリソースパートナー組織は、 \( \) Web サーバーがリソース側のフェデレーションサーバーによって保護されている可能性のある組織を表し \- ます。 リソースパートナーのフェデレーションサーバーは、アカウントパートナーによって生成されたセキュリティトークンを使用して、リソースパートナーに配置されている Web サーバーに要求を提供します。

フェデレーションサービスまたはアプリケーションへのアクセスを多数のユーザーに提供する必要があるシナリオでは、一部のユーザーが異なる組織に存在する場合、複数のアカウントパートナーをデプロイできるように、リソースフェデレーションサーバーを構成できます。

リソース パートナー組織のセットアップ方法と構成方法の詳細については、「 [Checklist: Configuring the Resource Partner Organization](../../ad-fs/deployment/Checklist--Configuring-the-Resource-Partner-Organization.md)」を参照してください。

## <a name="in-this-section"></a>このセクションの内容

-   [リソース パートナー内のフェデレーション サーバーの役割を確認する](Review-the-Role-of-the-Federation-Server-in-the-Resource-Partner.md)

-   [リソース パートナー内のフェデレーション サーバー プロキシの役割を確認する](Review-the-Role-of-the-Federation-Server-Proxy-in-the-Resource-Partner.md)

-   [リソース パートナーでのフェデレーション アプリケーション戦略を決定する](Determine-Your-Federated-Application-Strategy-in-the-Resource-Partner.md)


## <a name="see-also"></a>参照
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
