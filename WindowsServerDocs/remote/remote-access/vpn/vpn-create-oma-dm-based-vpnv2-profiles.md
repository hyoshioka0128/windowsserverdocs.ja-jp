---
title: Windows 10 デバイスに OMA-DM ベースの VPNv2 プロファイルを作成する
description: '2 つのいずれかを使用することができます、OMA-DM を作成するメソッド ベースの VPNv2 プロファイル。 '
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
ms.openlocfilehash: 9051a5b4dc8055885bdc1f8f727514b6e049d74d
ms.sourcegitcommit: 0948a1abff1c1be506216eeb51ffc6f752a9fe7e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2019
ms.locfileid: "66749506"
---
# <a name="step-75-create-oma-dm-based-vpnv2-profiles-to-windows-10-devices"></a>手順 7.5. 作成、OMA-DM ベースの Windows 10 デバイスへの VPNv2 プロファイル

>適用先:Windows Server 2016、Windows Server 2012 R2、Windows 10 の Windows Server (半期チャネル)

- [**先の：** 手順 7.4. ルート証明書の条件付きアクセスをオンプレミスにデプロイ AD](vpn-deploy-cond-access-root-cert-to-on-premise-ad.md)
- [**次に：** 条件付きアクセスの VPN 機能について説明します](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access)

