---
title: DirectAccess のトラブルシューティング
description: このトピックでは、Windows Server 2016 での DirectAccess 展開のトラブルシューティングについて説明します。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: 61040e19-5960-4eb0-b612-d710627988f7
ms.author: lizross
author: eross-msft
ms.openlocfilehash: bfd7d67a84eb6f2af4c52d05f3dc7c69835ed743
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856245"
---
# <a name="troubleshooting-directaccess"></a>DirectAccess のトラブルシューティング

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

リモートアクセス (DirectAccess) の問題のトラブルシューティングを行うには、次の手順に従います。  
  
|||  
|-|-|  
|**問題**|**解決方法**|  
|リモートアクセス管理コンソールで DirectAccess 構成を表示できない|**不足している構成情報を復元するには**<br />-マルチサイト展開のトラブルシューティングを行う場合は、エントリポイントに最も近いドメインコントローラーが使用可能であることを確認します。<br />- **Set-daentrypointdc**コマンドレットを使用して、エントリポイントに最も近いドメインコントローラーの名前を取得します。 ドメインコントローラーが実行されていない場合は、 **set-daentrypointdc**コマンドレットを使用して別のドメインコントローラーを指定します。<br />-サーバーで管理者特権でのコマンドプロンプトから**gpresult**を実行し、サーバーが DirectAccess グループポリシーオブジェクトを取得していることを確認します。<br />-ユーザーインターフェイス (UI) のログ記録を有効にします。<br />-次のコマンドを使用して、Windows PowerShell ログを開始します。<pre>logman create trace ETWTrace -ow -o c:\ETWTrace.etl -p {AAD4C46D-56DE-4F98-BDA2-B5EAEBDD2B04} 0xffffffffffffffff 0xff -nb 16 16 -bs 1024 -mode 0x2 -max 2048 -ets <br />logman update trace ETWTrace -p {62DFF3DA-7513-4FCA-BC73-25B111FBB1DB} 0xffffffffffffffff 0xff -ets</pre><repro>-ユーザーインターフェイスを閉じてから再度開きます。<br />-Windows Powershell のログ記録を無効にします。 イベントトレースログファイルを収集します。 また、 **% windir%/トレース**フォルダーからすべてのログを収集します。|  
|DirectAccess 構成の適用に失敗する|**DirectAccess 構成を更新するには**<br />-マルチサイト展開のトラブルシューティングを行う場合は、エントリポイントに最も近いドメインコントローラーが使用可能であることを確認します。<br />- **Set-daentrypointdc**コマンドレットを使用して、エントリポイントに最も近いドメインコントローラーの名前を取得します。 ドメインコントローラーが実行されていない場合は、 **set-daentrypointdc**コマンドレットを使用して別のドメインコントローラーを指定します。<br />-次のコマンドを使用して、Windows Powershell ログを開始します。<br /><pre>logman create trace ETWTrace -ow -o c:\ETWTrace.etl -p {AAD4C46D-56DE-4F98-BDA2-B5EAEBDD2B04} 0xffffffffffffffff 0xff -nb 16 16 -bs 1024 -mode 0x2 -max 2048 -ets<br />logman update trace ETWTrace -p {62DFF3DA-7513-4FCA-BC73-25B111FBB1DB} 0xffffffffffffffff 0xff -ets</pre>    <repro><br />**[適用]** をクリックします。<br />-エラーが発生した後、Windows Powershell のログ記録を無効にし、イベントトレースログを収集します。|  
|DirectAccess は構成されていますが、クライアントが内部リソースに接続できません|**クライアント接続の問題のトラブルシューティングを行うには**<br />-リモートアクセス管理コンソールの **[操作の状態]** タブをクリックし、すべてのコンポーネントに緑色のアイコンが表示されていることを確認します。 それ以外の場合は、エラーの詳細を確認し、解決手順に従います。<br />-リモートアクセスサーバーベストプラクティスアナライザー (BPA) を実行します。 警告またはエラーが発生した場合は、解決手順に従って問題を解決します。|  
|マルチサイト構成に関連する問題の検出 (マルチサイトの有効化、エントリポイントの追加、エントリポイントのドメインコントローラーの設定など)|「[マルチサイト展開のトラブルシューティング](https://technet.microsoft.com/library/jj554657(v=ws.11).aspx)」の手順に従います。|  
|ダッシュボードの [構成の状態] タイルで警告またはエラーが表示される|「[リモートアクセスサーバーの構成配布ステータスを監視](https://technet.microsoft.com/library/jj574221(v=ws.11).aspx)する」の手順に従います。|  
|負荷分散の構成に関連する問題 (たとえば、負荷分散を有効にしたときに構成が失敗する、またはクラスターのサーバーを追加または削除するときに問題が発生する)|負荷分散を有効にした場合、または **[適用]** をクリックしたときに構成が更新され、クラスターがサーバー上で正しく形成されなかった場合は、 **cmd.exe/c "reg add HKLM\SYSTEM\CurrentControlSet\Services\RaMgmtSvc\Parameters/F/v debugflag/t REG_DWORD/d" "0xffffffff" ""** というコマンドを実行して、新しいサーバーのユーザーインターフェイスログを収集します。|  
|操作の状態は、次の手順を実行してエラーまたは警告を表示し、状況を修正します。|操作の状態に誤った情報 (修正後もエラーなど) が表示されている場合は、次のようになります。<p>-レジストリキー **cmd.exe/c "reg add HKLM\SYSTEM\CurrentControlSet\Services\RaMgmtSvc\Parameters/f/V EnableTracing/t REG_DWORD/d" "5" "** " を有効にします。<br />-操作の状態を更新し、 **% windir%/トレース**からログを収集します。|  
|Windows 8 以降の DirectAccess クライアントコンピューターは、DirectAccess 接続の状態として "No Internet" を報告し、ネットワーク接続状態インジケーター (NCSI) は限られた接続性を報告します。|これは、DirectAccess 構成で強制トンネリングが有効になっている場合に発生する可能性があります。そのため、IPHTTPS のみが使用されています。 この問題を解決するには、プロキシサーバーを作成して構成します。 次に、NCSI はプロキシサーバーを使用して、インターネット接続チェックを実行します。 次の手順に従って、名前解決ポリシーテーブル (NRPT) に静的プロキシを追加することをお勧めします。<p>この手順のコマンドを実行する前に、すべてのドメイン名、コンピューター名、およびその他の Windows PowerShell コマンド変数を、展開に適した値に置き換えてください。<p>**NRPT 規則の静的プロキシの構成**<br />1. "." を表示します。NRPT ルール: `Get-DnsClientNrptRule -GpoName "corp.example.com\DirectAccess Client Settings" -Server <DomainControllerNetBIOSName>`<br />2. "." の名前 (GUID) に注意してください。NRPT ルール。 名前 (GUID) は、 **DA-{..}** で始まる必要があります<br />3. "." にプロキシを設定します。NRPT ルールから**proxy.corp.example.com:8080**: `Set-DnsClientNrptRule -Name "DA-{..}" -Server <DomainControllerNetBIOSName> -GPOName "corp.example.com\DirectAccess Client Settings" -DAProxyServerName "proxy.corp.example.com:8080" -DAProxyType "UseProxyName"`<br />4. "." を表示します。`Get-DnsClientNrptRule`を実行し、 **Proxyfqdn: port**が正しく構成されていることを確認してから、NRPT ルールを再実行します。<br />5. クライアントが内部で接続されているときに DirectAccess クライアントで `gpupdate /force` を実行してグループポリシーを更新し、`Get-DnsClientNrptPolicy` を使用して NRPT を表示し、"." 規則に**Proxyfqdn: port**が表示されていることを確認します。|  
  


