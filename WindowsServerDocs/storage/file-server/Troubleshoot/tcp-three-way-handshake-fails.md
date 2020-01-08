---
title: SMB 接続中の TCP の3方向ハンドシェイクエラー
description: SMB 接続中の TCP 3 方向ハンドシェイクエラーについて説明します。
author: Deland-Han
manager: dcscontentpm
audience: ITPro
ms.topic: article
ms.author: delhan
ms.date: 12/25/2019
ms.openlocfilehash: 8cef47e164b8768747cb383f4d7012130c7cb516
ms.sourcegitcommit: 8cf04db0bc44fd98f4321dca334e38c6573fae6c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75654633"
---
# <a name="tcp-three-way-handshake-failure-during-smb-connection"></a>SMB 接続中の TCP の3方向ハンドシェイクエラー

ネットワークトレースを分析すると、SMB の問題が発生する原因となる、伝送制御プロトコル (TCP) の3方向ハンドシェイクエラーが発生していることがわかります。 この記事では、この状況をトラブルシューティングする方法について説明します。

## <a name="troubleshooting"></a>[トラブルシューティング]

一般に、トラフィックをブロックするローカルまたはインフラストラクチャのファイアウォールが原因です。 この問題は、次のいずれかのシナリオで発生する可能性があります。

## <a name="scenario-1"></a>例 1

SMB サーバーで TCP SYN パケットが到着しましたが、SMB サーバーは TCP SYN ACK パケットを返しません。

このシナリオのトラブルシューティングを行うには、次の手順を実行します。

### <a name="step-1"></a>手順 1

**Netstat**または**NetTcpConnection**を実行して、システムプロセスによって所有される必要がある、TCP ポート445のリスナーがあることを確認します。

```cmd
netstat -ano | findstr :445
```

```PowerShell
Get-NetTcpConnection -LocalPort 445
```

### <a name="step-2"></a>手順 2

サーバーサービスが開始され、実行されていることを確認します。

### <a name="step-3"></a>手順 3

Windows Filtering Platform (WFP) キャプチャを使用して、どのルールまたはプログラムがトラフィックを破棄しているかを判断します。 これを行うには、コマンドプロンプトウィンドウで次のコマンドを実行します。

```cmd
netsh wfp capture start
```

問題を再現してから、次のコマンドを実行します。

```cmd
netsh wfp capture stop
```

シナリオトレースを実行し、SMB トラフィック (TCP ポート 445) で WFP が削除されていないかどうかを確認します。

必要に応じて、常に WFP ベースではないため、ウイルス対策プログラムを削除することもできます。

### <a name="step-4"></a>手順 4

Windows ファイアウォールが有効になっている場合は、ファイアウォールのログ記録を有効にして、トラフィックを破棄するかどうかを判断します。

**セキュリティが強化された Windows ファイアウォール**の \> 受信の規則で、適切な "ファイルとプリンターの共有 (SMB**受信**)" 規則が有効になっていることを確認します。

> [!NOTE]
> コンピューターのセットアップ方法によっては、"windows ファイアウォール" が "Windows Defender ファイアウォール" と呼ばれることがあります。

## <a name="scenario-2"></a>シナリオ 2

SMB サーバーで TCP SYN パケットが受信されることはありません。

このシナリオでは、ネットワークパスに従ってデバイスを調査する必要があります。 各デバイスでキャプチャされたネットワークトレースを分析して、どのデバイスがトラフィックをブロックしているかを判断することができます。
