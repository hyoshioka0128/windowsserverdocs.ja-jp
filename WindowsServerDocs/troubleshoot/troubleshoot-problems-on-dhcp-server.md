---
title: DHCP サーバーでの問題のトラブルシューティング
description: この artilce では、DHCP サーバーの問題をトラブルシューティングし、データを収集する方法について説明します。
ms.service: na
manager: dcscontentpm
ms.date: 5/26/2020
ms.topic: article
author: Deland-Han
ms.author: delhan
ms.openlocfilehash: d6fc69c15c3465769232d89f70a65ca915d0584e
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87989035"
---
# <a name="troubleshoot-problems-on-the-dhcp-server"></a>DHCP サーバーでの問題のトラブルシューティング

この記事では、DHCP サーバーで発生した問題をトラブルシューティングする方法について説明します。

## <a name="troubleshooting-checklist"></a>トラブルシューティングのチェックリスト

次の設定を確認してください。

  - DHCP サーバーサービスが開始され、実行されています。 この設定を確認するには、 **net start**コマンドを実行し、 **DHCP サーバー**を探します。

  - DHCP サーバーが承認されている。 「[ドメインに参加しているシナリオでの WINDOWS DHCP サーバーの承認」を](/openspecs/windows_protocols/ms-dhcpe/56f8870b-a7c1-4db1-8a86-f69079fe5077)参照してください。

  - DHCP クライアントがあるサブネットの DHCP サーバースコープで IP アドレスリースが使用可能であることを確認します。 これを行うには、DHCP サーバー管理コンソールで適切なスコープの統計情報を参照してください。

  - \_アドレスのリースに無効なアドレスの一覧があるかどうかを確認します。

  - ネットワーク上のどのデバイスにも、DHCP スコープから除外されていない静的 IP アドレスがあるかどうかを確認します。

  - DHCP サーバーがバインドされている IP アドレスが、IP アドレスをリースする必要があるスコープのサブネット内にあることを確認します。これは、使用可能なリレーエージェントがない場合に当てはまります。 これを行うには、 **DhcpServerv4Binding**または**DhcpServerv6Binding**コマンドレットを実行します。

  - DHCP サーバーのみが UDP ポート67および68でリッスンしていることを確認します。 他のプロセスまたは他のサービス (WDS、PXE など) では、これらのポートを占有しません。 これを行うには、コマンドを実行し `netstat -anb` ます。

  - IPsec によって展開された環境を扱う場合は、DHCP サーバー IPsec 除外が追加されていることを確認します。

  - リレーエージェントの IP アドレスが DHCP サーバーから ping できることを確認します。

  - 構成された DHCP ポリシーとフィルターを列挙して確認します。

## <a name="event-logs"></a>イベント ログ

監視対象の問題に関連する報告された問題については、システムおよび DHCP サーバーサービスのイベントログ (**Applications and Services logs** \> **Microsoft** \> **Windows** \> **DHCP-Server**) を確認してください。
問題の種類に応じて、イベントは次のいずれかのイベントチャネルに記録されます。 [dhcp サーバーの操作イベント](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn800668\(v=ws.11\)) 
 [dhcp サーバーの管理イベント](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn800668\(v=ws.11\)) 
 [dhcp サーバーシステムイベント](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn800668\(v=ws.11\)) 
 [dhcp サーバーのフィルター通知イベント](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn800668\(v=ws.11\))dhcp サーバー 
 [監査イベント](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn800668\(v=ws.11\))

## <a name="data-collection"></a>データ コレクション

### <a name="dhcp-server-log"></a>DHCP サーバーログ

DHCP サーバーサービスのデバッグログには、DHCP サーバーによって実行される IP アドレスのリース割り当てと DNS 動的更新に関する詳細情報が記載されています。 既定では、これらのログは% windir% \\ System32 Dhcp にあり \\ ます。
詳細については、「 [DHCP サーバーのログファイルの分析](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd183591\(v=ws.10\))」を参照してください。

### <a name="network-trace"></a>ネットワーク トレース

関連付けられているネットワークトレースは、イベントがログに記録されたときに DHCP サーバーが何を行っていたかを示す場合があります。 このようなトレースを作成するには、次の手順を実行します。

1.  [GitHub](https://github.com/CSS-Windows/WindowsDiag/tree/master/ALL/TSS)にアクセスし、 [tss \_tools.zip](https://github.com/CSS-Windows/WindowsDiag/blob/master/ALL/TSS/tss_tools.zip)ファイルをダウンロードします。

2.  Tss \_tools.zip ファイルをコピーし、C: tools フォルダーなどのローカルディスク上の場所に展開し \\ ます。

3.  \\管理者特権でのコマンドプロンプトウィンドウで、C: tools から次のコマンドを実行します。
    ```console
    TSS Ron Trace <Stop:Evt:>20321:<Other:>DhcpAdminEvents NoSDP NoPSR NoProcmon NoGPresult
    ```

    >[!Note]
    >このコマンドで、とを、 \<*Stop:Evt:*\> \<*Other:*\> トレースセッションでフォーカスを移動するイベント ID とイベントチャネルに置き換えます。
    >\_ \_ Tsstools.zip ファイルに含まれている Tss ReadMeHelp.docx ファイルは、 \_ 使用可能なすべての設定に関する詳細情報を提供します。

4.  イベントがトリガーされると、このツールは C: MS DATA という名前のフォルダーを作成し \\ \_ ます。 このフォルダーには、コンピューターのネットワークとドメインの構成に関する一般的な情報を提供する便利な出力ファイルがいくつか含まれています。
    このフォルダー内の最も興味深いファイルは、% Computername% \_ date \_ time \_ packetcapture \_ internetclient \_ dbg. etl です。
    [ネットワークモニター](https://www.microsoft.com/download/4865)アプリケーションを使用すると、ファイルを読み込み、"DHCP または DNS" プロトコルの表示フィルターを設定して、バックグラウンドで何が起こっているかを調べることができます。