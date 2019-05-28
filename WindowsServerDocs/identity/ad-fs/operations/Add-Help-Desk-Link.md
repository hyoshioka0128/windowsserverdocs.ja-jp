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
ms.openlocfilehash: fb186c3ba5cfb3acb9bfd0c3139b09b992fb8863
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190209"
---
# <a name="add-help-desk-link"></a>ヘルプ デスク リンクの追加 


## <a name="to-add-a-help-desk-link"></a>ヘルプ デスク リンクを追加するには  
符号に表示されるヘルプ デスク リンクを追加する\- ページで、次の Windows PowerShell コマンドレットと構文を使用します。  

![ヘルプ デスクを追加します。](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)
  

`Set-AdfsGlobalWebContent -HelpDeskLink https://fs1.contoso.com/help/ -HelpDeskLinkText Help`  
 
  
> [!IMPORTANT]  
> このコマンドレットの `linkText` パラメーターは、既定値である *Help* を使用する場合は必要ありません。 既定値には、すべてのクライアント ロケールでローカライズ済みであるという利点があります。 ページをカスタマイズすると、カスタマイズ設定が優先されるため、サポートするすべての言語でページをカスタマイズする必要があります。  


## <a name="additional-references"></a>その他の参照情報 
[AD FS のユーザー サインイン カスタマイズ](AD-FS-user-sign-in-customization.md)  
