---
title: ドメインに参加しているデバイスの公開キー認証
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 7bd17803-6e42-4a3b-803f-e47c74725813
manager: alanth
author: michikos
ms.technology: security-authentication
ms.date: 08/18/2017
ms.openlocfilehash: 80906e7cfe3740200938704a4b4eaf0759af303a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59885033"
---
# <a name="domain-joined-device-public-key-authentication"></a>ドメインに参加しているデバイスの公開キー認証

>適用対象:Windows Server 2016 の場合は Windows 10

Kerberos には、Windows Server 2012 および Windows 8 で証明書の先頭を使用してサインインをドメインに参加しているデバイスのサポートが追加されます。 この変更により、サードパーティのベンダーをプロビジョニングして、ドメインの認証に使用するドメインに参加しているデバイスの証明書を初期化するソリューションを作成します。 

## <a name="automatic-public-key-provisioning"></a>自動公開キーのプロビジョニング

Windows 10 バージョン 1507、Windows Server 2016 以降、ドメイン参加済みデバイスは自動的に、Windows Server 2016 ドメイン コント ローラー (DC) にバインドされている公開キーをプロビジョニングします。 キーをプロビジョニングすると、Windows は、ドメインに公開キー認証を使用することができます。

### <a name="public-key-generation"></a>パブリック キーの生成
Credential Guard を実行してデバイスの場合は、公開キーが Credential Guard で保護されて作成されます。 

Credential Guard をご利用いただけません、TPM は、の場合は、公開キーが TPM によって保護されている作成されます。 

使用可能な場合、どちらもキーは生成されませんし、デバイスは、パスワードを使用してのみ認証できます。

### <a name="provisioning-computer-account-public-key"></a>コンピューター アカウントのパブリック キーのプロビジョニング
Windows の起動時に、コンピューター アカウントの公開キーがプロビジョニングされるかどうかが確認されます。 できない場合は、バインドされた公開キーを生成し、Windows Server 2016 または高い DC を使用して AD でそのアカウントを構成します。 すべての Dc が下位レベルの場合は、キーが提供されません。

### <a name="configuring-device-to-only-use-public-key"></a>公開キーのみを使用するデバイスを構成します。
場合、グループ ポリシー設定**証明書を使用してデバイス認証のサポート**に設定されている**Force**デバイスは、Windows Server 2016 を実行している DC を検索するか、後で認証を必要があります。 管理用テンプレートは、設定 > システム > Kerberos。

### <a name="configuring-device-to-only-use-password"></a>のみのパスワードを使用するデバイスを構成します。
場合、グループ ポリシー設定**証明書を使用してデバイス認証のサポート**が無効で、パスワードが常に使用します。 管理用テンプレートは、設定 > システム > Kerberos。

## <a name="domain-joined-device-authentication-using-public-key"></a>公開キーを使用してドメイン参加済みデバイスの認証
Windows ドメイン参加済みデバイスの証明書が Kerberos 最初を使用して認証証明書とパスワードを使用してエラーの再試行します。 これにより、ダウンレベルのドメイン コント ローラーへの認証にデバイスができます。

自動的にプロビジョニングされたパブリック キーがあるため、自己署名証明書、キー信頼アカウントのマッピングをサポートしていないドメイン コント ローラーで証明書の検証が失敗します。 既定では、Windows は、デバイスのドメインのパスワードを使用して認証を再試行します。


