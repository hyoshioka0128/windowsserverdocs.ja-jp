---
ms.assetid: 1ca6f87f-7272-4767-b609-3e295ac7d32f
title: "プライバシー リンクを追加します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 81a453b45693b8222bdfc0231885b506fdfcd2fc
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="add-privacy-link"></a>プライバシー リンクを追加します。 

>適用対象: Windows Server 2016、Windows Server 2012 R2

サインイン ページに表示されるプライバシー リンクを追加するには、次の Windows PowerShell コマンドレットと構文を使用します。  

![プライバシー リンクを追加します。](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png) 
  
 
`Set-AdfsGlobalWebContent -PrivacyLink https://fs1.contoso.com/privacy/ -PrivacyLinkText Privacy`  
 
  
> [!IMPORTANT]  
> `linkText`このコマンドレットのパラメーターは、これは、既定値を使用する場合は必要ありません*プライバシー*します。 既定値を使用する利点は、ページがすべてのクライアント ロケールにローカライズされています。 サインイン ページをカスタマイズすると、カスタマイズ設定が優先されます。そのため、すべての言語をサポートするでカスタマイズする必要があります。 すべてのカスタマイズ コンテンツは、ロケール パラメーターを受け取ります。 ローカライズされたコンテンツを構成するときにする必要がありますが構成され、country\ を含まないロケール最初に、たとえば、"en"国および region\ に固有のロケールをよう構成する前に"en\-ご"です。  

## <a name="additional-references"></a>その他の参照 
[AD FS のユーザーのサインイン カスタマイズ](AD-FS-user-sign-in-customization.md)  
