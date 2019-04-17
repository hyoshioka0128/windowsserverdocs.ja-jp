---
title: Windows 10 デバイスに OMA-DM ベースの VPNv2 プロファイルを作成する
description: '2 つのいずれかを使用する OMA DM を作成するメソッド ベースの VPNv2 プロファイルです。 '
services: active-directory
ms.prod: windows-server-threshold
ms.technology: networking-ras
documentationcenter: ''
ms.assetid: ''
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2018
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.reviewer: deverette
ms.openlocfilehash: 1ce20d09c304b26e3708429cc45da06d020e5809
ms.sourcegitcommit: 4147e092d77d9458696e6686bccefe3788c90508
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/28/2019
ms.locfileid: "9031296"
---
# 手順 7.5.  作成 OMA-DM ベースの Windows 10 デバイスに VPNv2 プロファイル

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows 10

& #171 です。 [**前:** 手順 7.4 します。条件付きアクセス ルート証明書をオンプレミスに展開 AD](vpn-deploy-cond-access-root-cert-to-on-premise-ad.md)<br>
& #187 です。[ **[次へ]:** 条件付きアクセス for VPN のしくみを学習](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access)

この手順では、OMA DM を作成することができますベースの VPNv2 プロファイルの VPN デバイスの構成ポリシーを展開する Intune を使用します。 SCCM または PowerShell スクリプトを使用して VPNv2 プロファイルを作成する場合は、詳細については[VPNv2 CSP の設定](https://docs.microsoft.com/windows/client-management/mdm/vpnv2-csp)を参照してください。 

## Intune を使用して管理対象の展開

このセクションで説明されているすべての情報は、VPN の条件付きアクセスと連携させるために必要な最小値です。 分割トンネリング、WIP を使用して、AutoVPN を取得するカスタムの Intune デバイス構成プロファイルまたは SSO の作成は説明しません。 [手順 5. で作成した VPN プロファイルには、以下の設定を統合します。VPN 接続で常に Windows 10 クライアントを構成する](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md)します。この例ではに統合するポリシーを[Intune を使用して、VPN クライアントを構成します](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md#configure-the-vpn-client-by-using-intune)。 

**前提条件:**<p>
Windows 10 クライアント コンピューターは、Intune を使用して、VPN 接続で既に設定されています。   


**手順:**

1. Azure portal で、クリックして**Intune** > **デバイス構成** >  [Intune を使用して、VPN クライアントの構成](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md#configure-the-vpn-client-by-using-intune)で作成した**プロファイル**と VPN プロファイルを選択します。
    
2. ポリシー エディターで、[**プロパティ**] を選択 > **設定** > **ベースの VPN**します。 VPN クライアントの最初の証明書を使用することができる機会をそのままではなく、ユーザーの証明書ストアから AAD の条件付きアクセスの証明書を取得するために必要なロジックを提供するフィルターを含めるには、既存の**EAP Xml**を拡張します。検出します。

    >[!NOTE]
    >これ、VPN クライアントは、特定の VPN 接続に失敗、オンプレミスの証明機関から発行されたユーザーの証明書を取得可能性があります。

    ![Intune ポータル](../../media/Always-On-Vpn/intune-eap-xml.png)

3. **\_LT_/AcceptServerName>\</EapType>** で終了するセクションに移動し、これら 2 つの条件付きアクセスの AAD 証明書を選択するためのロジックに VPN クライアントを提供する値の間で次の文字列を挿入します。

    ```XML
    <TLSExtensions xmlns="http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2"><FilteringInfo xmlns="http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV3"><EKUMapping><EKUMap><EKUName>AAD Conditional Access</EKUName><EKUOID>1.3.6.1.4.1.311.87</EKUOID></EKUMap></EKUMapping><ClientAuthEKUList Enabled="true"><EKUMapInList><EKUName>AAD Conditional Access</EKUName></EKUMapInList></ClientAuthEKUList></FilteringInfo></TLSExtensions>
    ```

4. **条件付きアクセス**のブレードを切り替えを**有効に****この VPN 接続の条件付きアクセス**を選択します。<p>この設定の変更**\<DeviceCompliance>\<Enabled>true\</Enabled>** VPNv2 プロファイル XML の設定を有効にします。

    ![Always On VPN のプロパティの条件付きアクセス](../../media/Always-On-Vpn/vpn-conditional-access-azure-ad.png)

6. **[OK]** をクリックします。

6. [**割り当て**、[インクルード、**含めるグループを選択**します。

7. このポリシーを受信する**VPN ユーザー**グループを選択し、[**保存**] をクリックします。

    ![自動 VPN ユーザーの割り当ての上限](../../media/Always-On-Vpn/cap-for-auto-vpn-users-assignments.png)

## クライアントの MDM ポリシーの同期を強制します。
Settings\\Network & Internet\\VPN、下、クライアント デバイスで VPN プロファイルが表示されない場合は、同期する MDM ポリシーを強制できます。

1. **VPN ユーザー**グループのメンバーとしてドメインに参加しているクライアント コンピューターにサインインします。

2. [スタート] メニューで、**アカウント**を入力し、Enter キーを押します。

3.  左側のナビゲーション ウィンドウで、[**職場または学校へ**] をクリックします。

5.  [職場または学校へ、 **<\domain> MDM に接続**をクリックし、**情報**をクリックします。

6.  [**同期**] をクリックし、Settings\\Network & Internet\\VPN [VPN プロファイルが表示されることを確認します。


## 次の手順
完了したら、Azure AD の条件付きアクセスを使用する VPN プロファイルを構成します。 

|目的の処理  |参照先  |
|---------|---------|
|Vpn の条件付きアクセスのしくみについて詳しく知る  |[VPN および条件付きアクセス](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access): このページには条件付きアクセスの詳細については、Vpn を使用します。      |
|高度な VPN 機能について詳しく知る  |[VPN の高度な機能](always-on-vpn/deploy/always-on-vpn-adv-options.md#advanced-vpn-features): このページは、VPN トラフィック フィルターを有効にする方法、アプリのトリガーを使用して自動 VPN 接続を構成する方法、および Azure によって発行された証明書を使用してクライアントから VPN 接続のみを許可するように NPS を構成する方法に関するガイダンスを示しますAD します。        |


---

## 関連トピック
- [VPNv2 CSP](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/vpnv2-csp): このトピックで説明する VPNv2 CSP の概要を説明します。 VPNv2 構成サービス プロバイダーは、デバイスの VPN プロファイルを構成するモバイル デバイス管理 (MDM) サーバーを使用します。

- [Windows 10 クライアント常に VPN 接続の構成](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/vpn-deploy-client-vpn-connections): このトピックでは ProfileXML VPN を作成する方法と、ProfileXML オプションと、スキーマに関する情報を提供します。 サーバー インフラストラクチャをセットアップしたら、VPN 接続では、そのインフラストラクチャとの通信に windows 10 クライアント コンピューターを構成する必要があります。 

- [Intune を使用して、VPN クライアントの構成](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/vpn-deploy-client-vpn-connections#configure-the-vpn-client-by-using-intune): このトピックでは、Windows 10 リモート アクセス Always On VPN プロファイルを展開する方法の情報を提供します。 Intune は、Azure AD のグループを使用してできるようになりました。 場合は、Azure AD Connect に、Azure AD をオンプレミスで VPN ユーザー グループが同期されるは、Intune を使用して VPN クライアントを構成する必要はありません。

---
