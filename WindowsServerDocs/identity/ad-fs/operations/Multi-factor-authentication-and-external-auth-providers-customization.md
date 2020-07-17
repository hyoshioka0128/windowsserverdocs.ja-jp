---
title: 多要素認証と外部認証プロバイダーのカスタマイズ
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.assetid: 08724d45-9be4-4c56-a5f1-2cf40864e136
ms.technology: identity-adfs
ms.openlocfilehash: 8252244738d59f11a07c3bebadbbf2a5f4818845
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80816235"
---
# <a name="multi-factor-authentication-and-external-authentication-providers-customization"></a>多要素認証と外部認証プロバイダーのカスタマイズ 



AD FS では、多要素認証のサポートが\-ボックス\-の\-提供されています。 たとえば、2番目の要素認証として証明書認証に構築された\-を使用するように AD FS を構成できます。 また、外部認証プロバイダーを使用することもできます。 このアプローチにより、AD FS を Azure Multi-factor Authentication などの追加サービスと統合したり、独自のプロバイダーを開発したりすることができます。 AD FS を使用して外部認証プロバイダーを登録する方法の詳細については、「[ソリューションガイド: マルチ\-ファクターによるリスク管理」 Access Control](https://technet.microsoft.com/library/dn280937.aspx)を参照してください。  
  
外部認証プロバイダーは、認証 UI を作成するためにに用意されて AD FS いる .css ファイルで定義されているクラスを使用することをお勧めします。 次のコマンドレットを使用して既定の Web テーマをエクスポートし、.css ファイルに定義されているユーザー インターフェイスのクラスと要素を確認できます。 .Css ファイルは、外部認証プロバイダーのユーザーインターフェイスの sign\-の開発に使用できます。  
  

    Export-AdfsWebTheme -Name default -DirectoryPath C:\theme  
 
  
次に示すのは、外部認証プロバイダーによって赤で強調表示されている、ユーザーインターフェイスの sign\-の例です。 ユーザーインターフェイスは、AD FS .css ファイルの UI クラスを使用します。  
  
![AD FS と MFA](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom8.png)  
  
新しいカスタム認証方法を作成する前に、AD FS のテーマとスタイルの定義について学習し、コンテンツ作成の要件を理解しておくことをお勧めします。  
  
-   カスタム認証方法で作成されるのは、ページ内の AD FS 署名\-の HTML セグメントだけで、完全なページは作成されません。 一貫した外観と動作を得るには、AD FS のスタイル定義を使用する必要があります。  
  
![AD FS と MFA](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom9.png)  
  
-   AD FS 管理者は、AD FS スタイルをカスタマイズできることに注意してください。 。 独自のスタイルをハードコーディングすることはお勧めしません。 代わりに、可能な限り AD FS スタイルを使用することをお勧めします。  
  
-   ボックス\-の\-、AD FS スタイルは\-1 つので作成され、右\-LTR \(スタイル、および右\)\-RTL\-左 \(ます。\) 管理者は、両方をカスタマイズできます。また、web テーマ定義を使用して言語\-固有のスタイルを提供できます。 各スタイル シートには次の 3 つのセクションがあり、それぞれにコメントが付いています。  
  
    -   **テーマスタイル**\- これらのスタイルは使用できません。 これらのスタイルは、すべてのページでテーマを定義するために用意されています。 各スタイルは要素 ID によって意図的に定義されており、再利用することはできません。  
  
    -   **共通スタイル**\- コンテンツに使用するスタイルです。  
  
    -   **フォームファクタースタイル**\-、さまざまなフォームファクターのスタイルです。 スマートフォンやタブレットなど、異なるフォーム ファクターでコンテンツが確実に動作するように構成するには、このセクションの内容を理解する必要があります。  
  
詳細については、「[ソリューションガイド: マルチ\-ファクターによるリスク管理](https://technet.microsoft.com/library/dn280937.aspx)」を参照してください Access Control と[ソリューションガイド: 追加の\-多要素認証による個人情報アプリケーションのリスク管理](https://tnstage.redmond.corp.microsoft.com/library/dn280949.aspx)」を参照してください。  

## <a name="additional-references"></a>その他の参照情報 
[AD FS ユーザーサインインのカスタマイズ](AD-FS-user-sign-in-customization.md) 
