---
ms.assetid: 1ca6f87f-7272-4767-b609-3e295ac7d32f
title: プライバシー リンクの追加
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: cd559e38c38e96d1417257fe7d6ff8ccfa180c6b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358421"
---
# <a name="add-privacy-link"></a>プライバシー リンクの追加 


[Sign @ no__t] ページに表示されるプライバシーリンクを追加するには、次の Windows PowerShell コマンドレットと構文を使用します。  

![プライバシーリンクの追加](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png) 
  
 
`Set-AdfsGlobalWebContent -PrivacyLink https://fs1.contoso.com/privacy/ -PrivacyLinkText Privacy`  
 
  
> [!IMPORTANT]  
> このコマンドレットの `linkText` パラメーターは、既定値である *Privacy* を使用する場合は必要ありません。 既定値には、すべてのクライアント ロケールでページがローカライズ済みであるという利点があります。 [Sign @ no__t-0in] ページをカスタマイズすると、カスタマイズが優先されます。そのため、サポートするすべての言語でをカスタマイズする必要があります。 すべてのカスタマイズ コンテンツには、ロケール パラメーターが設定されます。 ローカライズされたコンテンツを構成する場合は、"en" のように、country および region @ no__t 固有のロケール ("en @ no__t-2us" など) を構成する前に、まず country @ no__t-0less ロケールで構成する必要があります。  

## <a name="additional-references"></a>その他の参照情報 
[AD FS ユーザーサインインのカスタマイズ](AD-FS-user-sign-in-customization.md)  
