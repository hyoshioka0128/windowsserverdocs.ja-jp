---
title: Azure AD で VPN 認証のルート証明書を作成する
description: Azure AD は、vpn 証明書を使用して、VPN 接続用の Azure AD に対して認証するときに、Windows 10 クライアントに対して発行された証明書に署名します。 プライマリとしてマークされている証明書は Azure AD が使用する発行者です。
services: active-directory
ms.prod: windows-server
ms.technology: networking-ras
ms.workload: identity
ms.topic: article
ms.date: 06/28/2019
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.reviewer: deverette
ms.openlocfilehash: 41e98648ab963347f8370233c320f5e38b5d4d96
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71388008"
---
# <a name="step-72-create-conditional-access-root-certificates-for-vpn-authentication-with-azure-ad"></a>手順 7.2. Azure AD を使用した VPN 認証用の条件付きアクセスルート証明書の作成

>適用対象:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows 10

- [**先の：** 手順 7.1. 証明書失効リスト (CRL) の確認が無視されるように EAP-TLS を構成する](vpn-config-eap-tls-to-ignore-crl-checking.md)
- [**次に：** 手順 7.3. 条件付きアクセス ポリシーを構成する](vpn-config-conditional-access-policy.md)

この手順では、Azure AD で VPN 認証用の条件付きアクセスルート証明書を構成します。これにより、テナントに VPN サーバーというクラウドアプリが自動的に作成されます。 VPN 接続の条件付きアクセスを構成するには、次のことを行う必要があります。

1. Azure portal に VPN 証明書を作成します。
2. VPN 証明書をダウンロードします。
3. VPN サーバーと NPS サーバーに証明書を展開します。

> [!IMPORTANT]
> Azure portal に VPN 証明書が作成されると、Azure AD は短時間の証明書を VPN クライアントに発行するためにすぐに使用を開始します。 Vpn クライアントの資格情報の検証に関する問題を回避するために、vpn 証明書を VPN サーバーに直ちに展開することが重要です。

ユーザーが VPN 接続を試行すると、VPN クライアントは Windows 10 クライアントで Web アカウントマネージャー (WAM) を呼び出します。 WAM は、VPN サーバークラウドアプリの呼び出しを行います。 条件付きアクセスポリシーの条件と制御が満たされると、Azure AD は、有効期間が短い (1 時間) 証明書の形式のトークンを WAM に発行します。 WAM は、ユーザーの証明書ストアに証明書を配置し、VPN クライアントに制御を渡します。  

VPN クライアントは、資格情報の検証のために Azure AD によって証明書の問題を VPN に送信します。  

> [!NOTE]
> Azure AD は、最後に作成された証明書を、発行者として VPN 接続ブレードに使用します。

**作業**

1. 全体管理者として[Azure portal](https://portal.azure.com)にサインインします。
2. 左側のメニューで、 **[Azure Active Directory]** をクリックします。
3. **[Azure Active Directory]** ページの **[管理]** セクションで、 **[条件付きアクセス]** をクリックします。
4. **[条件付きアクセス]** ページの **[管理]** セクションで、 **[VPN 接続 (プレビュー)]** をクリックします。
5. **[VPN 接続]** ページで、 **[新しい証明書]** をクリックします。
6. **[新規]** ページで、次の手順を実行します。 a. **[期間の選択**] で、1、2、または3年を選択します。
   b. **[作成]** を選択します。

## <a name="next-steps"></a>次の手順

[手順 7.3.条件付きアクセスポリシー @ no__t を構成します。この手順では、VPN 接続の条件付きアクセスポリシーを構成します。
