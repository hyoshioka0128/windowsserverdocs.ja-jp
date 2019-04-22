---
ms.assetid: da035189-e87f-4597-9933-49bf391a8d5d
title: ホーム リンクの追加
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: fb903c62e717e36099934e64e1c939a502f691a3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823013"
---
# <a name="add-home-link"></a>ホーム リンクの追加 

>適用先:Windows Server 2016、Windows Server 2012 R2

サインインに表示されるホーム リンクを追加する\- ページで、次の Windows PowerShell コマンドレットと構文を使用します。 


![ホーム リンクを追加します。](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png) 
  

`Set-AdfsGlobalWebContent -HomeLink https://fs1.contoso.com/home/ -HomeLinkText Home ` 
 
  
> [!IMPORTANT]  
> このコマンドレットの `linkText` パラメーターは、既定値である *Home*を使用する場合は必要ありません。 既定値には、すべてのクライアント ロケールでローカライズ済みであるという利点があります。 記号の後\- ページでは、カスタマイズすると、カスタマイズ設定が優先されるため、サポートするすべての言語の情報をカスタマイズする必要があります。

## <a name="additional-references"></a>その他の参照情報 
[AD FS のユーザー サインイン カスタマイズ](AD-FS-user-sign-in-customization.md)  
