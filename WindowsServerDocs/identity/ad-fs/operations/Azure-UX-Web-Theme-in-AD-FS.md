---
title: AD FS での azure AD の UX Web テーマ
description: 次のドキュメントでは、Azure AD のユーザー エクスペリエンスのように、AD FS フォーム サインインを変更する方法について説明します。
author: billmath
ms.author: billmath
manager: femila
ms.date: 10/24/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 8d6afd7829c92382815e95b8c43a054b000359e2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887883"
---
# <a name="using-an-azure-ad-ux-web-theme-in-active-directory-federation-services"></a>Active Directory フェデレーション サービスで Azure AD のユーザー エクスペリエンスの Web テーマを使用します。
AD FS サインインのフォームで現在はミラー化は、Azure または O365 のサインイン エクスペリエンス。  エンドユーザー向けのより同型でシームレスなエクスペリエンスを提供するには、に従ってカスケード スタイル シートの web テーマ、AD FS サーバーに適用できるをリリースしました。  現時点では、フォーム サインインが次のような Windows Server 2016 の AD FS の:

![現在のサインイン](media/Azure-UX-Web-Theme-in-AD-FS/one.png)


新しいスタイル シートを使用してユーザー エクスペリエンスが Azure および Office 365 サインイン エクスペリエンスのようになります。

## <a name="download-the-css-style-sheet"></a>CSS スタイル シートをダウンロードします。
Web テーマをダウンロードするには次の Github から[場所](https://github.com/Microsoft/adfsWebCustomization/tree/master/centeredUi)します。


## <a name="enabling-the-new-web-theme"></a>新しい web テーマを有効にします。
新しい web テーマを有効にするには、次の手順に従います。

### <a name="to-enable-the-new-azure-ad-ux-web-theme-in-ad-fs"></a>AD FS での新しい Azure AD の UX web テーマを有効にするには
1.  管理者として PowerShell を起動します。
2.  PowerShell を使用して新しい web テーマを作成します。  `New-AdfsWebTheme –Name custom –StyleSheet @{path="c:\NewTheme.css"}`
3.  PowerShell を使用してアクティブ テーマとして新しいテーマを設定します。`Set-AdfsWebConfig -ActiveThemeName custom`
![PowerShell](media/Azure-UX-Web-Theme-in-AD-FS/two.png)
4.  Https:// に移動してサインイン テスト<AD FS name.domain>/adfs/ls/idpinitiatedsignon.htm![サインオン](media/Azure-UX-Web-Theme-in-AD-FS/three.png)

> ![注]その idpinitiatedsignon を有効になっていることを確認する必要があります。  既定で無効です。  有効にするのには、idpinitiatedsignon は、次の PowerShell コマンドを使用します。  `Set-AdfsProperties –EnableIdpInitiatedSignonPage $True`

## <a name="image-recommendations"></a>イメージの推奨事項
中央揃えの UI を有効にするには、同じイメージ背景およびロゴに会社のブランドを Azure Active Directory に既に存在する可能性がありますを使用することができます。 一般に、サイズ、比率、および形式の同じ推奨事項は適用します。

### <a name="logo"></a>ロゴ
説明 | 制約 | 推奨事項
------- | ------- | ----------
ロゴはログイン パネル上に表示されます。 | 透過 JPG または PNG<br>高さの最大値:36 px<br>幅の最大値:245 ピクセル | ここで、組織のロゴを使用します。<br>透明なイメージを使用します。 背景を白になることを想定しません。<br>画像のロゴの周囲にパディングを追加しないでください、または、ロゴが過度に小さくなります。

### <a name="background"></a>背景
説明 | 制約 | 推奨事項
------- | ------- | ----------
これは、表示可能な領域、およびスケールをブラウザー ウィンドウをトリミングの中央に固定されていますがオプションは、サインイン ページの背景に表示されます。    <br>携帯電話などの幅の狭い画面では、このイメージは表示されません。<br>ページが読み込まれるときに、この画像を不透明度 0.55 の黒いマスクが適用されます。 | JPG または PNG<br>画像のサイズ:1920 x 1080 ピクセル<br>ファイル サイズ:&lt; 300 KB | <br>イメージを使用して、強力なサブジェクト フォーカスのないです。 非透過のサインイン フォームは、このイメージの中央に表示され、ブラウザー ウィンドウのサイズに応じて画像の一部を覆うことができます。<br>ファイル サイズが小さくをすばやく読み込み時間を確認します。

## <a name="next-steps"></a>次の手順
- [Windows Server 2016 で AD FS のカスタマイズ](AD-FS-Customization-in-Windows-Server-2016.md)
- [高度なカスタマイズ](Advanced-Customization-of-AD-FS-Sign-in-Pages.md)
- [カスタム web テーマ](Custom-Web-Themes-in-AD-FS.md)
