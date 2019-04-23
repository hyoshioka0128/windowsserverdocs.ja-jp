---
title: BranchCache 機能をインストールし、サービス接続ポイントによってホスト型キャッシュ サーバーを構成する
description: このガイドでは、Windows Server 2016 および Windows 10 を実行するコンピューターでホスト型キャッシュ モードで BranchCache の展開の説明
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: 9adf420b-5a58-4e59-9906-71bd58f757fd
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 6619b09df0d4c161148d22091337a5039c7ea3af
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849653"
---
# <a name="install-the-branchcache-feature-and-configure-the-hosted-cache-server-by-service-connection-point"></a>BranchCache 機能をインストールし、サービス接続ポイントによってホスト型キャッシュ サーバーを構成する

>適用対象:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

この手順を使用するには、ホスト型キャッシュ サーバーで、HCS1、BranchCache 機能をインストールして、サービス接続ポイントを登録するサーバーを構成する\(SCP\) Active Directory Domain Services で\(AD DS\).

AD DS で SCP をホスト型キャッシュ サーバーを登録するときに、SCP は、SCP を AD DS を照会して、ホスト型キャッシュ サーバーを自動的に検出を正しく構成されているコンピューター クライアントをできます。 この操作を実行するクライアント コンピューターを構成する方法については、このガイドの後半で提供されます。

>[!IMPORTANT]
>この手順を実行する前に、コンピューターをドメインに参加させるし、静的 IP アドレスを持つコンピューターを構成する必要があります。

この手順を実行するには、Administrators グループのメンバである必要があります。

## <a name="to-install-the-branchcache-feature-and-configure-the-hosted-cache-server"></a>BranchCache 機能をインストールして、ホスト型キャッシュ サーバーを構成するには  

1. サーバー コンピューターには、管理者として Windows PowerShell を実行します。 次のコマンドを入力し、Enter キーを押します。

    ``` 
    Install-WindowsFeature BranchCache
    ```

2.  BranchCache 機能をインストールした後、ホスト型キャッシュ サーバーとしてコンピューターを構成して、AD DS でサービス接続ポイントを登録するには、Windows PowerShell で次のコマンドを入力し、ENTER キーを押します。

    ```  
    Enable-BCHostedServer -RegisterSCP
    ```  

3. ホスト型キャッシュ サーバーの構成を確認するには、次のコマンドを入力し、ENTER キーを押します。

    ```  
    Get-BCStatus  
    ```  
  
    コマンドの結果は、BranchCache インストールのすべての側面の状態を表示します。 次に、BranchCache の設定および項目ごとに適切な値のいくつか示します。  
  
    -   BranchCacheIsEnabled:True

    -   HostedCacheServerIsEnabled:True

    -   HostedCacheScpRegistrationEnabled:True

4. コンテンツ サーバーから、ホスト型キャッシュ サーバーに、データ パッケージをコピーのステップの準備、いずれか特定ホスト型キャッシュ サーバー上の既存の共有または新しいフォルダーを作成し、コンテンツ サーバーからアクセスできるように、フォルダーを共有します。 コンテンツ サーバーで、データ パッケージを作成した後は、ホスト型キャッシュ サーバー上でこの共有フォルダーにデータ パッケージがコピーされます。
  
5. 1 つ以上のホスト型キャッシュ サーバーを展開する場合は、各サーバーで、この手順を繰り返します。

このガイドを続行する、次を参照してください。[移動し、ホスト型キャッシュのサイズを変更&#40;(省略可能)&#41;](6-Bc-Move-Resize-Cache.md)します。
