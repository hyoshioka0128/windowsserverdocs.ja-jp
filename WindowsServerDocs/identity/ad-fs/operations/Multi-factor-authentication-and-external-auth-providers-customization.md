---
title: 多要素認証と外部認証プロバイダーのカスタマイズ
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 08724d45-9be4-4c56-a5f1-2cf40864e136
ms.technology: identity-adfs
ms.openlocfilehash: 347b4783e82a6561334f8757029b1fddec6a85a3
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66189085"
---
# <a name="multi-factor-authentication-and-external-authentication-providers-customization"></a>多要素認証と外部認証プロバイダーのカスタマイズ 



AD FS で多要素認証のサポートが提供されている\-の\-、\-ボックス。 AD FS を構成するなど、使用して構築された\-証明書認証では第 2 要素認証として。 また、外部認証プロバイダーを使用することもできます。 このアプローチには、Azure 多要素認証などの他のサービスと統合する AD FS が有効にすることができますか、独自のプロバイダーを開発することができます。 参照してください[ソリューション ガイド。マルチによるリスク管理\-要素アクセス制御](https://technet.microsoft.com/library/dn280937.aspx)AD FS を使用して外部認証プロバイダーを登録する方法の詳細について。  
  
外部認証プロバイダーが認証 UI を作成する AD FS を提供する .css ファイルで定義されているクラスを使用することをお勧めします。 次のコマンドレットを使用して既定の Web テーマをエクスポートし、.css ファイルに定義されているユーザー インターフェイスのクラスと要素を確認できます。 符号の開発では、.css ファイルを使用できます\-外部認証プロバイダーのユーザー インターフェイスでします。  
  

    Export-AdfsWebTheme -Name default -DirectoryPath C:\theme  
 
  
符号の例を次に\-ユーザー インターフェイスでこれが赤色で強調表示、外部認証プロバイダーによって。 ユーザー インターフェイスは、AD FS の .css ファイルの UI クラスを使用します。  
  
![AD FS と MFA](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom8.png)  
  
新しいカスタム認証方法を記述する前に、コンテンツ作成の要件を理解する AD FS のテーマとスタイルの定義を学習することをお勧めします。  
  
-   カスタム認証方法を AD FS のサインインで、HTML セグメント人の作成者のみ\-ページとページ全体ではありません。 AD FS のスタイル定義を使用して、一貫した外観と動作を取得する必要があります。  
  
![AD FS と MFA](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom9.png)  
  
-   AD FS 管理者が AD FS のスタイルをカスタマイズすることができますに注意します。 . 独自のスタイルをハードコーディングすることはお勧めしません。 代わりに、使用可能な限り、AD FS のスタイルをお勧めします。  
  
-   Out\-の\-ボックスで、AD FS のスタイルは、1 つ左ので作成された\-に\-右\(LTR\)スタイルと 1 つの右\-に\-左\(RTL\). 管理者が、両方をカスタマイズし、言語を提供できます\-web テーマの定義を特定のスタイル。 各スタイル シートには次の 3 つのセクションがあり、それぞれにコメントが付いています。  
  
    -   **テーマ スタイル**\-これらのスタイルを持たないとは使用できません。 これらのスタイルは、すべてのページでテーマを定義するために用意されています。 各スタイルは要素 ID によって意図的に定義されており、再利用することはできません。  
  
    -   **共通スタイル**\-スタイル、コンテンツのために使用する必要があります。  
  
    -   **フォーム ファクター スタイル**\-のさまざまなフォーム ファクター スタイルです。 スマートフォンやタブレットなど、異なるフォーム ファクターでコンテンツが確実に動作するように構成するには、このセクションの内容を理解する必要があります。  
  
詳細については、次を参照してください。[ソリューション ガイド。マルチによるリスク管理\-要素アクセス制御](https://technet.microsoft.com/library/dn280937.aspx)と[ソリューション ガイド。その他のマルチによるリスク管理\-Factor Authentication for Sensitive Applications](https://tnstage.redmond.corp.microsoft.com/library/dn280949.aspx)します。  

## <a name="additional-references"></a>その他の参照情報 
[AD FS のユーザー サインイン カスタマイズ](AD-FS-user-sign-in-customization.md) 
