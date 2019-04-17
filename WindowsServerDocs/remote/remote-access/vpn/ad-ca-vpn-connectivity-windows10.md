---
title: Azure AD を使用した VPN 接続への条件付きアクセス
description: このオプションの手順では、VPN ユーザー アクセスを承認する方法に条件付きアクセスの Azure Active Directory (Azure AD) を使って、リソースを微調整できます。
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.topic: article
ms.assetid: ''
ms.localizationpriority: medium
ms.author: pashort
author: shortpatti
ms.date: 07/13/2018
ms.reviewer: deverette
ms.openlocfilehash: c9104a5d9ae3069e753b8b771270502c4264db96
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2018
ms.locfileid: "6067299"
---
# 手順 7.  (省略可能)Azure AD を使用して VPN 接続の条件付きアクセス

& #171 です。 [**前:** 手順 6 します。VPN 接続で常に Windows 10 クライアントを構成します。](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md)<br>
& #187 です。[ **[次へ]:** 手順 7.1 します。構成証明書失効リスト (CRL) チェックを無視するには、EAP-TLS](vpn-config-eap-tls-to-ignore-crl-checking.md)

このオプションの手順では、VPN ユーザーが[Azure Active Directory (Azure AD) の条件付きアクセス](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)を使って、リソースにアクセスする方法を微調整できます。 仮想プライベート ネットワーク (VPN) 接続の条件付きアクセスを Azure AD、VPN 接続を保護できます。 条件付きアクセスはポリシー ベースの評価エンジンであり、これを利用することで、Azure Active Directory (Azure AD) に接続されるアプリケーションのアクセス規則を作成できます。 

## 前提条件

次のトピックに慣れて。
- [Azure Active Directory の条件付きアクセス](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal)
- [VPN および条件付きアクセス](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access)

VPN 接続の Azure Active Directory の条件付きアクセスを構成するには、次の構成されている必要があります。
- [サーバー インフラストラクチャ](always-on-vpn/deploy/vpn-deploy-server-infrastructure.md)
- [Always On VPN のリモート アクセス サーバー](always-on-vpn/deploy/vpn-deploy-ras.md)
- [ネットワーク ポリシー サーバー](always-on-vpn/deploy/vpn-deploy-nps.md)
- [DNS とファイアウォールの設定](always-on-vpn/deploy/vpn-deploy-dns-firewall.md)
- [Always On VPN 接続の Windows 10 クライアント](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md)

## [手順 7.1.  証明書失効リスト (CRL) が無視されるように EAP-TLS を構成する](vpn-config-eap-tls-to-ignore-crl-checking.md)

この手順では、 **IgnoreNoRevocationCheck**を追加し、証明書に CRL 配布ポイントが含まれていない場合は、クライアントの認証を許可するように設定します。 既定では、IgnoreNoRevocationCheck が 0 (無効) に設定されます。

NPS サーバー (ルート証明書を含む) の証明書チェーンの失効チェックが完了するとしない限り、EAP-TLS クライアントが接続できません。 Azure AD によって、ユーザーに発行された証明書をクラウドでは、1 時間の有効期間での有効期間が短い証明書であるため、CRL を必要はありません。 NPS で EAP crl 休暇を無視するように構成する必要があります。 認証方法は、EAP-TLS であるために、このレジストリ値は**EAP\13**でのみ必要です。 他の EAP 認証方法を使用している場合、レジストリ値する必要があります下に追加されるものもします。 




## [手順 7.2.  Azure AD で VPN 認証のルート証明書を作成する](vpn-create-root-cert-for-vpn-auth-azure-ad.md)

この手順では、テナントに自動的に VPN サーバーのクラウド アプリを作成する、Azure AD を使って VPN 認証のルート証明書を構成します。  

VPN 接続の条件付きアクセスを構成する必要があります。
1. (複数の証明書を作成することができます)、Azure portal での VPN 証明書を作成します。
2. VPN 証明書をダウンロードします。
3. VPN サーバーに証明書を展開します。

## [手順 7.3.  条件付きアクセス ポリシーを構成する](vpn-config-conditional-access-policy.md)

この手順では、VPN 接続の条件付きアクセス ポリシーを構成します。 

