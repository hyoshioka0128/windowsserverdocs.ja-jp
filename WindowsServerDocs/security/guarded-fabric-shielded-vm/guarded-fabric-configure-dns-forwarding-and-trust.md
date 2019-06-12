---
title: DNS の転送とドメインの信頼を構成します。
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 3f9083d749ba9251ba47ecb64b7cb3d7c6290f1d
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66443770"
---
# <a name="configure-dns-forwarding-in-the-hgs-domain-and-a-one-way-trust-with-the-fabric-domain"></a>ファブリックのドメインとの一方向の信頼と HGS のドメインの DNS の転送を構成します。

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

>[!IMPORTANT]
>AD モードでは、Windows Server 2019 以降推奨されていません。 TPM 構成証明が可能な環境では、次のように構成します。[ホスト キーの構成証明](guarded-fabric-initialize-hgs-key-mode.md)します。 ホスト キーの構成証明は、AD モードのような保証しを設定する方が簡単です。 

次の手順を使用して、DNS の転送を設定し、ファブリックのドメインとの一方向の信頼を確立します。 これらの手順では、ドメイン コント ローラー ファブリックを検索するように HGS を許可して、HYPER-V ホストのグループ メンバーシップを検証します。

1.  DNS の転送を構成する管理者特権の PowerShell セッションで次のコマンドを実行します。 Fabrikam.com を fabric ドメインの名前に置き換えるし、fabric ドメインに DNS サーバーの IP アドレスを入力します。 高い可用性を実現するには、1 つ以上の DNS サーバーをポイントします。

    ```powershell
    Add-DnsServerConditionalForwarderZone -Name "fabrikam.com" -ReplicationScope "Forest" -MasterServers <DNSserverAddress1>, <DNSserverAddress2>
    ```

2.  一方向のフォレストの信頼を作成するには、管理者特権でコマンド プロンプトで、次のコマンドを実行します。

    置換`bastion.local`HGS ドメインの名前と`fabrikam.com`fabric ドメインの名前に置き換えます。 ファブリックのドメインの管理者のパスワードを提供します。

        netdom trust bastion.local /domain:fabrikam.com /userD:fabrikam.com\Administrator /passwordD:<password> /add

## <a name="next-step"></a>次の手順 

> [!div class="nextstepaction"]
> [HTTPS の構成](guarded-fabric-configure-hgs-https.md)
