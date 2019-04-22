---
title: 防止 Kerberos RC4 秘密キーを使用するパスワードを変更します。
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: de207d55-aa3d-4c16-bd3b-496db43663a4
manager: alanth
author: justinha
ms.technology: security-crdential-protection-and-management
ms.date: 11/09/2016
ms.openlocfilehash: 3cfa4ae2442f0cd1e3e4110a355da675fa2d61db
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816273"
---
# <a name="preventing-kerberos-change-password-that-uses-rc4-secret-keys"></a>Kerberos での RC4 秘密キーを使用するパスワードの変更を防ぐ

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2008 R2、および Windows Server 2008

IT プロフェッショナルは、このトピックでは、Kerberos プロトコル、ユーザーのアカウントを乗っ取る悪意のあるユーザーを引き起こす可能性のあるいくつかの制限について説明します。 これは、攻撃者が、ユーザーとして認証または、攻撃者がユーザーの秘密キーを知っている場合、そのユーザーのパスワードを変更、業界内でよく知られている Kerberos ネットワーク認証サービス (V5) 標準 (RFC 4120) で制限があります。

所有しているユーザーのパスワードから派生した Kerberos 秘密キー (RC4 および Advanced Encryption Standard [AES] 既定で) は、RFC 4757 ごとの Kerberos パスワード変更の交換中に検証されます。 ユーザーのプレーン テキスト パスワードではキー配布センター (KDC) には提供されませんし、既定では、Active Directory ドメイン コント ローラーを所有していないアカウントのパスワードをプレーン テキストのコピー。 ドメイン コント ローラーが Kerberos 暗号化の種類をサポートしていない場合は、パスワードを変更する秘密キーを使用できません。 

このトピックの冒頭にある対象の一覧で指定されている Windows オペレーティング システムでは、RC4 秘密キーで Kerberos を使用してパスワードを変更する機能をブロックする 3 つの方法があります。

- ユーザーの構成アカウント オプションのスマート カードを含めるアカウントが対話型ログオンに必要です。 これは、のみ、有効なスマート カード サインイン RC4 (AS 条件) の認証サービス要求を拒否するためにユーザーを制限します。 アカウントのアカウントのオプションを設定するには、アカウントのプロパティ をクリックします右クリックし、アカウント タブをクリックします。 

- すべてのドメイン コント ローラーで Kerberos の RC4 サポートを無効にします。 これには、Windows Server 2008 ドメインの機能レベルと Kerberos のすべてのクライアント、アプリケーション サーバー、およびドメインとの間の信頼関係が AES をサポートする必要があります、環境の最小値が必要です。 AES のサポートは、Windows Server 2008 および Windows Vista で導入されました。

    [!NOTE]
    これには、システムを再起動する可能性がある RC4 を無効にする場合の既知の問題です。 次の修正プログラムを参照してください。
    - [Windows Server 2012 R2](https://support.microsoft.com/en-us/kb/3038261)
    - [Windows Server 2012](https://support.microsoft.com/en-us/kb/3086213)
    - Windows Server の以前のバージョンの修正プログラムはありません。

- ドメインの機能レベルを Windows Server 2012 R2 以降、ドメインのセットをデプロイし、Protected Users セキュリティ グループのメンバーとしてユーザーを構成します。 この機能は、Kerberos プロトコルの RC4 の使用量だけを中断、ため、次のリソースを参照してください。[も参照してください](#see-also)セクション。

## <a name="see-also"></a>関連項目

- Windows Server 2012 R2 のドメインで、RC4 暗号化タイプの使用状況を回避する方法については、次を参照してください。 [Protected Users セキュリティ グループ](/../credentials-protection-and-management/protected-users-security-group.md)、および[How to Configure Protected Accounts](/../credentials-protection-and-management/how-to-configure-protected-accounts.md)します。

- 4120 の RFC と RFC 4757 に関する説明については、次を参照してください。 [IETF ドキュメント](http://tools.ietf.org/html/)します。
