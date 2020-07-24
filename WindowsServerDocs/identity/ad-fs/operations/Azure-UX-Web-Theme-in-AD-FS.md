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
ms.openlocfilehash: ce9bddbc9b03a9019860e9b831bb928326098b76
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86965954"
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
3. Powershell を使用して新しいテーマをアクティブテーマとして設定する: `Set-AdfsWebConfig -ActiveThemeName custom` 
    ![ powershell](media/Azure-UX-Web-Theme-in-AD-FS/two.png)
4. Https:// <AD FS name.domain> /adfs/ls/idpinitiatedsignon.htm サインオンにアクセスして、サインインをテストします。 ![](media/Azure-UX-Web-Theme-in-AD-FS/three.png)

> !付箋Idpinitiatedsignon.aspx オンが有効になっていることを確認する必要があります。  これは、既定では有効になっていません。  Idpinitiatedsignon.aspx オンを有効にするには、次の PowerShell コマンドを使用します。`Set-AdfsProperties –EnableIdpInitiatedSignonPage $True`

## <a name="image-recommendations"></a>イメージに関する推奨事項
中央の UI を有効にすると、Azure Active Directory 会社のブランド化に既に使用しているのと同じイメージを背景とロゴに使用することができます。 通常、サイズ、比率、および形式についても同じ推奨事項が適用されます。

### <a name="logo"></a>ロゴ

説明 | 制約 | 推奨事項
------- | ------- | ----------
ロゴは、[ログイン] パネルの上部に表示されます。 | 透過 JPG または透過 PNG<br>高さの最大値: 36 ピクセル<br>幅の最大値: 245 ピクセル | ここで組織のロゴを使用します。<br>透過画像を使用してください。 背景が白であることを想定しないでください。<br>画像のロゴの周囲にパディングを追加しないでください。追加すると、ロゴが過度に小さくなります。

### <a name="background"></a>バックグラウンド

説明 | 制約 | 推奨事項
------- | ------- | ----------
このオプションは、サインイン ページの背景に表示され、表示可能な領域の中央に固定されて、ブラウザー ウィンドウを埋めるように拡大縮小またはトリミングされます。    <br>携帯電話のように小さい画面では、この画像は表示されません。<br>ページが読み込まれるときに、不透明度 0.55 の黒いマスクがこの画像に適用されます。 | JPG または PNG<br>画像サイズ: 1920 x 1080 ピクセル<br>ファイル サイズ: &lt; 300 KB | <br>強調して表示したいものが集中していない場所でこの画像を使用します。 非透過のサインイン フォームがこの画像の中央に覆いかぶさるように表示され、ブラウザー ウィンドウのサイズに応じて画像の一部を覆うことができます。<br>ファイル サイズを小さいままにして、読み込み時間を短縮します。

## <a name="next-steps"></a>次の手順
- [Windows Server 2016 での AD FS のカスタマイズ](./ad-fs-customization-in-windows-server.md)
- [高度なカスタマイズ](Advanced-Customization-of-AD-FS-Sign-in-Pages.md)
- [カスタム web テーマ](Custom-Web-Themes-in-AD-FS.md)
