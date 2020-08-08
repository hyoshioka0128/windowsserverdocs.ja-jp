---
title: Azure AD で VPN 認証のルート証明書を作成する
description: Azure AD では、VPN 接続用に Azure AD で認証するときに、VPN 証明書を使用して Windows 10 クライアントに対して発行された証明書に署名します。 プライマリとしてマークされている証明書は Azure AD が使用する発行者です。
ms.topic: article
ms.date: 06/28/2019
ms.author: v-tea
author: Teresa-MOTIV
ms.localizationpriority: medium
ms.reviewer: deverette
ms.openlocfilehash: 098d2f2c17555c3e4375e4b54b676ef67a40dc4d
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87946575"
---
# <a name="step-72-create-conditional-access-root-certificates-for-vpn-authentication-with-azure-ad"></a>手順 7.2.  Azure AD を使用した VPN 認証用の条件付きアクセスルート証明書の作成

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows 10

- [**前へ:** 手順 7.1.証明書失効リスト (CRL) チェックを無視するように EAP-TLS を構成する](vpn-config-eap-tls-to-ignore-crl-checking.md)
- [**次のようになります。** 手順 7.3.条件付きアクセスポリシーを構成する](vpn-config-conditional-access-policy.md)

この手順では、Azure AD で VPN 認証用の条件付きアクセスルート証明書を構成します。これにより、テナントに VPN サーバーというクラウドアプリが自動的に作成されます。 VPN 接続用の条件付きアクセスを構成するには、以下の操作を行う必要があります。

1. Azure Portal で VPN 証明書を作成する。
2. VPN 証明書をダウンロードする。
3. VPN サーバーと NPS サーバーに証明書を展開します。

> [!IMPORTANT]
> Azure portal に VPN 証明書が作成されると、Azure AD は短時間の証明書を VPN クライアントに発行するためにすぐに使用を開始します。 Vpn クライアントの資格情報の検証に関する問題を回避するために、vpn 証明書を VPN サーバーに直ちに展開することが重要です。

ユーザーが VPN 接続を試行すると、VPN クライアントは Windows 10 クライアントで Web アカウントマネージャー (WAM) を呼び出します。 WAM は、VPN サーバークラウドアプリの呼び出しを行います。 条件付きアクセスポリシーの条件と制御が満たされると、Azure AD は、有効期間が短い (1 時間) 証明書の形式のトークンを WAM に発行します。 WAM は、ユーザーの証明書ストアに証明書を配置し、VPN クライアントに制御を渡します。 

VPN クライアントは、資格情報の検証のために Azure AD によって証明書の問題を VPN に送信します。 

> [!NOTE]
> Azure AD は、最後に作成された証明書を、発行者として VPN 接続ブレードに使用します。

**作業**

1. [Azure Portal](https://portal.azure.com) にグローバル管理者としてサインインします。
2. 左側のメニューで、**[Azure Active Directory]** をクリックします。
3. [ **Azure Active Directory** ] ページの [**管理**] セクションで、[**セキュリティ**] をクリックします。
4. [**セキュリティ**] ページの [**保護**] セクションで、[**条件付きアクセス**] をクリックします。
5. **条件付きアクセス |[ポリシー** ] ページの [**管理**] セクションで、[ **VPN 接続**] をクリックします。
5. **[VPN 接続]** ページで、**[新しい証明書]** をクリックします。
6. [**新規**] ページで、次の手順を実行します。 a. **[期間の選択**] で、1、2、または3年を選択します。
   b. **［作成］** を選択します

## <a name="next-steps"></a>次のステップ

[手順 7.3.条件付きアクセスポリシーを構成](vpn-config-conditional-access-policy.md)する: この手順では、VPN 接続の条件付きアクセスポリシーを構成します。
