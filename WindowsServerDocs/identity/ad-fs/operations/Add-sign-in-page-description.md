---
ms.assetid: 330c7b61-dde0-432f-9b74-d250ad9cc808
title: Add sign @ no__t-0in page description
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 3b34a4e54aebd5b9dc3655eecd770a25f7ea97cf
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407743"
---
# <a name="add-sign-in-page-description"></a>Add sign @ no__t-0in page description


## <a name="to-add-sign-in-page-description"></a>ページの説明に sign @ no__t-0in 追加するには  
ページの説明に sign @ no__t を追加するには、次の Windows PowerShell コマンドレットと構文を使用します。  

![サインインの説明の追加](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)

    Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in to Contoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>" 
 
  
> [!IMPORTANT]  
> `SignInPageDescriptionText` パラメーターの文字列では、タグ付きまたはタグなしのピュア HTML がサポートされています。 したがって、次のコマンドレットを実行するには、&lt;p @ no__t のタグを使用する必要があります。  `Set-AdfsGlobalWebContent -SignInPageDescriptionText "Sign-in to Contoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information." ` 

[Sign @ no__t-0in] ページをカスタマイズすると、カスタマイズが優先されます。そのため、サポートするすべての言語でをカスタマイズする必要があります。 すべてのカスタマイズ コンテンツには、ロケール パラメーターが設定されます。 ローカライズされたコンテンツを構成する場合は、"en" のように、country と region を構成する前に、"en" などの国の @ no__t-0less ロケールで構成する必要があります。  

## <a name="additional-references"></a>その他の参照情報 
[AD FS ユーザーサインインのカスタマイズ](AD-FS-user-sign-in-customization.md)  
