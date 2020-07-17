---
ms.assetid: a91339ef-6ad4-445f-8ecc-a95fbcc04296
title: Active Directory の設計と計画について
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/07/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 5f88458c8e3f50853229f6f8f9c74fa4b8feba40
ms.sourcegitcommit: 11421f4005f9f3a3f6c0db95b1836d0f765a9fa3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2020
ms.locfileid: "81624420"
---
# <a name="ad-ds-design-and-planning"></a>Active Directory の設計と計画について

> 適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

環境に Windows Server Active Directory Domain Services (AD DS) を展開することによって、AD DS によって提供される、一元化された、代理管理モデル、シングルサインオン (SSO) 機能を利用できます。 組織の展開タスクと現在の環境を特定したら、組織のニーズに合った AD DS 展開方法を作成できます。

## <a name="about-this-guide"></a>このガイドについて

このガイドでは、組織の要件と作成する特定の設計に基づいて、AD DS 展開戦略を策定する際に役立つ推奨事項について説明します。 このガイドは、インフラストラクチャの専門家やシステム アーキテクト向けです。 このガイドを読む前に、AD DS が機能レベルでどのように機能するかについて十分に理解しておく必要があります。 また、AD DS の展開戦略に反映される組織の要件について十分に理解している必要があります。

このガイドでは、Windows Server 2008 AD DS 展開のいくつかの開始点について、一連のタスクについて説明します。 このガイドは、ご使用の環境に最適な展開戦略を判断するのに役立ちます。

このガイドに記載されている戦略は、ほぼすべてのサーバーオペレーティングシステムの展開に適していますが、10万人未満のユーザーが含まれ、1000サイトよりも少ない環境に対しては、特に28.8 キロビット/秒 (Kbps) のネットワーク接続を使用してテストおよび検証されています。 環境がこれらの条件を満たしていない場合は、より複雑な環境で AD DS のデプロイ経験を持つコンサルティング会社を使用することを検討してください。

AD DS のデプロイプロセスのテストの詳細については、「[デプロイプロセスのテストと検証](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc772722(v=ws.10))」を参照してください。

## <a name="in-this-guide"></a>このガイドの内容

[AD DS の設計とは](Understanding-AD-DS-Design.md)

[AD DS の設計と展開の要件を識別する](Identifying-Your-AD-DS-Design-and-Deployment-Requirements.md)

[AD DS の展開戦略に要件をマッピングする](Mapping-Your-Requirements-to-an-AD-DS-Deployment-Strategy.md)

[Windows Server 2008 の論理構造の設計 AD DS](Designing-the-Logical-Structure.md)

[Windows Server 2008 用のサイトトポロジの設計 AD DS](Designing-the-Site-Topology.md)

[AD DS の高度な機能を有効にする](Enabling-Advanced-Features-for-AD-DS.md)

[AD DS の展開戦略の例を評価する](Evaluating-AD-DS-Deployment-Strategy-Examples.md)

[付録 A: 重要な AD DS の用語の確認](Appendix-A--Reviewing-Key-AD-DS-Terms.md)
