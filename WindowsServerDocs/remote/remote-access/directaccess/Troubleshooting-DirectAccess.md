---
title: DirectAccess のトラブルシューティング
description: このトピックでは、Windows Server 2016 での DirectAccess の展開のトラブルシューティングに関する情報を提供します。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 61040e19-5960-4eb0-b612-d710627988f7
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f49d9ab0e28e84cbb46015d50778653b35f5ea85
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67281943"
---
# <a name="troubleshooting-directaccess"></a>DirectAccess のトラブルシューティング

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

リモート アクセス (DirectAccess) の問題のトラブルシューティングを行うこれらの手順に従います。  
  
|||  
|-|-|  
|**問題**|**解決方法**|  
|リモート アクセス管理コンソールは、DirectAccess の構成を表示できません。|**不足している構成情報を復元するには**<br />マルチサイト展開のトラブルシューティングを行う場合は、エントリ ポイントに最も近いドメイン コント ローラーがあることを確認します。<br />-を使用して、 **Get DAEntrypointDC**エントリ ポイントに最も近いドメイン コント ローラーの名前を取得するコマンドレットです。 ドメイン コント ローラーが実行されていない場合は、使用、 **Set-daentrypointdc**コマンドレットをもう 1 つのドメイン コント ローラー をポイントします。<br />-実行**gpresult**サーバーが DirectAccess グループ ポリシー オブジェクトを取得するように、サーバーで管理者特権でコマンド プロンプトからです。<br />-ユーザー インターフェイス (UI) のログ記録を有効にします。<br />-Windows PowerShell のログ記録を開始する、次のコマンドを使います。<pre>logman create trace ETWTrace -ow -o c:\ETWTrace.etl -p {AAD4C46D-56DE-4F98-BDA2-B5EAEBDD2B04} 0xffffffffffffffff 0xff -nb 16 16 -bs 1024 -mode 0x2 -max 2048 -ets <br />logman update trace ETWTrace -p {62DFF3DA-7513-4FCA-BC73-25B111FBB1DB} 0xffffffffffffffff 0xff -ets</pre><repro>-終了し、ユーザー インターフェイスを閉じてください。<br />-Windows Powershell のログ記録を無効にします。 イベント トレース ログ ファイルを収集します。 またからのすべてのログを収集、 **%windir%/tracing**フォルダー。|  
|DirectAccess の構成の適用が失敗しました。|**DirectAccess の構成を更新するには**<br />マルチサイト展開のトラブルシューティングを行う場合は、エントリ ポイントに最も近いドメイン コント ローラーがあることを確認します。<br />-を使用して、 **Get DAEntrypointDC**エントリ ポイントに最も近いドメイン コント ローラーの名前を取得するコマンドレットです。 ドメイン コント ローラーが実行されていない場合は、使用、 **Set-daentrypointdc**コマンドレットをもう 1 つのドメイン コント ローラー をポイントします。<br />-Windows Powershell のログ記録を開始する、次のコマンドを使います。<br /><pre>logman create trace ETWTrace -ow -o c:\ETWTrace.etl -p {AAD4C46D-56DE-4F98-BDA2-B5EAEBDD2B04} 0xffffffffffffffff 0xff -nb 16 16 -bs 1024 -mode 0x2 -max 2048 -ets<br />logman update trace ETWTrace -p {62DFF3DA-7513-4FCA-BC73-25B111FBB1DB} 0xffffffffffffffff 0xff -ets</pre>    <repro><br />-**適用**します。<br />-障害が発生した後は、Windows Powershell のログ記録を無効にし、イベントのトレース ログを収集します。|  
|DirectAccess が構成されているが、クライアントが内部リソースに接続できません。|**クライアント接続の問題をトラブルシューティングするには**<br />-[クリックして、**操作の状況**] タブで、リモート アクセス管理コンソールをすべてのコンポーネントが緑色のアイコンを表示することを確認してください。 できない場合は、エラーの詳細を確認し、解決の手順に従います。<br />-リモート アクセス サーバー ベスト プラクティス アナライザー (BPA) を実行します。 警告またはエラーがある場合は、問題を解決する解決手順に従ってください。|  
|マルチサイトの構成 (、マルチサイト、追加のエントリ ポイントを有効にする。 または、エントリ ポイント ドメイン コント ローラー設定など) に関連する問題が発生してください。|次の手順では、[マルチサイト展開のトラブルシューティングを行う](https://technet.microsoft.com/library/jj554657(v=ws.11).aspx)します。|  
|構成の状態 ダッシュ ボードのタイルは、警告またはエラーを示しています。|次の手順では、[リモート アクセス サーバーの構成配布のステータスを監視](https://technet.microsoft.com/library/jj574221(v=ws.11).aspx)します。|  
|(例では、負荷分散を有効にするか、追加またはクラスターからサーバーを削除するときに問題があるときに、構成は失敗) の負荷分散の構成に関連する発生した問題|負荷分散または、ノードの追加を有効にされた場合にクリックしたときに、構成が更新**適用**、サーバーで、次のコマンドを実行、クラスターが正しく形成しませんでしたが、: **cmd.exe/c"reg add hklm \SYSTEM\CurrentControlSet\Services\RaMgmtSvc\Parameters/f/v DebugFlag/t REG_DWORD/d""0 xffffffff"""** インターフェイスが、新しいサーバーでログをユーザーを収集します。|  
|操作の状況を示します、エラーまたは警告後、次の手順で、問題を解決するには|操作の状況が (などのエラーであっても後に修正) が正しくない情報を表示: 場合<br /><br />-   Enable the registry key **cmd.exe /c "reg add HKLM\SYSTEM\CurrentControlSet\Services\RaMgmtSvc\Parameters /f /v EnableTracing /t REG_DWORD /d ""5"" "** .<br />-操作の状態を更新して、ログの収集 **%windir%/tracing**します。|  
|Windows 8 およびそれ以降の DirectAccess クライアント コンピューターは、DirectAccess 接続のステータスとして"No Internet"を報告し、ネットワーク接続状態インジケーター (NCSI) が制限された接続を報告します。|これは、DirectAccess の構成で強制トンネリングが有効になっているし、このため、IPHTTPS のみが使用されているときに発生します。 この問題を解決するは、作成し、プロキシ サーバーを構成します。 NCSI は、このプロキシ サーバーを使用してインターネット接続の確認を実行します。 静的プロキシ名前解決ポリシー テーブル (NRPT) を使用して追加する、次の手順をお勧めします。<br /><br />この手順では、コマンドを実行する前に、展開に適切な値には、すべてのドメイン名、コンピューター名、およびその他の Windows PowerShell コマンドの変数を置き換えることを確認します。<br /><br />**静的プロキシ NRPT ルールを構成します。**<br />1. 表示、"."NRPT 規則: `Get-DnsClientNrptRule -GpoName "corp.example.com\DirectAccess Client Settings" -Server <DomainControllerNetBIOSName>`<br />2. 名前 (GUID) に注意してください、"."NRPT 規則です。 (GUID) という名の先頭に**DA - {0}.}**<br />3.プロキシを設定します"."NRPT 規則を**proxy.corp.example.com:8080**:  `Set-DnsClientNrptRule -Name "DA-{..}" -Server <DomainControllerNetBIOSName> -GPOName "corp.example.com\DirectAccess Client Settings" -DAProxyServerName "proxy.corp.example.com:8080" -DAProxyType "UseProxyName"`<br />4。表示、"."NRPT ルールを実行して、もう一度`Get-DnsClientNrptRule`、いることを確認および**ProxyFQDN:port**が正しく構成されました。<br />5。実行してグループ ポリシーを更新`gpupdate /force`DirectAccess クライアント、クライアントが内部的には、接続されている場合、表示 NRPT を使用して、`Get-DnsClientNrptPolicy`いることを確認し、"."ルールの表示**ProxyFQDN:port**します。|  
  


