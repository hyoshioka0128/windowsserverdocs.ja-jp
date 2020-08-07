---
title: BranchCache 機能をインストールし、サービス接続ポイントによってホスト型キャッシュ サーバーを構成する
description: このガイドでは、Windows Server 2016 と Windows 10 を実行するコンピューターに、ホスト型キャッシュモードで BranchCache を展開する手順について説明します。
manager: brianlic
ms.topic: article
ms.assetid: 9adf420b-5a58-4e59-9906-71bd58f757fd
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 7aca1cc28086761b18e559210aeaf21e87612ed3
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87937467"
---
# <a name="install-the-branchcache-feature-and-configure-the-hosted-cache-server-by-service-connection-point"></a>BranchCache 機能をインストールし、サービス接続ポイントによってホスト型キャッシュ サーバーを構成する

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

次の手順を使用して、ホスト型キャッシュサーバー HCS1 に BranchCache 機能をインストールし、サービス接続ポイント SCP を Active Directory Domain Services AD DS に登録するようにサーバーを構成でき \( \) \( \) ます。

AD DS で SCP を使用してホスト型キャッシュサーバーを登録すると、scp の AD DS に対してクエリを実行することで、ホスト型キャッシュサーバーを自動的に検出するように構成されているクライアントコンピューターでは、この scp が許可されます。 この操作を実行するようにクライアントコンピューターを構成する方法については、このガイドの後半で説明します。

>[!IMPORTANT]
>この手順を実行する前に、コンピューターをドメインに参加させ、静的 IP アドレスを使用してコンピューターを構成する必要があります。

この手順を実行するには、Administrators グループのメンバである必要があります。

## <a name="to-install-the-branchcache-feature-and-configure-the-hosted-cache-server"></a>BranchCache 機能をインストールし、ホスト型キャッシュサーバーを構成するには

1. サーバーコンピューターで、管理者として Windows PowerShell を実行します。 次のコマンドを入力して、Enter キーを押します。

    ```
    Install-WindowsFeature BranchCache
    ```

2.  BranchCache 機能をインストールした後にコンピューターをホスト型キャッシュサーバーとして構成し、AD DS にサービス接続ポイントを登録するには、Windows PowerShell で次のコマンドを入力し、enter キーを押します。

    ```
    Enable-BCHostedServer -RegisterSCP
    ```

3. ホスト型キャッシュサーバーの構成を確認するには、次のコマンドを入力し、enter キーを押します。

    ```
    Get-BCStatus
    ```

    コマンドの結果は、BranchCache インストールのすべての側面の状態を表示します。 次に、BranchCache の設定のいくつかと、各項目の正しい値を示します。

    -   BranchCacheIsEnabled: True

    -   HostedCacheServerIsEnabled: True

    -   HostedCacheScpRegistrationEnabled: True

4. コンテンツサーバーからホスト型キャッシュサーバーにデータパッケージをコピーする手順を準備するには、ホスト型キャッシュサーバー上の既存の共有を識別するか、新しいフォルダーを作成して、コンテンツサーバーからアクセスできるようにフォルダーを共有します。 コンテンツサーバーにデータパッケージを作成した後は、データパッケージをホスト型キャッシュサーバー上のこの共有フォルダーにコピーします。

5. 複数のホスト型キャッシュサーバーを展開する場合は、各サーバーでこの手順を繰り返します。

このガイドを続行するには、「[ホスト型キャッシュの移動とサイズ変更 &#40;オプション&#41;](6-Bc-Move-Resize-Cache.md)」を参照してください。
