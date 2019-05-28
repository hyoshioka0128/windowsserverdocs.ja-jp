---
ms.assetid: 1ca6f87f-7272-4767-b609-3e295ac7d32f
title: プライバシー リンクの追加
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3617335a179ab419982ab57343999ad4fcaf522a
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190163"
---
# <a name="add-privacy-link"></a>プライバシー リンクの追加 


サインインに表示されるプライバシー リンクを追加する\- ページで、次の Windows PowerShell コマンドレットと構文を使用します。  

![プライバシー リンクを追加します。](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png) 
  
 
`Set-AdfsGlobalWebContent -PrivacyLink https://fs1.contoso.com/privacy/ -PrivacyLinkText Privacy`  
 
  
> [!IMPORTANT]  
> このコマンドレットの `linkText` パラメーターは、既定値である *Privacy* を使用する場合は必要ありません。 既定値には、すべてのクライアント ロケールでページがローカライズ済みであるという利点があります。 記号の後\- ページでは、カスタマイズすると、カスタマイズ設定が優先されるため、サポートするすべての言語の情報をカスタマイズする必要があります。 すべてのカスタマイズ コンテンツには、ロケール パラメーターが設定されます。 ローカライズされたコンテンツを構成するときに、国を構成する必要があります\-少ないロケール最初に、たとえば、"en"、country と region を構成する前に\-特定のロケールなど"en\-私たち"です。  

## <a name="additional-references"></a>その他の参照情報 
[AD FS のユーザー サインイン カスタマイズ](AD-FS-user-sign-in-customization.md)  
