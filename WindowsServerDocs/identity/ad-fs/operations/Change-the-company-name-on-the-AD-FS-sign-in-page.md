---
ms.assetid: 28043fc4-a34d-4710-ac3b-5c9d4d6a895c
title: "AD FS サインイン ページで、会社名を変更します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 8e99f6fed8922ed15bf78a98b207b6f46767763a
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="change-the-company-name-on-the-ad-fs-sign-in-page"></a>AD FS サインイン ページで、会社名を変更します。

>適用対象: Windows Server 2016、Windows Server 2012 R2
 
サインイン ページに表示される会社の名前を変更するには、次の Windows PowerShell の PowerShell コマンドレットと構文を使用します。 この値は、セットアップ中に入力したフェデレーション サービス表示名から値を使用して既定で設定されます。  

![名前を変更します。](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom1.png)
  
  
    Set-AdfsGlobalWebContent –CompanyName "Contoso Corp"  
 
  
> [!NOTE]  
> また、会社名を変更するのに Windows PowerShell Integrated Scripting Environment \(ISE\) を使用することができます。 Windows PowerShell ISE を使用すると、ユニコード準拠の環境でコンテンツを表示することができます。 詳細については、次を参照してください。 [Windows PowerShell ISE の紹介](https://technet.microsoft.com/library/dd315244.aspx)します。  

## <a name="additional-references"></a>その他の参照 
[AD FS のユーザーのサインイン カスタマイズ](AD-FS-user-sign-in-customization.md)  
  
