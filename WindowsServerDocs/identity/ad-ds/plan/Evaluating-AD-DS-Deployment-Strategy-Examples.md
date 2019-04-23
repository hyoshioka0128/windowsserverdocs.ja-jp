---
ms.assetid: 4f835b82-67b9-428c-b634-ce133cca5113
title: AD DS の展開戦略の例を評価する
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 169d0a55f9fb167390c13ac1c89f8d68427f318d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842113"
---
# <a name="evaluating-ad-ds-deployment-strategy-examples"></a>AD DS の展開戦略の例を評価する

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

架空の会社 Contoso Pharmaceuticals は、その環境で Active Directory Domain Services (AD DS) を展開するは、次の例を検討してください。 Contoso 環境は、4 つのドメインで構成されます。 フォレストの機能レベルは、Windows Server 2003 です。 次の図は、Contoso 組織の現在のドメイン構造を示します。  
  
![AD DS の展開戦略](media/Evaluating-AD-DS-Deployment-Strategy-Examples/3dd79e00-48f8-4927-989c-c55a79caf1be.gif)  
  
既存の環境を確認し、その展開の目標の特定、した後は、Contoso には、次の AD DS の展開戦略が確立されています。  
  
-   Windows Server 2008 のドメインには、Windows Server 2003 ドメインをアップグレードします。  
  
-   Windows Server 2008 へのドメインとフォレストの機能レベルを発生させることによって、高度な AD DS の機能を有効にします。  
  
-   Emea.concorp.contoso.con ドメインとそのドメインを統合するフォレスト内にある africa.concorp.contoso.com ドメインの再構築します。  
  
Windows Server 2008 へのフォレスト機能レベルを上げると、AD DS の新機能の活用するために Contoso が有効になります。 次の図に示すように、フォレスト内のドメインを再構築すると、管理ドメインを管理するために必要な量を削減します。  
  
![AD DS の展開戦略](media/Evaluating-AD-DS-Deployment-Strategy-Examples/1c061755-413d-452d-b121-6910f8555327.gif)  
  


