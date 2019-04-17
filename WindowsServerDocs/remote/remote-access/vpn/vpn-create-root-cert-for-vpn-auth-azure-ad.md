---
title: Azure AD で VPN 認証のルート証明書を作成する
description: Azure AD は、認証時に VPN 接続の Azure AD は、Windows 10 のクライアントに発行された証明書の署名に VPN 証明書を使用します。 プライマリとマークされている証明書では、Azure AD を使用している発行元です。
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
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2018
ms.locfileid: "6067291"
---
# 手順 7.2.  Azure AD と条件付きアクセス VPN 認証のルート証明書の作成します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows 10

& #171 です。 [**前:** 手順 7.1 します。証明書失効リスト (CRL) チェックを無視するには、EAP-TLS を構成します。](vpn-config-eap-tls-to-ignore-crl-checking.md)<br>
& #187 です。[ **[次へ]:** 手順 7.3 します。条件付きアクセス ポリシーを構成する](vpn-config-conditional-access-policy.md)

この手順では、テナント VPN サーバーと呼ばれるクラウド アプリを自動的に作成、Azure AD を使ってルート証明書 VPN 認証のための条件付きアクセスを構成します。 VPN 接続の条件付きアクセスを構成する必要があります。

1. (複数の証明書を作成することができます)、Azure portal での VPN 証明書を作成します。
2. VPN 証明書をダウンロードします。
2. VPN と NPS サーバーに証明書を展開します。

ユーザーは、VPN 接続を試みると、VPN クライアントは、Windows 10 クライアントで Web アカウント マネージャー (WAM) への呼び出しをします。 WAM により、VPN サーバーのクラウド アプリへの呼び出しです。 条件と条件付きアクセス ポリシー内のコントロールが満たされると、Azure AD は、WAM を (1 時間) の有効期間が短い証明書の形式でトークンを発行します。 WAM では、ユーザーの証明書ストアに証明書を配置し、VPN クライアントに制御を渡します。  

VPN クライアントは、証明書の問題を Azure AD によって、資格情報の確認の VPN にし、送信します。Azure AD は、**プライマリ**としてマークされている証明書を使用して発行者として VPN 接続のブレードします。 

Azure portal では、1 つの証明書が切れる場合は、切り替えを管理する 2 つの証明書を作成します。 証明書を作成するときはプライマリ証明書を認証時に、接続の証明書の署名に使用するかどうかを選択します。

**手順:**

1. 全体管理者として[Azure ポータル](https://portal.azure.com)にサインインします。

2. 左側のメニューで、 **Azure Active Directory**をクリックします。 

    ![Azure Active Directory を選択します。](../../media/Always-On-Vpn/01.png)

3. **Azure Active Directory** ] ページで、[**管理**] セクションでは、**条件付きアクセス**をクリックします。

    ![条件付きアクセスを選択します。](../../media/Always-On-Vpn/02.png)

4. **条件付きアクセス**] ページで、[**管理**] セクションでは、 **VPN 接続 (プレビュー)** をクリックします。

    ![VPN 接続を選択します。](../../media/Always-On-Vpn/03.png)

5. **VPN 接続**] ページで、**新しい証明書**をクリックします。

    ![新しい証明書を選択します。](../../media/Always-On-Vpn/04.png)

6. **新規作成**] ページで、次の手順に従います。

    ![期間とプライマリを選択します。](../../media/Always-On-Vpn/05.png)

    a.  **期間を選択する**と、1 または 2 年間を選択します。 証明書を切れるときの状態遷移を管理するには、最大 2 つの証明書を追加することができます。 どちらかは、プライマリ (、1 つの接続用の証明書の署名に認証時に使用) を選択できます。

    b.  **プライマリ**の **[はい]** を選択します。

    c. **[作成]** をクリックします。

## 次の手順
[手順 7.3 です。条件付きアクセス ポリシーを構成する](vpn-config-conditional-access-policy.md): この手順では VPN 接続の条件付きアクセス ポリシーを構成します。 

---