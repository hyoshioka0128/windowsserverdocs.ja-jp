---
title: AD FS での UX Web テーマの Azure AD
description: 次のドキュメントでは、Azure AD ユーザーエクスペリエンスに似た AD FS フォームサインインを変更する方法について説明します。
author: billmath
ms.author: billmath
manager: femila
ms.date: 10/24/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: f4dd1d45646475be3788cd6b615b1743976eedae
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358414"
---
# <a name="using-an-azure-ad-ux-web-theme-in-active-directory-federation-services"></a>Active Directory フェデレーションサービス (AD FS) での Azure AD UX Web テーマの使用
現在、AD FS フォームのサインインでは、Azure/O365 サインインエクスペリエンスは反映されません。  エンドユーザーに対してより一貫したシームレスなエクスペリエンスを提供するために、次のカスケードスタイルシートの web テーマをリリースしました。これは、AD FS サーバーに適用できます。  現時点では、Windows Server 2016 での AD FS のフォームサインインは次のようになります。

![現在のサインイン](media/Azure-UX-Web-Theme-in-AD-FS/one.png)


新しいスタイルシートでは、ユーザーエクスペリエンスは Azure と Office 365 サインインエクスペリエンスのようになります。

## <a name="download-the-css-style-sheet"></a>CSS スタイルシートをダウンロードする
Web テーマは、次の Github の[場所](https://github.com/Microsoft/adfsWebCustomization/tree/master/centeredUi)からダウンロードできます。


## <a name="enabling-the-new-web-theme"></a>新しい web テーマを有効にする
新しい web テーマを有効にするには、次の手順を使用します。

### <a name="to-enable-the-new-azure-ad-ux-web-theme-in-ad-fs"></a>で新しい Azure AD UX web テーマを有効にするには AD FS
1. 管理者として PowerShell を起動する
2. PowerShell を使用して新しい web テーマを作成する:`New-AdfsWebTheme –Name custom –StyleSheet @{path="c:\NewTheme.css"}`
3. PowerShell を使用して、新しいテーマをアクティブテーマとして設定します。`Set-AdfsWebConfig -ActiveThemeName custom`
   ![PowerShell](media/Azure-UX-Web-Theme-in-AD-FS/two.png)
4. Https://<AD FS name.domain>/adfs/ls/idpinitiatedsignon.htm ![サインオンにアクセスして、サインインをテストします。](media/Azure-UX-Web-Theme-in-AD-FS/three.png)

> !付箋Idpinitiatedsignon.aspx オンが有効になっていることを確認する必要があります。  既定では有効になっていません。  Idpinitiatedsignon.aspx オンを有効にするには、次の PowerShell コマンドを使用します。`Set-AdfsProperties –EnableIdpInitiatedSignonPage $True`

## <a name="image-recommendations"></a>イメージに関する推奨事項
中央の UI を有効にすると、Azure Active Directory 会社のブランド化に既に使用しているのと同じイメージを背景とロゴに使用することができます。 通常、サイズ、比率、および形式についても同じ推奨事項が適用されます。

### <a name="logo"></a>ロゴ

説明 | 制約 | 推奨事項
------- | ------- | ----------
ロゴは、[ログイン] パネルの上部に表示されます。 | 透明な JPG または PNG<br>高さの最大値:36 px<br>最大幅:245 px | ここで組織のロゴを使用します。<br>透過的な画像を使用します。 背景が白であることを想定しないでください。<br>画像のロゴの周囲にパディングを追加しないでください。そうしないと、ロゴが過度に小さくなります。

### <a name="background"></a>背景情報

説明 | 制約 | 推奨事項
------- | ------- | ----------
このオプションは、サインインページの背景に表示され、表示可能な領域の中央に固定されます。また、ブラウザーウィンドウに合わせて拡大縮小し、トリミングします。    <br>携帯電話などの狭い画面では、この画像は表示されません。<br>ページが読み込まれるときに、不透明度が0.55 のブラックマスクがこのイメージに適用されます。 | JPG または PNG<br>画像の大きさ:1920 x 1080 px<br>ファイルサイズ:&lt;300 KB | <br>厳密な件名のフォーカスがないイメージを使用します。 不透明なサインインフォームは、このイメージの中央に表示され、ブラウザーウィンドウのサイズによっては、イメージの任意の部分に対応できます。<br>高速な読み込み時間を確保するために、ファイルサイズを小さくしておきます。

## <a name="next-steps"></a>次の手順
- [Windows Server 2016 での AD FS のカスタマイズ](AD-FS-Customization-in-Windows-Server-2016.md)
- [高度なカスタマイズ](Advanced-Customization-of-AD-FS-Sign-in-Pages.md)
- [カスタム web テーマ](Custom-Web-Themes-in-AD-FS.md)
