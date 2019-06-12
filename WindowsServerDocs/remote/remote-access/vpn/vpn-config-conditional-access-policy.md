---
title: 条件付きアクセス ポリシーを構成する
description: ルート証明書が作成された後、VPN 接続は、顧客のテナントで 'VPN サーバー' クラウド アプリケーションの作成をトリガーします。
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
ms.openlocfilehash: 466e76d01ca99a1e1ed72fa955ccd287ae63c5df
ms.sourcegitcommit: 0948a1abff1c1be506216eeb51ffc6f752a9fe7e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2019
ms.locfileid: "66749497"
---
# <a name="step-73-configure-the-conditional-access-policy"></a>手順 7.3. 条件付きアクセス ポリシーを構成します。

>適用先:Windows Server 2016、Windows Server 2012 R2、Windows 10 の Windows Server (半期チャネル)

- [**先の：** 手順 7.2. Azure AD で VPN 認証のルート証明書を作成する](vpn-create-root-cert-for-vpn-auth-azure-ad.md)
- [**次に：** 手順 7.4. ルート証明書の条件付きアクセスをオンプレミスにデプロイ AD](vpn-deploy-cond-access-root-cert-to-on-premise-ad.md)

この手順では、VPN 接続用の条件付きアクセス ポリシーを構成します。 'VPN 接続' ブレードで、最初のルート証明書が作成されると、自動的に、テナントで 'VPN サーバー' クラウド アプリケーションを作成します。

VPN ユーザー グループのスコープに割り当てられている条件付きアクセス ポリシーを作成、**クラウド アプリ**に**VPN サーバー**:

- **Users**:VPN ユーザー
- **アプリをクラウド**:VPN サーバー
- **Grant (アクセス制御)** :多要素認証が必要です。 ' 必要な場合は、他のコントロールを使用できます。

**手順:** この手順では、最も基本的な条件付きアクセス ポリシーの作成について説明します。  必要に応じて、追加の条件とコントロールが使用できます。


1. **条件付きアクセス**ページで、上部のツールバーで選択**追加**します。

    ![条件付きアクセス ページの追加 を選択](../../media/Always-On-Vpn/07.png)

2. **新規**ページで、**名前**ボックスに、ポリシーの名前を入力します。 たとえば、入力**VPN ポリシー**します。

    ![条件付きアクセス ページで、ポリシーの名前を追加します。](../../media/Always-On-Vpn/08.png)

3. **割り当て**セクションで、**ユーザーとグループ**します。

    ![ユーザーとグループを選択します。](../../media/Always-On-Vpn/09.png)

4. **ユーザーとグループ**ページで、次の手順を実行します。

    ![テスト ユーザーを選択](../../media/Always-On-Vpn/10.png)

    a. 選択**ユーザーとグループを選択**します。

    b. 選択**選択**します。

    c. **選択**ページで、選択、 **VPN ユーザー** 、グループ化し、**選択**。

    d. **ユーザーとグループ**] ページで、[**完了**します。

5. **新規**ページで、次の手順を実行します。

    ![クラウド アプリを選択します。](../../media/Always-On-Vpn/11.png)

    a. **割り当て**セクションで、**クラウド アプリ**します。

    b. **クラウド アプリ**] ページで、[**アプリを選択します。** します。

    d. 選択**VPN サーバー**します。

6.  **新規** ページで、開く、 **Grant**  ページの 、**コントロール**セクションで、 **Grant**します。

    ![許可を選択します。](../../media/Always-On-Vpn/13.png)

7.  **Grant**ページで、次の手順を実行します。

    ![必要な多要素認証を選択します](../../media/Always-On-Vpn/14.png)

    a. 選択**多要素認証を要求する**します。

    b. 選択**選択**します。

8.  **新規**] ページ [**ポリシーを有効にする**を選択します**で**します。

    ![ポリシーを有効にします。](../../media/Always-On-Vpn/15.png)

9.  **新規**] ページで、[**作成**です。


## <a name="next-steps"></a>次のステップ
[手順 7.4.ルート証明書の条件付きアクセスをオンプレミスにデプロイ AD](vpn-deploy-cond-access-root-cert-to-on-premise-ad.md):この手順では、条件付きアクセスのルート証明書として展開 VPN 認証用の信頼されたルート証明書をオンプレミス AD。
