---
title: Azure AD を使用した VPN 接続への条件付きアクセス
description: この省略可能な手順では、Azure Active Directory (Azure AD) 条件付きアクセスを使用して、承認された VPN ユーザーがリソースにアクセスする方法を微調整できます。
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.localizationpriority: medium
ms.author: v-tea
author: Teresa-MOTIV
ms.date: 06/28/2019
ms.reviewer: deverette
ms.openlocfilehash: da32df185cb0c0c2370e60119dd9c2fbd510bd08
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86964264"
---
# <a name="step-7-optional-conditional-access-for-vpn-connectivity-using-azure-ad"></a>手順 7. OptionalAzure AD を使用した VPN 接続の条件付きアクセス

- [**前へ:** 手順 6.Windows 10 クライアント Always On VPN 接続を構成する](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md)
- [**次のようになります。** 手順 7.1.証明書失効リスト (CRL) チェックを無視するように EAP-TLS を構成する](vpn-config-eap-tls-to-ignore-crl-checking.md)

この省略可能な手順では、 [Azure Active Directory (Azure AD) 条件付きアクセス](/azure/active-directory/active-directory-conditional-access-azure-portal)を使用して、VPN ユーザーがリソースにアクセスする方法を微調整できます。 仮想プライベートネットワーク (VPN) 接続の条件付きアクセスを使用する Azure AD と、VPN 接続を保護することができます。 条件付きアクセスはポリシー ベースの評価エンジンであり、これを利用することで、Azure Active Directory (Azure AD) に接続されるアプリケーションのアクセス規則を作成できます。

## <a name="prerequisites"></a>前提条件

次のトピックについて理解している必要があります。

- [Azure Active Directory での条件付きアクセス](/azure/active-directory/active-directory-conditional-access-azure-portal)
- [VPN と条件付きアクセス](/windows/access-protection/vpn/vpn-conditional-access)

VPN 接続用に Azure Active Directory 条件付きアクセスを構成するには、次の構成を行う必要があります。

- [サーバーインフラストラクチャ](always-on-vpn/deploy/vpn-deploy-server-infrastructure.md)
- [Always On VPN 用のリモートアクセスサーバー](always-on-vpn/deploy/vpn-deploy-ras.md)
- [ネットワーク ポリシー サーバー](always-on-vpn/deploy/vpn-deploy-nps.md)
- [DNS とファイアウォールの設定](always-on-vpn/deploy/vpn-deploy-dns-firewall.md)
- [Windows 10 クライアント Always On VPN 接続](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md)

## <a name="step-71-configure-eap-tls-to-ignore-certificate-revocation-list-crl-checking"></a>[手順 7.1.証明書失効リスト (CRL) の確認が無視されるように EAP-TLS を構成する](vpn-config-eap-tls-to-ignore-crl-checking.md)

この手順では、 **Ignorenorevocationcheck**を追加し、証明書に CRL 配布ポイントが含まれていない場合にクライアントの認証を許可するように設定できます。 既定では、IgnoreNoRevocationCheck は 0 (無効) に設定されています。

EAP-TLS クライアントは、NPS サーバーが証明書チェーン (ルート証明書を含む) の失効確認を完了しない限り、接続できません。 Azure AD によってユーザーに発行されたクラウド証明書には CRL がありません。有効期間が1時間の有効期間が短い証明書であるためです。 CRL の存在を無視するように NPS の EAP を構成する必要があります。 認証方法は EAP-TLS であるため、このレジストリ値は**Eap/13**の下でのみ必要です。 他の EAP 認証方法が使用されている場合は、その下にレジストリ値も追加する必要があります。

## <a name="step-72-create-root-certificates-for-vpn-authentication-with-azure-ad"></a>[手順 7.2.Azure AD で VPN 認証のルート証明書を作成する](vpn-create-root-cert-for-vpn-auth-azure-ad.md)

この手順では、Azure AD で VPN 認証用のルート証明書を構成します。これにより、VPN サーバークラウドアプリがテナントに自動的に作成されます。  

VPN 接続用の条件付きアクセスを構成するには、以下の操作を行う必要があります。

1. Azure Portal で VPN 証明書を作成する。
2. VPN 証明書をダウンロードする。
3. 証明書を VPN サーバーにデプロイする。

> [!IMPORTANT]
> Azure portal に VPN 証明書が作成されると、Azure AD は短時間の証明書を VPN クライアントに発行するためにすぐに使用を開始します。 Vpn クライアントの資格情報の検証に関する問題を回避するために、vpn 証明書を VPN サーバーに直ちに展開することが重要です。

