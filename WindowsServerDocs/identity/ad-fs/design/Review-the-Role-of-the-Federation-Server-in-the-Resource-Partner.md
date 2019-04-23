---
ms.assetid: f88238ea-d851-4129-8b4e-a3a62b813614
title: リソース パートナー内のフェデレーション サーバーの役割を確認する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 6d4c7763d7204dd2340d10a234e48f47c96788dc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841843"
---
# <a name="review-the-role-of-the-federation-server-in-the-resource-partner"></a>リソース パートナー内のフェデレーション サーバーの役割を確認する

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

リソース パートナー組織のフェデレーション サーバーは、アカウント フェデレーション サーバーによって送信されるセキュリティ トークンの受信をインターセプト、検証し署名しておよび Web を宛先とする独自のセキュリティ トークンを発行し、\-ベースアプリケーション。  
  
> [!NOTE]  
> Web にアクセスする、フェデレーション ユーザーが自分の Web ブラウザーを使用すると\-ベースのアプリケーション、リソース パートナー組織のフェデレーション サーバーは新しい認証クッキーをビルドし、ブラウザーに書き込みます。 この cookie により、1 つ\-サインオン\-で\(SSO\)機能もう一度ログオンするアカウント パートナーのフェデレーション サーバーで、ユーザーが、別の Web にアクセスしようとしていますときにユーザーがいないように\-。リソース パートナーのアプリケーションに基づいています。  
  
Web SSO 設計で、境界ネットワーク内の少なくとも 1 つのフェデレーション サーバーをインストールする必要があります。 フェデレーション Web SSO 設計で、アカウント パートナー組織の企業ネットワークにインストールされている少なくとも 1 つのフェデレーション サーバーとリソース パートナー組織の企業ネットワークにインストールされている少なくとも 1 つのフェデレーション サーバーに必要があります。  
  
> [!NOTE]  
> リソース パートナー組織のフェデレーション サーバー コンピューターをセットアップすることができます、前に、リソース パートナー組織内の任意の Active Directory ドメインにコンピューターを最初に参加する必要があります。 詳細については、次を参照してください。[チェックリスト。フェデレーション サーバーを設定する](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md)します。  
  
## <a name="see-also"></a>関連項目
[Windows Server 2012 で AD FS 設計ガイドします。](AD-FS-Design-Guide-in-Windows-Server-2012.md)

