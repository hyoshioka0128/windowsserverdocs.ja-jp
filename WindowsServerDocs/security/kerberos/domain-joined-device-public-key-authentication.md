---
title: "デバイスのドメインに参加している公開キーの認証"
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 7bd17803-6e42-4a3b-803f-e47c74725813
manager: alanth
author: michikos
ms.technology: security-authentication
ms.date: 8/18/2017
ms.openlocfilehash: 65f39f4900fcd99ef90b160d3db7099edb73bc1c
ms.sourcegitcommit: e94838df702ff0135ebe7c179b228aa67b772d35
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/28/2017
---
# <a name="domain-joined-device-public-key-authentication"></a>デバイスのドメインに参加している公開キーの認証

>適用対象: Windows Server 2016、Windows 10

Kerberos は、証明書の先頭を Windows Server 2012 と Windows 8 を使用したサインインをドメインに参加しているデバイスのサポートを追加します。 この変更により、サード パーティのベンダーのプロビジョニングし、ドメイン認証に使用するドメインに参加しているデバイスの証明書を初期化するソリューションを作成します。 

## <a name="automatic-public-key-provisioning"></a>自動公開キーのプロビジョニング

Windows 10 バージョン 1507 および Windows Server 2016 以降では、ドメインに参加しているデバイスは自動的に、Windows Server 2016 ドメイン コントローラー (DC) にバインドされている公開キーをプロビジョニングします。 キーがプロビジョニングされた後、Windows は、ドメインを公開キーの認証を使用できます。

### <a name="public-key-generation"></a>公開キーの生成
デバイスは、Credential Guard を実行している、し、公開キーが作成 Credential Guard によって保護されます。 

Credential Guard が使用できず、TPM が搭載されている場合、公開キーが TPM によって保護された作成されます。 

どちらが使用可能な場合は、キーが生成されませんし、デバイスは、パスワードを使用してだけ認証できます。

### <a name="provisioning-computer-account-public-key"></a>コンピューター アカウントの公開キーのプロビジョニング
Windows 起動すると、そのコンピューター アカウントに対して公開キーがプロビジョニングされたかどうかを確認します。 ない場合、バインドされている公開キーを生成し、Windows Server 2016 または高い DC を使用して AD でそのアカウントのように構成します。 すべての Dc が下位レベルの場合は、キーはプロビジョニングされません。

### <a name="configuring-device-to-only-use-public-key"></a>公開キーのみを使用するデバイスを構成します。
場合、グループ ポリシー設定**証明書を使用してデバイス認証のサポート**に設定されている**Force**、デバイスは、Windows Server 2016 を実行している DC を検索またはそれ以降を認証する必要があります。 設定は、[管理用テンプレート > システム > Kerberos します。

### <a name="configuring-device-to-only-use-password"></a>のみのパスワードを使用するデバイスを構成します。
場合、グループ ポリシー設定**証明書を使用してデバイス認証のサポート**は無効にすると、パスワードが常に使用します。 設定は、[管理用テンプレート > システム > Kerberos します。

## <a name="domain-joined-device-authentication-using-public-key"></a>公開キーを使用してドメインに参加しているデバイスの認証
Windows では、ドメインに参加しているデバイスの証明書には、Kerberos 最初に認証証明書を使用してパスワードを使用してエラーの再試行します。 これにより、ダウン レベルのドメイン コントローラーへの認証にデバイスができます。

自動的にプロビジョニングされた公開キーがあるため、自己署名証明書、キーの信頼アカウントへのマッピングをサポートしていないドメイン コントローラーで証明書の検証が失敗します。 既定では、Windows は、デバイスのドメインのパスワードを使用して認証を再試行します。


