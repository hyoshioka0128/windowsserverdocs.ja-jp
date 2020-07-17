---
ms.assetid: da035189-e87f-4597-9933-49bf391a8d5d
title: ホーム リンクの追加
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: f4a6210b1b7475a4ec34bbe0575915f376381fe1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859385"
---
# <a name="add-home-link"></a>ホーム リンクの追加 

[\-のサインイン] ページに表示されるホームリンクを追加するには、次の Windows PowerShell コマンドレットと構文を使用します。 


![ホームリンクの追加](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png) 
  

`Set-AdfsGlobalWebContent -HomeLink https://fs1.contoso.com/home/ -HomeLinkText Home ` 
 
  
> [!IMPORTANT]  
> このコマンドレットの `linkText` パラメーターは、既定値である *Home* を使用する場合は必要ありません。 既定値には、すべてのクライアント ロケールでローカライズ済みであるという利点があります。 ページの [\-の署名] がカスタマイズされると、カスタマイズが優先されます。そのため、サポートするすべての言語でをカスタマイズする必要があります。

## <a name="additional-references"></a>その他の参照情報 
[AD FS ユーザーサインインのカスタマイズ](AD-FS-user-sign-in-customization.md)  
