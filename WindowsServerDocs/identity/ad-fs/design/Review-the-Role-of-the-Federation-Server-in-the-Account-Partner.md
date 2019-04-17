---
ms.assetid: d0ba3c0d-869f-4e24-89d7-499da7576f22
title: "アカウント パートナーのフェデレーション サーバーの役割を確認します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 0914d32e8f24d5e7db0a25c733342c1bde3e0329
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="review-the-role-of-the-federation-server-in-the-account-partner"></a>アカウント パートナーのフェデレーション サーバーの役割を確認します。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Active Directory フェデレーション サービス \(AD FS\) 内のフェデレーション サーバーは、セキュリティ トークンの発行元として機能します。 フェデレーション サーバーは、ローカル属性内に存在する値を格納アカウントに基づいて信頼性情報を生成し、ユーザーが Web browser\-ベースのアプリケーションをシームレスにアクセスできるようにセキュリティ トークンにパッケージ化 \ (リソース パートナー組織でホストされている単一の sign\ で \(SSO\)\) を使用します。  
  
> [!NOTE]  
> ユーザー アクセス権は、Web ブラウザーを使用してアプリケーションをフェデレーション、フェデレーション サーバーは自動的にその Web browser\-ベース アプリケーション用のログオン状態を維持するためにユーザーに Cookie を発行します。 これらの Cookie には、ユーザーの信頼性情報が含まれます。 Cookie は SSO 機能を有効にできるように、ユーザーは、さまざまな Web browser\-ベース、リソース パートナー アプリケーションにアクセスするたびに資格情報を入力する必要はありません。  
  
Web SSO 設計では、インターネット ユーザー アプリケーションへのアクセスを許可する境界ネットワークでの組織は、境界ネットワーク内のフェデレーション サーバー プロキシをインストールする必要があります。 フェデレーション Web SSO デザインで、少なくとも 1 つのフェデレーション サーバーが、アカウント パートナー組織の企業ネットワークにインストールされていると、リソース パートナー組織の企業ネットワークにインストールされている少なくとも 1 台のフェデレーション サーバーに必要があります。  
  
> [!NOTE]  
> アカウント パートナー組織内のフェデレーション サーバー コンピューターをセットアップすることができます、前にそのフォレストからユーザーを認証するフェデレーション サーバーを使用する Active Directory フォレスト内の任意のドメインを最初にコンピューターを参加する必要があります。 詳細については、次を参照してください。[チェックリスト: フェデレーション サーバーの設定](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md)します。  
  
## <a name="see-also"></a>参照してください。
[Windows Server 2012 で AD FS 設計ガイドします。](AD-FS-Design-Guide-in-Windows-Server-2012.md)
