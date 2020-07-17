---
ms.assetid: 692bd2af-deee-44cf-9af9-f364677e267f
title: ドメイン コント ローラー配置の計画
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: bb68a3551b362f0beb5d42a92a7c18d0913e47bc
ms.sourcegitcommit: 11421f4005f9f3a3f6c0db95b1836d0f765a9fa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81624090"
---
# <a name="planning-domain-controller-placement"></a>ドメイン コント ローラー配置の計画

> 適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

サイトトポロジの設計に使用するすべてのネットワーク情報を収集したら、ドメインコントローラーを配置する場所を計画します。これには、フォレストルートドメインコントローラー、地域ドメインコントローラー、操作マスターの役割所有者、およびグローバルカタログサーバーが含まれます。

Windows Server 2008 では、読み取り専用ドメインコントローラー (Rodc) を利用することもできます。 RODC は新しい種類のドメイン コントローラーで、Active Directory データベースの読み取り専用パーティションをホストします。 RODC は、アカウント パスワードを除いて、すべての Active Directory オブジェクトと、書き込み可能なドメイン コント ローラーを保持する属性を保持します。 ただし、RODC に格納されているデータベースに変更を行うことはできません。 変更は、書き込み可能なドメイン コント ローラーに対して実行され、RODC にレプリケートされるする必要があります。

RODC は、主にリモートまたはブランチオフィス環境に展開されるように設計されています。この環境では、ユーザー数が比較的少なく、物理的なセキュリティが不十分で、ハブサイトへのネットワーク帯域幅が比較的少なく、情報技術 (IT) に関する知識が限られている人もいます。 Rodc を展開すると、セキュリティが強化され、ネットワークリソースにより効率的にアクセスできるようになります。 RODC の機能の詳細については、「 [AD DS: 読み取り専用ドメインコントローラー](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc732801(v=ws.10))」を参照してください。 RODC を展開する方法の詳細については、「[読み取り専用ドメインコントローラーのステップバイステップガイド](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc772234(v=ws.10))」を参照してください。

> [!NOTE]
> このガイドでは、各サイトで表される各ドメインについて、適切な数のドメインコントローラーおよびドメインコントローラーのハードウェア要件を決定する方法については説明しません。

## <a name="in-this-section"></a>このセクションの内容

- [フォレスト ルート ドメイン コントローラーの配置を計画する](../../ad-ds/plan/Planning-Forest-Root-Domain-Controller-Placement.md)

- [地域ドメインコントローラーの配置の計画](../../ad-ds/plan/Planning-Regional-Domain-Controller-Placement.md)

- [グローバル カタログ サーバーの配置を計画する](../../ad-ds/plan/Planning-Global-Catalog-Server-Placement.md)

- [操作マスターの役割の配置を計画する](../../ad-ds/plan/Planning-Operations-Master-Role-Placement.md)

