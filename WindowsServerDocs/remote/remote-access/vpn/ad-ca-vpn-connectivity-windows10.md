---
title: Azure AD を使用した VPN 接続への条件付きアクセス
description: この省略可能な手順では、Azure Active Directory (Azure AD) 条件付きアクセスを使用して、承認された VPN ユーザーがリソースにアクセスする方法を微調整できます。
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.localizationpriority: medium
ms.author: pashort
author: shortpatti
ms.date: 06/28/2019
ms.reviewer: deverette
ms.openlocfilehash: be50c8eaf789b6f0737cbe07cf10d041d25e74f3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71388205"
---
# <a name="step-7-optional-conditional-access-for-vpn-connectivity-using-azure-ad"></a>手順 7. OptionalAzure AD を使用した VPN 接続の条件付きアクセス

- [**前へ:** 手順 6.Windows 10 クライアント Always On VPN 接続を構成する](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md)
- [**次のようになります。** 手順 7.1.証明書失効リスト (CRL) チェックを無視するように EAP-TLS を構成する](vpn-config-eap-tls-to-ignore-crl-checking.md)

この省略可能な手順では、 [Azure Active Directory (Azure AD) 条件付きアクセス](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)を使用して、VPN ユーザーがリソースにアクセスする方法を微調整できます。 仮想プライベートネットワーク (VPN) 接続の条件付きアクセスを使用する Azure AD と、VPN 接続を保護することができます。 条件付きアクセスはポリシー ベースの評価エンジンであり、これを利用することで、Azure Active Directory (Azure AD) に接続されるアプリケーションのアクセス規則を作成できます。

## <a name="prerequisites"></a>前提条件

次のトピックについて理解している必要があります。

- [Azure Active Directory での条件付きアクセス](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)
- [VPN と条件付きアクセス](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access)

VPN 接続用に Azure Active Directory 条件付きアクセスを構成するには、次の構成を行う必要があります。

- [サーバーインフラストラクチャ](always-on-vpn/deploy/vpn-deploy-server-infrastructure.md)
- [Always On VPN 用のリモートアクセスサーバー](always-on-vpn/deploy/vpn-deploy-ras.md)
- [ネットワークポリシーサーバー](always-on-vpn/deploy/vpn-deploy-nps.md)
- [DNS とファイアウォールの設定](always-on-vpn/deploy/vpn-deploy-dns-firewall.md)
- [Windows 10 クライアント Always On VPN 接続](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md)

## <a name="step-71-configure-eap-tls-to-ignore-certificate-revocation-list-crl-checkingvpn-config-eap-tls-to-ignore-crl-checkingmd"></a>[手順 7.1.証明書失効リスト (CRL) チェックを無視するように EAP-TLS を構成する](vpn-config-eap-tls-to-ignore-crl-checking.md)

この手順では、 **Ignorenorevocationcheck**を追加し、証明書に CRL 配布ポイントが含まれていない場合にクライアントの認証を許可するように設定できます。 既定では、IgnoreNoRevocationCheck は 0 (無効) に設定されています。

EAP-TLS クライアントは、NPS サーバーが証明書チェーン (ルート証明書を含む) の失効確認を完了しない限り、接続できません。 Azure AD によってユーザーに発行されたクラウド証明書には CRL がありません。有効期間が1時間の有効期間が短い証明書であるためです。 CRL の存在を無視するように NPS の EAP を構成する必要があります。 認証方法は EAP-TLS であるため、このレジストリ値は**Eap/13**の下でのみ必要です。 他の EAP 認証方法が使用されている場合は、その下にレジストリ値も追加する必要があります。

## <a name="step-72-create-root-certificates-for-vpn-authentication-with-azure-advpn-create-root-cert-for-vpn-auth-azure-admd"></a>[手順 7.2.Azure AD を使用した VPN 認証用のルート証明書の作成](vpn-create-root-cert-for-vpn-auth-azure-ad.md)

この手順では、Azure AD で VPN 認証用のルート証明書を構成します。これにより、VPN サーバークラウドアプリがテナントに自動的に作成されます。  

VPN 接続の条件付きアクセスを構成するには、次のことを行う必要があります。

1. Azure portal に VPN 証明書を作成します。
2. VPN 証明書をダウンロードします。
3. 証明書を VPN サーバーに展開します。

> [!IMPORTANT]
> Azure portal に VPN 証明書が作成されると、Azure AD は短時間の証明書を VPN クライアントに発行するためにすぐに使用を開始します。 Vpn クライアントの資格情報の検証に関する問題を回避するために、vpn 証明書を VPN サーバーに直ちに展開することが重要です。

## <a name="step-73-configure-the-conditional-access-policyvpn-config-conditional-access-policymd"></a>[手順 7.3.条件付きアクセスポリシーを構成する](vpn-config-conditional-access-policy.md)

