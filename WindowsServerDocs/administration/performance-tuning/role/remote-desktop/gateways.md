---
title: パフォーマンス チューニングのリモート デスクトップ ゲートウェイ
description: パフォーマンスのチューニング推奨設定のリモート デスクトップ ゲートウェイ
ms.prod: windows-server-threshold
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: HammadBu; VladmiS
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 70b27d45acbfb046d52271a50ca7deffb226b8d0
ms.sourcegitcommit: d84dc3d037911ad698f5e3e84348b867c5f46ed8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/28/2019
ms.locfileid: "66266728"
---
# <a name="performance-tuning-remote-desktop-gateways"></a>パフォーマンス チューニングのリモート デスクトップ ゲートウェイ

> [!Note]
> Windows 8 以降、Windows Server 2012 R2 以降では、リモート デスクトップ ゲートウェイ (RD ゲートウェイ) は、TCP、UDP、および従来の RPC トランスポートをサポートします。 次のデータのほとんどはについては、従来の RPC トランスポート。 従来の RPC トランスポートが使用されていない場合はこのセクションでは適用されません。

このトピックでは、顧客の展開のパフォーマンスを向上させるのに役立つパフォーマンスに関連するパラメーターと、顧客のネットワークの使用パターンに依存するチューニングについて説明します。

基本的には、RD ゲートウェイは、多くのパケットがリモート デスクトップ接続のインスタンスと、お客様のネットワーク内の RD セッション ホスト サーバー インスタンス間での操作の転送を実行します。

> [!Note]
> 次のパラメーターは、RPC トランスポートのみに適用されます。

インターネット インフォメーション サービス (IIS) と RD ゲートウェイ、RD ゲートウェイでのシステム パフォーマンスを向上させるのには、次のレジストリ パラメーターをエクスポートします。

**スレッドのチューニング**

-   **Maxiothreads**

    ``` syntax
    HKLM\Software\Microsoft\Terminal Server Gateway\Maxiothreads (REG_DWORD)
    ```

    このアプリに固有のスレッド プールには、受信要求を処理するために RD ゲートウェイを作成するスレッドの数を指定します。 このレジストリ設定が存在する場合は、有効になります。 スレッドの数では、論理プロセスの数と同じです。 論理プロセッサの数が 5 未満の場合は、既定値は 5 つのスレッドです。

-   **MaxPoolThreads**

    ``` syntax
    HKLM\System\CurrentControlSet\Services\InetInfo\Parameters\MaxPoolThreads (REG_DWORD)
    ```

    このパラメーターは、論理プロセッサごとに作成する IIS プールのスレッドの数を指定します。 IIS プールのスレッドでは、要求のネットワークを監視し、すべての受信要求を処理します。 **MaxPoolThreads** RD ゲートウェイを使用するスレッドは含まれません。 既定値は 4 です。

**RD ゲートウェイのリモート プロシージャ呼び出しのチューニング**

次のパラメーターは、リモート デスクトップ接続と RD ゲートウェイのコンピューターで受信したリモート プロシージャ コール (RPC) を調整できます。 ウィンドウを変更するは、データの量が各接続経由で流れておよび rpc over HTTP v2 のシナリオのパフォーマンスを向上させることができますを調整することができます。

-   **ServerReceiveWindow**

    ``` syntax
    HKLM\Software\Microsoft\Rpc\ServerReceiveWindow (REG_DWORD)
    ```

    既定値は、64 KB です。 この値は、サーバーが RPC プロキシから受信したデータを使用するウィンドウを指定します。 最小値は 8 KB に設定し、最大値は 1 GB に設定します。 値が存在しない場合は、既定値が使用されます。 この値に変更を行ったときに、変更を反映するの IIS を再起動する必要があります。

-   **ServerReceiveWindow**

    ``` syntax
    HKLM\Software\Microsoft\Rpc\ServerReceiveWindow (REG_DWORD)
    ```

    既定値は、64 KB です。 この値は、クライアントが RPC プロキシから受信したデータを使用するウィンドウを指定します。 最小値は 8 KB で、最大値は 1 GB です。 値が存在しない場合は、既定値が使用されます。

## <a name="monitoring-and-data-collection"></a>監視とデータの収集


RD ゲートウェイのリソースの使用状況を監視すると、次のパフォーマンス カウンターの一覧はカウンターの基準セットと見なされます。

-   \\ターミナル サービス ゲートウェイ\\\*

-   \\RPC/HTTP プロキシ\\\*

-   \\サーバーあたり RPC/HTTP プロキシ\\\*

-   \\Web サービス\\\*

-   \\W3SVC\_W3WP\\\*

-   \\IPv4\\\*

-   \\メモリ\\\*

-   \\Network Interface(\*)\\\*

-   \\Process(\*)\\\*

-   \\プロセッサ情報 (\*)\\\*

-   \\Synchronization(\*)\\\*

-   \\システム\\\*

-   \\TCPv4\\\*

次のパフォーマンス カウンターは、従来の RPC トランスポートのみに適用されます。

-   \\RPC/HTTP プロキシ\\\* RPC

-   \\サーバーあたり RPC/HTTP プロキシ\\\* RPC

-   \\Web サービス\\\* RPC

-   \\たとえば、W3SVC\_W3WP\\ \* RPC

**注**  該当する場合、追加、 \\IPv6\\ \*と\\TCPv6\\ \*オブジェクト。ReplaceThisText

 
