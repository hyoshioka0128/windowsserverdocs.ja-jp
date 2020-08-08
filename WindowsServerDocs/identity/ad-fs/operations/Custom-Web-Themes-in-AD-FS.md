---
ms.assetid: 0379abc3-25c7-46ab-9a6b-80a5152365b0
title: AD FS でのカスタム Web テーマ
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 99ea2ef8d2a4fca6733b5d314ab138adb55277aa
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87956409"
---
# <a name="custom-web-themes-in-ad-fs"></a>AD FS でのカスタム Web テーマ

\- \- 既定と呼ばれるのは、そのまま出荷されるテーマです \- 。 既定のテーマをエクスポートして使用すると、カスタマイズを簡単に開始できます。 カスタマイズできるのは外観と動作です。.css ファイルを変更してレイアウトを調整し、変更済みの新しいテーマをインポートして適用すると、カスタマイズされた外観と動作を使用できるようになります。 .css ファイルを使用することで、Web デザイナーとの共同作業も容易になります。

次のコマンドレットを実行すると、既定の Web テーマを複製してカスタム Web テーマが作成されます。

```powershell
New-AdfsWebTheme –Name custom –SourceName default
```

既存の .css ファイルを変更したり、新しい .css ファイルを使用して新しい Web テーマを構成したりできます。 Web テーマをエクスポートするには、次のコマンドレットを使用します。

```powershell
Export-AdfsWebTheme –Name default –DirectoryPath c:\theme
```

.css ファイルを新しいテーマに適用するには、次のコマンドレットを使用します。

```powershell
Set-AdfsWebTheme –TargetName custom –StyleSheet @{path="c:\NewTheme.css"}
```

新しいスタイル シートからカスタム Web テーマを作成するには、次のコマンドレットを使用します。

```powershell
New-AdfsWebTheme –Name custom –StyleSheet @{path="c:\NewTheme.css"} –RTLStyleSheetPath c:\NewRtlTheme.css
```

AD FS にカスタム web テーマを適用するには、次のコマンドレットを使用します。

```powershell
Set-AdfsWebConfig -ActiveThemeName custom
```

JavaScript を AD FS に追加するには、次のコマンドレットを使用します。

```powershell
Set-AdfsWebTheme -TargetName custom -AdditionalFileResource @{Uri=' /adfs/portal/script/onload.js';path="D:\inetpub\adfsassets\script\onload.js"}
```

## <a name="additional-references"></a>その他の参照情報

[AD FS ユーザーサインインのカスタマイズ](AD-FS-user-sign-in-customization.md)
