---
title: Windows Server Essentials におけるリモート Web アクセス接続のトラブルシューティング
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: d3642575-b3ee-4488-b654-5bf9d3b8c935
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 9fb3628ed519d5faae04787dbb84da37f27d96fb
ms.sourcegitcommit: 56ac7cf3f4bbcc5175f140d2df5f37cc42ba76d1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/23/2020
ms.locfileid: "85217492"
---
# <a name="troubleshoot-remote-web-access-connectivity-in-windows-server-essentials"></a>Windows Server Essentials におけるリモート Web アクセス接続のトラブルシューティング
 
>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials
  
 通常、Windows Server Essentials では、ルーターが UPnP 認定デバイスで、UPnP 設定がルーター上で有効になっている場合にはブロードバンド ルーターの自動構成が可能です。  
  
## <a name="possible-issues"></a>考えられる問題  
 リモート Web アクセス接続を使用すると、以下の問題が生じる可能性があります。  
  
-   ルーターの電源が入らないか、ネットワークに接続できません。  
  
-   ルーターの UPnP 設定が有効になりません。  
  
-   ルーターで UPnP 標準を完全にサポートできません。 Windows オペレーティング システムで機能するルーターの一覧を Microsoft は備えています。 Windows Server Essentials と互換性のあるルーター (ワイヤレス ルーターを含む) の一覧を確認するには、 [Windows 互換性センター](https://www.microsoft.com/windows/compatibility/CompatCenter/Home)にアクセスしてください。  
  
## <a name="possible-fixes"></a>考えられる修正方法  
 このような問題については、次の処置によって修正できる場合があります。  
  
- ルーターの電源が入っていること、および適切に機能していることを確認します。  
  
- サーバーが直接ルーターに接続されていること、またはルーターに接続しているスイッチにサーバーが接続していることを確認してください。  
  
- インターネット サービス プロバイダー (ISP) に接続しているブロードバンド デバイスの電源が入っていること、適切に機能していること、ルーターがそのブロードバンド デバイスに接続されていることを確かめます。  
  
- ルーターで UPnP 設定を有効にします。 ルーターの構成 Web ページに接続し、UPnP 設定を有効にします。 ルーターへのログオン方法、UPnP 設定を有効にする方法については、ご使用のルーターのドキュメントを参照してください。 UPnP 設定を有効にした後、リモート Web アクセスの有効化ウィザードをもう一度実行してルーターを構成します。  
  
- ルーターで UPnP 標準を完全にサポートしていない場合、自動構成は行えません。 ルーターを手動で構成するか、UPnP 標準をサポートしているルーターを購入する必要があります。  
  
   ルーターを手動で構成するには、次のタスクを実行します。  
  
  - Windows Server Essentials サーバー用に IP アドレスの予約を行います。  
  
     必要なポートを Windows Server Essentials に転送するようにルーターを手動で構成する前に、Windows Server Essentials を実行しているサーバーに関する動的ホスト構成プロトコル (DHCP) の予約をルーターで設定しなければなりません。 この手順により、ポートを転送する予定の IP アドレスが変更されないことを保証できます。  
  
     ルーターでサーバーの DHCP 予約を手動で設定する方法の詳細については、ルーターの製造元のドキュメントを参照してください。  
  
  - 次のポートに関するポート フォワーディングをルーターで構成します。  
  
    |サービスまたはプロトコル|Port|  
    |-------------------------|----------|  
    |HTTP|TCP 80|  
    |HTTPS|TCP 443|  
  
    ルーターでポートフォワーディングを手動で設定する方法については、製造元のドキュメントを参照してください。  
  
    通常、ルーターの構成ページには次のような表が含まれます。  
  
  > [!NOTE]
  >  この表の場合、Windows Server Essentials を実行しているコンピューターの IP アドレスは 192.168.0.100 です。 ご使用のコンピューターの IP アドレスを判別し、その IP アドレスを、表で示されている IP アドレスの代わりに使用してください。  
  
  |IP アドレス|プロトコル (TCP/UDP)|スケジュール|受信フィルター|  
  |----------------|---------------------------|--------------|--------------------|  
  |192.168.0.100|TCP 80|Always|すべて許可する|  
  |192.168.0.100|TCP 443|Always|すべて許可する|  
  
   ルーターを手動で構成した後、[リモート Web アクセスを有効にする] ウィザードを実行して、 **[はじめに] ページで**[**ルーターのセットアップをスキップ**する] オプションが選択されていることを確認します。  
  
- ルーターが UPnP 標準を完全にサポートしていない場合には、新しいルーターを購入してください。  
  
> [!TIP]
>  ルーターに最新の BIOS ファームウェアがインストールされていることを確認します。 多くの場合、ルーターの構成 Web ページから、ルーターの BIOS ファームウェアを更新できます。 詳細については、ルーターのドキュメントをご覧ください。 ルーターの更新後、[Anywhere Access のセットアップ] ウィザードを実行します。  
  
## <a name="see-also"></a>関連項目  
  
-   [リモート Web アクセスの使用](../use/Use-Remote-Web-Access-in-Windows-Server-Essentials.md)  
  
-   [リモート Web アクセスの管理](../manage/Manage-Remote-Web-Access-in-Windows-Server-Essentials.md)  
  
-   [Anywhere Access の管理](../manage/Manage-Anywhere-Access-in-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials の管理](../manage/Manage-Windows-Server-Essentials.md)  

-   [Windows Server Essentials のサポート](../support/Support-Windows-Server-Essentials.md)