条件付きアクセス ポリシーを構成する必要があります。
1. VPN ユーザーに割り当てられている条件付きアクセス ポリシーを作成します。
2. **VPN サーバー**には、クラウド アプリを設定します。
3. **多要素認証を要求**するには、許可 (アクセス制御) を設定します。  必要に応じて、その他のコントロールを使用することができます。

## [手順 7.4.  条件付きアクセスのルート証明書をオンプレミスに展開 AD](vpn-deploy-cond-access-root-cert-to-on-premise-ad.md)

この手順でオンプレミスに VPN 認証用の信頼されたルート証明書を展開する AD します。

信頼されたルート証明書を展開する必要があります。
1. *信頼されたルート CA VPN 認証*として、ダウンロードした証明書を追加します。
2. VPN サーバーと VPN クライアントには、ルート証明書をインポートします。
3. 証明書が存在して、表示することを確認信頼されました。


## [手順 7.5.  Windows 10 デバイスに OMA-DM ベースの VPNv2 プロファイルを作成する](vpn-create-oma-dm-based-vpnv2-profiles.md)

この手順では、OMA DM を作成することができますベースのデバイス構成の VPN ポリシーを展開する Intune を使用して、VPNv2 プロファイルです。 VPNv2 プロファイルを作成する SCCM または PowerShell スクリプトを使用する場合は、詳細は[VPNv2 CSP の設定](https://docs.microsoft.com/windows/client-management/mdm/vpnv2-csp)を参照してください。 


## 次の手順
[手順 7.1 です。構成証明書失効リスト (CRL) チェックを無視するには、EAP-TLS](vpn-config-eap-tls-to-ignore-crl-checking.md): この手順で、 **IgnoreNoRevocationCheck**を追加し、証明書に CRL 配布ポイントが含まれていない場合は、クライアントの認証を許可するように設定する必要があります。 既定では、IgnoreNoRevocationCheck が 0 (無効) に設定されます。

---

## 関連トピック
- [VPNv2 プロファイルの構成](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access): VPN クライアントは、リモート クライアント用のデバイス コンプライアンスのオプションを提供するクラウド ベースの条件付きアクセス プラットフォームと統合することができるようになりました。 この手順でによる VPNv2 プロファイルを構成する**\ < DeviceCompliance > \ < 有効 > true\ </有効になっている >** します。 
 
- [自動の VPN プロファイルを使って Windows 10 でのリモート アクセスの向上](https://www.microsoft.com/itshowcase/Article/Content/894/Enhancing-remote-access-in-Windows-10-with-an-automatic-VPN-profile): Microsoft VPN 接続の条件付きアクセスを実装する方法について説明します。 VPN プロファイルには、デバイスがサポートされている認証方法と、VPN サーバーに接続するデバイスを含め、企業ネットワークへの接続に必要とするすべての情報が含まれます。 条件付きアクセスとシングル サインオンを含む、Windows 10 Anniversary Update での変更を行った、Always-On VPN 接続プロファイルを作成することも可能です。 に対する接続プロファイルを作成したドメインに参加していると System Center Configuration Manager コンソールを使用して Microsoft Intune で管理されたデバイス。 

- [Azure Active Directory でアクセス条件](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal): セキュリティは、クラウドを使用する組織にとって重要です。 クラウドのセキュリティの重要な側面は、クラウド リソースを管理する際に、id とアクセスします。 モバイル ファースト、クラウド ファーストの世界では、ユーザーはどこからでも、さまざまなデバイスとアプリを使用して、組織のリソースにアクセスできます。 このため、リソースにアクセスできるユーザーにのみ重点を置いて不十分ですできなくなりました。 マスターのセキュリティと生産性のバランスをするために IT 担当者は要因へのアクセス制御の意思決定にリソースにアクセスする方法も必要です。

- [VPN および条件付きアクセス](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access): VPN クライアントは、リモート クライアント用のデバイス コンプライアンスのオプションを提供するクラウド ベースの条件付きアクセス プラットフォームと統合することができるようになりました。 条件付きアクセスはポリシー ベースの評価エンジンであり、これを利用することで、Azure Active Directory (Azure AD) に接続されるアプリケーションのアクセス規則を作成できます。 

---