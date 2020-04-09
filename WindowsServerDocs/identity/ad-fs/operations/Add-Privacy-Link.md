---
ms.assetid: 1ca6f87f-7272-4767-b609-3e295ac7d32f
title: プライバシー リンクの追加
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: cf111fbfc14665d489201f7d88419bdeffb737f9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859395"
---
# <a name="add-privacy-link"></a>プライバシー リンクの追加 


[\-のサインイン] ページに表示されるプライバシーリンクを追加するには、次の Windows PowerShell コマンドレットと構文を使用します。  

![プライバシーリンクの追加](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png) 
  
 
`Set-AdfsGlobalWebContent -PrivacyLink https://fs1.contoso.com/privacy/ -PrivacyLinkText Privacy`  
 
  
> [!IMPORTANT]  
> このコマンドレットの `linkText` パラメーターは、既定値である *Privacy* を使用する場合は必要ありません。 既定値には、すべてのクライアント ロケールでページがローカライズ済みであるという利点があります。 ページの [\-の署名] がカスタマイズされると、カスタマイズが優先されます。そのため、サポートするすべての言語でをカスタマイズする必要があります。 すべてのカスタマイズ コンテンツには、ロケール パラメーターが設定されます。 ローカライズされたコンテンツを構成する場合は、"en\-us" などの特定のロケール\-国と地域を構成する前に、最初に "en" などの国\-小さいロケールで構成する必要があります。  

## <a name="additional-references"></a>その他の参照情報 
[AD FS ユーザーサインインのカスタマイズ](AD-FS-user-sign-in-customization.md)  
