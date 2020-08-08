---
ms.assetid: a8558c9d-0606-4881-93b2-f2d2716b18e7
title: Windows Server 2012 R2 での AD FS 設計ガイド
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 6ec9826ce2015197d96a182864807646a6b8115d
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87940408"
---
# <a name="ad-fs-design-guide-in-windows-server"></a>Windows Server の AD FS 設計ガイド

Active Directory フェデレーションサービス (AD FS) \( AD FS \) は、セキュリティで保護され \- \( \) た AD FS \- 企業、フェデレーションパートナー組織、またはクラウド内のアプリケーションへのアクセスを必要とするエンドユーザーに、簡素化されたセキュリティで保護された id フェデレーションと Web シングルサインオン SSO 機能を提供します。

Windows Server &reg; 2012 R2 では、AD FS にフェデレーションサービス役割サービスが含まれています。これは、id プロバイダーがユーザーを認証して、 \( AD FS を信頼するアプリケーションにセキュリティトークンを提供する \) か、フェデレーションプロバイダーが \( 他の id プロバイダーからのトークンを使用して、AD FS を信頼するアプリケーションにセキュリティトークンを提供し \) ます。

Windows Server 2012 R2 の AD FS によって保護されたアプリケーションやサービスへのエクストラネット アクセスを提供する機能は、Web アプリケーション プロキシと呼ばれる新しいリモート アクセス役割サービスによて実行されるようになりました。 以前のバージョンの Windows Server では、この機能は AD FS フェデレーション サーバー プロキシによって処理されていました。 Web アプリケーションプロキシは、AD FS \- 関連のエクストラネットシナリオやその他のエクストラネットシナリオにアクセスできるように設計されたサーバーの役割です。 Web アプリケーションプロキシの詳細については、 [Web アプリケーションプロキシのチュートリアルガイド](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn280944(v=ws.11))を参照してください。

## <a name="about-this-guide"></a>このガイドについて
このガイドでは、組織の要件に基づいて、AD FS の新しい展開を計画する際に役立つ推奨事項について説明します。 このガイドの対象読者は、インフラストラクチャ専門家またはシステム アーキテクトです。 AD FS の展開を計画する際に、主な意思決定点に焦点を当てます。 このガイドを読む前に、AD FS が機能レベルでどのように機能するかについて十分に理解しておく必要があります。 詳細については、「 [Understanding Key AD FS Concepts](../../ad-fs/technical-reference/Understanding-Key-AD-FS-Concepts.md)」を参照してください。

## <a name="in-this-guide"></a>このガイドの内容

-   [AD FS 展開目標の特定](Identify-Your-AD-FS-Deployment-Goals.md)

-   [AD FS 展開トポロジの計画](Plan-Your-AD-FS-Deployment-Topology.md)

-   [AD FS の要件](AD-FS-Requirements.md)


## <a name="see-also"></a>参照
[AD FS の設計](../../ad-fs/AD-FS-Design.md)

