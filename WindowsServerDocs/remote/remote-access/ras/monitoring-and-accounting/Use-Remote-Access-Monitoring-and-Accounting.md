---
title: リモート アクセスの監視とアカウンティングを使用する
description: このトピックは、Windows Server 2016 のリモートアクセスの監視とアカウンティングに関するガイドの一部です。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: 92519b49-0df4-43c1-9717-f13570644212
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 03d367f2f981ca3ed649f1ca4d5eca23967c9cfc
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80860515"
---
# <a name="use-remote-access-monitoring-and-accounting"></a>リモート アクセスの監視とアカウンティングを使用する

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

リモート アクセス監視では、DirectAccess 接続と VPN 接続に関するリモート ユーザーの活動と状態が報告されます。 クライアント接続の回数と期間 (他の統計も含めて) が追跡され、サーバーの操作状態が監視されます。 使いやすい監視コンソールでは、リモート アクセス インフラストラクチャ全体を表示できます。 監視ビューは、単一のサーバー、クラスター、およびマルチサイトの構成について表示できます。  
  
**注:** Windows Server 2012 が DirectAccess およびルーティングとリモート アクセス サービス (RRAS) を 1 つのリモート アクセス役割に結合します。  
  
> [!NOTE]  
> このトピックに加え、次のトピックをリモート アクセスの監視に利用できます。  
>   
> -   [リモート アクセス サーバー上の既存の負荷を監視する](Monitor-the-existing-load-on-the-Remote-Access-server.md)  
> -   [リモート アクセス サーバーの構成配布の状態を監視する](Monitor-the-configuration-distribution-status-of-the-Remote-Access-server.md)  
> -   [リモートアクセスサーバーとそのコンポーネントの操作の状態を監視する](Monitor-the-operations-status-of-the-Remote-Access-server-and-its-components.md)  
> -   [リモート アクセス サーバーの操作上の問題を特定して解決する](Identify-and-resolve-Remote-Access-server-operations-problems.md)  
> -   [接続しているリモート クライアントの活動と状態を監視する](Monitor-connected-remote-clients-for-activity-and-status.md)  
> -   [履歴データを使ってリモート クライアントの使用状況レポートを生成する](Generate-a-usage-report-for-remote-clients-using-historical-data.md)  

## <a name="in-this-guide"></a>このガイドの内容  
このドキュメントでは、リモート アクセスの監視機能を利用するために、DirectAccess 管理コンソールおよびそれに対応する Windows PowerShell コマンドレット (リモート アクセス サーバーの役割の一部として提供されます) を使用する手順を説明します。  
  
次に示す監視とアカウンティングのシナリオについて説明しています。  
  
1.  リモート アクセス サーバー上の既存の負荷を監視する  
  
2.  リモート アクセス サーバーの構成配布の状態を監視する  
  
3.  リモート アクセス サーバーとそのコンポーネントの操作状態を監視する  
  
4.  リモート アクセス サーバーの操作上の問題を特定して解決する  
  
5.  接続しているリモート クライアントの活動と状態を監視する  
  
6.  履歴データを使ってリモート クライアントの使用状況レポートを生成する  
  
### <a name="understand-monitoring-and-accounting"></a>監視とアカウンティングについて  
リモート クライアントの監視とアカウンティングを開始する前に、この 2 つのタスクの違いを理解しておく必要があります。  
  
-   **監視**では、任意の時点でアクティブに接続しているユーザーが示されます。  
  
-   **アカウンティング**では、企業ネットワークに接続したことのあるユーザーの履歴と、その使用状況の詳細が保持されます (法令遵守および監査の目的で)。  
  
リモート クライアントの監視は接続をベースにしています。 DirectAccess クライアントによって確立されるトンネル接続には、次の 2 つの種類があります。  
  
-   **コンピューター トンネル トラフィック接続**:このトンネルは、名前解決、認証、修復更新などに必要とされるサーバーにアクセスするために、システム コンテキストでコンピューターによって確立されます。  
  
-   **ユーザー トンネル トラフィック接続**:このトンネルは、ユーザーが企業ネットワーク上のリソースにアクセスするときに、ユーザー コンテキストでコンピューター上のユーザー アカウントによって確立されます。 展開の要件に応じて、ユーザーは企業ネットワーク上のリソースにアクセスするために、強力な資格情報を提供しなければならない場合があります (スマート カードの使用やワンタイム パスワードの入力などによって)。  
  
DirectAccess の場合、接続はリモート クライアントの IP アドレスによって一意に識別されます。 たとえば、クライアント コンピューターに対してコンピューター トンネルが確立されていて、ユーザーがそのコンピューターから接続する場合、どちらも同じ接続を使用します。 コンピューター トンネルがまだアクティブのときに、ユーザーがいったん接続を切断し、もう一度接続する状況では、この接続は単一の接続です。  
  


