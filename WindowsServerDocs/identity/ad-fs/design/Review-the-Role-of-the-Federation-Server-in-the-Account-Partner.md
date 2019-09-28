---
ms.assetid: d0ba3c0d-869f-4e24-89d7-499da7576f22
title: アカウント パートナー内のフェデレーション サーバーの役割を確認する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: ead8868f38faa570a0e524630e23d99e276a7c79
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407929"
---
# <a name="review-the-role-of-the-federation-server-in-the-account-partner"></a>アカウント パートナー内のフェデレーション サーバーの役割を確認する

Active Directory フェデレーションサービス (AD FS) \(AD FS @ no__t のフェデレーションサーバーは、セキュリティトークン発行者として機能します。 フェデレーションサーバーは、ローカル属性ストアに存在するアカウント値に基づいて要求を生成し、それらをセキュリティトークンにパッケージ化します。これにより、ユーザーは、シングルサイン @ no__t-3on を使用して、Web @ no__t-0browser @ no__t ベースの @no__t アプリケーションにシームレスにアクセスできるようになります。\(SSO @ no__t-5 @ no__t-6 リソースパートナー組織でホストされています。  
  
> [!NOTE]  
> ユーザーが Web ブラウザーを使用してフェデレーションアプリケーションにアクセスすると、フェデレーションサーバーは、その Web @ no__t-0browser @ no__t ベースのアプリケーションのログオン状態を維持するために、ユーザーに自動的に cookie を発行します。 これらのクッキーには、ユーザーの信頼性情報が含まれます。 Cookie によって SSO 機能が有効になり、ユーザーはリソースパートナーの別の Web @ no__t-0browser @ no__t ベースのアプリケーションにアクセスするたびに資格情報を入力する必要がなくなります。  
  
Web SSO の設計では、境界ネットワークを使用する組織は、インターネットユーザーがアプリケーションにアクセスできるようにするには、境界ネットワークにフェデレーションサーバープロキシをインストールする必要があります。 フェデレーション Web SSO 設計では、アカウントパートナー組織の企業ネットワークに少なくとも1つのフェデレーションサーバーがインストールされ、リソースパートナー組織の企業ネットワークに少なくとも1つのフェデレーションサーバーがインストールされている必要があります。  
  
> [!NOTE]  
> アカウントパートナー組織でフェデレーションサーバーコンピューターをセットアップする前に、まず、そのコンピューターを Active Directory フォレスト内の任意のドメインに参加させる必要があります。このフォレストでフェデレーションサーバーを使用して、そのフォレストからユーザーを認証します。 詳細については、「@no__t」チェックリストを参照してください。フェデレーションサーバー @ no__t をセットアップしています。  
  
## <a name="see-also"></a>関連項目
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
