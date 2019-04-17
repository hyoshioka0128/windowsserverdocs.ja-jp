---
ms.assetid: 692bd2af-deee-44cf-9af9-f364677e267f
title: "ドメイン コントローラーの配置を計画します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: c6d9ca064699f95390e5b95863a6871ea2dc9d6e
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="planning-domain-controller-placement"></a>ドメイン コントローラーの配置を計画します。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

すべてのサイト トポロジの設計、計画、フォレスト ルート ドメイン コントローラー、地域別のドメイン コントローラーを含むドメイン コントローラーを配置するに使用されるネットワーク情報を収集した後に操作マスターの役割所有者、およびグローバル カタログ サーバーのします。  
  
Windows Server 2008 でを活用することも読み取り専用ドメイン コントローラー (Rodc)。 RODC は、Active Directory データベースの読み取り専用のパーティションをホストするドメイン コントローラーの新しい型です。 RODC は、アカウントのパスワードを除いて、すべての Active Directory オブジェクトと、書き込み可能なドメイン コントローラーを保持する属性を保持します。 ただし、RODC に格納されているデータベースに変更を行うことはできません。 変更は、書き込み可能ドメイン コントローラーで行われたし、RODC にレプリケートする必要があります。  
  
RODC はリモートで展開するには、主に設計されていますか、ブランチ オフィス環境は、通常、比較的少数のユーザー、物理的なセキュリティのレベルが低い、ハブ サイト、および情報技術 (IT) の制限の知識を持つ担当者に比較的不適切なネットワーク帯域幅があります。 セキュリティの強化とネットワーク リソースへのアクセスをより効率的に Rodc の結果を展開します。 RODC の機能の詳細については、AD DS を参照してください: Read-Only ドメイン コントローラー ([https://go.microsoft.com/fwlink/?LinkID=106616](https://go.microsoft.com/fwlink/?LinkID=106616))。 RODC を展開する方法については、次を参照してください。、Step-by-Step Guide の Read-Only ドメイン コントローラー ([https://go.microsoft.com/fwlink/?LinkID=92728](https://go.microsoft.com/fwlink/?LinkID=92728)) します。  
  
> [!NOTE]  
> このガイドでは、ドメイン コントローラーと各サイトで表される各ドメインのドメイン コントローラーのハードウェア要件の適切な数を決定する方法を説明していません。  
  
## <a name="in-this-section"></a>このセクションで  
  
-   [フォレスト ルート ドメイン コントローラーの配置を計画します。](../../ad-ds/plan/Planning-Forest-Root-Domain-Controller-Placement.md)  
  
-   [地域ドメイン コントローラーの配置を計画します。](../../ad-ds/plan/Planning-Regional-Domain-Controller-Placement.md)  
  
-   [グローバル カタログ サーバーの配置を計画します。](../../ad-ds/plan/Planning-Global-Catalog-Server-Placement.md)  
  
-   [操作マスターの役割の配置を計画します。](../../ad-ds/plan/Planning-Operations-Master-Role-Placement.md)  
  


