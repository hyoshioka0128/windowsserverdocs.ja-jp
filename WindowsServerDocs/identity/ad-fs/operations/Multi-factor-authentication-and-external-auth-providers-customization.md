---
title: "多要素認証と外部認証プロバイダーのカスタマイズ"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 08724d45-9be4-4c56-a5f1-2cf40864e136
ms.technology: identity-adfs
ms.openlocfilehash: 6d06c017601003e3b93df32f5fa50190ce54541d
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="multi-factor-authentication-and-external-authentication-providers-customization"></a>多要素認証と外部認証プロバイダーのカスタマイズ 

>適用対象: Windows Server 2016、Windows Server 2012 R2

AD FS では、多要素認証のサポートは out\ of\ the\ ボックスに提供されます。 たとえば、第 2 要素認証として組み込みの証明書の認証を使用する AD FS を構成することができます。 また、外部認証プロバイダーを使用することができます。 このアプローチには、Azure の multi-factor Authentication などの他のサービスと統合する AD FS が有効にすることができますか、独自のプロバイダーを開発することができます。 参照してください[ソリューション ガイド: マルチ要素アクセス制御によるリスク管理](https://technet.microsoft.com/library/dn280937.aspx)詳細については、AD FS を使用して外部認証プロバイダーを登録する方法。  
  
外部認証プロバイダーが認証 UI を作成する AD FS を提供する .css ファイルで定義されているクラスを使用していることをお勧めします。 既定の Web テーマをエクスポートし、ユーザー インターフェイスのクラスと .css ファイルで定義されている要素を調べるには、次のコマンドレットを使用できます。 .Css ファイルは、外部認証プロバイダーのサインイン ユーザー インターフェイスの開発に使用できます。  
  

    Export-AdfsWebTheme -Name default -DirectoryPath C:\theme  
 
  
外部認証プロバイダーで、赤で強調表示されているサインイン ユーザー インターフェイスの例を次に示します。 ユーザー インターフェイスは、AD FS .css ファイルの UI クラスを使用します。  
  
![AD FS と MFA](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom8.png)  
  
新しいカスタム認証方法を記述する前に、コンテンツ作成の要件を理解する AD FS のテーマとスタイルの定義を学習することをお勧めします。  
  
-   カスタム認証方法で作成できるは、AD FS サインイン ページとページ全体での HTML セグメントのみです。 AD FS のスタイル定義を使用して、一貫性のある外観と動作を取得する必要があります。  
  
![AD FS と MFA](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom9.png)  
  
-   AD FS 管理者が AD FS のスタイルをカスタマイズできますを注意してください。 . お勧めしませんをハードコーディングする独自のスタイル。 代わりに、使用可能な限り、AD FS スタイルをお勧めします。  
  
-   Out\ of\ のボックスで、1 つのこれから右へと \(LTR\) スタイルと右から左へ記述の 1 つの \(RTL\) AD FS のスタイルを作成します。 管理者は、両方をカスタマイズし、Web テーマの定義を介して言語固有のスタイルを提供することができます。 各スタイル シートには、それぞれにコメントを 3 つのセクションがあります。  
  
    -   **テーマ スタイル**\-これらのスタイルがどうかし、は使用できません。 これらのスタイルは、すべてのページでテーマを定義するものです。 定義されている要素 ID によって意図的には再利用しないようにします。  
  
    -   **一般的なスタイル**\-これらは、スタイル、コンテンツのために使用する必要があります。  
  
    -   **フォーム ファクター スタイル**\-さまざまなフォーム ファクターのスタイルです。 このセクションのコンテンツで動作するさまざまなフォーム ファクターでは、たとえば、スマート フォンやタブレットを確認するを理解する必要があります。  
  
詳細については、次を参照してください。[ソリューション ガイド: マルチ要素アクセス制御によるリスク管理](https://technet.microsoft.com/library/dn280937.aspx)と[ソリューション ガイド: 追加のマルチ要素認証による個人情報アプリケーションのリスク管理](https://tnstage.redmond.corp.microsoft.com/library/dn280949.aspx)します。  

## <a name="additional-references"></a>その他の参照 
[AD FS のユーザーのサインイン カスタマイズ](AD-FS-user-sign-in-customization.md) 
