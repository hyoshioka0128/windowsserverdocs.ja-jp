---
title: "AD フォレストの回復の手順"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 47a471fb-3b0b-4aa8-8525-1c92d0d51e93
ms.technology: identity-adfs
ms.openlocfilehash: 91e3954c05fe3cd12d35b5db91afd29fb3a31e00
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/13/2017
---
# <a name="ad-forest-recovery---procedures"></a>AD フォレストの回復の手順


>Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 の R2 を適用対象:

This section contains procedures related to the forest recovery process. The procedures are applicable for Windows Server 2016, 2012 R2, 2012 and are also applicable to Windows Server 2008 R2 and 2008 with some minor exceptions. 

Procedures that include steps that vary for Windows Server 2003 are found in [Forest Recovery with Windows Server 2003 Domain Controllers](AD-Forest-Recovery-Windows-Server-2003.md).  

The following is a list of procedures that are used in backing up and restoring domain controllers and Active Directory.
  
-   [Backing up a full server](AD-Forest-Recovery-Backing-up-a-Full-Server.md)  
-   [システム状態データをバックアップします。](AD-Forest-Recovery-Backing-up-System-State.md)  
-   [Performing a full server recovery](AD-Forest-Recovery-Perform-a-Full-Recovery.md)  
-   [Performing an authoritative synch of DFSR-replicated SYSVOL](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md)
-   [Active Directory ドメイン サービスの非 authoritative restore を実行します。](AD-Forest-Recovery-Nonauthoritative-Restore.md)  
  
     These steps explain how to perform an authoritative restore of SYSVOL at the same time.  
-   [Configuring the DNS Server service](AD-Forest-Recovery-Configure-DNS.md)  
-   [Removing the global catalog](AD-Forest-Recovery-Remove-GC.md)  
-   [Raising the value of available RID pools](AD-Forest-Recovery-Raise-RID-Pool.md)  
-   [Invalidating the current RID pool](AD-Forest-Recovery-Invaildate-RID-Pool.md)  
-   [Seizing an operations master role](AD-Forest-Recovery-Seizing-Operations-Master-Role.md)  
-   [Cleaning up after a restore](AD-Forest-Recovery-Cleanup.md)
-   [Cleaning metadata of removed writable domain controllers](AD-Forest-Recovery-Cleaning-Metadata.md)  
-   [Resetting the computer account password of the domain controller](AD-Forest-Recovery-Reset-Computer-Account-DC.md)  
-   [Resetting the krbtgt password](AD-Forest-Recovery-Resetting-the-krbtgt-password.md)  
-   [信頼関係の 1 つの側での信頼のパスワードをリセットします。](AD-Forest-Recovery-Reset-Trust.md)  
-   [Adding the global catalog](AD-Forest-Recovery-Add-GC.md)  
-   [レプリケーションが動作していることを確認するリソース](AD-Forest-Recovery-Verify-Replication.md)  
  
  
## <a name="next-steps"></a>次の手順
-   [AD フォレストの回復の前提条件](AD-Forest-Recovery-Prerequisties.md)  
-   [AD フォレストの回復 - カスタム フォレスト回復計画を立てる](AD-Forest-Recovery-Devising-a-Plan.md)  
- [AD フォレストの回復 - 問題の特定](AD-Forest-Recovery-Identify-the-Problem.md)
-   [AD フォレストの回復 - を回復する方法を決定します。](AD-Forest-Recovery-Determine-how-to-Recover.md)
-   [AD フォレストの回復 - 最初の回復を実行](AD-Forest-Recovery-Perform-initial-recovery.md)  
-   [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md)  
-   [AD フォレストの回復のよく寄せられる質問](AD-Forest-Recovery-FAQ.md)  
-   [AD フォレストの回復であれば、マルチ ドメイン フォレスト内で 1 つのドメインの回復](AD-Forest-Recovery-Single-Domain-in-Multidomain-Recovery.md)  
-   [AD フォレストの回復 - Windows Server 2003 ドメイン コントローラーとフォレストの回復](AD-Forest-Recovery-Windows-Server-2003.md) 
