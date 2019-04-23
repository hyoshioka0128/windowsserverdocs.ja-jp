---
title: AD フォレストの回復の SYSVOL の権限のある同期
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 38a1c543-c76d-4b8e-a06b-53742aaa172f
ms.technology: identity-adds
ms.openlocfilehash: 246a2ea589ee05110362cff99d50e93a0a18c2b9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827003"
---
# <a name="ad-forest-recovery---performing-an-authoritative-synchronization-of-dfsr-replicated-sysvol"></a>DFSR でレプリケートされた SYSVOL の権限のある同期の実行 - AD フォレストの回復  

>適用先:Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 R2

SYSVOL の authoritative restore を実行するさまざまな方法はあります。 いずれかの編集ができます、 **msDFSR オプション**属性または wbadmin – authsysvol を使用してシステム状態の復元を実行します。 システム状態のバックアップを復元するオプションがあるかどうか (つまり、復元する AD DS、ハードウェアおよびオペレーティング システムの同じインスタンスに)、wbadmin – authsysvol を使用する方が簡単です。 ベア メタル復元を実行する必要があるかどうかは、編集する必要がありますが、 **msDFSR オプション**属性。  

(DFSR を使用してレプリケートされる) 場合、権限のない SYSVOL 同期を実行する、次の手順を使用して、編集することによって、 **msDFSR オプション**属性。 FRS を使用して SYSVOL をレプリケートする場合は、次を参照してください。[記事 290762](https://go.microsoft.com/fwlink/?LinkId=148443)します。  

## <a name="to-perform-an-authoritative-synchronization-of-dfsr-replicated-sysvol"></a>DFSR でレプリケートされた SYSVOL の権限を持つの同期を実行するには  

1. [Active Directory ユーザーとコンピューター] を開きます。  
2. クリックして**ビュー**、し、**ユーザー、連絡先、グループ、およびコンピューターをコンテナーとして**と**高度な機能**します。 

   ![SYSVOL](media/AD-Forest-Recovery-Authoritative-Recovery-SYSVOL/sysvol1.png) 

3. ツリー ビューで、クリックして**ドメイン コント ローラー**、復元する DC の名前**DFSR LocalSettings**、し**ドメイン システム ボリューム**します。 

   ![SYSVOL](media/AD-Forest-Recovery-Authoritative-Recovery-SYSVOL/sysvol2.png)  

4. 詳細ペインで右クリックして**SYSVOL サブスクリプション**、 をクリックして**プロパティ**、 をクリック**属性エディター**します。  

   ![SYSVOL](media/AD-Forest-Recovery-Authoritative-Recovery-SYSVOL/sysvol3.png) 

5. クリックして**msDFSR オプション**、 をクリックして**編集**、型**1**、 をクリック**ok**  

   ![SYSVOL](media/AD-Forest-Recovery-Authoritative-Recovery-SYSVOL/sysvol4.png) 

6. クリックして**OK**属性エディターを閉じます。  
  
## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md)