この手順では、VPN 接続の条件付きアクセスポリシーを構成します。

条件付きアクセスポリシーを構成するには、次のことを行う必要があります。

1. VPN ユーザーに割り当てられた条件付きアクセスポリシーを作成します。
2. クラウドアプリを**VPN サーバー**に設定します。
3. **Multi-factor authentication を要求**するように許可 (アクセス制御) を設定します。  必要に応じて、他のコントロールを使用できます。

## <a name="step-74-deploy-conditional-access-root-certificates-to-on-premises-advpn-deploy-cond-access-root-cert-to-on-premise-admd"></a>[手順 7.4.条件付きアクセスルート証明書をオンプレミスの AD にデプロイする](vpn-deploy-cond-access-root-cert-to-on-premise-ad.md)

この手順では、オンプレミスの AD に VPN 認証用の信頼されたルート証明書をデプロイします。

信頼されたルート証明書を展開するには、次のことを行う必要があります。

1. ダウンロードした証明書を*VPN 認証用の信頼されたルート CA*として追加します。
2. ルート証明書を VPN サーバーおよび VPN クライアントにインポートします。
3. 証明書が存在し、信頼済みとして表示されていることを確認します。

## <a name="step-75-create-oma-dm-based-vpnv2-profiles-to-windows-10-devicesvpn-create-oma-dm-based-vpnv2-profilesmd"></a>[手順 7.5.Windows 10 デバイスに OMA-URI ベースの VPNv2 プロファイルを作成する](vpn-create-oma-dm-based-vpnv2-profiles.md)

この手順では、Intune を使用して OMA-URI ベースの VPNv2 プロファイルを作成し、VPN デバイス構成ポリシーを展開することができます。 VPNv2 プロファイルを作成するために SCCM または PowerShell スクリプトを使用する場合、詳細については、 [VPNV2 CSP 設定](https://docs.microsoft.com/windows/client-management/mdm/vpnv2-csp)を参照してください。

## <a name="next-steps"></a>次のステップ

[手順 7.1.証明書失効リスト (CRL) の確認を無視するように EAP-TLS を構成](vpn-config-eap-tls-to-ignore-crl-checking.md)する: この手順では、 **Ignorenorevocationcheck**を追加し、証明書に CRL 配布ポイントが含まれていない場合にクライアントの認証を許可するように設定する必要があります。 既定では、IgnoreNoRevocationCheck は 0 (無効) に設定されています。

## <a name="related-topics"></a>関連トピック

- [VPNv2 プロファイルを構成](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access)する: VPN クライアントは、クラウドベースの条件付きアクセスプラットフォームと統合して、リモートクライアントのデバイスコンプライアンスオプションを提供できるようになりました。 この手順では、 **\<DeviceCompliance > \<有効 > true\<有効**になっている > を使用して、VPNv2 プロファイルを構成します。

- [Windows 10 での自動 vpn プロファイルを使用したリモートアクセスの強化](https://www.microsoft.com/itshowcase/Article/Content/894/Enhancing-remote-access-in-Windows-10-with-an-automatic-VPN-profile): MICROSOFT が VPN 接続の条件付きアクセスを実装する方法について説明します。 VPN プロファイルには、サポートされている認証方法や、デバイスが接続する必要のある VPN サーバーなど、企業ネットワークに接続するためにデバイスが必要とするすべての情報が含まれます。 Windows 10 の記念日更新プログラム (条件付きアクセスやシングルサインオンを含む) の変更により、Always On VPN 接続プロファイルを作成できるようになりました。 System Center Configuration Manager コンソールを使用して、ドメインに参加し、Microsoft Intune 管理されたデバイスの接続プロファイルを作成しました。

- [Azure Active Directory での条件付きアクセス](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal): セキュリティは、クラウドを使用している組織にとって最も重要な課題です。 クラウドセキュリティの重要な側面は、クラウドリソースの管理に関して、id とアクセスです。 モバイルファースト、クラウドファーストの世界では、ユーザーはどこからでもさまざまなデバイスやアプリを使用して組織のリソースにアクセスできます。 その結果、リソースにアクセスできるユーザーだけでは不十分です。 セキュリティと生産性のバランスを習得するために、IT プロフェッショナルは、アクセス制御の決定にリソースがどのようにアクセスされるかを考慮する必要もあります。

- [Vpn と条件付きアクセス](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access): vpn クライアントは、クラウドベースの条件付きアクセスプラットフォームと統合して、リモートクライアントのデバイスコンプライアンスオプションを提供できるようになりました。 条件付きアクセスはポリシー ベースの評価エンジンであり、これを利用することで、Azure Active Directory (Azure AD) に接続されるアプリケーションのアクセス規則を作成できます。
