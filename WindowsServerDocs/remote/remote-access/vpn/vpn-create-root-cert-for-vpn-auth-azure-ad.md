---
title: Azure AD で VPN 認証のルート証明書を作成する
description: Azure AD では、VPN 証明書を使用して、VPN 接続用の Azure AD に認証するときに、Windows 10 クライアントに発行された証明書に署名します。 プライマリとしてマークされている証明書は、Azure AD を使用する発行者です。
services: active-directory
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.workload: identity
ms.topic: article
ms.date: 06/28/2019
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.reviewer: deverette
ms.openlocfilehash: 40403f6be65c84cc1e2506a222a009400fcdaacc
ms.sourcegitcommit: 34232723f15c7b4d6a32ca38b7348a417ba30ae0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/28/2019
ms.locfileid: "67464958"
---
# <a name="step-72-create-conditional-access-root-certificates-for-vpn-authentication-with-azure-ad"></a>手順 7.2. 条件付きアクセスに Azure AD での VPN 認証用のルート証明書を作成します。

>適用対象:Windows Server 2016、Windows Server 2012 R2、Windows 10 の Windows Server (半期チャネル)

- [**先の：** 手順 7.1. 証明書失効リスト (CRL) の確認が無視されるように EAP-TLS を構成する](vpn-config-eap-tls-to-ignore-crl-checking.md)
- [**次に：** 手順 7.3. 条件付きアクセス ポリシーを構成する](vpn-config-conditional-access-policy.md)

この手順では、VPN 認証用のルート証明書の条件付きアクセスを構成する Azure ad テナントで VPN サーバーと呼ばれるクラウド アプリを自動的に作成します。 VPN 接続用の条件付きアクセスを構成する必要があります。

1. Azure portal で VPN 証明書を作成します。
2. VPN 証明書をダウンロードします。
3. VPN と NPS サーバーに証明書を展開します。

> [!IMPORTANT]
> Azure portal で VPN 証明書が作成されると、Azure AD は短い存続期間の証明書、VPN クライアントを発行するためにすぐに使用を開始します。 VPN 証明書が、VPN クライアントの資格情報の検証で問題を回避するために、VPN サーバーにすぐにデプロイすることが重要です。

ユーザーは、VPN 接続を試みると、VPN クライアントは、Windows 10 クライアントの Web アカウント マネージャー (WAM) への呼び出しをします。 WAM は、VPN サーバーのクラウド アプリへの呼び出しを実行します。 条件付きアクセス ポリシーのコントロールの条件が満たされると、Azure AD は、WAM を短時間 (1 時間) の証明書の形式でトークンを発行します。 WAM では、ユーザーの証明書ストアに証明書を配置し、VPN クライアントに制御を渡します。  

VPN クライアントは、証明書の問題を Azure AD によって、VPN 資格情報の検証にし、送信します。  

> [!NOTE]
> Azure AD では、発行者として、VPN 接続 ブレードで、最近作成された証明書を使用します。

**手順:**

1. サインイン、 [Azure portal](https://portal.azure.com)グローバル管理者として。
2. 左側のメニューでクリックして**Azure Active Directory**します。
3. **Azure Active Directory**ページで、**管理**セクションで、**条件付きアクセス**します。
4. **条件付きアクセス**ページで、**管理**セクションで、 **VPN 接続 (プレビュー)** します。
5. **VPN 接続**] ページで [**新しい証明書**します。
6. **新規**ページで、次の手順に従います: をします。 **の期間を選択**、1、2 または 3 年を選択します。
   b. **[作成]** を選択します。

## <a name="next-steps"></a>次のステップ

[手順 7.3.条件付きアクセス ポリシーを構成する](vpn-config-conditional-access-policy.md):この手順では、VPN 接続用の条件付きアクセス ポリシーを構成します。
