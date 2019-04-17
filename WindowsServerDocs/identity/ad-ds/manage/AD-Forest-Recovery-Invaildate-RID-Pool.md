---
title: "AD フォレストの回復 - RID プールを無効にします。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 2f5f84df-bd85-4ca4-bdd3-835bd1d45c11
ms.technology: identity-adfs
ms.openlocfilehash: cb024356ae5f872e93448d73ea54b271fe3fae4d
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="ad-forest-recovery---invalidating-the-current-rid-pool"></a>AD フォレストの回復 - 現在の RID プールを無効にします。  

>Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 の R2 を適用対象:

 ドメイン コントローラーでは、現在の RID プールを無効にするのにには、Windows PowerShell には、次の手順を使用します。 既定では、Windows Server 2012 と Windows Server 2008 R2、Windows Server 2008 いないを使用してインストールする必要がありますが、Windows PowerShell が有効になっている**機能の追加**します。 できます[ダウンロード](https://www.microsoft.com/download/details.aspx?id=20020)で Windows Server 2003 を実行します。  
  
 イベント ID 16654、コマンドが正常に完了したことを確認するには確認 (ソースはディレクトリ-サービス-SAM) イベント ビューアーの Windows Server 2012 でのシステム ログにします。 以前のバージョンの Windows では、このイベントはログオンできません。  
  
> [!NOTE]
>  RID プールを無効にした後に最初にしようとするセキュリティ プリンシパル (ユーザー、コンピューター、またはグループ) を作成するときに、エラーが表示されます。 オブジェクトを作成しようとすると、新しい RID プールの要求がトリガーされます。 新しい RID プールが割り当てられるために、操作の再試行が成功します。  
  
## <a name="to-invalidate-the-current-rid-pool"></a>現在の RID プールを無効にするには  
  
1.  管理者特権の Windows PowerShell セッションを開き、次のコマンドを実行 Enter キーを押します。  
  
    ```  
    $Domain = New-Object System.DirectoryServices.DirectoryEntry  
    $DomainSid = $Domain.objectSid  
    $RootDSE = New-Object System.DirectoryServices.DirectoryEntry("LDAP://RootDSE")  
    $RootDSE.UsePropertyCache = $false  
    $RootDSE.Put("invalidateRidPool", $DomainSid.Value)  
    $RootDSE.SetInfo()  
    ```  
  
## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md)
