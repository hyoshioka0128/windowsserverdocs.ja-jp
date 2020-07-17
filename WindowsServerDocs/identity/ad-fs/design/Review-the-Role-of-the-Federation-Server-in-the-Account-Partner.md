---
ms.assetid: d0ba3c0d-869f-4e24-89d7-499da7576f22
title: アカウント パートナー内のフェデレーション サーバーの役割を確認する
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 2d51f0091746d2d5e816108e3b92d0cb1a8267cd
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858535"
---
# <a name="review-the-role-of-the-federation-server-in-the-account-partner"></a>アカウント パートナー内のフェデレーション サーバーの役割を確認する

Active Directory フェデレーションサービス (AD FS) \(のフェデレーションサーバーは、セキュリティトークン発行者として AD FS\) 機能します。 フェデレーションサーバーは、ローカル属性ストアに存在するアカウント値に基づいて要求を生成し、それらをセキュリティトークンにパッケージ化します。これにより、ユーザーは、リソースパートナー組織でホストされている \(SSO\)でシングルサイン\-を使用 \(て、Web\-ブラウザー\-ベースのアプリケーションにシームレスにアクセスできるようになります。\)  
  
> [!NOTE]  
> ユーザーが Web ブラウザーを使用してフェデレーションアプリケーションにアクセスすると、フェデレーションサーバーは、ユーザーに自動的に cookie を発行して、その Web\-ブラウザー\-ベースのアプリケーションのログオン状態を維持します。 これらのクッキーには、ユーザーの信頼性情報が含まれます。 Cookie によって SSO 機能が有効になり、ユーザーはリソースパートナー内のさまざまな Web\-ブラウザー\-ベースのアプリケーションにアクセスするたびに資格情報を入力する必要がなくなります。  
  
Web SSO の設計では、境界ネットワークを使用する組織は、インターネットユーザーがアプリケーションにアクセスできるようにするには、境界ネットワークにフェデレーションサーバープロキシをインストールする必要があります。 フェデレーション Web SSO 設計では、アカウントパートナー組織の企業ネットワークに少なくとも1つのフェデレーションサーバーがインストールされ、リソースパートナー組織の企業ネットワークに少なくとも1つのフェデレーションサーバーがインストールされている必要があります。  
  
> [!NOTE]  
> アカウントパートナー組織でフェデレーションサーバーコンピューターをセットアップする前に、まず、そのコンピューターを Active Directory フォレスト内の任意のドメインに参加させる必要があります。このフォレストでフェデレーションサーバーを使用して、そのフォレストからユーザーを認証します。 詳細については、「 [Checklist: Setting Up a Federation Server](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md)」を参照してください。  
  
## <a name="see-also"></a>参照
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
