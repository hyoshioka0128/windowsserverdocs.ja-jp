---
title: Windows 10 デバイスに OMA-DM ベースの VPNv2 プロファイルを作成する
description: '2つの方法のいずれかを使用して、OMA-URI ベースの VPNv2 プロファイルを作成できます。 '
services: active-directory
ms.prod: windows-server
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
ms.openlocfilehash: 67d8a66552f77a66e1689989f412a844ef527880
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404331"
---
# <a name="step-75-create-oma-dm-based-vpnv2-profiles-to-windows-10-devices"></a>手順 7.5. Windows 10 デバイスに OMA-URI ベースの VPNv2 プロファイルを作成する

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows 10

- [**先の：** 手順 7.4. 条件付きアクセスルート証明書をオンプレミスの AD @ no__t にデプロイする
- [**次に：** VPN の条件付きアクセスのしくみについて説明します @ no__t-0

この手順では、Intune を使用して OMA-URI ベースの VPNv2 プロファイルを作成し、VPN デバイス構成ポリシーを展開することができます。 VPNv2 プロファイルを作成するために SCCM または PowerShell スクリプトを使用する場合、詳細については、 [VPNV2 CSP 設定](https://docs.microsoft.com/windows/client-management/mdm/vpnv2-csp)を参照してください。 

## <a name="managed-deployment-using-intune"></a>Intune を使用した管理された展開

このセクションで説明するすべてのものは、VPN を条件付きアクセスで動作させるために最低限必要です。 WIP を使用した分割トンネリングについては説明しません。また、カスタムの Intune デバイス構成プロファイルを作成して AutoVPN の機能を取得します。 以下の設定を [Step 5 の前に作成した VPN プロファイルに統合します。Windows 10 クライアント Always On VPN 接続を構成する @ no__t-0  この例では、 [Intune ポリシーを使用して VPN クライアントを構成](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md#configure-the-vpn-client-by-using-intune)します。 

**要件**

Windows 10 クライアントコンピューターは、Intune を使用して VPN 接続を使用して既に構成されています。   


**作業**

1. Azure portal で、[ **intune** > **デバイス構成** > **プロファイル**] を選択し、「 [intune を使用して vpn クライアントを構成](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md#configure-the-vpn-client-by-using-intune)する」の手順で作成した vpn プロファイルを選択します。
    
2. ポリシーエディターで、 **[プロパティ]** を選択し  >  [**設定** > **Base VPN**] を選択します。 既存の**EAP Xml**を拡張して、最初の証明書を使用できるようにするのではなく、ユーザーの証明書ストアから AAD 条件付きアクセス証明書を取得するために必要なロジックを VPN クライアントに付与するフィルターを含めるようにします。さ.

    >[!NOTE]
    >これを行わない場合、VPN クライアントは、オンプレミスの証明機関から発行されたユーザー証明書を取得することができ、その結果、VPN 接続が失敗します。

    ![Intune ポータル](../../media/Always-On-Vpn/intune-eap-xml.png)

3. **@No__t-1/AcceptServerName > \</EapType >** で終わるセクションを見つけて、これら2つの値の間に次の文字列を挿入します。これにより、VPN クライアントに AAD 条件付きアクセス証明書を選択するためのロジックを提供します。

    ```XML
    <TLSExtensions xmlns="http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2"><FilteringInfo xmlns="http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV3"><EKUMapping><EKUMap><EKUName>AAD Conditional Access</EKUName><EKUOID>1.3.6.1.4.1.311.87</EKUOID></EKUMap></EKUMapping><ClientAuthEKUList Enabled="true"><EKUMapInList><EKUName>AAD Conditional Access</EKUName></EKUMapInList></ClientAuthEKUList></FilteringInfo></TLSExtensions>
    ```

4. **[条件付きアクセス]** ブレードを選択し、**この VPN 接続のトグル条件付きアクセス**を**有効**にします。
   
   この設定を有効にすると、VPNv2 Profile XML 内の **\<DeviceCompliance > \<Enabled > true @ no__t/enabled >** 設定が変更されます。

    ![Always On VPN の条件付きアクセス-プロパティ](../../media/Always-On-Vpn/vpn-conditional-access-azure-ad.png)

5. **[OK]** を選択します。

6. **[割り当て]** を選択し、含める で **[含めるグループ]** を選択 を選択します。

7. このポリシーを受信する**VPN ユーザー**グループを選択し、 **[保存]** を選択します。

    ![自動 VPN ユーザーの上限-割り当て](../../media/Always-On-Vpn/cap-for-auto-vpn-users-assignments.png)

## <a name="force-mdm-policy-sync-on-the-client"></a>クライアントで MDM ポリシーの同期を強制する

VPN プロファイルがクライアントデバイスに表示されない場合は、[設定 @ no__t-0Network & Internet @ no__t-1VPN] で、MDM ポリシーを強制的に同期させることができます。

1. ドメインに参加しているクライアントコンピューターに、 **VPN ユーザー**グループのメンバーとしてサインインします。

2. [スタート] メニューで、「 **account**」と入力し、enter キーを押します。

3. 左側のナビゲーションウィンドウで、[**職場または学校にアクセス**する] を選択します。

4. [職場または学校にアクセスする] で、[接続先] を選択し **< \domain > MDM**に選択し、 **[情報]** を選択します。

5. **同期** を選択し、設定 @ No__t-1network & Internet @ NO__T-2vpn の下に vpn プロファイルが表示されていることを確認します。


## <a name="next-steps"></a>次の手順

Azure AD 条件付きアクセスを使用するように VPN プロファイルを構成しました。 

|目的の処理  |参照先  |
|---------|---------|
|Vpn での条件付きアクセスのしくみについての詳細情報  |[VPN と条件付きアクセス](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access):このページでは、Vpn での条件付きアクセスのしくみについて詳しく説明します。      |
|高度な VPN 機能についての詳細情報  |[高度な VPN 機能](always-on-vpn/deploy/always-on-vpn-adv-options.md#advanced-vpn-features):このページでは、VPN トラフィックフィルターを有効にする方法、アプリトリガーを使用した自動 VPN 接続の構成方法、Azure AD によって発行された証明書を使用するクライアントからの VPN 接続のみを許可するように NPS を構成する方法について説明します。        |


## <a name="related-topics"></a>関連トピック

- [VPNV2 CSP](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/vpnv2-csp):このトピックでは、VPNv2 CSP の概要について説明します。 VPNv2 構成サービスプロバイダーを使用すると、モバイルデバイス管理 (MDM) サーバーでデバイスの VPN プロファイルを構成できます。

- [Windows 10 クライアント ALWAYS ON VPN 接続を構成](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/vpn-deploy-client-vpn-connections)します。このトピックでは、ProfileXML オプションとスキーマ、および ProfileXML VPN の作成方法について説明します。 サーバーインフラストラクチャを設定したら、VPN 接続を使用して、そのインフラストラクチャと通信するように Windows 10 クライアントコンピューターを構成する必要があります。 

- [Intune を使用して VPN クライアントを構成する](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/vpn-deploy-client-vpn-connections#configure-the-vpn-client-by-using-intune):このトピックでは、Windows 10 リモートアクセス Always On VPN プロファイルを展開する方法について説明します。 Intune で Azure AD グループが使用されるようになりました。 VPN ユーザーグループをオンプレミスから Azure AD に同期 Azure AD Connect 場合、Intune を使用して VPN クライアントを構成する必要はありません。