## <a name="step-73-configure-the-conditional-access-policy"></a>[手順 7.3.条件付きアクセス ポリシーを構成する](vpn-config-conditional-access-policy.md)

この手順では、VPN 接続の条件付きアクセスポリシーを構成します。

条件付きアクセスポリシーを構成するには、次のことを行う必要があります。

1. VPN ユーザーに割り当てられた条件付きアクセスポリシーを作成します。
2. クラウドアプリを**VPN サーバー**に設定します。
3. **Multi-factor authentication を要求**するように許可 (アクセス制御) を設定します。  必要に応じて、他のコントロールを使用できます。

## <a name="step-74-deploy-conditional-access-root-certificates-to-on-premises-ad"></a>[手順 7.4.条件付きアクセスルート証明書をオンプレミスの AD にデプロイする](vpn-deploy-cond-access-root-cert-to-on-premise-ad.md)

この手順では、オンプレミスの AD に VPN 認証用の信頼されたルート証明書をデプロイします。

信頼されたルート証明書を展開するには、次のことを行う必要があります。

1. ダウンロードした証明書を*VPN 認証用の信頼されたルート CA*として追加します。
2. ルート証明書を VPN サーバーおよび VPN クライアントにインポートします。
3. 証明書が存在し、信頼済みとして表示されていることを確認します。

## <a name="step-75-create-oma-dm-based-vpnv2-profiles-to-windows-10-devices"></a>[手順 7.5.Windows 10 デバイスに OMA-DM ベースの VPNv2 プロファイルを作成する](vpn-create-oma-dm-based-vpnv2-profiles.md)

この手順では、Intune を使用して OMA-URI ベースの VPNv2 プロファイルを作成し、VPN デバイス構成ポリシーを展開することができます。 Configuration Manager または PowerShell スクリプトを使用して VPNv2 プロファイルを作成する場合、詳細については、 [VPNV2 CSP 設定](/windows/client-management/mdm/vpnv2-csp)を参照してください。

## <a name="next-steps"></a>次のステップ

[手順 7.1.証明書失効リスト (CRL) の確認を無視するように EAP-TLS を構成](vpn-config-eap-tls-to-ignore-crl-checking.md)する: この手順では、 **Ignorenorevocationcheck**を追加し、証明書に CRL 配布ポイントが含まれていない場合にクライアントの認証を許可するように設定する必要があります。 既定では、IgnoreNoRevocationCheck は 0 (無効) に設定されています。

## <a name="related-topics"></a>関連トピック

- [VPNv2 プロファイルを構成](/windows/access-protection/vpn/vpn-conditional-access)する: VPN クライアントは、クラウドベースの条件付きアクセスプラットフォームと統合して、リモートクライアントのデバイスコンプライアンスオプションを提供できるようになりました。 このステップでは、VPNv2 プロファイルを** \<DeviceCompliance> \<Enabled> true \</Enabled> **に設定します。

- [Windows 10 での自動 vpn プロファイルを使用したリモートアクセスの強化](https://www.microsoft.com/itshowcase/Article/Content/894/Enhancing-remote-access-in-Windows-10-with-an-automatic-VPN-profile): MICROSOFT が VPN 接続の条件付きアクセスを実装する方法について説明します。 VPN プロファイルには、サポートされている認証方法や、デバイスが接続する必要のある VPN サーバーなど、企業ネットワークに接続するためにデバイスが必要とするすべての情報が含まれます。 Windows 10 の記念日更新プログラム (条件付きアクセスやシングルサインオンを含む) の変更により、Always On VPN 接続プロファイルを作成できるようになりました。

- [Azure Active Directory での条件付きアクセス](/azure/active-directory/active-directory-conditional-access-azure-portal): セキュリティは、クラウドを使用している組織にとって最も重要な課題です。 クラウド セキュリティの重要な側面は、クラウド リソースを管理する際の ID とアクセスです。 モバイルを重視したクラウド中心の世界では、ユーザーはさまざまなデバイスやアプリを使用してどこからでも組織のリソースにアクセスできます。 このため、だれがリソースにアクセスできるかに重点を置くだけでは十分ではなくなっています。 セキュリティと生産性のバランスを習得するために、IT プロフェッショナルは、リソースへのアクセス方法も考慮してアクセスの制御を決定する必要があります。

- [Vpn と条件付きアクセス](/windows/access-protection/vpn/vpn-conditional-access): vpn クライアントは、クラウドベースの条件付きアクセスプラットフォームと統合して、リモートクライアントのデバイスコンプライアンスオプションを提供できるようになりました。 条件付きアクセスはポリシー ベースの評価エンジンであり、これを利用することで、Azure Active Directory (Azure AD) に接続されるアプリケーションのアクセス規則を作成できます。
