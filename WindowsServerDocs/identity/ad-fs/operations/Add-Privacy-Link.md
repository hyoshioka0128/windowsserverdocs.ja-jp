---
ms.assetid: 1ca6f87f-7272-4767-b609-3e295ac7d32f
title: プライバシー リンクの追加
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: c0e65053529999b8463223f7654b357464b90642
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954278"
---
# <a name="add-privacy-link"></a>プライバシー リンクの追加


サインインページに表示されるプライバシーリンクを追加するには、 \- 次の Windows PowerShell コマンドレットと構文を使用します。

![プライバシーリンクの追加](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)


`Set-AdfsGlobalWebContent -PrivacyLink https://fs1.contoso.com/privacy/ -PrivacyLinkText Privacy`


> [!IMPORTANT]
> このコマンドレットの `linkText` パラメーターは、既定値である *Privacy* を使用する場合は必要ありません。 既定値には、すべてのクライアント ロケールでページがローカライズ済みであるという利点があります。 サインインページをカスタマイズすると、 \- カスタマイズが優先されるため、サポートするすべての言語に合わせてカスタマイズする必要があります。 すべてのカスタマイズ コンテンツには、ロケール パラメーターが設定されます。 ローカライズされたコンテンツを構成する場合は、最初に "en" などの国のロケールを使用しないように構成して \- から、国と地域 \- に固有のロケール ("en-us" など) を構成する必要があり \- ます。

## <a name="additional-references"></a>その他の参照情報
[AD FS ユーザーサインインのカスタマイズ](AD-FS-user-sign-in-customization.md)
