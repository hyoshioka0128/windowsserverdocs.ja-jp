---
ms.assetid: d0ba3c0d-869f-4e24-89d7-499da7576f22
title: アカウント パートナー内のフェデレーション サーバーの役割を確認する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 5bc304277b872bd9b99b79b84694dd0cb1eb73ba
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190883"
---
# <a name="review-the-role-of-the-federation-server-in-the-account-partner"></a>アカウント パートナー内のフェデレーション サーバーの役割を確認する

Active Directory フェデレーション サービスでフェデレーション サーバー \(AD FS\)セキュリティ トークンの発行元として機能します。 フェデレーション サーバーがローカル属性内に存在する値のストア アカウントに基づいて信頼性情報を生成し、Web をシームレスにアクセスできるように、セキュリティ トークンにパッケージ化\-ブラウザー\-ベースのアプリケーション\(を使用してシングル サインオン\-で\(SSO\) \)がリソース パートナー組織でホストされます。  
  
> [!NOTE]  
> フェデレーション サーバーが、その Web 用のログオン状態を維持するためにユーザーに、cookie を自動的に発行する、ユーザーは、Web ブラウザーを使用してフェデレーション アプリケーションをアクセス、\-ブラウザー\-ベースのアプリケーション。 これらのクッキーには、ユーザーの信頼性情報が含まれます。 Cookie は、ユーザーは別の Web にアクセスするたびに資格情報を入力する必要があるないように、SSO 機能を有効にする\-ブラウザー\-ベースのリソース パートナー アプリケーション。  
  
Web SSO 設計では、インターネット ユーザーがアプリケーションへのアクセスを許可する境界ネットワークでの組織は、境界ネットワーク内のフェデレーション サーバー プロキシをインストールする必要があります。 フェデレーション Web SSO 設計で、アカウント パートナー組織の企業ネットワークにインストールされている少なくとも 1 つのフェデレーション サーバーとリソース パートナー組織の企業ネットワークにインストールされている少なくとも 1 つのフェデレーション サーバーに必要があります。  
  
> [!NOTE]  
> アカウント パートナー組織のフェデレーション サーバー コンピューターをセットアップすることができます、前に、そのフォレストからユーザーを認証するフェデレーション サーバーを使用、Active Directory フォレスト内のドメインにコンピューターを最初に参加する必要があります。 詳細については、次を参照してください。[チェックリスト。フェデレーション サーバーを設定する](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md)します。  
  
## <a name="see-also"></a>関連項目
[Windows Server 2012 での AD FS 設計ガイド](AD-FS-Design-Guide-in-Windows-Server-2012.md)
