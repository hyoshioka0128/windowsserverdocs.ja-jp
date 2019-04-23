---
ms.assetid: 2bac7744-9de3-491a-b0a2-4e843cec7344
title: ヘルプ デスク リンクの追加
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 1654add6a81169b3d4831d6ebba320402e0734c5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849863"
---
# <a name="add-help-desk-link"></a>ヘルプ デスク リンクの追加 

>適用先:Windows Server 2016、Windows Server 2012 R2


## <a name="to-add-a-help-desk-link"></a>ヘルプ デスク リンクを追加するには  
符号に表示されるヘルプ デスク リンクを追加する\- ページで、次の Windows PowerShell コマンドレットと構文を使用します。  

![ヘルプ デスクを追加します。](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)
  

`Set-AdfsGlobalWebContent -HelpDeskLink https://fs1.contoso.com/help/ -HelpDeskLinkText Help`  
 
  
> [!IMPORTANT]  
> このコマンドレットの `linkText` パラメーターは、既定値である *Help* を使用する場合は必要ありません。 既定値には、すべてのクライアント ロケールでローカライズ済みであるという利点があります。 ページをカスタマイズすると、カスタマイズ設定が優先されるため、サポートするすべての言語でページをカスタマイズする必要があります。  


## <a name="additional-references"></a>その他の参照情報 
[AD FS のユーザー サインイン カスタマイズ](AD-FS-user-sign-in-customization.md)  
