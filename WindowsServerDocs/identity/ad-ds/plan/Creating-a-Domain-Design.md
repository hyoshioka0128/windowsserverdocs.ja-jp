---
ms.assetid: 2a25bf86-a8ec-4b1a-9cbb-924d5b574481
title: フォレスト設計の作成
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: ad2cf439b5d85e72f1a9dbfbf1d0cb1afcadff7e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80822795"
---
# <a name="creating-a-domain-design"></a>フォレスト設計の作成

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

フォレストの所有者は、フォレストのドメイン設計を作成します。 ドメイン設計を作成するには、レプリケーションの要件とネットワークインフラストラクチャの既存の容量を調べ、Active Directory Domain Services (AD DS) が最も効率的な方法で機能するようにドメイン構造を構築する必要があります。 ドメインはディレクトリをパーティション分割するために使用されます。これにより、ディレクトリ内の情報を企業全体で効率的に配布し、管理することができます。 ドメイン設計の目的は、レプリケーションで使用できるネットワーク帯域幅が多すぎないようにしながら、ネットワークの日常的な操作に干渉しないように、Active Directory レプリケーショントポロジの効率を最大化することです。  
  
## <a name="in-this-section"></a>このセクションの内容  
  
-   [ドメインモデルの確認](../../ad-ds/plan/Reviewing-the-Domain-Models.md)  
  
-   [必要なドメイン数を決定する](../../ad-ds/plan/Determining-the-Number-of-Domains-Required.md)  
  
-   [既存のドメインをアップグレードするか新しいドメインを展開するかを決定する](../../ad-ds/plan/Determining-Whether-to-Upgrade-Existing-Domains-or-Deploy-New-Domains.md)  
  
-   [ドメイン名を割り当てる](../../ad-ds/plan/Assigning-Domain-Names.md)  
  
-   [フォレスト ルート ドメインを選択する](../../ad-ds/plan/Selecting-the-Forest-Root-Domain.md)  
  


