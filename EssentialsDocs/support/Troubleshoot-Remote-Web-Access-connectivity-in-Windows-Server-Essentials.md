---
title: "Windows Server Essentials でのリモート Web アクセス接続をトラブルシューティングします。"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d3642575-b3ee-4488-b654-5bf9d3b8c935
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: af4725fd3b1861c847434e3ed62c3da030689fb5
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="troubleshoot-remote-web-access-connectivity-in-windows-server-essentials"></a>Windows Server Essentials でのリモート Web アクセス接続をトラブルシューティングします。
 
>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:
  
 通常場合は、ルーターが UPnP 認定デバイスで、ルーターで UPnP 設定が有効になっているかどうかは、Windows Server Essentials はブロード バンド ルーターを構成に自動的にできます。  
  
## <a name="possible-issues"></a>考えられる問題  
 リモート Web アクセス接続で次の問題が発生する可能性があります。  
  
-   ルーターが有効でないまたは、ネットワークに接続されていません。  
  
-   ルーターで UPnP 設定が無効になります。  
  
-   ルーターは、UPnP 標準を完全にサポートしない可能性があります。 Microsoft では、Windows オペレーティング システムで機能するルーターの一覧を保持します。 Windows Server Essentials と互換性のあるルーター (ワイヤレス ルーターを含む) の一覧を表示するには、次を参照してください。、[Windows 互換性センター](https://www.microsoft.com/windows/compatibility/CompatCenter/Home)します。  
  
## <a name="possible-fixes"></a>可能な修正方法  
 次の操作は、これらの問題を解決する可能性があります。  
  
-   ルーターの電源が入っていることを確認し、正常に機能します。  
  
-   サーバーが直接ルーターに接続されているルーターに接続されているスイッチに接続されていることを確認します。  
  
-   インターネット サービス プロバイダー (ISP) に接続しているブロード バンド デバイスが入っている、正しく機能していることを確認し、ルーターがそのブロード バンド デバイスに接続されています。  
  
-   ルーターの UPnP 設定を有効にします。 UPnP 設定を有効にするように、ルーターの構成 Web ページに接続します。 UPnP 設定を有効にする方法と、ルーターにログオンする方法については、ルーターのドキュメントを参照してください。 UPnP 設定を有効にした後は、有効にするでリモート Web アクセス ウィザード、ルーターを構成するには、もう一度を実行します。  
  
-   ルーターが UPnP 標準を完全にサポートしない場合に自動的に構成できません。 手動でルーターを構成または UPnP 標準をサポートするルーターを購入する必要があります。  
  
     ルーターを手動で構成するのには、次のタスクを実行します。  
  
    -   Windows Server Essentials サーバーの IP アドレスの予約を作成します。  
  
         Windows Server Essentials に必要なポートを転送するようにルーターを手動で構成する前に、ルーターの Windows Server Essentials を実行しているサーバーの動的ホスト構成プロトコル (DHCP) の予約を設定する必要があります。 この手順では、IP アドレスを変更しないでくださいにポートを転送することが保証されます。  
  
         ルーターにおいて、サーバーの DHCP 予約を手動で設定する方法については、ルーターの製造元のドキュメントを参照してください。  
  
    -   次のポート、ルーターでポート フォワーディングを構成します。  
  
        |サービスまたはプロトコル|ポート|  
        |-------------------------|----------|  
        |HTTP|TCP 80|  
        |HTTPS|TCP 443|  
  
     ルーターでポート フォワーディングを手動で設定する方法については、製造元のドキュメントを参照してください。  
  
     通常、ルーターの構成] ページには、次のような表が含まれています。  
  
    > [!NOTE]
    >  この表では、Windows Server Essentials を実行しているコンピューターの IP アドレスは 192.168.0.100 です。 コンピューターの IP アドレスを決定し、その IP アドレスの表に、IP アドレスに置き換えてください。  
  
    |IP アドレス|プロトコル (TCP または UDP)|スケジュール|受信フィルター|  
    |----------------|---------------------------|--------------|--------------------|  
    |192.168.0.100|TCP 80|いつも|すべて許可します。|  
    |192.168.0.100|TCP 443|いつも|すべて許可します。|  
  
     ルーターを手動で構成した後、有効にする [リモート Web アクセス ウィザードを実行を選択していることを確認、**ルーターのセットアップをスキップ**] オプションを選択、**Getting started**ページ。  
  
-   ルーターが UPnP 標準を完全にサポートしていない場合は、新しいルーターを購入します。  
  
> [!TIP]
>  ルーターの最新の BIOS ファームウェアがインストールされていることを確認します。 多くの場合、ルーターの構成 Web ページから、ルーターの BIOS ファームウェアを更新できます。 詳細については、ルーターのドキュメントを参照してください。 ルーターを更新した後、設定の Anywhere Access のウィザードを実行します。  
  
## <a name="see-also"></a>参照してください。  
  
-   [リモート Web アクセスを使用します。](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md)  
  
-   [リモート Web アクセスを管理します。](../manage/Manage-Remote-Web-Access-in-Windows-Server-Essentials.md)  
  
-   [Anywhere Access を管理します。](../manage/Manage-Anywhere-Access-in-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials を管理します。](../manage/Manage-Windows-Server-Essentials.md)  
  

-   [Windows Server Essentials をサポートします。](Support-Windows-Server-Essentials.md)

-   [Windows Server Essentials をサポートします。](../support/Support-Windows-Server-Essentials.md)

