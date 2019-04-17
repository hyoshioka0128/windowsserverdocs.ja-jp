---
ms.assetid: 0379abc3-25c7-46ab-9a6b-80a5152365b0
title: "AD FS でのカスタム Web テーマ"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 300c9fda84285ddfc52a4f47ea0198deb6fd33ef
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="custom-web-themes-in-ad-fs"></a>AD FS でのカスタム Web テーマ 

>適用対象: Windows Server 2016、Windows Server 2012 R2

テーマは出荷 out\ of\-the\ のボックスには、既定は呼び出されます。 既定のテーマをエクスポートし、すばやく開始できるように使用できます。 外観と .css ファイルを変更することで、画面のレイアウトが含まれている動作をカスタマイズ、インポートし、新しいテーマを適用でき、カスタマイズされた外観と動作を使用します。 .Css ファイルを使用してもしやすく、Web デザイナーを使用します。  
  
次のコマンドレットは、既定の Web テーマを複製して、カスタム Web テーマを作成します。  
  
  
`New-AdfsWebTheme –Name custom –SourceName default ` 

  
.Css ファイルを変更して、新しい .css ファイルを使用して新しい Web テーマを構成することができます。 Web テーマをエクスポートするには、次のコマンドレットを使用します。  
  

    Export-AdfsWebTheme –Name default –DirectoryPath c:\theme  

  
.Css ファイルを新しいテーマに適用するには、次のコマンドレットを使用します。  
  

    Set-AdfsWebTheme –TargetName custom –StyleSheet @{path=”c:\NewTheme.css”}  
  
  
次のコマンドレットは、新しいスタイル シートからカスタム Web テーマを作成します。  
  
  
`New-AdfsWebTheme –Name custom –StyleSheet @{path=”c:\NewTheme.css”} –RTLStyleSheetPath c:\NewRtlTheme.css ` 
  
  
  
AD FS にカスタム Web テーマを適用するには、次のコマンドレットを使用します。  
  

`Set-AdfsWebConfig -ActiveThemeName custom`  

  
AD FS には、JavaScript を追加するには、次のコマンドレットを使用します。  
  
 
    Set-AdfsWebTheme -TargetName custom -AdditionalFileResource @{Uri=’ /adfs/portal/script/onload.js’;path="D:\inetpub\adfsassets\script\onload.js"}  


## <a name="additional-references"></a>その他の参照 
[AD FS のユーザーのサインイン カスタマイズ](AD-FS-user-sign-in-customization.md)  
