---
title: Azure AD を使用した VPN 接続への条件付きアクセス
description: この省略可能な手順では、Azure Active Directory (Azure AD) の条件付きアクセスを使用して、リソース VPN ユーザーのアクセスを承認する方法を微調整できます。
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: ''
ms.localizationpriority: medium
ms.author: pashort
author: shortpatti
ms.date: 07/13/2018
ms.reviewer: deverette
ms.openlocfilehash: c87d0075696bf8ab5794667d42c40829c3eb61bd
ms.sourcegitcommit: 0948a1abff1c1be506216eeb51ffc6f752a9fe7e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2019
ms.locfileid: "66749529"
---
# <a name="step-7-optional-conditional-access-for-vpn-connectivity-using-azure-ad"></a>手順 7. (省略可能)Azure AD を使用して VPN 接続用の条件付きアクセス

- [**先の：** 手順 6.Windows 10 クライアントの Always On VPN 接続を構成する](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md)
- [**次に：** 手順 7.1. 証明書失効リスト (CRL) の確認が無視されるように EAP-TLS を構成する](vpn-config-eap-tls-to-ignore-crl-checking.md)

このオプションの手順で VPN ユーザーを使用して、リソースにアクセスする方法を微調整できます[Azure Active Directory (Azure AD) の条件付きアクセス](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)します。 仮想プライベート ネットワーク (VPN) 接続用の Azure AD の条件付きアクセス、VPN 接続を保護できます。 条件付きアクセスはポリシー ベースの評価エンジンであり、これを利用することで、Azure Active Directory (Azure AD) に接続されるアプリケーションのアクセス規則を作成できます。 

## <a name="prerequisites"></a>前提条件

次のトピックを熟知の方します。
- [Azure Active Directory の条件付きアクセス](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)
- [VPN と条件付きアクセス](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access)

VPN 接続用の Azure Active Directory 条件付きアクセスを構成するには、以下を構成する必要があります。
- [サーバー インフラストラクチャ](always-on-vpn/deploy/vpn-deploy-server-infrastructure.md)
- [Always On VPN リモート アクセス サーバー用](always-on-vpn/deploy/vpn-deploy-ras.md)
- [ネットワーク ポリシー サーバー](always-on-vpn/deploy/vpn-deploy-nps.md)
- [DNS とファイアウォールの設定](always-on-vpn/deploy/vpn-deploy-dns-firewall.md)
- [VPN 接続の Always On Windows 10 クライアント](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md)

## <a name="step-71-configure-eap-tls-to-ignore-certificate-revocation-list-crl-checkingvpn-config-eap-tls-to-ignore-crl-checkingmd"></a>[手順 7.1.証明書失効リスト (CRL) の確認が無視されるように EAP-TLS を構成する](vpn-config-eap-tls-to-ignore-crl-checking.md)

この手順で追加することができます**IgnoreNoRevocationCheck**し、証明書に CRL 配布ポイントが含まれていない場合は、クライアントの認証を許可するように設定します。 既定では、IgnoreNoRevocationCheck は、0 (無効) に設定されます。

NPS サーバーの証明書チェーン (ルート証明書を含む) の失効確認が完了しない限り、EAP-TLS クライアントは接続できません。 ユーザーに Azure AD によって発行された証明書をクラウドでは、1 時間の有効期間を持つ証明書を短時間であるため、CRL を必要はありません。 NPS で EAP は、CRL の休暇を無視するように構成する必要があります。 このレジストリ値が下でのみ必要な認証方法が EAP-TLS 認証のため、 **EAP\13**します。 その他の EAP 認証メソッドを使用している場合、レジストリ値必要があります追加ものでも。

## <a name="step-72-create-root-certificates-for-vpn-authentication-with-azure-advpn-create-root-cert-for-vpn-auth-azure-admd"></a>[手順 7.2.Azure AD で VPN 認証のルート証明書を作成する](vpn-create-root-cert-for-vpn-auth-azure-ad.md)

この手順では、テナントに自動的に VPN サーバーのクラウド アプリを作成する Azure AD に VPN 認証用のルート証明書を構成します。  

VPN 接続用の条件付きアクセスを構成する必要があります。
1. (1 つ以上の証明書を作成することができます)、Azure portal で VPN 証明書を作成します。
2. VPN 証明書をダウンロードします。
3. VPN サーバーに証明書を展開します。

## <a name="step-73-configure-the-conditional-access-policyvpn-config-conditional-access-policymd"></a>[手順 7.3.条件付きアクセス ポリシーを構成する](vpn-config-conditional-access-policy.md)

