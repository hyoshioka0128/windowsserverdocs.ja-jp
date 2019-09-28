---
title: AD フォレストの回復-RID プールを無効にする
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 2f5f84df-bd85-4ca4-bdd3-835bd1d45c11
ms.technology: identity-adds
ms.openlocfilehash: c3c477e21a455e5e5777da00b064ca7a02672571
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71390412"
---
# <a name="ad-forest-recovery---invalidating-the-current-rid-pool"></a>AD フォレストの回復-現在の RID プールを無効にする  

>適用先:Windows Server 2016、Windows Server 2012、および 2012 R2、Windows Server 2008 および 2008 R2

Windows PowerShell を使用して、ドメインコントローラーの現在の RID プールを無効にするには、次の手順を使用します。 Windows PowerShell は、windows server 2012 および Windows Server 2008 R2 では既定で有効になっていますが、Windows Server 2008 では、 **[機能の追加]** を使用してインストールする必要があります。 Windows Server 2003 で実行するために[ダウンロード](https://www.microsoft.com/download/details.aspx?id=20020)できます。  

コマンドが正常に完了したことを確認するには、Windows Server 2012 のイベントビューアーシステムログで、イベント ID 16654 (ソースがディレクトリサービス-SAM) であることを確認します。 以前のバージョンの Windows では、このイベントはログに記録されません。  
  
> [!NOTE]
> RID プールを無効にした後、セキュリティプリンシパル (ユーザー、コンピューター、またはグループ) を最初に作成しようとすると、エラーが表示されます。 オブジェクトを作成しようとすると、新しい RID プールの要求がトリガーされます。 新しい RID プールが割り当てられるため、操作の再試行は成功します。  
  
## <a name="to-invalidate-the-current-rid-pool"></a>現在の RID プールを無効にするには  
  
- 管理者特権の Windows PowerShell セッションを開き、次のコマンドを実行して enter キーを押します。  

   ```powershell
   $Domain = New-Object System.DirectoryServices.DirectoryEntry  
   $DomainSid = $Domain.objectSid  
   $RootDSE = New-Object System.DirectoryServices.DirectoryEntry("LDAP://RootDSE")  
   $RootDSE.UsePropertyCache = $false  
   $RootDSE.Put("invalidateRidPool", $DomainSid.Value)  
   $RootDSE.SetInfo()  
   ```  

## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復 - 手順](AD-Forest-Recovery-Procedures.md)
