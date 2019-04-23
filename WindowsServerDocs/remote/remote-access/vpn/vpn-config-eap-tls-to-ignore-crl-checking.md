---
title: 証明書失効リスト (CRL) が無視されるように EAP-TLS を構成する
description: NPS サーバーがクライアントの証明書チェーン (ルート証明書を含む) の失効確認が完了して、証明書が失効を検証しますしない限り、EAP-TLS クライアントは接続できません。
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
ms.openlocfilehash: ac59c554c69a6138a106a648c3fab3ed4fe05b7b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59836423"
---
# <a name="step-71-configure-eap-tls-to-ignore-certificate-revocation-list-crl-checking"></a>手順 7.1.  証明書失効リスト (CRL) が無視されるように EAP-TLS を構成する

>適用先:Windows Server 2016、Windows Server 2012 R2、Windows 10 の Windows Server (半期チャネル)

&#171;  [**先の：** 手順 7.(省略可能)Azure AD を使用して VPN 接続用の条件付きアクセス](ad-ca-vpn-connectivity-windows10.md)<br>
&#187;[ **[次へ]。** 手順 7.2. Azure AD での VPN 認証用のルート証明書を作成します。](vpn-create-root-cert-for-vpn-auth-azure-ad.md)

>[!IMPORTANT]
>このレジストリの変更を実装するためにエラーによって PEAP が失敗し、クラウドの証明書の使用の IKEv2 接続が、オンプレミスで CA から発行されたクライアント認証証明書を使用する IKEv2 接続は継続して動作します。

この手順で追加することができます**IgnoreNoRevocationCheck**し、証明書に CRL 配布ポイントが含まれていない場合は、クライアントの認証を許可するように設定します。 既定では、IgnoreNoRevocationCheck は、0 (無効) に設定されます。

>[!NOTE]
>Windows ルーティングとリモート アクセス サーバー (RRAS) は、NPS を使用している場合、2 つ目の NPS を RADIUS を呼び出すプロキシにし、設定する必要があります**IgnoreNoRevocationCheck = 1**両方のサーバーにします。

NPS サーバーの証明書チェーン (ルート証明書を含む) の失効確認が完了しない限り、EAP-TLS クライアントは接続できません。 ユーザーに Azure AD によって発行された証明書をクラウドでは、1 時間の有効期間を持つ証明書を短時間であるため、CRL を必要はありません。 NPS で EAP は、CRL の休暇を無視するように構成する必要があります。 既定では、IgnoreNoRevocationCheck は、0 (無効) に設定されます。 IgnoreNoRevocationCheck を追加し、証明書に CRL 配布ポイントが含まれていない場合は、クライアントの認証を許可する 1 に設定します。 

認証方法が EAP-TLS であるために、このレジストリ値は EAP\13 下でのみ必要です。 その他の EAP 認証メソッドを使用している場合、レジストリ値必要があります追加ものでも。 

**プロシージャ**

1. 開いている**regedit.exe** NPS サーバーでします。

2. 移動します**HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\RasMan\PPP\EAP\13**します。

3. をクリックして**編集 > 新規**選択と**DWORD (32 ビット) 値**と種類**IgnoreNoRevocationCheck**。

4. ダブルクリック**IgnoreNoRevocationCheck**に値のデータを設定および**1**します。

5. をクリックして**OK**サーバーを再起動します。 RRAS および NPS サービスを再起動するだけでは不十分です。

詳細については、次を参照してください。[を有効にするか、クライアントで証明書失効確認 (CRL) を無効にする方法](https://technet.microsoft.com/library/bb680540.aspx)します。


|レジストリ パス  |EAP の拡張機能  |
|---------|---------|
|HKLM\SYSTEM\CurrentControlSet\Services\RasMan\PPP\EAP\13     |EAP-TLS         |
|HKLM\SYSTEM\CurrentControlSet\Services\RasMan\PPP\EAP\25     |PEAP         |
|HKLM\SYSTEM\CurrentControlSet\Services\RasMan\PPP\EAP\26     |EAP-MSCHAP v2         |

## <a name="next-step"></a>次の手順

[手順 7.2 です。Azure AD での VPN 認証用のルート証明書の作成](vpn-create-root-cert-for-vpn-auth-azure-ad.md):この手順では、テナントに自動的に VPN サーバーのクラウド アプリを作成する Azure AD に VPN 認証用のルート証明書の条件付きアクセスを構成します。 

---