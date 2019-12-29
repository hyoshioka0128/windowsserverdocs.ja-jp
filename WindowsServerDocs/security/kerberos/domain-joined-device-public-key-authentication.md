---
title: ドメインに参加しているデバイスの公開キー認証
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: 7bd17803-6e42-4a3b-803f-e47c74725813
manager: alanth
author: michikos
ms.technology: security-authentication
ms.date: 08/18/2017
ms.openlocfilehash: 616ebf1a8e01f84618d22d535609a0dc8414d718
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403496"
---
# <a name="domain-joined-device-public-key-authentication"></a>ドメインに参加しているデバイスの公開キー認証

>適用対象:Windows Server 2016 の場合は Windows 10

Kerberos では、Windows Server 2012 および Windows 8 以降の証明書を使用してサインインするために、ドメインに参加しているデバイスのサポートが追加されました。 この変更により、サードパーティベンダーは、ドメインに参加しているデバイスでドメイン認証に使用する証明書をプロビジョニングおよび初期化するソリューションを作成できます。 

## <a name="automatic-public-key-provisioning"></a>自動公開キーのプロビジョニング

Windows 10 バージョン1507および Windows Server 2016 以降では、ドメインに参加しているデバイスによって、バインドされた公開キーが Windows Server 2016 ドメインコントローラー (DC) に自動的にプロビジョニングされます。 キーがプロビジョニングされると、Windows は公開キー認証をドメインに使用できるようになります。

### <a name="public-key-generation"></a>公開キーの生成
デバイスで Credential Guard が実行されている場合は、Credential Guard によって保護される公開キーが作成されます。 

Credential Guard が使用できず、TPM がの場合は、公開キーが TPM によって保護されます。 

どちらも使用できない場合、キーは生成されず、デバイスはパスワードを使用してのみ認証できます。

### <a name="provisioning-computer-account-public-key"></a>コンピューターアカウントの公開キーを準備しています
Windows が起動すると、そのコンピューターアカウントに公開キーがプロビジョニングされているかどうかを確認します。 そうでない場合は、バインドされた公開キーを生成し、Windows Server 2016 以降の DC を使用して AD のアカウント用に構成します。 すべての Dc がダウンレベルの場合、キーはプロビジョニングされません。

### <a name="configuring-device-to-only-use-public-key"></a>公開キーのみを使用するようにデバイスを構成する
**[証明書を使用したデバイス認証のサポート]** をグループポリシー設定 が **[強制]** に設定されている場合、デバイスは、Windows Server 2016 以降を実行している DC を認証する必要があります。 この設定は、[管理用テンプレート > システム > Kerberos] の下にあります。

### <a name="configuring-device-to-only-use-password"></a>パスワードのみを使用するようにデバイスを構成する
[**証明書を使用したデバイス認証のサポート**をグループポリシー設定] が無効になっている場合は、常にパスワードが使用されます。 この設定は、[管理用テンプレート > システム > Kerberos] の下にあります。

## <a name="domain-joined-device-authentication-using-public-key"></a>公開キーを使用した、ドメインに参加しているデバイスの認証
Windows がドメインに参加しているデバイス用の証明書を持っている場合、Kerberos はまず、証明書を使用して認証を行い、パスワードを使用して失敗したときに再試行します。 これにより、デバイスはダウンレベルの Dc に対して認証を行うことができます。

自動的にプロビジョニングされた公開キーには自己署名証明書があるため、キー信頼アカウントマッピングをサポートしていないドメインコントローラーでは証明書の検証に失敗します。 既定では、Windows はデバイスのドメインパスワードを使用して認証を再試行します。


