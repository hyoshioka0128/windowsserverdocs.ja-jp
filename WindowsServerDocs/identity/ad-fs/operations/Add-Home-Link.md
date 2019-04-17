---
ms.assetid: da035189-e87f-4597-9933-49bf391a8d5d
title: "ホーム リンクを追加します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: fb903c62e717e36099934e64e1c939a502f691a3
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="add-home-link"></a>ホーム リンクを追加します。 

>適用対象: Windows Server 2016、Windows Server 2012 R2

サインイン ページに表示されるホーム リンクを追加するには、次の Windows PowerShell コマンドレットと構文を使用します。 


![ホーム リンクを追加します。](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png) 
  

`Set-AdfsGlobalWebContent -HomeLink https://fs1.contoso.com/home/ -HomeLinkText Home ` 
 
  
> [!IMPORTANT]  
> `linkText`このコマンドレットのパラメーターは、これは、既定値を使用する場合は必要ありません*ホーム*します。 既定値を使用する利点は、すべてのクライアント ロケールにローカライズされます。 サインイン ページをカスタマイズすると、カスタマイズ設定が優先されます。そのため、すべての言語をサポートするでカスタマイズする必要があります。

## <a name="additional-references"></a>その他の参照 
[AD FS のユーザーのサインイン カスタマイズ](AD-FS-user-sign-in-customization.md)  