この手順では、VPN 接続用の条件付きアクセス ポリシーを構成します。

条件付きアクセス ポリシーを構成するには、する必要があります。

1. VPN ユーザーに割り当てられている条件付きアクセス ポリシーを作成します。
2. クラウド アプリを設定**VPN サーバー**します。
3. 付与 (アクセス制御) を設定**多要素認証を要求する**します。  必要に応じて、他のコントロールを使用できます。

## <a name="step-74-deploy-conditional-access-root-certificates-to-on-premises-advpn-deploy-cond-access-root-cert-to-on-premise-admd"></a>[手順 7.4.ルート証明書の条件付きアクセスをオンプレミスにデプロイ AD](vpn-deploy-cond-access-root-cert-to-on-premise-ad.md)

この手順で、オンプレミスに VPN 認証用の信頼されたルート証明書を展開する AD。

信頼されたルート証明書を展開するには、する必要があります。
1. としてダウンロードした証明書を追加、 *VPN 認証用の信頼されたルート CA*します。
2. VPN サーバーと VPN クライアント ルート証明書をインポートします。
3. 証明書が存在し表示することを確認します。 信頼できます。

## <a name="step-75-create-oma-dm-based-vpnv2-profiles-to-windows-10-devicesvpn-create-oma-dm-based-vpnv2-profilesmd"></a>[手順 7.5.Windows 10 デバイスに OMA-DM ベースの VPNv2 プロファイルを作成する](vpn-create-oma-dm-based-vpnv2-profiles.md)

この手順では、OMA-DM を作成できますベースの VPNv2 プロファイルが Intune を使用して VPN デバイス構成ポリシーを展開します。 VPNv2 プロファイルを作成するを参照してください、SCCM または PowerShell スクリプトを使用したい場合[VPNv2 CSP 設定](https://docs.microsoft.com/windows/client-management/mdm/vpnv2-csp)の詳細。 

## <a name="next-steps"></a>次のステップ

[手順 7.1.構成証明書失効リスト (CRL) チェックを無視するには、EAP-TLS](vpn-config-eap-tls-to-ignore-crl-checking.md):この手順で追加する必要があります**IgnoreNoRevocationCheck**し、証明書に CRL 配布ポイントが含まれていない場合は、クライアントの認証を許可するように設定します。 既定では、IgnoreNoRevocationCheck は、0 (無効) に設定されます。

## <a name="related-topics"></a>関連トピック

- [VPNv2 プロファイルを構成する](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access):VPN クライアントは、クラウド ベースの条件付きアクセス プラットフォームと統合して、リモート クライアント用のデバイス コンプライアンス オプションを提供することができるようになりました。 このステップでの VPNv2 プロファイルを構成する **\<DeviceCompliance >\<有効 > true\</有効に >** します。 

- [Windows 10 で、自動 VPN プロファイルのリモート アクセスの強化](https://www.microsoft.com/itshowcase/Article/Content/894/Enhancing-remote-access-in-Windows-10-with-an-automatic-VPN-profile):Microsoft が VPN 接続用の条件付きアクセスを実装する方法について説明します。 VPN プロファイルには、デバイスがサポートされている認証方法と、VPN サーバーに接続するデバイスを含め、企業ネットワークに接続する必要がありますすべての情報が含まれます。 条件付きアクセスとシングル サインオンを含む、Windows 10 Anniversary Update での変更を行った Always-On VPN 接続プロファイルを作成することも可能です。 接続プロファイルを作成したドメインに参加していると System Center Configuration Manager コンソールを使用して Microsoft Intune で管理されたデバイス。

- [Azure Active Directory の条件付きアクセス](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal):セキュリティは、クラウドを使用している組織にとって最大の関心事です。 クラウド セキュリティの重要な側面は、クラウド リソースを管理する際に id およびアクセス。 モバイル ファースト、クラウド ファーストの世界では、ユーザーがどこからでも、さまざまなデバイスとアプリを使用して、組織のリソースをアクセスできます。 このため、リソースにアクセスできるユーザーにだけ注目は不十分ですできなくなります。 セキュリティと生産性のバランスを習得するために IT プロフェッショナルもする必要があります、アクセス制御の決定にリソースのアクセス方法を考慮します。

- [VPN と条件付きアクセス](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access):VPN クライアントは、クラウド ベースの条件付きアクセス プラットフォームと統合して、リモート クライアント用のデバイス コンプライアンス オプションを提供することができるようになりました。 条件付きアクセスはポリシー ベースの評価エンジンであり、これを利用することで、Azure Active Directory (Azure AD) に接続されるアプリケーションのアクセス規則を作成できます。
