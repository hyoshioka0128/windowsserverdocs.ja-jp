---
title: 条件付きアクセス ポリシーを構成する
description: ルート証明書が作成されると、"VPN 接続" によって、顧客のテナントに "VPN サーバー" クラウドアプリケーションの作成がトリガーされます。
services: active-directory
ms.prod: windows-server
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
ms.openlocfilehash: 22983c085f2b9d9e7e16810e25c6fa50111f9fa6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404348"
---
# <a name="step-73-configure-the-conditional-access-policy"></a>手順 7.3. 条件付きアクセスポリシーを構成する

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows 10

- [**先の：** 手順 7.2. Azure AD で VPN 認証のルート証明書を作成する](vpn-create-root-cert-for-vpn-auth-azure-ad.md)
- [**次に：** 手順 7.4. 条件付きアクセスルート証明書をオンプレミスの AD @ no__t にデプロイする

この手順では、VPN 接続の条件付きアクセスポリシーを構成します。 [VPN 接続] ブレードに最初のルート証明書が作成されると、"VPN サーバー" クラウドアプリケーションがテナントに自動的に作成されます。

VPN ユーザーグループに割り当てられている条件付きアクセスポリシーを作成し、**クラウドアプリ**を**vpn サーバー**にスコープを指定します。

- **Users**:VPN ユーザー
- **クラウドアプリ**:VPN サーバー
- **Grant (アクセス制御)** :' Multi-factor authentication が必要です。 ' 必要に応じて、他のコントロールを使用できます。

**作業**この手順では、最も基本的な条件付きアクセスポリシーの作成について説明します。  必要に応じて、追加の条件とコントロールを使用できます。


1. **[条件付きアクセス]** ページの上部にあるツールバーで、 **[追加]** を選択します。

    ![[条件付きアクセス] ページで [追加] を選択します。](../../media/Always-On-Vpn/07.png)

2. **[新規]** ページの **[名前]** ボックスに、ポリシーの名前を入力します。 たとえば、「 **VPN ポリシー**」と入力します。

    ![条件付きアクセスページでポリシーの名前を追加する](../../media/Always-On-Vpn/08.png)

3. **[割り当て]** セクションで、 **[ユーザーとグループ]** を選択します。

    ![ユーザーとグループの選択](../../media/Always-On-Vpn/09.png)

4. **[ユーザーとグループ]** ページで、次の手順を実行します。

    ![テストユーザーの選択](../../media/Always-On-Vpn/10.png)

    a. **[ユーザーとグループの選択]** を選択します。

    b. **[選択]** を選択します。

    c. **[選択]** ページで、 **[VPN ユーザー]** グループを選択し、 **[選択]** を選択します。

    d. **[ユーザーとグループ]** ページで、 **[完了]** を選択します。

5. **[新規]** ページで、次の手順を実行します。

    ![クラウドアプリの選択](../../media/Always-On-Vpn/11.png)

    a. **[割り当て]** セクションで、 **[クラウドアプリ]** を選択します。

    b. **[クラウドアプリ]** ページで、 **[アプリの選択]** を選択します。

    d. **[VPN サーバー]** を選択します。

6.  **[新規]** ページで **[許可]** ページを開くには、 **[コントロール]** セクションで **[許可]** を選択します。

    ![許可の選択](../../media/Always-On-Vpn/13.png)

7.  **[許可]** ページで、次の手順を実行します。

    ![[多要素認証を要求する] を選択します。](../../media/Always-On-Vpn/14.png)

    a. **[多要素認証を要求する]** を選択します。

    b. **[選択]** を選択します。

8.  **[新規]** ページの **[ポリシーの有効化]** で、 **[オン]** を選択します。

    ![ポリシーを有効にする](../../media/Always-On-Vpn/15.png)

9.  **[新規]** ページで、 **[作成]** を選択します。


## <a name="next-steps"></a>次の手順
[手順 7.4.条件付きアクセスルート証明書をオンプレミスの AD @ no__t にデプロイします。このステップでは、オンプレミスの AD への VPN 認証用の信頼されたルート証明書として、条件付きアクセスルート証明書をデプロイします。
