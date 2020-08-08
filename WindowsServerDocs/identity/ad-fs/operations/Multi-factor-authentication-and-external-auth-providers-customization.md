---
title: 多要素認証と外部認証プロバイダーのカスタマイズ
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.assetid: 08724d45-9be4-4c56-a5f1-2cf40864e136
ms.openlocfilehash: 47a03b43d8ac1a52453741974d4243f8aafc391c
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87949786"
---
# <a name="multi-factor-authentication-and-external-authentication-providers-customization"></a>多要素認証と外部認証プロバイダーのカスタマイズ

AD FS では、多要素認証のサポートがすぐに提供され \- \- \- ます。 たとえば、 \- 2 番目の要素認証として組み込みの証明書認証を使用するように AD FS を構成できます。 また、外部認証プロバイダーを使用することもできます。 このアプローチにより、AD FS を Azure Multi-factor Authentication などの追加サービスと統合したり、独自のプロバイダーを開発したりすることができます。 AD FS を使用して外部認証プロバイダーを登録する方法の詳細については、「[ソリューションガイド: 多 \- 要素によるリスク管理 Access Control](./manage-risk-with-conditional-access-control.md) 」を参照してください。

外部認証プロバイダーは、認証 UI を作成するためにに用意されて AD FS いる .css ファイルで定義されているクラスを使用することをお勧めします。 次のコマンドレットを使用して既定の Web テーマをエクスポートし、.css ファイルに定義されているユーザー インターフェイスのクラスと要素を確認できます。 .Css ファイルは、 \- 外部認証プロバイダーのサインインユーザーインターフェイスの開発に使用できます。

```powershell
Export-AdfsWebTheme -Name default -DirectoryPath C:\theme
```

\-外部認証プロバイダーによって赤で強調表示されているサインインユーザーインターフェイスの例を次に示します。 ユーザーインターフェイスは、AD FS .css ファイルの UI クラスを使用します。

![AD FS と MFA](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom8.png)

新しいカスタム認証方法を作成する前に、AD FS のテーマとスタイルの定義について学習し、コンテンツ作成の要件を理解しておくことをお勧めします。

-   カスタム認証方法で作成されるのは、ページ全体ではなく AD FS サインインページの HTML セグメントのみ \- です。 一貫した外観と動作を得るには、AD FS のスタイル定義を使用する必要があります。

![AD FS と MFA](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom9.png)

-   AD FS 管理者は、AD FS スタイルをカスタマイズできることに注意してください。 . 独自のスタイルをハードコーディングすることはお勧めしません。 代わりに、可能な限り AD FS スタイルを使用することをお勧めします。

-   すぐ \- に \- 使用できるように、AD FS スタイルは左から右に1つ右の LTR スタイルを使用して作成され \- \- \( \) \- \- \( \) ます。 管理者は、両方をカスタマイズしたり、 \- web テーマ定義を使用して言語固有のスタイルを提供したりすることができます。 各スタイル シートには次の 3 つのセクションがあり、それぞれにコメントが付いています。

    -   **テーマスタイル** \-これらのスタイルは使用できません。また、使用することもできません。 これらのスタイルは、すべてのページでテーマを定義するために用意されています。 各スタイルは要素 ID によって意図的に定義されており、再利用することはできません。

    -   **一般的なスタイル** \-これらは、コンテンツに使用するスタイルです。

    -   **フォームファクターのスタイル** \-これらは、さまざまなフォームファクターのスタイルです。 スマートフォンやタブレットなど、異なるフォーム ファクターでコンテンツが確実に動作するように構成するには、このセクションの内容を理解する必要があります。

詳細については、「[ソリューションガイド: 多 \- 要素によるリスク管理 Access Control](./manage-risk-with-conditional-access-control.md) 」および「[ソリューションガイド: 追加の多要素認証による個人情報 \- アプリケーションのリスク管理](https://tnstage.redmond.corp.microsoft.com/library/dn280949.aspx)」を参照してください。

## <a name="additional-references"></a>その他の参照情報
[AD FS ユーザーサインインのカスタマイズ](AD-FS-user-sign-in-customization.md)
