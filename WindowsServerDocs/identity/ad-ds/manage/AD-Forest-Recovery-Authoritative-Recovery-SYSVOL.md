---
title: "AD フォレストの回復 - SYSVOL の権限の同期"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 38a1c543-c76d-4b8e-a06b-53742aaa172f
ms.technology: identity-adfs
ms.openlocfilehash: 5bdc619ddf9f28fb074e90dfbf22a7be076a05d9
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="ad-forest-recovery---performing-an-authoritative-synchronization-of-dfsr-replicated-sysvol"></a>AD フォレストの回復 - DFSR でレプリケートされた SYSVOL の権限のある同期の実行  

>Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 の R2 を適用対象:

 SYSVOL の authoritative restore を実行するさまざまな方法があります。 いずれかの編集することができます、 **msDFSR オプション**属性または wbadmin – authsysvol を使用してシステム状態の復元を実行します。 システム状態のバックアップを復元するオプションがあるかどうか (つまり、復元する AD DS を同じハードウェアとオペレーティング システムのインスタンス)、wbadmin – authsysvol を使用する方が簡単です。 ベア メタル復元を実行する必要があるかどうかは、編集する必要がありますが、 **msDFSR オプション**属性です。  
  
 編集することによって (DFSR を使用してレプリケートされる) 場合は、SYSVOL の権限のある、同期を実行する、次の手順を使用して、 **msDFSR オプション**属性です。 FRS を使用して SYSVOL をレプリケートする場合は、次を参照してください。[記事 290762](https://go.microsoft.com/fwlink/?LinkId=148443)します。  
  
## <a name="to-perform-an-authoritative-synchronization-of-dfsr-replicated-sysvol"></a>DFSR でレプリケートされた SYSVOL の権限を持つの同期を実行するには  
  
1.  Active Directory ユーザーとコンピューターを開きます。  
2.  をクリックして**ビュー**、し、[**ユーザー、連絡先、グループ、およびコンピューターをコンテナーとして**と**高度な機能**します。 
![SYSVOL](media/AD-Forest-Recovery-Authoritative-Recovery-SYSVOL/sysvol1.png) 
3.  ツリー ビューで、クリックして**ドメイン コント ローラー**、復元すると、DC の名前**DFSR LocalSettings**、し、**ドメイン システム ボリューム**します。 
![SYSVOL](media/AD-Forest-Recovery-Authoritative-Recovery-SYSVOL/sysvol2.png)  
4.  詳細ウィンドウで右クリックして**SYSVOL サブスクリプション**、] をクリックして**プロパティ**、] をクリック**属性エディター**します。  
![SYSVOL](media/AD-Forest-Recovery-Authoritative-Recovery-SYSVOL/sysvol3.png) 
5.  をクリックして**msDFSR オプション**、] をクリックして**編集**、種類**1**、] をクリック**-OK**  
![SYSVOL](media/AD-Forest-Recovery-Authoritative-Recovery-SYSVOL/sysvol4.png) 
6.  をクリックして**OK**属性エディターを閉じます。  
  
## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md)
