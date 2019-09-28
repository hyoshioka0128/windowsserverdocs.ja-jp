---
ms.assetid: 4f835b82-67b9-428c-b634-ce133cca5113
title: AD DS の展開戦略の例を評価する
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 3d04530c53150a3222b609a80938d7fdfcdfeff7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402591"
---
# <a name="evaluating-ad-ds-deployment-strategy-examples"></a>AD DS の展開戦略の例を評価する

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

次の例では、Contoso 製薬という架空の会社の例を考えてみます。これは Active Directory Domain Services (AD DS) を環境に展開しています。 Contoso 環境は、4つのドメインで構成されています。 フォレストの機能レベルは Windows Server 2003 です。 次の図は、Contoso 組織の現在のドメイン構造を示しています。  
  
![AD DS の展開方法](media/Evaluating-AD-DS-Deployment-Strategy-Examples/3dd79e00-48f8-4927-989c-c55a79caf1be.gif)  
  
Contoso では、既存の環境を確認し、その展開の目標を特定した後、次の AD DS 展開戦略を確立しました。  
  
-   Windows Server 2003 ドメインを Windows Server 2008 ドメインにアップグレードします。  
  
-   ドメインとフォレストの機能レベルを Windows Server 2008 に上げることにより、高度な AD DS 機能を有効にします。  
  
-   フォレスト内の africa.concorp.contoso.com ドメインを再構築して、そのドメインを emea. contoso. のドメインと統合します。  
  
フォレストの機能レベルを Windows Server 2008 に上げると、Contoso は新しい AD DS 機能を最大限に活用することができます。 次の図に示すように、フォレスト内のドメインを再構築すると、ドメインの管理に必要な管理の量が減少します。  
  
![AD DS の展開方法](media/Evaluating-AD-DS-Deployment-Strategy-Examples/1c061755-413d-452d-b121-6910f8555327.gif)  
  


