---
title: BranchCache 機能をインストールし、サービス接続ポイントによるホスト型キャッシュ サーバーを構成します。
description: このガイドでは、Windows Server 2016 および Windows 10 を実行するコンピューターでホスト型キャッシュ モードで BranchCache を展開するの説明
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: 9adf420b-5a58-4e59-9906-71bd58f757fd
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 854ff9f80a2221a857fab4e6ea7f7c8e6d51f1ef
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="install-the-branchcache-feature-and-configure-the-hosted-cache-server-by-service-connection-point"></a>BranchCache 機能をインストールし、サービス接続ポイントによるホスト型キャッシュ サーバーを構成します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

この手順を使用するには、ホスト型キャッシュ サーバーで、HCS1、BranchCache 機能をインストールし、サービス接続ポイントを登録するサーバーを構成する Active Directory Domain Services \(AD DS\) で \(SCP\) します。

ホスト型キャッシュ サーバーを AD DS の SCP を登録するときに、SCP によりクライアント SCP を AD DS を照会して、ホスト型キャッシュ サーバーを自動的に検出を正しく構成されているコンピューター。 この操作を実行するクライアント コンピューターを構成する方法については、このガイドの後半で説明します。

>[!IMPORTANT]
>この手順を実行する前に、コンピューターをドメインに参加させるし、静的 IP アドレスを持つコンピューターを構成する必要があります。

この手順を実行するには、Administrators グループのメンバーがあります。

## <a name="to-install-the-branchcache-feature-and-configure-the-hosted-cache-server"></a>BranchCache 機能をインストールして、ホスト型キャッシュ サーバーを構成するには  

1. サーバーのコンピューターでは、管理者として Windows PowerShell を実行します。 次のコマンドを入力し、し、ENTER キーを押します。

    ``` 
    Install-WindowsFeature BranchCache
    ```

2.  BranchCache 機能のインストール後、ホスト型キャッシュ サーバーとしてコンピューターを構成して、AD DS のサービス接続ポイントを登録するには、Windows PowerShell で、次のコマンドを入力し、し、ENTER キーを押します。

    ```  
    Enable-BCHostedServer -RegisterSCP
    ```  

3. ホスト型キャッシュ サーバーの構成を確認するには、次のコマンドを入力し、ENTER キーを押します。

    ```  
    Get-BCStatus  
    ```  
  
    コマンドの結果は、BranchCache、インストールのすべての側面のステータスを表示します。 BranchCache の設定と各項目の正しい値の一部を次に示します。  
  
    -   BranchCacheIsEnabled: True

    -   HostedCacheServerIsEnabled: True

    -   HostedCacheScpRegistrationEnabled: True

4. ホスト型キャッシュ サーバーをコンテンツ サーバーからデータを使ってパッケージをコピーする手順の準備として、いずれか特定、ホスト型キャッシュ サーバー上の既存の共有または新しいフォルダーを作成し、フォルダーを共有するコンテンツ サーバーからアクセスできるようにします。 コンテンツ サーバー上のデータを使ってパッケージを作成した後は、ホスト型キャッシュ サーバー上でこの共有フォルダーにデータ パッケージがコピーされます。
  
5. 1 つ以上のホスト型キャッシュ サーバーを展開する場合は、各サーバーで、この手順を繰り返します。

このガイドでは、続行するのを参照してください。[移動およびサイズを変更するホスト型キャッシュ (&) #40";"オプション"&"#41 です。](6-Bc-Move-Resize-Cache.md).
