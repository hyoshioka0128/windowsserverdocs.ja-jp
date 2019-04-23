---
title: テスト ラボ ガイド - Windows NLB を使用するクラスターでの DirectAccess のデモンストレーション
description: このトピックは一部のテスト ラボ ガイド - Windows Server 2016 で Windows NLB を使用するクラスターでの DirectAccess のデモンストレーション
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: db15dcf5-4d64-48d7-818a-06c2839e1289
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 910afa78553c828aff954f7677869569068198aa
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59869523"
---
# <a name="test-lab-guide-demonstrate-directaccess-in-a-cluster-with-windows-nlb"></a>テスト ラボ ガイド:Windows NLB を使用するクラスターでの DirectAccess をデモンストレーションします。

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

リモート アクセスは、リモート ユーザーが DirectAccess または RRAS VPN を使用して内部ネットワーク リソースに安全にアクセスできるようにする Windows Server 2012 R2 andWindows Server 2012 オペレーティング システム、Windows Server 2016 でサーバーの役割です。 このガイドには拡張するための手順が含まれています、[テスト ラボ ガイド。IPv4 と IPv6 混在での DirectAccess 単一サーバー セットアップのデモンストレーション](https://go.microsoft.com/fwlink/p/?LinkId=237004)に DirectAccess ネットワーク負荷分散とクラスターの構成を示します。  
  
## <a name="about-this-guide"></a>このガイドについて  
このガイドでは、6 台のサーバーと 2 台のクライアント コンピューターを使うリモート アクセスを構成し、デモンストレーションを行う手順について説明します。 NLB を使うリモート アクセスのテスト ラボが完成すると、イントラネット、インターネット、ホーム ネットワークをシミュレートでき、さまざまなインターネット接続シナリオでリモート アクセス機能のデモンストレーションを行うことができます。  
  
> [!IMPORTANT]  
> このラボは、最小限のコンピューターを使って概念を実証するためのものです。 このガイドで詳しく説明されている構成は、テスト ラボでの使用のみを目的としています。運用環境では使用しないでください。  
  
## <a name="KnownIssues"></a>既知の問題  
クラスター構成シナリオには、次の既知の問題があります。  
  
-   単一のネットワーク アダプターを使用して IPv4 のみの展開で DirectAccess を構成し、既定の DNS64 (":3333::" を含む IPv6 アドレス) がネットワーク アダプターに自動的に構成された後で、リモート アクセス管理コンソールを使用して負荷分散を有効にしようとすると、IPv6 DIP の指定を求められます。 クリックすると、構成が失敗する場合、IPv6 DIP を指定すると、**コミット**エラー。パラメーターが正しくありません。  
  
    この問題の解決策は、以下のとおりです。  
  
    1.  「 [Back up and Restore Remote Access Configuration (リモート アクセスの構成のバックアップと復元)](https://gallery.technet.microsoft.com/Back-up-and-Restore-Remote-e157e6a6)」からバックアップおよび復元用のスクリプトをダウンロードします。  
  
    2.  ダウンロードしたスクリプト Backup-RemoteAccess.ps1 を使用して、リモート アクセス GPO をバックアップします。  
  
    3.  失敗した手順まで、負荷分散の有効化を試みます。 [負荷分散の有効化] ダイアログ ボックスで、詳細領域を展開し、詳細領域内を右クリックして、 **[スクリプトのコピー]** をクリックします。  
  
    4.  メモ帳を開き、クリップボードの内容を貼り付けます。 例:  
  
        ```  
        Set-RemoteAccessLoadBalancer -InternetDedicatedIPAddress @('10.244.4.19/255.255.255.0','fdc4:29bd:abde:3333::2/128') -InternetVirtualIPAddress @('fdc4:29bd:abde:3333::1/128', '10.244.4.21/255.255.255.0') -ComputerName 'DA1.domain1.corp.contoso.com' -Verbose  
        ```  
  
    5.  開いているリモート アクセス ダイアログ ボックスをすべて閉じ、リモート アクセス管理コンソールを閉じます。  
  
    6.  貼り付けたテキストを編集して、IPv6 アドレスを削除します。 次に、例を示します。  
  
        ```  
        Set-RemoteAccessLoadBalancer -InternetDedicatedIPAddress @('10.244.4.19/255.255.255.0') -InternetVirtualIPAddress @('10.244.4.21/255.255.255.0') -ComputerName 'DA1.domain1.corp.contoso.com' -Verbose  
        ```  
  
    7.  管理者特権の PowerShell ウィンドウで、前の手順のコマンドを実行します。  
  
    8.  コマンドレットが実行中に (不正入力値以外の理由で) 失敗する場合は、コマンド Restore-RemoteAccess.ps1 を実行し、手順に従って元の構成の整合性が維持されていることを確認します。  
  
    9. リモート アクセス管理コンソールを再び開くことができるようになります。  
  


