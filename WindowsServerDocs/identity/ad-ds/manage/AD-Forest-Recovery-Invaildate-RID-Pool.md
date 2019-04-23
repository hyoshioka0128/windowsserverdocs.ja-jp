---
title: AD フォレストの回復の RID プールを無効化
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 2f5f84df-bd85-4ca4-bdd3-835bd1d45c11
ms.technology: identity-adds
ms.openlocfilehash: 46115991e48da301a8a739009bac27415ebe73df
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842513"
---
# <a name="ad-forest-recovery---invalidating-the-current-rid-pool"></a>AD フォレストの回復 - 現在の RID プールを無効化  

>適用先:Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 R2

ドメイン コント ローラー上の現在の RID プールを無効にするのにには、Windows PowerShell に次の手順を使用します。 既定では Windows Server 2012 と Windows Server 2008 R2、Windows Server 2008 いないを使用してインストールする必要がありますで Windows PowerShell が有効になっている**機能の追加**します。 できます[ダウンロード](https://www.microsoft.com/download/details.aspx?id=20020)で Windows Server 2003 を実行します。  

イベント ID 16654、コマンドが正常に完了したことを確認するには確認 (ソースはディレクトリ-サービス-SAM) Windows Server 2012 でのイベント ビューアーのシステム ログにします。 Windows の以前のバージョンでは、このイベントは記録しません。  
  
> [!NOTE]
> RID プールを無効にした後に最初にセキュリティ プリンシパル (ユーザー、コンピューター、またはグループ) の作成を試行するときに、エラーを受け取ります。 オブジェクトを作成する試みは、新しい RID プール要求をトリガーします。 新しい RID プールが割り当てられるために、操作の再試行が成功します。  
  
## <a name="to-invalidate-the-current-rid-pool"></a>現在の RID プールを無効にするには  
  
- 管理者特権の Windows PowerShell セッションを開き、次のコマンドを実行 ENTER キーを押します。  

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
- [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md)
