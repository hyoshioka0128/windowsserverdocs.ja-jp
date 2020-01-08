---
title: SMB マルチチャネルのトラブルシューティング
description: SMB マルチチャネルのトラブルシューティング方法について説明します。
author: Deland-Han
manager: dcscontentpm
audience: ITPro
ms.topic: article
ms.author: delhan
ms.date: 12/25/2019
ms.openlocfilehash: 91f034a0062f509b1185f04554af4383022a68e1
ms.sourcegitcommit: 8cf04db0bc44fd98f4321dca334e38c6573fae6c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/03/2020
ms.locfileid: "75654543"
---
# <a name="smb-multichannel-troubleshooting"></a>SMB マルチチャネルのトラブルシューティング

この記事では、SMB マルチチャネルに関連する問題をトラブルシューティングする方法について説明します。

## <a name="check-the-network-interface-status"></a>ネットワークインターフェイスの状態を確認する

SMB クライアント (MS\_クライアント) および SMB サーバー (MS\_サーバー) で、ネットワークインターフェイスのバインドが**True**に設定されていることを確認します。 次のコマンドを実行すると、両方のネットワークインターフェイスで [**有効** **] の**下に出力が表示されます。

```PowerShell
Get-NetAdapterBinding -ComponentID ms_server,ms_msclient
```

その後、次のコマンドの出力にネットワークインターフェイスが表示されていることを確認します。

```PowerShell
Get-SmbServerNetworkInterface
```

```PowerShell
Get-SmbClientNetworkInterface
```

**Get NetAdapter**コマンドを実行してインターフェイスのインデックスを表示し、結果を確認することもできます。 インターフェイスインデックスには、適切なインターフェイスにアクティブにバインドされているすべてのアクティブな SMB アダプターが表示されます。

## <a name="check-the-firewall"></a>ファイアウォールを確認する

リンクローカル IP アドレスのみが存在し、パブリックにルーティング可能なアドレスがない場合は、ネットワークプロファイルが**パブリック**に設定されている可能性があります。 これは、既定で SMB がファイアウォールでブロックされることを意味します。

次のコマンドは、使用されている接続プロファイルを示します。 ネットワークと共有センターを使用してこの情報を取得することもできます。

**Get NetConnectionProfile**

**[ファイルとプリンターの共有]** グループの下で、ファイアウォールの受信規則を確認して、正しいプロファイルに対して "SMB 受信" が有効になっていることを確認します。

![SMB インルール](media/smb-multichannel-troubleshooting-1.png)

**[ネットワークと共有センター]** ウィンドウで、**ファイルとプリンターの共有**を有効にすることもできます。 これを行うには、左側のメニューで **[共有の詳細設定を変更]** する を選択し、プロファイルの **[ファイルとプリンターの共有を有効にする]** を選択します。 このオプションを選択すると、ファイルとプリンターの共有のファイアウォール規則が有効になります。

![[共有の詳細設定の変更]](media/smb-multichannel-troubleshooting-2.png)

## <a name="capture-client-and-server-sided-traffic-for-troubleshooting"></a>トラブルシューティングのためにクライアントとサーバーの間のトラフィックをキャプチャする

TCP 3 ウェイハンドシェイクから開始する SMB 接続トレース情報が必要です。 キャプチャを開始する前に、すべてのアプリケーション (特に Windows エクスプローラー) を閉じることをお勧めします。 SMB クライアントで**ワークステーション**サービスを再起動し、パケットキャプチャを開始して、問題を再現します。

SMBv3 接続がネゴシエートされていること、およびサーバーとクライアントの間の何も言語ネゴシエーションに影響していないことを確認*します。* SMBv2 以前のバージョンでは、マルチチャネルはサポートされていません。

ネットワーク\_インターフェイス\_情報パケットを探します。 ここで smb クライアントは、SMB サーバーからアダプターの一覧を要求します。 これらのパケットが交換されない場合、マルチチャネルは機能しません。

サーバーは、有効なネットワークインターフェイスの一覧を返すことによって応答します。 その後、SMB クライアントは、マルチチャネル用に使用可能なアダプターの一覧にそれらを追加します。 この時点で、マルチチャネルが開始され、少なくとも接続を開始しようとします。

詳しくは、次の記事をご覧ください。

- [3.2.4.20.10 アプリケーションがサーバーのネットワークインターフェイスのクエリを要求する](https://docs.microsoft.com/openspecs/windows_protocols/ms-smb2/147adde4-d936-4597-924a-8caa3429c6b0)

- [2.2.32.5 NETWORK\_INTERFACE\_情報応答](https://docs.microsoft.com/openspecs/windows_protocols/ms-smb2/fcd862d1-1b85-42df-92b1-e103199f531f)

- [3.2.5.14.11 ネットワークインターフェイス応答の処理](https://docs.microsoft.com/openspecs/windows_protocols/ms-smb2/5459722b-1eaa-4ead-b465-284363264cad)

次のシナリオでは、アダプターを使用できません。

- クライアントにルーティングに関する問題があります。 これは、通常、間違ったインターフェイスでトラフィックを強制する間違ったルーティングテーブルが原因で発生します。

- マルチチャネルの制約が設定されています。 詳細については、「 [SmbMultichannelConstraint](https://docs.microsoft.com/powershell/module/smbshare/new-smbmultichannelconstraint)」を参照してください。

- ネットワークインターフェイスの要求パケットと応答パケットがブロックされました。

- クライアントとサーバーは、追加のネットワークインターフェイスを経由して通信することはできません。 たとえば、TCP の3方向ハンドシェイクに失敗した場合、接続がファイアウォールによってブロックされている、セッションのセットアップに失敗したなどがあります。

アダプターとその IPv6 アドレスがサーバーから送信された一覧にある場合は、次の手順では、そのインターフェイス上で通信が試行されているかどうかを確認します。 リンクローカルアドレスと SMB トラフィックでトレースをフィルター処理し、接続試行を探します。 これが NetConnection トレースの場合は、Windows Filtering Platform (WFP) イベントを調べて、接続がブロックされているかどうかを確認することもできます。
