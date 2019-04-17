---
title: オンプレミスの AD に条件付きアクセス ルート証明書を展開する
description: ''
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
ms.openlocfilehash: 210540846f5d62dfc74a2e629a6b7675ccf9894d
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2018
ms.locfileid: "6067307"
---
# 手順 7.4.  条件付きアクセスのルート証明書をオンプレミスに展開 AD

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows 10

この手順でに展開する条件付きアクセスのルート証明書 VPN 認証のための信頼されたルート証明書としてオンプレミス AD します。

& #171 です。 [**前:** 手順 7.3 します。条件付きアクセス ポリシーを構成します。](vpn-config-conditional-access-policy.md)<br>
& #187 です。[ **[次へ]:** 手順 7.5 します。作成 OMA DM は、Windows 10 デバイスに VPNv2 プロファイルをベース](vpn-create-oma-dm-based-vpnv2-profiles.md)

1. **VPN 接続**] ページで、[**証明書をダウンロード**] をクリックします。 
   
    ![条件付きアクセス用の証明書をダウンロードします。](../../media/Always-On-Vpn/06.png)

    >[!NOTE]
    >**Base64 証明書をダウンロード**オプションは、展開の base64 証明書を必要とする一部の構成に使用できます。 

2. エンタープライズ管理者権限を持つドメインに参加しているコンピューターにログオンし、*エンタープライズ NTauth*ストアにクラウドのルート証明書を追加する管理者のコマンド プロンプトから次のコマンドを実行します。

    >[!NOTE]
    >VPN サーバーが Active Directory ドメインに参加していない場所環境には、_信頼されたルート証明機関_ストアに手動でクラウド ルート証明書を追加します。

    |コマンド  |説明  |  
    |---------|-------------| 
    |`certutil -dspublish -f VpnCert.cer RootCA`     |下にある 2 つの**Microsoft VPN ルート CA 世代 1**コンテナーを作成、 **CN = AIA**と**CN = 証明機関**コンテナー、し、両方**Microsoft VPN ルートの_cACertificate_属性の値としての各ルート証明書の公開CA 世代 1**コンテナー。|  
    |`certutil -dspublish -f VpnCert.cer NTAuthCA`   |1 つ作成**CN = NTAuthCertificates**の下のコンテナー、 **CN = AIA**と**CN = 証明機関**コンテナー、 **CN の_cACertificate_属性の値として各ルート証明書を発行し、=NTAuthCertificates**コンテナー。 |  
    |`gpupdate /force`     |ルート証明書を追加する、Windows サーバーおよびクライアント コンピューターに迅速に処理します。  |

3.  ルート証明書がエンタープライズ NTauth ストアと信頼済みと表示であることを確認するには。

    a.   インストールされている**証明書機関の管理ツール**を持つ企業の管理者権限を持つサーバーにログオンします。

    >[!NOTE]
    >既定では、**証明書機関の管理ツール**はインストールされている証明書機関サーバーです。 これらは、サーバー マネージャーで**役割管理ツール**の一部として他のメンバー サーバーにインストールできます。

    b.   VPN サーバーで、スタート メニューで、エンタープライズ PKI ダイアログを開く**pkiview.msc**を入力します。

    c.  スタート メニューからエンタープライズ PKI ダイアログを開く**pkiview.msc**を入力します。

    d.  **エンタープライズ PKI**を右クリックし、**広告のコンテナーの管理**を選択します。

    d.  各 Microsoft VPN ルート CA 世代 1 証明書が下に存在することを確認します。<ul><li>NTAuthCertificates</li><li>AIA コンテナー</li><li>証明書機関コンテナー</li></ul>

    
## 次の手順
[手順 7.5 です。作成 OMA DM は、Windows 10 デバイスに VPNv2 プロファイルをベース](vpn-create-oma-dm-based-vpnv2-profiles.md): この手順では、OMA DM を作成することができますベースのデバイス構成の VPN ポリシーを展開する Intune を使用して、VPNv2 プロファイルです。 VPNv2 プロファイルを作成する SCCM または PowerShell スクリプトを必要する場合は、詳細については[VPNv2 CSP の設定](https://docs.microsoft.com/windows/client-management/mdm/vpnv2-csp)を参照してください。

---
