---
title: オンプレミスの AD に条件付きアクセス ルート証明書を展開する
description: ''
services: active-directory
ms.prod: windows-server-threshold
ms.technology: networking-ras
ms.workload: identity
ms.topic: article
ms.date: 06/28/2019
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.reviewer: deverette
ms.openlocfilehash: 200d3b96ee24b5e1264b4bf2e42d636f9e07fbef
ms.sourcegitcommit: 63926404009f9e1330a4a0aa8cb9821a2dd7187e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/29/2019
ms.locfileid: "67469678"
---
# <a name="step-74-deploy-conditional-access-root-certificates-to-on-premises-ad"></a>手順 7.4. ルート証明書の条件付きアクセスをオンプレミスにデプロイ AD

>適用対象:Windows Server 2016、Windows Server 2012 R2、Windows 10 の Windows Server (半期チャネル)

この手順では、条件付きアクセスのルート証明書として展開 VPN 認証用の信頼されたルート証明書をオンプレミス AD。

- [**先の：** 手順 7.3. 条件付きアクセス ポリシーを構成する](vpn-config-conditional-access-policy.md)
- [**次に：** 手順 7.5. Windows 10 デバイスに OMA-DM ベースの VPNv2 プロファイルを作成する](vpn-create-oma-dm-based-vpnv2-profiles.md)

1. **VPN 接続**] ページで、[**証明書のダウンロード**します。

   >[!NOTE]
   >**Base64 証明書のダウンロード**オプションは、展開を base64 証明書を必要とするいくつかの構成を使用します。

2. エンタープライズ管理者権限と実行、cloud を追加する管理者のコマンド プロンプトから次のコマンド ルートに証明書をドメインに参加しているコンピューターにログオン、 *Enterprise NTauth*を格納します。

   >[!NOTE]
   >VPN サーバーが Active Directory ドメインに参加していない、環境、クラウドのルート証明書に追加する必要があります、_信頼されたルート証明機関_手動で保存します。

   | コマンド | 説明 |
   | --- | --- |
   | `certutil -dspublish -f VpnCert.cer RootCA` | 2 つ作成されます**Microsoft VPN ルート CA gen 1**下にあるコンテナー、 **CN = AIA**と**CN 証明機関を =** コンテナー、しの値として各ルート証明書を発行_cACertificate_両方の属性**Microsoft VPN ルート CA gen 1**コンテナー。 |
   | `certutil -dspublish -f VpnCert.cer NTAuthCA` | 1 つ作成**CN = NTAuthCertificates**の下のコンテナー、 **CN = AIA**と**CN 証明機関を =** コンテナー、しの値として各ルート証明書を発行_cACertificate_の属性、 **CN = NTAuthCertificates**コンテナー。 |
   | `gpupdate /force` | Windows サーバーおよびクライアント コンピューターにルート証明書を追加する迅速に処理します。 |

3. ルート証明書が信頼済みとして表示するエンタープライズ NTauth ストア内にあることを確認します。
   1. 持つエンタープライズ管理者権限を持つサーバーにログオン、**証明書機関の管理ツール**をインストールします。

   >[!NOTE]
   >既定では、**証明書機関の管理ツール**証明機関サーバーがインストールされています。 一部として他のメンバー サーバーにインストールすることができます、**役割管理ツール**サーバー マネージャーでします。

   1. VPN サーバーの [スタート] メニューで、[次のように入力します。 **pkiview.msc**エンタープライズ PKI] ダイアログを開きます。
   1. スタート メニューから次のように入力します。 **pkiview.msc**エンタープライズ PKI ダイアログを開きます。
   1. 右クリック**エンタープライズ PKI**選択**AD コンテナーの管理**します。
   1. 各 Microsoft VPN ルート CA gen 1 証明書が 存在することを確認するには。
      - NTAuthCertificates
      - AIA コンテナー
      - 証明書機関コンテナー

## <a name="next-steps"></a>次のステップ

[手順 7.5.作成、OMA-DM ベースの Windows 10 デバイスに VPNv2 プロファイル](vpn-create-oma-dm-based-vpnv2-profiles.md):この手順では、OMA-DM を作成できますベースの VPNv2 プロファイルが Intune を使用して VPN デバイス構成ポリシーを展開します。 VPNv2 プロファイルを作成する SCCM または PowerShell スクリプトを指定する場合は参照[VPNv2 CSP 設定](https://docs.microsoft.com/windows/client-management/mdm/vpnv2-csp)の詳細。
