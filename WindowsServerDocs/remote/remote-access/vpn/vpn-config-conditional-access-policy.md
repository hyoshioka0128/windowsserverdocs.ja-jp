---
title: 条件付きアクセス ポリシーを構成する
description: ルート証明書が作成されたら、VPN 接続は、顧客のテナントで 'VPN サーバー' クラウド アプリケーションの作成をトリガーします。
services: active-directory
ms.prod: windows-server-threshold
ms.technology: networking-ras
documentationcenter: ''
ms.assetid: ''
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2018
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.reviewer: deverette
ms.openlocfilehash: 8c00855c50de79efa1b48c7b8762e1b679db4a87
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2018
ms.locfileid: "6067296"
---
# 手順 7.3.  条件付きアクセス ポリシーを構成します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows 10

& #171 です。 [**前:** 手順 7.2 します。Azure AD と VPN 認証のルート証明書を作成します。](vpn-create-root-cert-for-vpn-auth-azure-ad.md)<br>
& #187 です。[ **[次へ]:** 手順 7.4 します。条件付きアクセスのルート証明書をオンプレミスに展開 AD](vpn-deploy-cond-access-root-cert-to-on-premise-ad.md)

この手順では、VPN 接続の条件付きアクセス ポリシーを構成します。 'VPN 接続' ブレードで、最初のルート証明書を作成するときに自動的に、テナント 'VPN サーバー' クラウド アプリケーションを作成します。 

VPN のユーザーのグループとスコープ**の VPN サーバー**には、**クラウド アプリ**に割り当てられている、条件付きアクセス ポリシーを作成します。 

- **ユーザー**: VPN ユーザー
- **クラウド アプリ**: VPN サーバー
- **許可 (アクセス制御)**: '多要素認証を要求する]。 必要に応じて、その他のコントロールを使用することができます。

**プロシージャ:** この手順では、最も基本的な条件付きアクセス ポリシーの作成について説明します。必要に応じて、追加の条件とコントロールが使用できます。


1. **条件付きアクセス**] ページで、上部のツールバーで、[**追加**] をクリックします。

    ![条件付きアクセス ページの追加] を選択](../../media/Always-On-Vpn/07.png)

2. **新規作成**] ページで、 **[名前**] ボックスで、ポリシーの名前を入力します。 たとえば、 **VPN ポリシー**を入力します。

    ![条件付きアクセスのページで、ポリシーの名前を追加します。](../../media/Always-On-Vpn/08.png)

3. **割り当て**] セクションでは、**ユーザーとグループ**をクリックします。

    ![[ユーザーとグループ](../../media/Always-On-Vpn/09.png)

4. **ユーザーとグループ**] ページで、次の手順に従います。

    ![[テスト ユーザー](../../media/Always-On-Vpn/10.png)

    a.  **[ユーザーとグループ**をクリックします。

    b.  [**選択**] をクリックします。

    c. [**選択**] ページで、 **VPN ユーザー**グループを選択し、**選択**] をクリックします。

    d. **ユーザーとグループ**] ページで、[**完了**] をクリックします。

5. **新規作成**] ページで、次の手順に従います。

    ![クラウド アプリを選択します。](../../media/Always-On-Vpn/11.png)

    a.  [**割り当て**] セクションでは、**クラウド アプリ**をクリックします。

    b.  **クラウド アプリ**] ページで、**アプリを選択**] をクリックします。

    d. **VPN サーバー**を選択します。

13. [**新規作成**] ページで開くには、**許可**ページ**コントロール**] セクションで、**許可**をクリックします。

    ![許可を選択します。](../../media/Always-On-Vpn/13.png)

14. [**許可**] ページで、次の手順に従います。

    ![選択が多要素認証を要求します。](../../media/Always-On-Vpn/14.png)

    a.  **多要素認証を要求する**かを選択します。

    b.  [**選択**] をクリックします。

15. **新規作成**] ページで、**ポリシーを有効にする**には、[**上**をクリックします。

    ![ポリシーを有効にします。](../../media/Always-On-Vpn/15.png)

16. [**新規作成**] ページで、**作成**をクリックします。


## 次の手順
[手順 7.4 です。条件付きアクセスのルート証明書をオンプレミスに展開 AD](vpn-deploy-cond-access-root-cert-to-on-premise-ad.md): この手順でに展開する条件付きアクセスのルート証明書 VPN 認証のための信頼されたルート証明書としてオンプレミス AD します。

---