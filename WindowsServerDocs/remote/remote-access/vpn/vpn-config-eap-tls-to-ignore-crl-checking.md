---
title: 証明書失効リスト (CRL) が無視されるように EAP-TLS を構成する
description: EAP-TLS クライアントは、NPS サーバーがクライアントの証明書チェーン (ルート証明書を含む) の失効確認を完了し、証明書が失効していることを確認しない限り、接続できません。
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.date: 07/13/2018
ms.author: v-tea
author: Teresa-MOTIV
ms.localizationpriority: medium
ms.reviewer: deverette
ms.openlocfilehash: e97556ab35471c1745c01b6ebd047cd1451ffb27
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86966754"
---
# <a name="step-71-configure-eap-tls-to-ignore-certificate-revocation-list-crl-checking"></a>手順 7.1.  証明書失効リスト (CRL) が無視されるように EAP-TLS を構成する

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows 10

- [**前へ:** 手順 7.OptionalAzure AD を使用した VPN 接続の条件付きアクセス](ad-ca-vpn-connectivity-windows10.md)
- [**次のようになります。** 手順 7.2.Azure AD を使用した VPN 認証用のルート証明書の作成](vpn-create-root-cert-for-vpn-auth-azure-ad.md)

>[!IMPORTANT]
>このレジストリ変更を実装しないと、PEAP を使用したクラウド証明書を使用した IKEv2 接続は失敗しますが、オンプレミスの CA から発行されたクライアント認証証明書を使用した IKEv2 接続は引き続き機能します。

この手順では、 **Ignorenorevocationcheck**を追加し、証明書に CRL 配布ポイントが含まれていない場合にクライアントの認証を許可するように設定できます。 既定では、IgnoreNoRevocationCheck は 0 (無効) に設定されています。

>[!NOTE]
>Windows ルーティングとリモートアクセスサーバー (RRAS) が NPS を使用して2番目の NPS への RADIUS 呼び出しをプロキシする場合、両方のサーバーで**Ignorenorevocationcheck = 1**を設定する必要があります。

EAP-TLS クライアントは、NPS サーバーが証明書チェーン (ルート証明書を含む) の失効確認を完了しない限り、接続できません。 Azure AD によってユーザーに発行されたクラウド証明書には CRL がありません。有効期間が1時間の有効期間が短い証明書であるためです。 CRL の存在を無視するように NPS の EAP を構成する必要があります。 既定では、IgnoreNoRevocationCheck は 0 (無効) に設定されています。 IgnoreNoRevocationCheck を追加し、それを1に設定して、証明書に CRL 配布ポイントが含まれていない場合のクライアントの認証を許可します。 

認証方法は EAP-TLS であるため、このレジストリ値は EAP/13の下でのみ必要です。 他の EAP 認証方法が使用されている場合は、その下にレジストリ値も追加する必要があります。 

**作業**

1. NPS サーバーで**regedit.exe**を開きます。

2. **HKEY_LOCAL_MACHINE \system\currentcontrolset\services\rasman\ppp\eap\13**に移動します。

3. [**編集 > 新規作成**] を選択し、[ **DWORD (32 ビット)] 値**を選択して、「 **Ignorenorevocationcheck**」と入力します。

4. [ **Ignorenorevocationcheck** ] をダブルクリックし、[値のデータ] を**1**に設定します。

5. [ **OK]** を選択し、サーバーを再起動します。 RRAS と NPS サービスを再起動しても十分ではありません。

詳細については、「[クライアントで証明書失効確認 (CRL) を有効または無効にする方法](/previous-versions/system-center/configuration-manager-2007/bb680540(v=technet.10))」を参照してください。


|レジストリ パス  |EAP 拡張機能  |
|---------|---------|
|HKLM\SYSTEM\CurrentControlSet\Services\RasMan\PPP\EAP\13     |EAP-TLS         |
|HKLM\SYSTEM\CurrentControlSet\Services\RasMan\PPP\EAP\25     |PEAP         |
|HKLM\SYSTEM\CurrentControlSet\Services\RasMan\PPP\EAP\26     |EAP-MSCHAP v2         |

## <a name="next-steps"></a>次のステップ

[手順 7.2.Azure AD を使用した VPN 認証用のルート証明書を作成](vpn-create-root-cert-for-vpn-auth-azure-ad.md)する: この手順では、Azure AD で vpn 認証用の条件付きアクセスルート証明書を構成します。これにより、テナントに Vpn サーバークラウドアプリが自動的に作成されます。
