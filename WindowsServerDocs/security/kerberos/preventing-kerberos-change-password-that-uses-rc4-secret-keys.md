---
title: "防止 Kerberos RC4 秘密キーを使用するパスワードを変更します。"
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: de207d55-aa3d-4c16-bd3b-496db43663a4
manager: alanth
author: justinha
ms.technology: security-crdential-protection-and-management
ms.date: 11/09/2016
ms.openlocfilehash: 3cfa4ae2442f0cd1e3e4110a355da675fa2d61db
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2017
---
# <a name="preventing-kerberos-change-password-that-uses-rc4-secret-keys"></a>防止 Kerberos RC4 秘密キーを使用するパスワードを変更します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2008 R2、および Windows Server 2008

IT プロフェッショナル向けのこのトピックでは、Kerberos プロトコルのユーザーのアカウントの制御、悪意のあるユーザーにつながる可能性のあるいくつかの制限について説明します。 これは、業界では、これにより、攻撃者がユーザーとして認証したり、攻撃者がユーザーの秘密キーを知っている場合、そのユーザーのパスワードを変更内でよく知られている Kerberos ネットワーク認証サービス (V5) standard (RFC 4120) の制限があります。

所有しているユーザーのパスワードから派生した Kerberos シークレット キー (RC4 と高度暗号化標準 [AES] 既定) の RFC 4757 ごとには、Kerberos パスワード変更交換中に検証されます。 ユーザーのプレーン テキスト パスワードではキー配布センター (KDC) には提供されませんし、既定では、Active Directory ドメイン コントローラがないアカウントのパスワードをプレーン テキストのコピーします。 ドメイン コントローラーが Kerberos 暗号化の種類をサポートしていない場合は、パスワードの変更をその秘密キーを使用できません。 

このトピックの冒頭に対象の一覧で指定されている Windows オペレーティング システムでは、RC4 秘密キーに Kerberos を使用してパスワードを変更する機能をブロックする 3 つの方法があります。

- 構成、ユーザー アカウント オプション スマート カードを含めるにアカウントが対話型ログオンに必要です。 これにより、のみでログインして有効なスマート カードは、RC4 認証サービス要求 (As-req) の拒否されるように、ユーザーが制限されます。 アカウントのアカウントのオプションを設定するには、プロパティ] をクリックして、アカウントを右クリックし、アカウント] タブをクリックします。 

- すべてのドメイン コントローラーで Kerberos の RC4 サポートを無効にします。 これには、Windows Server 2008 ドメインの機能レベルと、Kerberos のすべてのクライアント、アプリケーション サーバー、およびドメインとの間の信頼関係が AES をサポートする必要があります、環境の最小値が必要です。 AES のサポートは、Windows Server 2008 および Windows Vista で導入されました。

    [!NOTE]
    RC4 に再起動が発生することができますを無効にする場合の既知の問題があります。 次の修正プログラムを参照してください。
    - [Windows Server 2012 R2](https://support.microsoft.com/en-us/kb/3038261)
    - [Windows Server 2012](https://support.microsoft.com/en-us/kb/3086213)
    - Windows Server の以前のバージョンの利用可能な修正プログラムはありません。

- Windows Server 2012 R2 ドメインの機能レベルを以上に上げます、ドメインのセットを展開し、Protected Users セキュリティ グループのメンバーとして、ユーザーを構成します。 この機能では、Kerberos プロトコルでの RC4 使用率だけでなくが中断であるため、次のリソースを参照してください。[も参照してください](#see-also)セクションです。

## <a name="see-also"></a>参照してください。

- Windows Server 2012 R2 のドメインでの RC4 暗号化の種類の使用状況を回避する方法については、次を参照してください。[Protected Users セキュリティ グループ](/../credentials-protection-and-management/protected-users-security-group.md)、および[保護されるアカウントの構成方法](/../credentials-protection-and-management/how-to-configure-protected-accounts.md)します。

- RFC 4120 および RFC 4757 に関する説明は、次を参照してください。[IETF のドキュメント](http://tools.ietf.org/html/)します。
