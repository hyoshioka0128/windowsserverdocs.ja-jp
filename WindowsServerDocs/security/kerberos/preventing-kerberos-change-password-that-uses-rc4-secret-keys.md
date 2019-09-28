---
title: RC4 秘密キーを使用する Kerberos 変更パスワードの防止
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: de207d55-aa3d-4c16-bd3b-496db43663a4
manager: alanth
author: justinha
ms.technology: security-crdential-protection-and-management
ms.date: 11/09/2016
ms.openlocfilehash: 64018f7f118086f3d290cb1ffa9b8d2b3e81c27c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386270"
---
# <a name="preventing-kerberos-change-password-that-uses-rc4-secret-keys"></a>Kerberos での RC4 秘密キーを使用するパスワードの変更を防ぐ

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2008 R2、および Windows Server 2008

IT 担当者向けのこのトピックでは、悪意のあるユーザーがユーザーのアカウントを制御する可能性がある、Kerberos プロトコルのいくつかの制限事項について説明します。 Kerberos ネットワーク認証サービス (V5) 標準 (RFC 4120) には、業界内でよく知られている制限があります。攻撃者がユーザーとして認証したり、攻撃者がユーザーの秘密キーを知っていれば、そのユーザーのパスワードを変更したりできます。

ユーザーのパスワードで派生した Kerberos シークレットキー (既定では RC4 および Advanced Encryption Standard [AES]) の所有は、RFC 4757 に従って Kerberos パスワード変更交換中に検証されます。 ユーザーのプレーンテキストパスワードがキー配布センター (KDC) に提供されることはありません。既定では、Active Directory ドメインコントローラーは、アカウントのプレーンテキストパスワードのコピーを保持しません。 ドメインコントローラーが Kerberos 暗号化の種類をサポートしていない場合は、その秘密キーを使用してパスワードを変更することはできません。 

このトピックの冒頭にある「適用対象」の一覧に記載されている Windows オペレーティングシステムでは、次の3つの方法で、Kerberos を使用してパスワードを変更できないようにします。

- アカウントを含めるようにユーザーアカウントを構成する対話型ログオンにはスマートカードが必要です。 これにより、ユーザーは、有効なスマートカードを使用したサインインのみに制限されるため、RC4 認証サービスの要求が拒否されます。 アカウントのアカウントオプションを設定するには、アカウントを右クリックし、[プロパティ] をクリックして、[アカウント] タブをクリックします。 

- すべてのドメインコントローラーで、Kerberos の RC4 サポートを無効にします。 これには、Windows Server 2008 ドメインの機能レベルと、ドメインとの間のすべての Kerberos クライアント、アプリケーションサーバー、および信頼関係が AES をサポートする必要がある環境が必要です。 AES のサポートは、Windows Server 2008 および Windows Vista で導入されました。

    [!NOTE]
    RC4 を無効にすると、システムの再起動が発生することがあるという既知の問題があります。 次の修正プログラムを参照してください。
    - [Windows Server 2012 R2](https://support.microsoft.com/en-us/kb/3038261)
    - [Windows Server 2012](https://support.microsoft.com/en-us/kb/3086213)
    - 以前のバージョンの Windows Server では修正プログラムを利用できません

- Windows Server 2012 R2 ドメインの機能レベル以上に設定されたドメインを展開し、Protected Users セキュリティグループのメンバーとしてユーザーを構成します。 この機能は、Kerberos プロトコルでの RC4 の使用よりも中断するため[、次の「関連](#see-also)項目」セクションのリソースを参照してください。

## <a name="see-also"></a>関連項目

- Windows Server 2012 R2 ドメインで RC4 暗号化の種類が使用されないようにする方法については、「 [Protected Users セキュリティグループ](/../credentials-protection-and-management/protected-users-security-group.md)」と「[保護されたアカウントの構成方法](/../credentials-protection-and-management/how-to-configure-protected-accounts.md)」を参照してください。

- RFC 4120 および RFC 4757 の説明については、「 [IETF Documents](http://tools.ietf.org/html/)」を参照してください。
