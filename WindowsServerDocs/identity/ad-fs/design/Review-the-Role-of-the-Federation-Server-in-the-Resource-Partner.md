---
ms.assetid: f88238ea-d851-4129-8b4e-a3a62b813614
title: "リソース パートナーのフェデレーション サーバーの役割を確認します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 6d4c7763d7204dd2340d10a234e48f47c96788dc
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="review-the-role-of-the-federation-server-in-the-resource-partner"></a>リソース パートナーのフェデレーション サーバーの役割を確認します。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リソース パートナー組織をインターセプト受信セキュリティ トークン、アカウント フェデレーション サーバーによって送信される内のフェデレーション サーバーは、検証および署名して、Web ベース アプリケーションの配信される、独自のセキュリティ トークンを発行します。  
  
> [!NOTE]  
> フェデレーション ユーザーは、Web ベース アプリケーションにアクセスする、Web ブラウザーを使用して、リソース パートナー組織内のフェデレーション サーバーは新しい認証クッキーをビルドし、ブラウザーに書き込みます。 この Cookie は、できるように、ユーザーは、再度ログオン アカウント パートナーのフェデレーション サーバーで、ユーザーがリソース パートナー内の別の Web ベース アプリケーションにアクセスしようとする必要はありません、シングル sign\-で \(SSO\) 機能を使用できます。  
  
Web SSO 設計では、少なくとも 1 つのフェデレーション サーバーを境界ネットワークにインストールしなければなりません。 フェデレーション Web SSO デザインで、少なくとも 1 つのフェデレーション サーバーが、アカウント パートナー組織の企業ネットワークにインストールされていると、リソース パートナー組織の企業ネットワークにインストールされている少なくとも 1 台のフェデレーション サーバーに必要があります。  
  
> [!NOTE]  
> リソース パートナー組織のフェデレーション サーバー コンピューターをセットアップすることができます、前に最初コンピューターをリソース パートナー組織内の任意の Active Directory ドメインに参加する必要があります。 詳細については、次を参照してください。[チェックリスト: フェデレーション サーバーの設定](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md)します。  
  
## <a name="see-also"></a>参照してください。
[Windows Server 2012 で AD FS 設計ガイドします。](AD-FS-Design-Guide-in-Windows-Server-2012.md)