この手順では、OMA-DM を作成できますベースの VPNv2 プロファイルが Intune を使用して VPN デバイス構成ポリシーを展開します。 VPNv2 プロファイルを作成するを参照してください、SCCM または PowerShell スクリプトを使用したい場合[VPNv2 CSP 設定](https://docs.microsoft.com/windows/client-management/mdm/vpnv2-csp)の詳細。 

## <a name="managed-deployment-using-intune"></a>Intune を使用して管理対象の展開

このセクションで説明したすべてのものは、VPN の条件付きアクセスを処理するために必要な最小値です。 分割トンネリングは、WIP を使用して、または SSO の操作、AutoVPN を取得するカスタムの Intune デバイス構成プロファイルを作成するには含まれません。 以下の設定に、VPN プロファイルの下で、先ほど作成した統合[手順 5 です。VPN 接続で常に Windows 10 クライアントを構成](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md)します。  この例で統合に、 [Intune を使用して、VPN クライアントを構成する](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md#configure-the-vpn-client-by-using-intune)ポリシー。 

**前提条件:**

Intune を使用して VPN 接続を Windows 10 クライアント コンピューターは既に構成されています。   


**手順:**

1. Azure portal で次のように選択します**Intune** > **デバイス構成** > **プロファイル**で先ほど作成したVPNプロファイルを選択します。[Intune を使用して、VPN クライアントを構成する](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md#configure-the-vpn-client-by-using-intune)します。
    
2. ポリシー エディターで**プロパティ** > **設定** > **基本 VPN**します。 既存の拡張**EAP Xml** VPN クライアントのロジックを提供するフィルターを含めるように、最初に使用することができます可能性を残さずに、ユーザーの証明書ストアから AAD の条件付きアクセスの証明書を取得する必要があります証明書が検出されました。

    >[!NOTE]
    >これを行わない、VPN クライアントは、特定 VPN 接続の失敗の結果、オンプレミスでの証明機関から発行されたユーザー証明書を取得でした。

    ![Intune ポータル](../../media/Always-On-Vpn/intune-eap-xml.png)

3. 終了するセクションを見つけます **\</AcceptServerName >\</EapType >** AAD 条件を選択するためのロジックに VPN クライアントを提供するこれら 2 つの値の間で、次の文字列を挿入アクセスの証明書:

    ```XML
    <TLSExtensions xmlns="http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2"><FilteringInfo xmlns="http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV3"><EKUMapping><EKUMap><EKUName>AAD Conditional Access</EKUName><EKUOID>1.3.6.1.4.1.311.87</EKUOID></EKUMap></EKUMapping><ClientAuthEKUList Enabled="true"><EKUMapInList><EKUName>AAD Conditional Access</EKUName></EKUMapInList></ClientAuthEKUList></FilteringInfo></TLSExtensions>
    ```

4. 選択、**条件付きアクセス**ブレードとトグル**この VPN 接続の条件付きアクセス**に**有効**します。
   
   この設定の変更を有効、  **\<DeviceCompliance >\<有効 > true\</有効に >** VPNv2 プロファイル xml を設定します。

    ![Always On VPN - プロパティの条件付きアクセス](../../media/Always-On-Vpn/vpn-conditional-access-azure-ad.png)

5. **[OK]** を選択します。

6. 選択**割り当て**、Include の **含めるグループを選択**します。

7. 選択、 **VPN ユーザー**ポリシーおよび選択を受信するグループ**保存**します。

    ![自動 VPN ユーザーの割り当ての上限](../../media/Always-On-Vpn/cap-for-auto-vpn-users-assignments.png)

## <a name="force-mdm-policy-sync-on-the-client"></a>クライアントを MDM のポリシー同期を強制します。

[設定] で、クライアント デバイス上に VPN プロファイルが表示されない場合\\ネットワークとインターネット\\VPN、同期を MDM ポリシーを強制することができます。

1. メンバーとして、ドメインに参加しているクライアント コンピューターにサインイン、 **VPN ユーザー**グループ。

2. [スタート] メニューで、次のように入力します。**アカウント**、Enter キーを押します。

3. 左側のナビゲーション ウィンドウで選択**アクセス職場または学校**します。

4. アクセスの職場または学校では、次のように選択します。 **< \domain > MDM に接続されている**を選択し、**情報**します。

5. 選択**同期**[設定] で VPN プロファイルが表示されることを確認および\\ネットワークとインターネット\\VPN。


## <a name="next-steps"></a>次のステップ

完了したら Azure AD 条件付きアクセスを使用する VPN プロファイルを構成します。 

|目的の処理  |参照先  |
|---------|---------|
|Vpn を使用した条件付きアクセスの動作の詳細します。  |[VPN と条件付きアクセス](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access):このページは、条件付きアクセスの詳細については、Vpn を使用した機能を提供します。      |
|高度な VPN 機能を詳細します。  |[VPN 機能を高度な](always-on-vpn/deploy/always-on-vpn-adv-options.md#advanced-vpn-features):このページは、VPN トラフィックのフィルターを有効にする方法、アプリのトリガーを使用した自動 VPN 接続を構成する方法、および Azure AD によって発行された証明書を使用するクライアントから VPN 接続のみを許可するように NPS を構成する方法のガイダンスを提供します。        |


## <a name="related-topics"></a>関連トピック

- [VPNv2 CSP](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/vpnv2-csp):このトピックでは、VPNv2 CSP の概要について説明します。 VPNv2 構成サービス プロバイダーがデバイスの VPN プロファイルを構成するモバイル デバイス管理 (MDM) サーバーを許可します。

- [VPN 接続で常に Windows 10 クライアントを構成](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/vpn-deploy-client-vpn-connections):このトピックでは、それを ProfileXML オプションとスキーマについては、それを ProfileXML VPN を作成する方法を提供します。 サーバー インフラストラクチャを設定した後は、VPN 接続を持つそのインフラストラクチャと通信するために Windows 10 クライアント コンピューターを構成する必要があります。 

- [Intune を使用して、VPN クライアントを構成する](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/vpn-deploy-client-vpn-connections#configure-the-vpn-client-by-using-intune):このトピックでは、Windows 10 のリモート アクセス常に VPN プロファイルを展開する方法について説明します。 Intune は、Azure AD グループを使用します。 Azure AD Connect は、Intune を使用して VPN クライアントを構成する必要はありませんし、オンプレミスから、Azure AD への VPN ユーザー グループを同期します。 場合、
