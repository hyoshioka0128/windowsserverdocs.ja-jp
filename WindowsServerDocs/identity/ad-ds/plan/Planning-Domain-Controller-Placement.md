---
ms.assetid: 692bd2af-deee-44cf-9af9-f364677e267f
title: ドメイン コント ローラー配置の計画
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 68406d4973dd585bf0a98562c987c1b1512c095c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59883363"
---
# <a name="planning-domain-controller-placement"></a>ドメイン コント ローラー配置の計画

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

すべてのサイト トポロジの設計に使用されるネットワーク情報を収集した後は、フォレスト ルート ドメイン コント ローラー、地域別のドメイン コント ローラー、操作マスターの役割の所有者などのドメイン コント ローラーを配置する位置を計画し、グローバル カタログ サーバー。  
  
Windows Server 2008 を活用することも読み取り専用ドメイン コント ローラー (Rodc)。 RODC は、Active Directory データベースの読み取り専用のパーティションをホストするドメイン コント ローラーの新しい型です。 RODC は、アカウント パスワードを除いて、すべての Active Directory オブジェクトと、書き込み可能なドメイン コント ローラーを保持する属性を保持します。 ただし、RODC に格納されているデータベースに変更を行うことはできません。 変更は、書き込み可能なドメイン コント ローラーに対して実行され、RODC にレプリケートされるする必要があります。  
  
RODC はリモートで展開するには、主に設計されていますか、ブランチ オフィス環境は、通常は比較的少数のユーザー、物理的なセキュリティの低下、ハブ サイト、および人員についての知識を比較的不適切なネットワーク帯域幅があります。技術 (IT)。 セキュリティの向上とネットワーク リソースにアクセスをより効率的では、Rodc の結果を展開します。 RODC の機能の詳細については、AD DS を参照してください。読み取り専用ドメイン コント ローラー ([https://go.microsoft.com/fwlink/?LinkID=106616](https://go.microsoft.com/fwlink/?LinkID=106616))。 RODC をデプロイする方法については、読み取り専用ドメイン コント ローラーのステップ バイ ステップ ガイドを参照してください。 ([https://go.microsoft.com/fwlink/?LinkID=92728](https://go.microsoft.com/fwlink/?LinkID=92728))。  
  
> [!NOTE]  
> このガイドでは、適切な数のドメイン コント ローラーと各サイトで表される各ドメインのドメイン コント ローラーのハードウェア要件を特定する方法を説明していません。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [フォレスト ルート ドメイン コント ローラー配置の計画](../../ad-ds/plan/Planning-Forest-Root-Domain-Controller-Placement.md)  
  
-   [地域ドメイン コント ローラーの配置の計画](../../ad-ds/plan/Planning-Regional-Domain-Controller-Placement.md)  
  
-   [グローバル カタログ サーバーの配置の計画](../../ad-ds/plan/Planning-Global-Catalog-Server-Placement.md)  
  
-   [操作マスターの役割の配置の計画](../../ad-ds/plan/Planning-Operations-Master-Role-Placement.md)  
  


