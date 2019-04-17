---
ms.assetid: 2bac7744-9de3-491a-b0a2-4e843cec7344
title: "ヘルプ デスク リンクを追加します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 6d16cc0a75bfe636c29b44687b669e87f31b69ce
ms.sourcegitcommit: 76e57a5453d6ee9a04dcff6a8cca087132cb1d5f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2018
---
# <a name="add-help-desk-link"></a>ヘルプ デスク リンクを追加します。 

>適用対象: Windows Server 2016、Windows Server 2012 R2


## <a name="to-add-a-help-desk-link"></a>ヘルプ デスク リンクを追加するには  
サインイン ページに表示されるヘルプ デスク リンクを追加するには、次の Windows PowerShell の PowerShell コマンドレットと構文を使用します。  

![ヘルプ デスクを追加します。](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)
  

`Set-AdfsGlobalWebContent -HelpDeskLink https://fs1.contoso.com/help/ -HelpDeskLinkText Help`  
 
  
> [!IMPORTANT]  
> `linkText`このコマンドレットのパラメーターは、これは、既定値を使用する場合は必要ありません*ヘルプ*します。 既定値を使用する利点は、すべてのクライアント ロケールにローカライズされます。 ページをカスタマイズすると、カスタマイズ設定が優先されます。そのため、すべての言語をサポートするでカスタマイズする必要があります。  


## <a name="additional-references"></a>その他の参照 
[AD FS のユーザーのサインイン カスタマイズ](AD-FS-user-sign-in-customization.md)  
