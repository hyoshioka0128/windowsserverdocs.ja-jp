---
ms.assetid: 4f835b82-67b9-428c-b634-ce133cca5113
title: "AD DS 展開戦略の例を評価します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 4cac1e344cfed078927f2945048807d686deebd1
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="evaluating-ad-ds-deployment-strategy-examples"></a>AD DS 展開戦略の例を評価します。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Contoso Pharmaceuticals は、その環境で Active Directory ドメイン サービス (AD DS) の展開は、架空の会社の次の例を検討してください。 Contoso の環境は、4 つのドメインで構成されます。 フォレストの機能レベルは、Windows Server 2003 です。 次の図は、Contoso 組織の現在のドメイン構造を示しています。  
  
![AD DS の展開戦略](media/Evaluating-AD-DS-Deployment-Strategy-Examples/3dd79e00-48f8-4927-989c-c55a79caf1be.gif)  
  
確認した後、既存の環境と Contoso の展開の目標を識別するには、次の AD DS の展開戦略を確立します。  
  
-   Windows Server 2008 ドメインを Windows Server 2003 ドメインをアップグレードします。  
  
-   Windows Server 2008 ドメインとフォレストの機能レベルを上げるによって高度な AD DS の機能を有効にします。  
  
-   Emea.concorp.contoso.con ドメインとそのドメインを統合するフォレスト内にある africa.concorp.contoso.com ドメインの再構築します。  
  
Windows Server 2008 にフォレストの機能レベルを上げると、AD DS の新機能をフル活用する contoso 社が有効になります。 次の図に示すように、フォレスト内のドメインの再構築すると、ドメインを管理するために必要な管理の量を減らすことができます。  
  
![AD DS の展開戦略](media/Evaluating-AD-DS-Deployment-Strategy-Examples/1c061755-413d-452d-b121-6910f8555327.gif)  
  


