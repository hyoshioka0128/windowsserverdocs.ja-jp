---
title: 証明書失効リスト (CRL) が無視されるように EAP-TLS を構成する
description: NPS サーバーがクライアントの証明書チェーン (ルート証明書を含む) の失効チェックを完了し、証明書が失効していないことを確認する場合を除き、EAP-TLS クライアントが接続できません。
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
ms.sourcegitcommit: 4893d79345cea85db427224bb106fc1bf88ffdbc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2018
ms.locfileid: "6067371"
---
# 手順 7.1.  証明書失効リスト (CRL) が無視されるように EAP-TLS を構成する

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows 10

& #171 です。 [**前:** 手順 7 です。(省略可能)Azure AD を使用して VPN 接続の条件付きアクセス](ad-ca-vpn-connectivity-windows10.md)<br>
& #187 です。[ **[次へ]:** 手順 7.2 します。Azure AD と VPN 認証のルート証明書を作成](vpn-create-root-cert-for-vpn-auth-azure-ad.md)

>[!IMPORTANT]
>IKEv2 の接続に失敗した場合、PEAP とクラウドの証明書の使用により、このレジストリの変更を実装するエラーが、社内の CA から発行されたクライアント認証証明書を使用して、IKEv2 接続は引き続き機能します。

この手順では、 **IgnoreNoRevocationCheck**を追加し、証明書に CRL 配布ポイントが含まれていない場合は、クライアントの認証を許可するように設定します。 既定では、IgnoreNoRevocationCheck が 0 (無効) に設定されます。

>[!NOTE]
>Windows のルーティングとリモート アクセス サーバー (RRAS) は、NPS を使用している場合、2 つ目の NPS を RADIUS を呼び出すプロキシにし、設定する必要があります**IgnoreNoRevocationCheck = 1**両方のサーバー。

NPS サーバー (ルート証明書を含む) の証明書チェーンの失効チェックが完了するとしない限り、EAP-TLS クライアントが接続できません。 Azure AD によって、ユーザーに発行された証明書をクラウドでは、1 時間の有効期間での有効期間が短い証明書であるため、CRL を必要はありません。 NPS で EAP crl 休暇を無視するように構成する必要があります。 既定では、IgnoreNoRevocationCheck が 0 (無効) に設定されます。 IgnoreNoRevocationCheck を追加し、証明書に CRL 配布ポイントが含まれていない場合は、クライアントの認証を許可する 1 に設定します。 

認証方法は、EAP-TLS であるために、このレジストリ値は EAP\13 でのみ必要です。 他の EAP 認証方法を使用している場合、レジストリ値する必要があります下に追加されるものもします。 

**手順**

1. NPS サーバーで、 **regedit.exe**を開きます。

2. **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\RasMan\PPP\EAP\13**に移動します。

3. クリックして**編集 > 新規** **DWORD (32 ビット) 値**を選択し、 **IgnoreNoRevocationCheck**を入力します。

4. **IgnoreNoRevocationCheck**をダブルクリックし、値のデータを**1**に設定します。

5. **[Ok]** をクリックし、サーバーを再起動します。 RRAS および NPS サービスを再起動するだけでは不十分です。

詳細については、[有効またはクライアントに証明書失効チェック (CRL) を無効にする方法](https://technet.microsoft.com/library/bb680540.aspx)を参照してください。


|レジストリ パス  |EAP の拡張機能  |
|---------|---------|
|HKLM\SYSTEM\CurrentControlSet\Services\RasMan\PPP\EAP\13     |EAP-TLS         |
|HKLM\SYSTEM\CurrentControlSet\Services\RasMan\PPP\EAP\25     |PEAP         |
|HKLM\SYSTEM\CurrentControlSet\Services\RasMan\PPP\EAP\26     |EAP-MSCHAP v2         |

## 次の手順

[手順 7.2 です。Azure AD と VPN 認証のルート証明書を作成](vpn-create-root-cert-for-vpn-auth-azure-ad.md): この手順で、テナントに自動的に VPN サーバーのクラウド アプリを作成する、Azure AD を使ってルート証明書 VPN 認証のための条件付きアクセスを構成します。 

---