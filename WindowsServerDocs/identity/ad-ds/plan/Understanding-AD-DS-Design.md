---
ms.assetid: d590c90e-9adf-4305-b226-eb2a5743337b
title: AD DS の設計とは
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/07/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 734d5eaef97b23b774eb286134d07a17dc380da1
ms.sourcegitcommit: 11421f4005f9f3a3f6c0db95b1836d0f765a9fa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81623910"
---
# <a name="understanding-ad-ds-design"></a>AD DS の設計とは

> 適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

組織は、Windows Server の Active Directory Domain Services (AD DS) を使用して、スケーラブルで安全な、管理性に優れたインフラストラクチャを作成しながら、ユーザーとリソースの管理を簡略化することができます。 AD DS を使用して、ブランチオフィス、Microsoft Exchange Server、および複数のフォレスト環境を含むネットワークインフラストラクチャを管理できます。

AD DS 配置プロジェクトには、設計フェーズ、配置フェーズ、操作フェーズという3つのフェーズが含まれます。 設計段階では、設計チームは、ディレクトリサービスを使用する組織内の各部門のニーズに最適な AD DS 論理構造の設計を作成します。 設計が承認されると、配置チームはラボ環境でデザインをテストし、運用環境で設計を実装します。 テストは配置チームによって実行されるため、設計フェーズに影響する可能性があります。これは、設計と配置の両方に重複する中間アクティビティです。 デプロイが完了すると、運用チームはディレクトリサービスの保守を担当します。

このガイドに記載されている Windows Server AD DS の設計と展開の戦略は、さまざまなラボおよびパイロットプログラムのテストと、お客様の環境での正常な実装に基づいていますが、特定の複雑な環境に合わせて、AD DS の設計と展開をカスタマイズすることが必要になる場合があります。

- ブランチオフィス環境で AD DS を展開する方法の詳細については、「[読み取り専用ドメインコントローラー (RODC) のブランチオフィス計画ガイド](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd734758(v=ws.10))」を参照してください。
- Exchange 環境で AD DS を展開する方法の詳細については、 [Exchange Server 組織の Active Directory](https://docs.microsoft.com/Exchange/plan-and-deploy/active-directory/active-directory)に関する記事を参照してください。
- 複数のフォレスト環境で AD DS を展開する方法の詳細については、「 [windows 2000 および Windows Server 2003 における複数のフォレストに関する考慮事項](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc739395(v=ws.10))」を参照してください。
