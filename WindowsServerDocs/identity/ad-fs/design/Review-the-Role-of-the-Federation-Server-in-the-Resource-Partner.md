---
ms.assetid: f88238ea-d851-4129-8b4e-a3a62b813614
title: リソース パートナー内のフェデレーション サーバーの役割を確認する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: fd9f20eb7559f5862ee50bdd8364fa1604d3c1b6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358967"
---
# <a name="review-the-role-of-the-federation-server-in-the-resource-partner"></a>リソース パートナー内のフェデレーション サーバーの役割を確認する

リソースパートナー組織のフェデレーションサーバーは、アカウントフェデレーションサーバーによって送信された受信セキュリティトークンをインターセプトし、検証および署名してから、Web @ no__t ベースのアプリケーション用の独自のセキュリティトークンを発行します.  
  
> [!NOTE]  
> フェデレーションユーザーが web ブラウザーを使用して Web @ no__t ベースのアプリケーションにアクセスすると、リソースパートナー組織のフェデレーションサーバーは新しい認証クッキーを作成し、それをブラウザーに書き込みます。 この cookie は \(SSO @ no__t-3 機能で1つの @ no__t-0sign @ no__t-1on 有効にします。これにより、ユーザーがリソース内の別の Web @ no__t-4based のアプリケーションにアクセスしようとしたときに、アカウントパートナーのフェデレーションサーバーで再度ログオンする必要がなくなります。企業.  
  
Web SSO 設計では、少なくとも1つのフェデレーションサーバーが境界ネットワークにインストールされている必要があります。 フェデレーション Web SSO 設計では、アカウントパートナー組織の企業ネットワークに少なくとも1つのフェデレーションサーバーがインストールされ、リソースパートナー組織の企業ネットワークに少なくとも1つのフェデレーションサーバーがインストールされている必要があります。  
  
> [!NOTE]  
> リソースパートナー組織でフェデレーションサーバーコンピューターをセットアップする前に、まず、そのコンピューターをリソースパートナー組織内の任意の Active Directory ドメインに参加させる必要があります。 詳細については、「@no__t」チェックリストを参照してください。フェデレーションサーバー @ no__t をセットアップしています。  
  
## <a name="see-also"></a>関連項目
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)

