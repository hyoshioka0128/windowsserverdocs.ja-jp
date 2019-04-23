---
title: Azure AD で VPN 認証のルート証明書を作成する
description: Azure AD では、VPN 証明書を使用して、VPN 接続用の Azure AD に認証するときに、Windows 10 クライアントに発行された証明書に署名します。 プライマリとしてマークされている証明書は、Azure AD を使用する発行者です。
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
ms.openlocfilehash: 14ef17ab403cc4e7c9891f4ede48e41c25e8522d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59851563"
---
# <a name="step-72-create-conditional-access-root-certificates-for-vpn-authentication-with-azure-ad"></a>手順 7.2.  条件付きアクセスに Azure AD での VPN 認証用のルート証明書を作成します。

>適用先:Windows Server 2016、Windows Server 2012 R2、Windows 10 の Windows Server (半期チャネル)

&#171;  [**先の：** 手順 7.1. 証明書失効リスト (CRL) チェックを無視するには、EAP-TLS の構成します。](vpn-config-eap-tls-to-ignore-crl-checking.md)<br>
&#187;[ **[次へ]。** 手順 7.3. 条件付きアクセス ポリシーを構成します。](vpn-config-conditional-access-policy.md)

この手順では、VPN 認証用のルート証明書の条件付きアクセスを構成する Azure ad テナントで VPN サーバーと呼ばれるクラウド アプリを自動的に作成します。 VPN 接続用の条件付きアクセスを構成する必要があります。

1. (1 つ以上の証明書を作成することができます)、Azure portal で VPN 証明書を作成します。
2. VPN 証明書をダウンロードします。
2. VPN と NPS サーバーに証明書を展開します。

ユーザーは、VPN 接続を試みると、VPN クライアントは、Windows 10 クライアントの Web アカウント マネージャー (WAM) への呼び出しをします。 WAM は、VPN サーバーのクラウド アプリへの呼び出しを実行します。 条件付きアクセス ポリシーのコントロールの条件が満たされると、Azure AD は、WAM を短時間 (1 時間) の証明書の形式でトークンを発行します。 WAM では、ユーザーの証明書ストアに証明書を配置し、VPN クライアントに制御を渡します。  

VPN クライアントは、証明書の問題を Azure AD によって、VPN 資格情報の検証にし、送信します。  Azure AD としてマークされている証明書を使用して **プライマリ** を発行者として、VPN 接続 ブレードでします。 

Azure portal では、1 つの証明書の期限切れが近づくときの移行を管理する 2 つの証明書を作成します。 証明書を作成するときに、認証中に、接続の証明書の署名に使用するプライマリ証明書であるかどうかを選択します。

**手順:**

1. サインイン、 [Azure portal](https://portal.azure.com)グローバル管理者として。

2. 左側のメニューでクリックして**Azure Active Directory**します。 

    ![Azure Active Directory を選択します。](../../media/Always-On-Vpn/01.png)

3. **Azure Active Directory**ページで、**管理**セクションで、**条件付きアクセス**します。

    ![条件付きアクセスを選択します。](../../media/Always-On-Vpn/02.png)

4. **条件付きアクセス**ページで、**管理**セクションで、 **VPN 接続 (プレビュー)** します。

    ![VPN 接続を選択します。](../../media/Always-On-Vpn/03.png)

5. **VPN 接続**] ページで [**新しい証明書**します。

    ![新しい証明書を選択します。](../../media/Always-On-Vpn/04.png)

6. **新規**ページで、次の手順を実行します。

    ![時間とプライマリを選択します。](../../media/Always-On-Vpn/05.png)

    a.  **の期間を選択**、1 または 2 年を選択します。 証明書の期限切れが近づくときの移行を管理するに最大 2 つの証明書を追加することができます。 どれがプライマリ (、1 つの認証時に接続の証明書に署名するために使用) を選択できます。

    b.  **プライマリ**、**はい**します。

    c. **[作成]** をクリックします。

## <a name="next-step"></a>次の手順
[手順 7.3 です。条件付きアクセス ポリシーを構成する](vpn-config-conditional-access-policy.md):この手順では、VPN 接続用の条件付きアクセス ポリシーを構成します。 

---