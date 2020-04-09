---
ms.assetid: 0379abc3-25c7-46ab-9a6b-80a5152365b0
title: AD FS でのカスタム Web テーマ
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 69255eeaecd3e5198054242c1ab6dd1d0a58ce33
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80816425"
---
# <a name="custom-web-themes-in-ad-fs"></a>AD FS でのカスタム Web テーマ 

\-ボックス\-の\-出荷されるテーマは、Default と呼ばれます。 既定のテーマをエクスポートして使用すると、カスタマイズを簡単に開始できます。 カスタマイズできるのは外観と動作です.css ファイルを変更してレイアウトを調整し、変更済みの新しいテーマをインポートして適用すると、カスタマイズされた外観と動作を使用できるようになります。 .css ファイルを使用することで、Web デザイナーとの共同作業も容易になります。  
  
次のコマンドレットを実行すると、既定の Web テーマを複製してカスタム Web テーマが作成されます。  
  
  
`New-AdfsWebTheme –Name custom –SourceName default ` 

  
既存の .css ファイルを変更したり、新しい .css ファイルを使用して新しい Web テーマを構成したりできます。 Web テーマをエクスポートするには、次のコマンドレットを使用します。  
  

    Export-AdfsWebTheme –Name default –DirectoryPath c:\theme  

  
.css ファイルを新しいテーマに適用するには、次のコマンドレットを使用します。  
  

    Set-AdfsWebTheme –TargetName custom –StyleSheet @{path="c:\NewTheme.css"}  
  
  
新しいスタイル シートからカスタム Web テーマを作成するには、次のコマンドレットを使用します。  
  
  
`New-AdfsWebTheme –Name custom –StyleSheet @{path="c:\NewTheme.css"} –RTLStyleSheetPath c:\NewRtlTheme.css ` 
  
  
  
AD FS にカスタム web テーマを適用するには、次のコマンドレットを使用します。  
  

`Set-AdfsWebConfig -ActiveThemeName custom`  

  
JavaScript を AD FS に追加するには、次のコマンドレットを使用します。  
  
 
    Set-AdfsWebTheme -TargetName custom -AdditionalFileResource @{Uri=' /adfs/portal/script/onload.js';path="D:\inetpub\adfsassets\script\onload.js"}  


## <a name="additional-references"></a>その他の参照情報 
[AD FS ユーザーサインインのカスタマイズ](AD-FS-user-sign-in-customization.md)  
