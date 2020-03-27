---
title: オンプレミスの AD に条件付きアクセス ルート証明書を展開する
description: ''
services: active-directory
ms.prod: windows-server
ms.technology: networking-ras
ms.workload: identity
ms.topic: article
ms.date: 06/28/2019
ms.author: lizross
author: eross-msft
ms.localizationpriority: medium
ms.reviewer: deverette
ms.openlocfilehash: aeb35d8c3eafd436330b66ca7d5be68d78045df0
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80307845"
---
# <a name="step-74-deploy-conditional-access-root-certificates-to-on-premises-ad"></a>手順 7.4. 条件付きアクセスルート証明書をオンプレミスの AD にデプロイする

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows 10

このステップでは、オンプレミスの AD への VPN 認証用の信頼されたルート証明書として、条件付きアクセスルート証明書をデプロイします。

- [**前へ:** 手順 7.3.条件付きアクセスポリシーを構成する](vpn-config-conditional-access-policy.md)
- [**次のようになります。** 手順 7.5.Windows 10 デバイスに OMA-URI ベースの VPNv2 プロファイルを作成する](vpn-create-oma-dm-based-vpnv2-profiles.md)

1. **[VPN 接続]** ページで、 **[証明書のダウンロード]** を選択します。

   >[!NOTE]
   >**[Base64 証明書のダウンロード]** オプションは、展開に base64 証明書を必要とする一部の構成で使用できます。

2. エンタープライズ管理者権限でドメインに参加しているコンピューターにログオンし、管理者のコマンドプロンプトから次のコマンドを実行して、クラウドのルート証明書を*エンタープライズ NTauth*ストアに追加します。

   >[!NOTE]
   >VPN サーバーが Active Directory ドメインに参加していない環境では、クラウドルート証明書を信頼された_ルート証明機関_ストアに手動で追加する必要があります。

   | コマンド | 説明 |
   | --- | --- |
   | `certutil -dspublish -f VpnCert.cer RootCA` | **Cn = AIA**および**Cn = 証明機関**のコンテナーの下に2つの**microsoft vpn ルート ca gen 1**コンテナーを作成し、各ルート証明書を**Microsoft Vpn ルート CA gen 1**コンテナーの_cacertificate を_属性の値として発行します。 |
   | `certutil -dspublish -f VpnCert.cer NTAuthCA` | Cn = **AIA**および**Cn = 証明機関**コンテナーの下に1つの**cn = ntauthcertificates**コンテナーを作成し、各ルート証明書を**Cn = ntauthcertificates**コンテナーの_cacertificate を_属性の値として発行します。 |
   | `gpupdate /force` | Windows サーバーとクライアントコンピューターにルート証明書を追加します。 |

3. ルート証明書がエンタープライズ NTauth ストアに存在し、信頼済みとして表示されていることを確認します。
   1. **証明機関管理ツール**がインストールされているエンタープライズ管理者権限でサーバーにログオンします。

   >[!NOTE]
   >既定では、**証明機関の管理ツール**は、証明機関のサーバーにインストールされます。 サーバーマネージャーの**役割管理ツール**の一部として、他のメンバーサーバーにインストールすることができます。

   1. VPN サーバーの [スタート] メニューで、「 **pkiview .msc** 」と入力して、[エンタープライズ PKI] ダイアログを開きます。
   1. [スタート] メニューから、「 **pkiview .msc** 」と入力して、[エンタープライズ PKI] ダイアログを開きます。
   1. **[エンタープライズ PKI]** を右クリックし、 **[AD コンテナーの管理]** を選択します。
   1. 各 Microsoft VPN ルート CA gen 1 証明書が次の下に存在することを確認します。
      - NTAuthCertificates
      - AIA コンテナー
      - 証明機関コンテナー

## <a name="next-steps"></a>次のステップ:

[手順 7.5.OMA-URI ベースの VPNv2 プロファイルを Windows 10 デバイスに作成](vpn-create-oma-dm-based-vpnv2-profiles.md)する: この手順では、Intune を使用して oma-uri ベースの VPNv2 プロファイルを作成し、VPN デバイス構成ポリシーを展開することができます。 VPNv2 プロファイルを作成するために Microsoft エンドポイント Configuration Manager または PowerShell スクリプトを使用する場合は、 [VPNV2 CSP の設定](https://docs.microsoft.com/windows/client-management/mdm/vpnv2-csp)に関する詳細を参照してください。
