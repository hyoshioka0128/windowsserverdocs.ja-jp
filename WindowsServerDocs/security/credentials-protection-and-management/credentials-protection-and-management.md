---
title: 資格情報の保護と管理
description: Windows Server のセキュリティ
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-credential-protection
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e457229c-0126-40fe-948c-101c943e1b57
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 16cc1f2260bf0552da6902dc3e97de65d29c7931
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812203"
---
# <a name="credentials-protection-and-management"></a>資格情報の保護と管理

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

IT プロフェッショナルは、このトピックでは、機能と資格情報の盗難を軽減するには、Windows Server 2012 R2 と資格情報の保護とドメイン認証コントロール用の Windows 8.1 で導入された方法について説明します。

## <a name="BKMK_CredentialsProtectionManagement"></a>
### <a name="restricted-admin-mode-for-remote-desktop-connection"></a>リモート デスクトップ接続のための制限付き管理モード
制限付き管理モードでは、サーバーに資格情報を送信せずにリモート ホスト サーバーに対話的にログオンできます。 これにより、サーバーが侵害されていても、最初の接続処理の際に資格情報が回収されるのを防ぎます。

管理者資格情報と共にこのモードを使用することで、リモート デスクトップ クライアントは、このモードをサポートするホストに資格情報を送信せずに対話的にログオンを試みます。 ホストに接続するユーザー アカウントに管理者権限が割り当てられていることをホストが確認し、ホストが制限付きの管理モードをサポートしていると、接続が確立されます。 これ以外の場合は、接続の試行は失敗します。 制限付き管理モードでは、どの時点であっても資格情報がプレーンテキストまたは他の再利用可能な形式でリモート コンピューターに送信されることはありません。

### <a name="lsa-protection"></a>LSA の保護
ローカル セキュリティ機関セキュリティ サービス (LSASS) プロセス内に存在するローカル セキュリティ機関 (LSA) は、ローカルおよびリモート サインインでユーザーを検証し、ローカル セキュリティ ポリシーを適用します。 Windows 8.1 オペレーティング システムでは、保護されていないプロセスによるコード インジェクションを防止するために LSA の保護を提供します。 これにより、LSA が格納して管理する資格情報のセキュリティが強化されます。 LSA の場合は、この保護されたプロセス設定は、Windows 8.1 で構成できますが、Windows RT 8.1 では既定でオンになってし、変更ことはできません。

LSA 保護の構成の詳細については、「 [Configuring Additional LSA Protection](configuring-additional-lsa-protection.md)」を参照してください。

### <a name="protected-users-security-group"></a>Protected Users セキュリティ グループ
この新しいドメイン グローバル グループは、新しい保護グループが構成可能なデバイスと Windows Server 2012 R2 および Windows 8.1 を実行しているホスト コンピューターをトリガーします。 Protected Users グループは、ドメイン コント ローラーと Windows Server 2012 R2 のドメイン内のドメインの追加の保護を使用できます。 これによって、ユーザーが侵害されていないコンピューターからネットワーク上のコンピューターにサインインするときに使用できる資格情報の種類が制限されます。

Protected Users グループのメンバーは、以下の認証方法によって更に制限を受けます。

-   Protected Users グループのメンバーは Kerberos プロトコルのみを使用してサインオンできます。 NTLM、ダイジェスト認証、または CredSSP を使用してアカウントを認証できません。 Windows 8.1 を実行しているデバイス、パスワードはキャッシュされません、のでこれらのセキュリティ サポート プロバイダー (Ssp) のいずれかを使用するデバイスは、アカウントが保護されたユーザー グループのメンバーである、ドメインに対する認証に失敗します。

-   Kerberos プロトコルは、事前認証プロセスで強度の低い DES または RC4 暗号化タイプを使用しません。 つまり、少なくとも AES 暗号スイートをサポートするようにドメインを構成する必要があります。

-   ユーザーのアカウントの Kerberos 制約付きまたは制約なし委任できない委任します。 つまり、ユーザーが Protected Users グループのメンバーである場合、他のシステムへの以前の接続が失敗する可能性があります。

-   既定の Kerberos Ticket Granting Ticket (TGT) の 4 時間という有効期間設定は、Active Directory 管理センター (ADAC) からアクセスする認証ポリシーとサイロを使用して構成できます。 つまり、4 時間が経過すると、ユーザーは再認証する必要があります。

> [!WARNING]
> サービスとコンピューターのアカウントは、Protected Users グループのメンバーにしないでください。 パスワードまたは証明書は常にホストで使用できるので、このグループにローカルの保護機能はありません。 認証は失敗のエラーで「ユーザー名またはパスワードが正しくありません」のすべてのサービスまたは Protected Users グループに追加されているコンピューター。

このグループの詳細については、「[Protected Users セキュリティ グループ](protected-users-security-group.md)」を参照してください。

### <a name="authentication-policy-and-authentication-policy-silos"></a>認証ポリシーと認証ポリシー サイロ
Active Directory のフォレストに基づいたポリシーが導入されていると、Windows Server 2012 R2 のドメイン機能レベルを持つドメイン内のアカウントに適用できます。 これらの認証ポリシーによって、ユーザーがサインインに使用できるホストを管理できます。 ポリシーは Protect Users セキュリティ グループと連携して機能し、管理者は認証のアクセス制御条件をアカウントに適用できます。 これらの認証ポリシーは、関連アカウントを分離させてネットワークの範囲を制限します。

新しい Active Directory オブジェクト クラスで、認証ポリシーを使用すると、Windows Server 2012 R2 のドメイン機能レベルを持つドメイン内のアカウント クラスに認証構成を適用できます。 認証ポリシーは、Kerberos AS または TGS の交換時に適用されます。 次の Active Directory アカウント クラスがあります。

-   ユーザー

-   コンピューター

-   管理されたサービス アカウント

-   グループ管理サービス アカウント

詳細については、「[認証ポリシーと認証ポリシー サイロ](authentication-policies-and-authentication-policy-silos.md)」を参照してください。

保護されたアカウントの構成方法の詳細については、「[保護されるアカウントの構成方法](how-to-configure-protected-accounts.md)」を参照してください。

## <a name="see-also"></a>関連項目
LSA と LSASS の詳細については、「 [Windows のログオンと認証の技術概要](https://technet.microsoft.com/library/dn169029(v=ws.10).aspx)」を参照してください。



