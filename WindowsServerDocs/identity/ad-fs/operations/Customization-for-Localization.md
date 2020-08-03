---
ms.assetid: 38bbc002-a8fa-4211-9328-4ef67fca0acf
title: ローカライズのカスタマイズ
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: a0fb1e286e4b6479a95114fd8d2ad90ffa57b7c8
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2020
ms.locfileid: "87519751"
---
# <a name="customization-for-localization"></a>ローカライズのカスタマイズ

Web コンテンツを英語以外の言語にローカライズできます。 ローカライズを行う場合は、次の考慮事項に注意してください。

コンテンツをカスタマイズすると、カスタマイズ設定が優先されるため、サポートするすべての言語でコンテンツをカスタマイズする必要があります。 すべてのカスタマイズ コンテンツには、ロケール パラメーターが設定されます。 ローカライズされたコンテンツを構成する場合は、"en" など \- の国と地域に固有のロケールを構成する前に、最初に "en" などの国のロケールで構成し \- \- ます。

追加のコード例を次に示します。

```powershell
Set-AdfsWebTheme -TargetName default -Logo @{Locale="";Path="c:\contoso.png"}
Set-AdfsWebTheme -TargetName default -Illustration @{Locale="";Path="c:\illustration.png"}
```

追加のコード例を次に示します。

```powershell
Set-AdfsGlobalWebContent -ErrorPageDescriptionText "This is Contoso's error page description" –locale "en"

Set-AdfsGlobalWebContent -ErrorPageDescriptionText "Il s'agit de description de page erreur de Contoso" –locale "fr"
```

Unicode の入力が必要な英語以外の言語に web コンテンツをカスタマイズする場合は、Windows PowerShell ISE を使用することをお勧めします。 詳細について[は、「Windows PowerShell ISE の概要](/previous-versions/mt707506(v=msdn.10))」を参照してください。

## <a name="additional-references"></a>その他のリファレンス

[AD FS ユーザーサインインのカスタマイズ](AD-FS-user-sign-in-customization.md)
