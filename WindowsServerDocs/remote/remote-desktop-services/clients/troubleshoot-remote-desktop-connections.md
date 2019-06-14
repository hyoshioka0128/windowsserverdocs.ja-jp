---
title: リモート デスクトップ接続のトラブルシューティング
description: 現象ごとに配置され、トラブルシューティング手順
ms.custom: na
ms.reviewer: rklemen; josh.bender
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: troubleshooting
ms.assetid: ''
author: RobVyK
manager: ''
ms.author: kaushika; rklemen; josh.bender; v-tea
ms.date: 02/22/2019
ms.localizationpriority: medium
ms.openlocfilehash: 43e40f8442600dfc66dafd6b8b210274908b4595
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446722"
---
# <a name="troubleshooting-remote-desktop-connections"></a>リモート デスクトップ接続のトラブルシューティング
リモート デスクトップ サービス (RDS) の一般的な問題のいくつかの簡単な説明については、次を参照してください。 [、リモート デスクトップ クライアントについてよく寄せられる質問](https://review.docs.microsoft.com/en-us/windows-server/remote/remote-desktop-services/clients/remote-desktop-client-faq)します。 この記事では、接続の問題をトラブルシューティングするいくつかのより高度なアプローチについて説明します。 これらの手順の多くには、1 つの物理コンピューターが別の物理コンピューター、またはより複雑な構成への接続などの単純な構成のトラブルシューティングを行うかどうかが適用されます。 いくつかの手順より複雑なマルチ ユーザー シナリオでのみ発生する問題に対処します。 詳細については、リモート デスクトップ コンポーネントとどのように連動する、次を参照してください。[リモート デスクトップ サービスのアーキテクチャ](https://docs.microsoft.com/en-us/windows-server/remote/remote-desktop-services/desktop-hosting-logical-architecture)します。

> [!NOTE]  
> この記事で説明されている手順の多くは、リモートでアクセスする必要がありますうちいくつかの複数のコンピューターにアクセスすることが必要です。 リモート管理ツールとその構成方法の詳細については、次を参照してください。 [Windows オペレーティング システムのリモート サーバー管理ツール (RSAT)](https://support.microsoft.com/en-us/help/2693643/remote-server-administration-tools-rsat-for-windows-operating-systems)します。

次の一覧で、ユーザー (またはユーザー) が発生している現象の種類を特定します。

- [リモート デスクトップ クライアントがリモートのデスクトップに接続できませんが、具体的な現象やメッセージ (全般のトラブルシューティングの手順) はありません。](#no-specific-symptoms-or-messages-general-troubleshooting-steps)
- [リモート デスクトップ クライアントがリモートのデスクトップに接続できず、「クラスは登録されていません」のメッセージを受信](#client-cannot-connect-class-not-registered)
- [リモート デスクトップ クライアントは、リモートのデスクトップに接続できない送受信、「ライセンスはありません」または「セキュリティ エラー」メッセージ](#client-cannot-connect-no-licenses-available)
- [ユーザーは、「アクセス拒否」メッセージを受信または資格情報を 2 回指定する必要があります。](#user-cannot-authenticate-or-must-authenticate-twice)
- [に接続することで、「リモート デスクトップ サービスは現在ビジー状態」のメッセージを受信](#on-connecting-user-receives-remote-desktop-service-is-currently-busy-message)
- [リモート デスクトップ クライアントを切断し、同じセッションに再接続することはできません。](#rd-client-disconnects-and-cannot-reconnect-to-the-same-session)
- [ユーザーが、ワイヤレス ネットワーク経由でリモート ラップトップに接続して、ラップトップがネットワークから切断し、](#remote-laptop-disconnects-from-wireless-network)します。
- [ユーザー エクスペリエンスのパフォーマンスの低下やリモート アプリケーションの問題](#user-experiences-poor-performance-or-application-problems)

> [!NOTE]  
> 現在の RDP 接続解除のコードの一覧を表示するには、次を参照してください。 [ExtendedDisconnectReasonCode 列挙](https://docs.microsoft.com/en-us/windows/desktop/TermServ/extendeddisconnectreasoncode)します。 

## <a name="no-specific-symptoms-or-messages-general-troubleshooting-steps"></a>ない具体的な現象またはメッセージ (全般のトラブルシューティングの手順)

リモート デスクトップ クライアントは、リモート デスクトップに接続できませんが、メッセージまたは際に役立つその他の症状、原因を特定します。 は実現されない場合は、次の手順を使用します。 このような問題の最も一般的な原因の多くを解決するには、次のメソッドを使用します。

- [RDP プロトコルの状態を確認してください。](#check-the-status-of-the-rdp-protocol)
- [RDP サービスの状態を確認してください。](#check-the-status-of-the-rdp-services)
- [RDP リスナーが機能していることを確認します。](#check-that-the-rdp-listener-is-functioning)
- [RDP リスナー ポートを確認してください。](#check-the-rdp-listener-port)

### <a name="check-the-status-of-the-rdp-protocol"></a>RDP プロトコルの状態を確認してください。

#### <a name="check-the-status-of-the-rdp-protocol-on-a-local-computer"></a>ローカル コンピューター上の RDP プロトコルの状態を確認してください。

チェックし、ローカル コンピューター上の RDP プロトコルの状態を変更する、次を参照してください。[リモート デスクトップを有効にする方法](https://docs.microsoft.com/en-us/windows-server/remote/remote-desktop-services/clients/remote-desktop-allow-access#how-to-enable-remote-desktop)します。

> [!NOTE]  
> リモート デスクトップのオプションが利用できない場合を参照してください。 [、グループ ポリシー オブジェクトで RDP がブロックしているかどうかを確認](#check-whether-a-group-policy-object-gpo-is-blocking-rdp-on-a-local-computer)します。

#### <a name="check-the-status-of-the-rdp-protocol-on-a-remote-computer"></a>リモート コンピューターで RDP プロトコルの状態を確認してください。

> [!IMPORTANT]  
> 慎重にこのセクションの手順に従います。 誤ってレジストリを変更すると、重大な問題が発生する可能性があります。 変更する前に[復元するためのレジストリをバックアップする](https://support.microsoft.com/en-us/help/322756%22%20target=%22_self%22)問題が発生した場合。

確認して、リモート コンピューターで RDP プロトコルの状態の変更、レジストリのネットワーク接続を使用します。

1. 選択**開始**を選択します**実行**、し、入力**regedt32**します。
2. レジストリ エディターで、選択**ファイル**、し、**ネットワーク レジストリへの接続**します。
3. **コンピューターの選択**] ダイアログ ボックスをリモート コンピューターの名前を入力し、選択**名前の確認**、し、[ **OK**。
4. 移動します**HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\ターミナル サーバー**します。  
   ![レジストリ エディター、fDenyTSConnections エントリを表示](../media/troubleshoot-remote-desktop-connections/RegEntry_fDenyTSConnections.png)
   - 場合の値、 **fDenyTSConnections**キーが**0**RDP を有効にし、
   - 場合の値、 **fDenyTSConnections**キーが**1**RDP は無効です
5. RDP を有効にするには、値を変更**fDenyTSConnections**から**1**に**0**します。

#### <a name="check-whether-a-group-policy-object-gpo-is-blocking-rdp-on-a-local-computer"></a>グループ ポリシー オブジェクト (GPO) に、ローカル コンピューターで RDP がブロックしているかどうかを確認します。

ユーザー インターフェイスの RDP を有効にできない場合、または場合の値**fDenyTSConnections**に戻ります**1**それを変更した後 GPO がコンピューター レベルの設定をオーバーライドする可能性があります。

ローカル コンピューターのグループ ポリシーの構成を確認するには、管理者は、コマンド プロンプト ウィンドウを開き、次のコマンドを入力します。
```
gpresult /H c:\gpresult.html
```
このコマンドの終了後、gpresult.html を開きます。 **コンピューターの構成\\管理用テンプレート\\Windows コンポーネント\\リモート デスクトップ サービス\\リモート デスクトップ セッション ホスト\\接続**、検索、**にリモート デスクトップ サービスを使用してリモートで接続できるように**ポリシー。

- このポリシー設定がある場合**有効**、グループ ポリシーが RDP 接続をブロックしていません。
- このポリシー設定がある場合**無効**、確認**優勢な GPO**します。 これは、RDP 接続をブロックしている GPO です。
  ![例のセグメントを gpresult.html のドメイン レベルの GPO * * ブロック RDP * * が RDP 無効にします。](../media/troubleshoot-remote-desktop-connections/GPResult_RDSH_Connections_GP.png)
   
  ![例のセグメントを gpresult.html の * * ローカル グループ ポリシー * * が RDP 無効にします。](../media/troubleshoot-remote-desktop-connections/GPResult_RDSH_Connections_LGP.png)

#### <a name="check-whether-a-gpo-is-blocking-rdp-on-a-remote-computer"></a>GPO にリモート コンピューターで RDP がブロックしているかどうかを確認します。

リモート コンピューターのグループ ポリシーの構成を確認するには、コマンドは、ローカル コンピューターの場合とほぼ同じです。
```
gpresult /S <computer name> /H c:\gpresult-<computer name>.html
```
このコマンドを生成するファイル (**gpresult -\<コンピューター名\>.html**) ローカル コンピューターのバージョンと同じ情報の形式を使用して (**gpresult.html**) を使用します。

#### <a name="modifying-a-blocking-gpo"></a>ブロックしている GPO の変更

グループ ポリシー オブジェクト エディター (GPE) およびグループ ポリシー管理コンソール (GPM) でこれらの設定を変更することができます。 グループ ポリシーを使用する方法の詳細については、次を参照してください。 [Advanced Group Policy Management](https://docs.microsoft.com/en-us/microsoft-desktop-optimization-pack/agpm/)します。

ブロックのポリシーを変更するには、するには、次のメソッドのいずれかを使用します。

- GPE、GPO の (ローカルまたはドメイン) などの適切なレベルにアクセスしに移動します**コンピューターの構成\\管理用テンプレート\\Windows コンポーネント\\Remote Desktop Services\\リモート デスクトップ セッション ホスト\\接続**\\**にリモート デスクトップ サービスを使用してリモートで接続できるように**します。  
   1. ポリシーを設定**有効**または**未構成**します。
   2. 影響を受けたコンピューターで、管理者としてコマンド プロンプト ウィンドウを開き実行して、 **gpupdate/force**コマンド。
- GPM では、影響を受けるコンピューターに、ブロックするポリシーを適用する OU に移動し、OU からポリシーを削除します。

### <a name="check-the-status-of-the-rdp-services"></a>RDP サービスの状態を確認してください。

ローカル (クライアント) コンピューターとリモート (対象) コンピューターの両方では、次のサービスが実行されている必要があります。

- リモート デスクトップ サービス (TermService)
- Remote Desktop Services UserMode Port リダイレクター (UmRdpService)

サービス MMC スナップインを使用すると、ローカルまたはリモート サービスを管理します。 ローカルまたはリモートに、PowerShell を使用することもできます (かどうか、リモート コンピューターが構成されているリモートの PowerShell コマンドも受け入れるように)。

![サービス MMC スナップインでリモート デスクトップ サービス。 既定のサービス設定を変更しないでください。](../media/troubleshoot-remote-desktop-connections/RDSServiceStatus.png)

一方のコンピューターで 1 つまたは両方のサービスが実行されていない場合開始します。

> [!NOTE]  
> リモート デスクトップ サービスのサービスを開始する場合にクリックします**はい**リモート デスクトップ サービスのユーザー モード ポート リダイレクター サービスを自動的に再起動します。

### <a name="check-that-the-rdp-listener-is-functioning"></a>RDP リスナーが機能していることを確認します。

> [!IMPORTANT]  
> 慎重にこのセクションの手順に従います。 誤ってレジストリを変更すると、重大な問題が発生する可能性があります。 変更する前に[復元するためのレジストリをバックアップする](https://support.microsoft.com/en-us/help/322756%22%20target=%22_self%22)問題が発生した場合。

#### <a name="check-the-status-of-the-rdp-listener"></a>RDP リスナーの状態を確認してください。

この手順では、管理権限を持つ PowerShell インスタンスを使用します。 ローカルのコンピューターの管理権限を持つコマンド プロンプトを使用することもできます。 ただし、この手順は、ローカルとリモートの両方と同じコマンド動作するために PowerShell を使用します。

1. PowerShell ウィンドウを開きます。 リモート コンピューターに接続するには、入力**Enter-pssession-ComputerName\<コンピューター名\>** します。
2. 入力**qwinsta**します。 
    ![Qwinsta コマンドは、コンピューターのポートでリッスンしているプロセスを一覧表示します。](../media/troubleshoot-remote-desktop-connections/WPS_qwinsta.png)
3. リストが含まれている場合**rdp tcp**の状態で**リッスン**、RDP リスナーが動作します。 続行する[RDP リスナー ポートを確認](#check-the-rdp-listener-port)します。 手順 4 に進んでください。
4. 動作中のコンピューターから RDP リスナーの構成をエクスポートします。
    1. 影響を受けるコンピューターは、同じバージョンのオペレーティング システムがあるコンピューターにサインインし、(たとえば、レジストリ エディターを使用) をそのコンピューターのレジストリにアクセスします。
    2. 次のレジストリ エントリに移動します。  
        **HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\ターミナル サーバー\\WinStations\\RDP Tcp**
    3. エントリを .reg ファイルにエクスポートします。 たとえば、レジストリ エディターで、エントリを右クリックして、選択**エクスポート**、エクスポートした設定のファイル名を入力します。
    4. 影響を受けるコンピューターにエクスポートした .reg ファイルをコピーします。
5. RDP リスナーの構成をインポートするには、影響を受けるコンピューターの管理アクセス許可がある (または PowerShell ウィンドウを開くおよび影響を受けるコンピューターにリモート接続する) を PowerShell ウィンドウを開きます。
   1. 既存のレジストリ エントリをバックアップするには、次のコマンドを入力します。  
   
      ```powershell  
      cmd /c 'reg export "HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-tcp" C:\Rdp-tcp-backup.reg'   
      ```  
   

   2. 既存のレジストリ エントリを削除するには、次のコマンドを入力します。  
   
      ```powershell  
      Remove-Item -path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-tcp' -Recurse -Force  
      ```
   
   3. 新しいレジストリ エントリをインポートすると、サービスを再起動して、次のコマンドを入力します。  
   
      ```powershell  
      cmd /c 'regedit /s c:\<filename>.reg'  
      Restart-Service TermService -Force  
      ```   
      場所\<filename\>エクスポートした .reg ファイルの名前を指定します。
6. リモート デスクトップ接続をもう一度試行することで、構成をテストします。 それでも接続できない場合は、影響を受けるコンピューターを再起動します。
7. それでも接続できない場合[RDP の自己署名証明書の状態を確認](#check-the-status-of-the-rdp-self-signed-certificate)します。

#### <a name="check-the-status-of-the-rdp-self-signed-certificate"></a>RDP の自己署名証明書の状態を確認してください。

1. それでも接続できない場合、証明書 MMC スナップインを開きます。 管理、選択するには、証明書ストアを選択するメッセージが表示されたら**コンピューター アカウント**、該当するコンピューターを選択します。
2. **証明書**の下のフォルダー**リモート デスクトップ**RDP の自己署名証明書を削除します。 
    ![MMC 証明書スナップインでリモート デスクトップ証明書。](../media/troubleshoot-remote-desktop-connections/MMCCert_Delete.png)
3. 対象のコンピューターで、リモート デスクトップ サービスのサービスを再起動します。
4. 証明書スナップインを更新します。
5. RDP の自己署名証明書が再作成されていない場合[MachineKeys フォルダーのアクセス許可を確認](#check-the-permissions-of-the-machinekeys-folder)します。

#### <a name="check-the-permissions-of-the-machinekeys-folder"></a>MachineKeys フォルダーのアクセス許可を確認します。

1. 影響を受けるコンピューターでは、エクスプ ローラーを開きに移動します**c:\\ProgramData\\Microsoft\\Crypto\\RSA\\** します。
2. 右クリック**MachineKeys**を選択します**プロパティ**を選択します**セキュリティ**、し、**詳細**します。
3. 次のアクセス許可が構成されていることを確認します。
      - Builtin\\管理者。フル コントロール
      - すべてのユーザー:読み取り、書き込み

### <a name="check-the-rdp-listener-port"></a>RDP リスナー ポートを確認してください。

ローカル (クライアント) コンピューターとリモート (対象) コンピューターの両方では、ポート 3389 で RDP リスナーをリッスンする必要があります。 他のアプリケーションする必要がありますいないこのポートを使用します。

> [!IMPORTANT]  
> 慎重にこのセクションの手順に従います。 誤ってレジストリを変更すると、重大な問題が発生する可能性があります。 変更する前に[復元するためのレジストリをバックアップする](https://support.microsoft.com/en-us/help/322756%22%20target=%22_self%22)問題が発生した場合。

RDP ポートを変更、または確認するには、レジストリ エディターを使用します。

1. 開始を選択して、**実行**、し、入力**regedt32**します。
      - リモート コンピューターに接続するには、選択**ファイル**、し、**ネットワーク レジストリへの接続**します。
      - **コンピューターの選択**] ダイアログ ボックスをリモート コンピューターの名前を入力し、選択**名前の確認**、し、[ **OK**。
2. レジストリを開きに移動します**HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\ターミナル サーバー\\WinStations\\\<リスナー\>** します。 
    ![PortNumber のサブキーを RDP プロトコル。](../media/troubleshoot-remote-desktop-connections/RegEntry_PortNumber.png)
3. 場合**PortNumber**以外の値を持つ**3389**に変更して**3389**します。 
   > [!IMPORTANT]  
    > 別のポートを使用してリモート デスクトップ サービスを運用することができます。 ただし、このようにすることはお勧めできません。 このような構成のトラブルシューティングは、この記事の範囲外です。
4. ポート番号を変更した後、リモート デスクトップ サービスのサービスを再起動します。

#### <a name="check-that-another-application-is-not-trying-to-use-the-same-port"></a>別のアプリケーションが同じポートを使用するとしていないことを確認します。

この手順では、管理権限を持つ PowerShell インスタンスを使用します。 ローカルのコンピューターの管理権限を持つコマンド プロンプトを使用することもできます。 ただし、この手順は、同じコマンド、機能のローカルとリモートのために PowerShell を使用します。

1. PowerShell ウィンドウを開きます。 リモート コンピューターに接続するには、入力**Enter-pssession-ComputerName\<コンピューター名\>** します。
2. 次のコマンドを入力します。  
   
     ```powershell  
    cmd /c 'netstat -ano | find "3389"'  
    ```
  
    ![Netstat コマンドは、ポートとそれらをリッスンするサービスの一覧を生成します。](../media/troubleshoot-remote-desktop-connections/WPS_netstat.png)
3. 3. 状態が「**LISTENING**」の TCP ポート 3389 (または割り当てられた RDP ポート) のエントリを探します。 
    > [!NOTE]  
   > そのポートを使用しているプロセスまたはサービスの PID (プロセス ID) が [PID] 列の下に表示されます。
4. をどのアプリケーションがポート 3389 (または割り当てられている RDP ポート) を使用して確認するのには、次のコマンドを入力します。  
   
     ```powershell  
    cmd /c 'tasklist /svc | find "<pid listening on 3389>"'  
    ```  
  
    ![Tasklist コマンドでは、特定のプロセスの詳細を報告します。](../media/troubleshoot-remote-desktop-connections/WPS_tasklist.png)
5. ポートに関連付けられている PID 番号のエントリを探します (から、 **netstat**出力)。 サービスまたはその PID に関連付けられているプロセスが右側に表示します。
6. アプリケーションまたはリモート デスクトップ サービス (TermServ.exe) 以外のサービスは、ポートで使用されている場合は、次のメソッドのいずれかを使用して競合を解決できます。
      - その他のアプリケーションまたはサービス別のポート (推奨) を使用するを構成します。
      - その他のアプリケーションまたはサービスをアンインストールします。
      - 別のポートを使用する RDP を構成し、(推奨されません)、リモート デスクトップ サービスのサービスを再起動します。

#### <a name="check-whether-a-firewall-is-blocking-the-rdp-port"></a>ファイアウォールで RDP ポートがブロックしているかどうかを確認します。

使用して、 **psping**ポート 3389 を使用して、該当するコンピューターに到達できるかどうかをテストするためのツール。

1. 影響を受けるコンピューターとは異なるコンピューターでダウンロード**psping**から<https://live.sysinternals.com/psping.exe>します。
2. 管理者としてコマンド プロンプト ウィンドウを開き、インストールしたディレクトリに変更**psping**、次のコマンドを入力します。  
   
   ```  
   psping -accepteula <computer IP>:3389  
   ```
   
3. 出力を確認、 **psping**結果、次のコマンド。  
      - **接続する\<コンピューターの IP\>** :リモート コンピューターに到達します。
      - **(0 %loss)** :すべての接続試行が成功しました。
      - **リモート コンピューターには、ネットワーク接続が拒否された**:リモート コンピューターに到達できません。
      - **(損失が 100%)** :すべての接続試行が失敗しました。
1. 実行**psping**影響を受けるコンピューターに接続するには、その機能をテストする複数のコンピューターにします。
1. 影響を受けるコンピューターが他のすべてのコンピューター、他のコンピューターまたはその他の 1 つだけのコンピューターからの接続をブロックするかどうかに注意してください。
1. 次の手順をお勧めします。
      - ネットワークが影響を受けるコンピューターへの RDP トラフィックを許可することを確認する、ネットワーク管理者に情報交換できます。
      - ファイアウォールで RDP ポートがブロックしているかどうかを判断するには、移行元コンピューターと、該当するコンピューター (該当するコンピューターに Windows ファイアウォールを含む) 間のファイアウォールの構成を調べます。

## <a name="client-cannot-connect-class-not-registered"></a>クライアントが接続できない「クラスが登録されていません」

Windows 10 バージョン 1709 を実行しているクライアントを使用してリモート コンピューターに接続しようとすると、後で、クライアント接続できないリモート デスクトップ セッション ホスト サーバーがメッセージをレポート中には、「クラスが登録されていません (0x80040154)」エラー コードが含まれています。

この問題は、接続しようとしたユーザーが固定ユーザー プロファイルを持っている場合に発生します。 この問題を解決するには、インストール、 [2018 年 7 月 24 日 — KB4338817 (OS ビルド 16299.579)](https://support.microsoft.com/en-us/help/4338817/windows-10-update-kb4338817) Windows 10 更新プログラム。

## <a name="client-cannot-connect-no-licenses-available"></a>クライアントが接続できない、使用可能なライセンスがないです。

このような状況は、RDSH サーバーとリモート デスクトップ ライセンス サーバーを含む展開に適用されます。

どのような動作が発生しているユーザーを識別します。

- 使用可能なライセンスがないか、ライセンス サーバーが使用できないため、セッションが切断されました
- セキュリティ エラーのためのアクセスが拒否されました

ドメイン管理者として RD セッション ホストにサインインし、RD ライセンス診断ツールを開きます。 メッセージは、次のようになります。

  - 猶予期間、リモート デスクトップ セッション ホスト サーバーの有効期限が切れてが、ライセンス サーバーに RD セッション ホスト サーバーが構成されていません。 RD セッション ホスト サーバー ライセンス サーバーが構成されていなければ、RD セッション ホスト サーバーへの接続は拒否されます。
  - ライセンス サーバー\<コンピューター名\>は使用できません。 これは、ネットワーク接続の問題によって発生する可能性があります、ライセンス サーバーのリモート デスクトップ ライセンス サービスが停止または RD ライセンスは、コンピューターにインストールが不要になった。

これらの問題は、次のユーザー メッセージに関連する傾向があります。

  - このコンピューターのリモート デスクトップ クライアント アクセス ライセンスがないために、リモート セッションは切断されました。
  - リモート デスクトップ ライセンスを提供するサーバー ライセンスがないために、リモート セッションは切断されました。

この場合、 [RD ライセンス サービスを構成する](#configure-the-rd-licensing-service)します。

RD ライセンス診断ツールなど、「RDP プロトコル コンポーネント X.224 プロトコル ストリームにエラーが検出し、クライアントが切断されました」がある可能性があります、その他の問題を一覧表示する場合、ライセンスの証明書に影響を与える問題があります。 このような問題は、次のように、ユーザー メッセージに関連する傾向があります。

セキュリティ エラーのため、クライアントは、ターミナル サーバーに接続できませんでした。 ネットワークにログオンしていることを確認したら、サーバーへの接続をもう一度お試しください。

この場合、[更新 X509 証明書のレジストリ キー](#refresh-the-x509-certificate-registry-keys)します。

### <a name="configure-the-rd-licensing-service"></a>RD ライセンス サービスを構成します。

次の手順では、サーバー マネージャーを使用して、構成を変更します。 構成して、サーバー マネージャーを使用する方法については、次を参照してください。[サーバー マネージャー](https://docs.microsoft.com/en-us/windows-server/administration/server-manager/server-manager)します。

1. サーバー マネージャーを開きに移動し、 **Remote Desktop Services**します。
2. **展開の概要**を選択します**タスク**、し、**展開のプロパティの編集**します。
3. 選択**RD ライセンス**、展開に適切なライセンス モードを選択します (**デバイスあたり**または**ユーザーごと**)。
4. RD ライセンス サーバーの完全修飾ドメイン名 (FQDN) を入力し、**追加**します。
5. 1 つ以上の RD ライセンス サーバーがある場合は、サーバーごとに手順 4. を繰り返します。 
    ![RD ライセンス サーバー構成オプションでサーバー マネージャー。](../media/troubleshoot-remote-desktop-connections/RDLicensing_Configure.png)

### <a name="refresh-the-x509-certificate-registry-keys"></a>更新、X509 証明書のレジストリ キー

> [!IMPORTANT]  
> 慎重にこのセクションの手順に従います。 誤ってレジストリを変更すると、重大な問題が発生する可能性があります。 変更する前に[復元するためのレジストリをバックアップする](https://support.microsoft.com/en-us/help/322756%22%20target=%22_self%22)問題が発生した場合。

この問題を解決するには、バックアップし、削除、X509 証明書のレジストリ キー、コンピューター、および、再アクティブ化する、RD ライセンス サーバーを再起動します。 これを行うには、次の手順に従います。

> [!NOTE]  
> RDSH サーバーごとに、次の手順を実行します。

1. レジストリ エディターを開きに移動します**HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\ターミナル サーバー\\RCM**.
2. [レジストリ] メニューで、次のように選択します。**レジストリ ファイルのエクスポート**します。
3. 型**証明書のエクスポート**で、**ファイル名**ボックスを選び**保存**します。
4. Select の次の値をそれぞれ右クリック**削除**、し、**はい**削除を確認します。  
      - **Certificate**
      - **X509 Certificate**
      - **X509 Certificate ID**
      - **X509 Certificate2**
5. レジストリ エディターを終了し、RDSH サーバーを再起動します。

## <a name="user-cannot-authenticate-or-must-authenticate-twice"></a>ユーザーが認証されない、または 2 回認証する必要があります。

ユーザーの認証に影響する問題を引き起こす可能性のあるいくつかの問題があります。 このセクションでは、次の場合を取り上げます。

  - [ユーザーには、「ログオンの種類の制限」のメッセージを使用したアクセスが拒否されました](#access-denied-restricted-type-of-logon)
  - [ユーザーまたはアプリケーションには、イベント 16965 によるアクセスが拒否された、「SAM データベースへのリモート呼び出しが拒否されました」](#access-denied-a-remote-call-to-the-sam-database-has-been-denied)
  - [ユーザーはスマート カードを使用してサインインすることはできません。](#a-user-cannot-sign-in-by-using-a-smart-card)
  - [ユーザーがパスワードを 2 回入力する必要があるリモート PC がロックされている場合](#if-the-remote-pc-is-locked-a-user-needs-to-enter-a-password-twice)
  - [ユーザーがサインインできないし、「認証エラー」と「CredSSP 暗号化 oracle 修復」メッセージを受信](#user-cannot-sign-in-and-receives-authentication-error-and-credssp-encryption-oracle-remediation-messages)
  - [一部のユーザーが 2 回サインインする必要があるクライアント コンピューターを更新した後](#after-you-update-client-computers-some-users-need-to-sign-in-twice)します。
  - [ユーザーには、RemoteGuard を複数の RD 接続ブローカーを使用している展開のアクセスが拒否されました。](#users-are-denied-access-on-a-deployment-that-uses-remote-credential-guard-with-multiple-rd-connection-brokers)

### <a name="access-denied-restricted-type-of-logon"></a>アクセスが拒否されると、ログオンの制限付きの型

このような状況では、Windows 10 または Windows Server 2016 のコンピューターに接続しようとしています。 Windows 10 のユーザーには、次のメッセージを使用したアクセスが拒否されます。

> リモート デスクトップ接続:  
> システム管理者には、ログオンの種類が制限されている (ネットワークまたは対話型) を使用することがあります。 詳細については、システム管理者またはテクニカル サポートにお問い合わせください。

この問題は、ネットワーク レベル認証 (NLA) が、RDP 接続に必要で、ユーザーのメンバーでない場合に発生します。、 **Remote Desktop Users**グループ。 場合にも発生、 **Remote Desktop Users**にグループが割り当てられていない、**ネットワークからこのコンピューターにアクセス**ユーザー権限。

この問題を解決するには、手順のいずれかの手順に従います。

  - [ユーザーのグループ メンバーシップまたはユーザー権利の割り当て変更](#modify-the-users-group-membership-or-user-rights-assignment)します。
  - (非推奨) NLA オフにします。
  - Windows 10 以外のリモート デスクトップ クライアントを使用します。 たとえば、Windows 7 クライアントには、この問題はありません。

#### <a name="modify-the-users-group-membership-or-user-rights-assignment"></a>ユーザーのグループ メンバーシップまたはユーザー権利の割り当てを変更します。

この問題を最も簡単なソリューションがユーザーを追加するにはこの問題は、1 人のユーザーに影響する場合、 **Remote Desktop Users**グループ。

ユーザーがこのグループのメンバー (または複数のグループ メンバーに同じ問題があるかどうか) で既に場合は、リモートの Windows 10 または Windows Server 2016 のコンピューター上のユーザー権利の構成を確認します。

1. グループ ポリシー オブジェクト エディター (GPE) を開き、リモート コンピューターのローカル ポリシーに接続します。
2. 移動します**コンピューターの構成\\Windows 設定\\セキュリティ設定\\ローカル ポリシー\\ユーザー権利の割り当て**、右クリックして**このオプションを表示コンピューターをネットワークから**、し、**プロパティ**します。
3. ユーザーとグループの一覧を確認**Remote Desktop Users** (または親グループ)。
4. リストが含まれていない場合**Remote Desktop Users** (または親グループなど、 **Everyone**) 一覧に追加する必要があります (を展開に 1 つまたは 2 つのコンピューターがある場合は、グループ ポリシー オブジェクトを使用).  
    既定のメンバーシップなど**ネットワークからこのコンピューターにアクセス**が含まれています**Everyone**します。 かどうか、デプロイを使用してグループ ポリシー オブジェクトを削除**Everyone**、追加するグループ ポリシー オブジェクトを更新することでアクセスを復元する必要があります**Remote Desktop Users**します。

### <a name="access-denied-a-remote-call-to-the-sam-database-has-been-denied"></a>アクセスが拒否されました、SAM データベースへのリモート呼び出しが拒否されました

この動作は、最も 2016 以降、ドメイン コント ローラーが Windows Server を実行している、ユーザーがカスタマイズされた接続アプリを使用して接続しようとする場合に発生する可能性があります。 具体的には、Active Directory のユーザーのプロファイル情報にアクセスするアプリケーションには、アクセスが拒否されます。

この動作は、Windows に変更を結果します。 およびそれ以前では、Windows Server 2012 R2 バージョンでは、ユーザーがログオン リモート デスクトップ、リモート接続マネージャー (RCM) 連絡先に、ドメイン コント ローラー (DC) は、Active Directory ドメイン内のユーザー オブジェクトでは、リモート デスクトップに固有の構成を照会するにはサービス (AD DS)。 この情報は、Active Directory ユーザーとコンピューター MMC スナップインで、ユーザーのオブジェクトのプロパティの [リモート デスクトップ サービスのプロファイル] タブに表示されます。

Windows Server 2016 以降、RCM は不要になった、AD DS のユーザー オブジェクトを照会します。 リモート デスクトップ サービスの属性を使用しているため、AD DS を照会する RCM を必要とする場合、以前の RCM 動作を手動で有効にする必要があります。

> [!IMPORTANT]  
> 慎重にこのセクションの手順に従います。 誤ってレジストリを変更すると、重大な問題が発生する可能性があります。 変更する前に[復元するためのレジストリをバックアップする](https://support.microsoft.com/en-us/help/322756%22%20target=%22_self%22)問題が発生した場合。

RD セッション ホスト サーバー上の従来の RCM 動作を有効にする、次のレジストリ エントリを構成し、再起動、 **Remote Desktop Services**サービス。  
  - **HKEY\_ローカル\_マシン\\ソフトウェア\\ポリシー\\Microsoft\\Windows NT\\ターミナル サービス**
  - **HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\ターミナル サーバー\\WinStations\\\<Winstation 名\>\\**  
      - Name: **fQueryUserConfigFromDC**
      - タイプ: **Reg\_DWORD**
      - 値:**1** (10 進数)

RD セッション ホスト サーバー以外のサーバーでは、従来の RCM 動作を有効にするには、これらのレジストリ エントリと、次の追加のレジストリ エントリを構成する (およびサービスを再起動して)。
  - **HKEY\_ローカル\_マシン\\システム\\CurrentControlSet\\コントロール\\ターミナル サーバー**

この動作の詳細については、KB 3200967 を参照してください。 [in Windows Server にリモート接続マネージャーを変更](https://support.microsoft.com/en-us/help/3200967/changes-to-remote-connection-manager-in-windows-server)します。

### <a name="a-user-cannot-sign-in-by-using-a-smart-card"></a>ユーザーはスマート カードを使用してサインインすることはできません。

この記事では、次の 3 つの一般的な状況をユーザーにサインインできないリモート デスクトップ、スマート カードを使用して、扱います。  
  - [ユーザーは、読み取り専用ドメイン コント ローラー (RODC) を使用するブランチ オフィスにサインインできません。](#cannot-sign-in-with-a-smart-card-in-a-branch-office-with-a-rodc)
  - [ユーザーが最近更新されている Windows Server 2008 SP2 コンピューターにサインインできません。](#cannot-sign-in-with-a-smart-card-to-a-windows-server-2008-sp2-computer)
  - [ユーザーが最近更新されている Windows コンピューターにサインインしている維持できないし、リモート デスクトップ サービスのサービスが応答しない (ハング)](#cannot-stay-signed-in-with-a-smart-card-and-remote-desktop-services-service-hangs)

#### <a name="cannot-sign-in-with-a-smart-card-in-a-branch-office-with-a-rodc"></a>RODC のブランチ オフィス内のスマート カードがサインインすることはできません。

この問題は、RODC を使用する支社サイトを RDSH サーバーを含む展開で発生します。 RDSH サーバーは、ルート ドメインでホストされます。 ブランチ サイトのユーザーは、子ドメインに属しているし、スマート カード認証を使用します。 ユーザー パスワードのキャッシュ、RODC が構成されている (、RODC が属する、 **RODC Password Replication グループの許可**)。 "ログオンの試行が無効ですなど、メッセージを受信したユーザーは、RDSH サーバー上のセッションにサインインするときに。 これは、悪意のあるユーザー名または認証情報が原因です。"

これは、方法は、既知の問題をルート DC し、RODC は、ユーザーの資格情報の暗号化を管理します。 ルート DC は、暗号化キーを使用して、資格情報を暗号化して、RODC が復号化キーをクライアントに提供します。 ただし、2 つのキーが一致しません。

この問題を回避するには、パスワードが RODC にキャッシュを無効にすることで、またはブランチ サイトに書き込み可能 DC をデプロイすることで、DC トポロジの変更を検討します。 別の方法では、ユーザーと同じ子ドメインに RDSH サーバーを移動します。 別の方法では、スマート カードを使用せずにサインインできるようにします。 これらのソリューションには、パフォーマンスまたはレベルのセキュリティ侵害が必要です。

#### <a name="cannot-sign-in-with-a-smart-card-to-a-windows-server-2008-sp2-computer"></a>Windows Server 2008 SP2 のコンピューターにスマート カードがサインインすることはできません。

この問題は、KB4093227 で更新されている Windows Server 2008 SP2 コンピューターにサインインするときに発生します。 (2018.4B)。 ユーザーがスマート カードを使用してサインインしようとすると、"しない有効な証明書が見つかりませんなどのメッセージを使用したアクセスが拒否されました。 確認、カードが正しく挿入して、しっかり。" 同時に、Windows Server コンピューター イベントを記録アプリケーション"挿入されたスマート カードからデジタル証明書を取得中にエラーが発生しました。 無効な署名します。"

この問題を解決するには、2018.06 B の再リリース KB 4093227 での Windows Server コンピューターの更新[サービスの脆弱性を Windows Server 2008 での Windows リモート デスクトップ プロトコル (RDP) の拒否のセキュリティ更新プログラムの説明。2018 年 4 月 10 日](https://support.microsoft.com/en-us/help/4093227/security-update-for-vulnerabilities-in-windows-server-2008)します。

#### <a name="cannot-stay-signed-in-with-a-smart-card-and-remote-desktop-services-service-hangs"></a>スマート カードとリモート デスクトップ サービスのサービスが停止するを使用してサインインしたままことはできません。

この問題は、KB 4056446 で更新されている Windows または Windows Server コンピューターにサインインするときに発生します。 最初は、ユーザーは、スマート カードを使用して、システムにサインインすることができますが、受信し、"s カード\_E\_いいえ\_サービス"のエラー メッセージ。 リモート コンピューターが応答しなくなる可能性があります。

この問題を回避するには、リモート コンピューターを再起動します。

この問題を解決するには、適切な修正プログラムと、リモート コンピューターを更新します。

  - Windows Server 2008 SP2 の場合:KB 4090928、 [Windows lsm.exe プロセスのハンドルのリークが発生し、スマート カード アプリケーションを表示可能性があります"s カード\_E\_いいえ\_サービス"エラー](https://support.microsoft.com/en-us/help/4090928/scard-e-no-service-errors-when-windows-leaks-handles-in-the-lsm-exe)
  - Windows Server 2012 R2KB 4103724、 [、2018 年 5 月 17日: KB4103724 (月単位のロールアップのプレビュー)](https://support.microsoft.com/en-us/help/4103724/windows-81-update-kb4103724)
  - Windows Server 2016 および Windows 10 バージョン 1607:KB 4103720、 [、2018 年 5 月 17日: KB4103720 (OS ビルド 14393.2273)](https://support.microsoft.com/en-us/help/4103720/windows-10-update-kb4103720)

### <a name="if-the-remote-pc-is-locked-a-user-needs-to-enter-a-password-twice"></a>ユーザーがパスワードを 2 回入力する必要があるリモート PC がロックされている場合

この問題は、ユーザーが NLA は RDP 接続に必要ない展開で Windows 10 バージョン 1709 を実行しているリモート デスクトップに接続しようとしたときに発生する可能性があります。 これらの条件下で、リモート デスクトップがロックされている場合は、ユーザー必要がありますに接続するときに 2 回、自分の資格情報を入力します。

この問題を解決するには、サポート技術情報の 4343893 で Windows 10 バージョン 1709 のコンピューターを更新[、2018 年 8 月 30 日-KB4343893 (OS ビルド 16299.637)](https://support.microsoft.com/en-us/help/4343893/windows-10-update-kb4343893)します。

### <a name="user-cannot-sign-in-and-receives-authentication-error-and-credssp-encryption-oracle-remediation-messages"></a>ユーザーがサインインできないし、「認証エラー」と「CredSSP 暗号化 oracle 修復」メッセージを受信

ユーザーは、任意のバージョンの Windows Vista SP2 と以降のバージョンまたは Windows Server 2008 SP2 から Windows と以降のバージョンを使用してサインインするときに、これらアクセスが拒否され、次のメッセージを受信します。

  - 認証エラーが発生しました。 要求された関数がサポートされていません。
  - CredSSP 暗号化 oracle 改善策が考えられます

「CredSSP 暗号化 oracle 修復」は、3 月、年 4 月、および 2018 年 5 月にリリースされたセキュリティ更新プログラムのセットを指します。 CredSSP は、他のアプリケーションの認証要求を処理する認証プロバイダーです。 攻撃者が、ターゲット システムにコードを実行するユーザーの資格情報を中継でした悪用を 13、2018 年 3 月"3 b"と後続の更新に対応できます。

最初の更新プログラムには、新しいグループ ポリシー オブジェクトでは、サポートが追加されました。**暗号化 Oracle 修復**、を持つ、次の可能な設定。

  - **脆弱性のある**します。 CredSSP を使用するクライアント アプリケーションが安全でないバージョンに戻るにことができますが、この動作は、攻撃に対するリモート デスクトップを公開します。 CredSSP を使用するサービスには、更新されていないクライアントがそのまま使用します。
  - **軽減**します。 CredSSP を使用するクライアント アプリケーションが安全でないバージョンに戻るにことはできませんが、CredSSP を使用するサービスが更新されていないクライアントをそのまま使用します。
  - **強制クライアントを更新する**します。 CredSSP を使用するクライアント アプリケーションが安全でないバージョンに戻るにことはできませんし、CredSSP を使用するサービスには、未修正のクライアントは受け入れません。 
    注:すべてのリモート ホストは、最新バージョンをサポートするまで、この設定を展開する必要があります。

2018 年 5 月 8 日の更新プログラムは、既定値を変更**暗号化 Oracle 修復**設定から**Vulnerable**に**軽減**します。 この変更、更新プログラムのあるリモート デスクトップ クライアントは、それらを持っていない (または、再起動されていないサーバーを更新する) をサーバーに接続できません。 更新プログラムがブロックされている通信の種類の影響の詳細については、KB 4093492 を参照してください。 [0886-CVE-2018 の更新プログラムの CredSSP](https://support.microsoft.com/en-us/help/4093492/credssp-updates-for-cve-2018-0886-march-13-2018)します。

この問題を解決するには、すべてのシステムが完全更新し、再起動されることを確認します。 更新プログラムと脆弱性についての詳細の一覧については、次を参照してください[CVE-2018-0886 |。CredSSP リモート コード実行の脆弱性](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2018-0886)します。

更新が完了するまで、この問題を回避するには、KB 4093492 許可されている種類の接続を確認します。 可能な代替手段がない場合、次のメソッドのいずれかを考慮する場合があります。

- 影響を受けているクライアント コンピューターで、設定、**暗号化 Oracle 修復**ポリシーにバックアップ**Vulnerable**します。
- 次のポリシーの変更、**コンピューターの構成\\管理用テンプレート\\Windows コンポーネント\\Remote Desktop Services\\リモート デスクトップ セッション ホスト\\セキュリティ**グループ ポリシー フォルダー。  
  - **リモート (RDP) 接続に特定のセキュリティ レイヤーの使用を必要と**: に設定**有効**選択**RDP**します。
  - **ネットワーク レベル認証を使用してリモート接続のユーザー認証を必要と**: に設定**無効**します。
    > [!IMPORTANT]  
    > これらの変更には、デプロイのセキュリティが低下します。 一時的に使用する場合のみあります。

グループ ポリシーでの作業の詳細については、次を参照してください。[ブロックしている GPO を変更する](#modifying-a-blocking-gpo)します。

### <a name="after-you-update-client-computers-some-users-need-to-sign-in-twice"></a>一部のユーザーが 2 回サインインする必要があるクライアント コンピューターを更新した後

いくつか Windows 7 または Windows 10 バージョン 1709 のユーザーは、リモート デスクトップ セッションにサインインし、2 つ目のサインイン画面をすぐに確認します。 この問題は、クライアント コンピューターが次の更新プログラムを受信した場合に発生します。

  - Windows 7: KB 4103718、 [2018 年 5 月 8 日-KB4103718 (月間ロールアップ)](https://support.microsoft.com/en-us/help/4103718/windows-7-update-kb4103718)
  - Windows 10 1709:KB 4103727、 [2018 年 5 月 8 日-KB4103727 (OS ビルド 16299.431)](https://support.microsoft.com/en-us/help/4103727/windows-10-update-kb4103727)

この問題を解決するには、ユーザーが (および RDSH または RDVI サーバー) に接続するコンピューターが、2018 年 6 月まで完全に更新されることを確認します。 これには、次の更新プログラムが含まれます。

  - Windows Server 2016 の場合:KB 4284880、 [2018 年 6 月 12 日 — KB4284880 (OS ビルド 14393.2312)](https://support.microsoft.com/en-us/help/4284880/windows-10-update-kb4284880)
  - Windows Server 2012 R2KB 4284815、 [2018 年 6 月 12 日 — KB4284815 (月間ロールアップ)](https://support.microsoft.com/en-us/help/4284815/windows-81-update-kb4284815)
  - Windows Server 2012:KB 4284855、 [2018 年 6 月 12 日 — KB4284855 (月間ロールアップ)](https://support.microsoft.com/en-us/help/4284855/windows-server-2012-update-kb4284855)
  - Windows Server 2008 R2:KB 4284826、 [2018 年 6 月 12 日 — KB4284826 (月間ロールアップ)](https://support.microsoft.com/en-us/help/4284826/windows-7-update-kb4284826)
  - Windows Server 2008 SP2 の場合:KB4056564、 [Windows Server 2008、Windows Embedded POSReady 2009、Windows Embedded Standard 2009 で CredSSP のリモート コード実行の脆弱性のセキュリティ更新プログラムの説明。2018 年 3 月 13 日](https://support.microsoft.com/en-us/help/4056564/security-update-for-vulnerabilities-in-windows-server-2008)

### <a name="users-are-denied-access-on-a-deployment-that-uses-remote-credential-guard-with-multiple-rd-connection-brokers"></a>ユーザーには、複数の RD 接続ブローカーをリモートの Credential Guard を使用している展開のアクセスが拒否されました。

この問題は、Credential Guard をリモート Windows Defender を使用している場合に、2 つ以上リモート デスクトップ接続ブローカーを使用した高可用性の展開で発生します。 ユーザーは、リモート デスクトップにサインインできません。

この問題は、Credential Guard をリモート認証、Kerberos を使用して、NTLM を制限するために発生します。 ただし、負荷分散と高可用性構成で、RD 接続ブローカーは、Kerberos の操作をサポートできません。

RD 接続ブローカーの負荷分散と高可用性構成を使用する必要がある場合は、リモートの Credential Guard を無効にして、この問題を回避できます。 Credential Guard をリモート Windows Defender を管理する方法の詳細については、次を参照してください。 [Credential Guard をリモート Windows Defender でのリモート デスクトップを保護するための資格情報](https://docs.microsoft.com/en-us/windows/security/identity-protection/remote-credential-guard#enable-windows-defender-remote-credential-guard)します。

## <a name="on-connecting-user-receives-remote-desktop-service-is-currently-busy-message"></a>ユーザーが"リモート デスクトップ サービスが現在ビジー状態"というメッセージを受信する、接続する方法

この問題を適切な応答を確認するのには、次の手順を使用します。

1. リモート デスクトップ サービスのサービスが応答しなくなった ([ようこそ] 画面には、「ハング」して、リモート デスクトップ クライアント表示など)。  
      - サービスが応答不能になるを参照してください。 [RDSH サーバー メモリの問題](#rdsh-server-memory-issue)します。
      - クライアントは、通常、サービスに使用する表示されている場合は、次の手順に進みます。
2. 場合は、リモート デスクトップ セッションを切断する 1 つまたは複数のユーザーに、ユーザー再び接続しますか。  
   - ユーザーの数に関係なく接続を拒否する、サービスが解決しない場合は、セッションの切断を参照してください[RD リスナー問題](#rd-listener-issue)します。
   - 接続ユーザー数の後にもう一度、セッションが切断されているが、サービスの受け入れを開始する場合[接続制限のポリシーを確認する](#check-the-connection-limit-policy)します。

### <a name="rdsh-server-memory-issue"></a>RDSH サーバー メモリの問題

一部の Windows Server 2012 R2 RDSH サーバーでメモリ リークが検出されました。 時間の経過と共に、これらのサーバーはリモート デスクトップ接続と、次のメッセージを使用したサインインをローカルのコンソールの両方を拒否するように開始します。

> リモート デスクトップ サービスは現在ビジー状態であるために、実行しようとして、タスクを完了できません。 数分後にもう一度お試しください。 他のユーザーはサインインできる必要があります。

接続するリモート デスクトップ クライアントは、応答しなくなります。

この問題を回避するには、RDSH サーバーを再起動します。

この問題を解決するには、サポート技術情報の 4093114 を適用する [2018 年 4 月 10 日-KB4093114 (毎月 Rollup)](file:///C:/Users/v-jesits/AppData/Local/Microsoft/Windows/INetCache/Content.Outlook/FUB8OO45/April%2010,%202018—KB4093114%20(Monthly%20Rollup)) に、RDSH サーバー。

### <a name="rd-listener-issue"></a>RD リスナーの問題

Windows Server 2012 R2 を Windows Server 2008 R2 から直接アップグレード済みの一部の RDSH サーバーまたは Windows Server 2016 には、問題が記載されているがされています。 リモート デスクトップ クライアントは、RDSH サーバーに接続するとき、ユーザー セッションの RD リスナーを RDSH サーバーを作成します。 影響を受けるサーバーでは、RD リスナーを増やすように、接続することはありませんが減少の回数を保持します。

この問題を回避するには、次のメソッドを使用できます。

  - RD リスナーのカウントをリセットする RDSH サーバーを再起動します。
  - 非常に大きな値に設定すると、接続の制限ポリシーを変更します。 接続の制限ポリシーの管理に関する詳細については、次を参照してください。[接続制限のポリシーを確認する](#check-the-connection-limit-policy)します。

この問題を解決するには、RDSH サーバーに次の更新プログラムが適用されます。

  - Windows Server 2012 R2KB 4343891、 [、2018 年 8 月 30 日-KB4343891 (月単位のロールアップのプレビュー)](https://support.microsoft.com/en-us/help/4343891/windows-81-update-kb4343891)
  - Windows Server 2016 の場合:KB 4343884、 [、2018 年 8 月 30 日-KB4343884 (OS ビルド 14393.2457)](https://support.microsoft.com/en-us/help/4343884/windows-10-update-kb4343884)

### <a name="check-the-connection-limit-policy"></a>接続制限のポリシーを確認してください。

個々 のコンピューター レベルまたはグループ ポリシー オブジェクト (GPO) を構成することによって、同時にリモート デスクトップ接続の数に制限を設定できます。 既定では、制限が設定されていません。

現在の設定を確認し、RDSH サーバー上の既存の Gpo を特定、管理者としてコマンド プロンプト ウィンドウを開き、次のコマンドを入力します。
  
```
gpresult /H c:\gpresult.html
```
   
このコマンドが終了したら、開いている gpresult.html とで**コンピューターの構成\\管理用テンプレート\\Windows コンポーネント\\Remote Desktop Services\\リモート デスクトップ セッション ホスト\\接続**、検索、**接続の数を制限**ポリシー。

  - このポリシー設定がある場合**無効**、グループ ポリシーは、RDP 接続に制限はありません。
  - このポリシー設定がある場合**有効**、し確認**優勢な GPO**します。 削除するか、接続の制限を変更する必要がある場合は、この GPO を編集します。

ポリシーの変更を適用するには、対象のコンピューターでコマンド プロンプト ウィンドウを開き、次のコマンドを入力します。
  
```
gpupdate /force
```
  
## <a name="rd-client-disconnects-and-cannot-reconnect-to-the-same-session"></a>RD クライアントを切断し、同じセッションに再接続することはできません。

リモート デスクトップ クライアントのリモート デスクトップ接続を失った後、クライアントがすぐに再接続できません。 ユーザーは、次のエラー メッセージを受け取ります。

  - セキュリティ エラーのため、クライアントは、ターミナル サーバーに接続できませんでした。 ネットワークにログオンしていることを確認したら、サーバーへの接続をもう一度お試しください。
  - リモート デスクトップが切断されました。 セキュリティ エラーのため、クライアントは、リモート コンピューターに接続できませんでした。 ネットワークにログオンしているをもう一度接続を再試行することを確認します。

後では、リモート デスクトップ クライアントは、リモート デスクトップに再接続します。 ただし、元のセッションへの接続の代わりに RDSH サーバー、クライアント接続する新しいセッションにします。 RDSH サーバーを確認するには、元のセッションを切断の状態が入力されていませんが、代わりに、アクティブなままが表示されます。

この問題を回避することができます、**構成接続がキープ アライブ間隔**ポリシーで、**コンピューターの構成\\管理用テンプレート\\Windows コンポーネント\\リモート デスクトップ サービス\\リモート デスクトップ セッション ホスト\\接続**グループ ポリシー フォルダー。 このポリシーを有効にした場合は、キープ アライブ間隔を入力する必要があります。 キープアライブ間隔で、サーバーがセッション状態を何分ごとに確認するかが決定されます。

この問題は、認証および構成設定の構成の誤りによって発生することができます。 サーバー レベルまたは Gpo を使用して、これらの設定を構成できます。 グループ ポリシー設定が表示されます、**コンピューターの構成\\管理用テンプレート\\Windows コンポーネント\\Remote Desktop Services\\リモート デスクトップ セッション ホスト\\セキュリティ**グループ ポリシー フォルダー。

1. 3. RD セッション ホスト サーバーで、レジストリ エディターを開きます。
2. **接続**、接続の名前を右クリックし、クリックして**プロパティ**します。
3. **プロパティ**、接続のダイアログ ボックスで、**全般**] タブの [**セキュリティ**レイヤーでセキュリティ メソッドを選択します。
4. **暗号化レベル**レベルをクリックします。 選択することができます**低**、**クライアント互換**、**高**、または**FIPS 準拠している**します。

> [!NOTE]  
>  - クライアントと RD セッション ホスト サーバー間の通信には、最高レベルの暗号化が必要な場合、FIPS 準拠の暗号化を使用します。
>  - グループ ポリシーで構成する暗号化レベルの設定は、リモート デスクトップ サービスの構成ツールを使用して設定した構成をオーバーライドします。 また、有効にした場合、[システム暗号化。暗号化、ハッシュ、および署名のための FIPS 準拠アルゴリズムを使用して](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2003/cc780081\(v=ws.10\))ポリシーでは、この設定をオーバーライド、**クライアント接続の暗号化レベルを設定**ポリシー。 システムの暗号化ポリシー、**コンピューターの構成\\Windows 設定\\セキュリティ設定\\ローカル ポリシー\\セキュリティ オプション**フォルダー。
>  - 暗号化レベルを変更した場合、新しい暗号化レベルは、ユーザーが次回ログオンした時に有効になります。 複数の 1 つのサーバーの暗号化レベルを必要とする場合は、複数のネットワーク アダプターをインストールし、各アダプターを個別に構成します。
>  - その証明書が、リモート デスクトップ サービスの構成の対応する秘密キーを確認するには、証明書を表示するを選択する接続を右クリックし**全般**を選択します**編集**、表示、および選択を使用する証明書を選択します。**証明書の表示**します。 下部にある、**全般** タブで、このステートメントでは、「があるこの証明書に対応する秘密キー」が表示されます。 証明書スナップインを使用してこの情報を表示することもできます。
>  - FIPS 準拠の暗号化 (、**システム暗号化。暗号化、ハッシュ、および署名のための FIPS 準拠アルゴリズム**ポリシーまたは**FIPS 準拠している**リモート デスクトップ サーバーの構成で設定) を暗号化し、サーバーとの間に、クライアントから送信されたデータの暗号化を解除します。連邦情報処理規格 (FIPS) 140-1 の暗号化アルゴリズムでは、使用して、クライアントにサーバーでは、Microsoft の暗号化モジュールを使用します。 詳細については、次を参照してください。 [FIPS 140 検証](https://docs.microsoft.com/en-us/windows/security/threat-protection/fips-140-validation)です。
>  - **高**設定およびクライアントにサーバーからサーバーにクライアントを強力な 128 ビット暗号化を使用して送信されたデータを暗号化します。
>  - **クライアント互換**設定、クライアントと、クライアントでサポートされる最大のキー強度でサーバー間で送信されるデータを暗号化します。
>  - **低**設定 56 ビット暗号化を使用してサーバーに、クライアントから送信されたデータを暗号化します。

## <a name="remote-laptop-disconnects-from-wireless-network"></a>リモートのラップトップがワイヤレス ネットワークから切断します。

この問題は、リモート デスクトップ クライアントは、802.1 x ワイヤレス ネットワークを使用して、ラップトップ コンピューターに接続するときに発生する可能性があります。 断続的に、ラップトップがワイヤレス ネットワークから切断され、自動的に再接続しません。

これは、ワイヤレス ネットワーク接続に対してネットワーク認証の設定は、するときに発生する既知の問題**ユーザー認証**します。

この問題を回避するには、ネットワーク認証の設定を設定**ユーザーまたはコンピューターの認証**または**コンピューター認証**します。

 > [!NOTE]  
> 1 台のコンピューター上のネットワーク認証設定を変更するには、コントロール パネルの ネットワークと共有センターを使用して、新しい設定で、新しいワイヤレス接続を作成する必要があります。

Gpo を使用してワイヤレス ネットワーク設定を構成する方法の詳細については、次を参照してください。[構成のワイヤレス ネットワーク (IEEE 802.11) ポリシー](https://docs.microsoft.com/en-us/windows-server/networking/core-network-guide/cncg/wireless/e-wireless-access-deployment#bkmk_policies)します。

## <a name="user-experiences-poor-performance-or-application-problems"></a>ユーザー エクスペリエンスのパフォーマンスの低下やアプリケーションの問題

このセクションでは、ユーザーがリモート デスクトップ機能を使用するときに発生可能性があるいくつかの一般的な問題を取り上げます。

  - [断続的に新しい仮想マシン Microsoft Azure に接続するユーザーに問題が発生](#intermittent-problems-with-new-microsoft-azure-virtual-machines)します。
  - [Windows 10 バージョン 1709 のリモート デスクトップに接続するユーザーのビデオの再生の問題が発生](#video-playback-issues-on-windows-10-version-1709)します。
  - [Windows 10 のリモート デスクトップに接続している読み取り専用ユーザー プロファイルを持つユーザーは自分のデスクトップを共有できません。](#desktop-sharing-issues-on-windows-10)
  - [NLA が無効になっているときに、以前のバージョンの Windows 10 を実行するクライアントを使用して Windows 10 のリモート デスクトップに接続するユーザーがパフォーマンスの低下を発生します。](#performance-issues-when-mixing-versions-of-windows-10-if-nla-is-disabled)
  - [ユーザーは、リモート デスクトップ セッションで複数のアプリケーションを実行および切断し、再接続を頻繁に、再接続時に黒い画面が発生した可能性があります。](#black-screen-issue)

### <a name="intermittent-problems-with-new-microsoft-azure-virtual-machines"></a>新しい Microsoft Azure virtual machines での断続的な問題

この問題は、最近プロビジョニングされた仮想マシンに影響します。 リモート デスクトップ セッションでは、すべてのユーザーの設定は読み込まれないことがユーザーは、仮想マシンに接続した後正しくします。

この問題を回避するには、仮想マシンから切断、少なくとも 20 分間待機し、再接続します。

この問題を解決するには、必要に応じて、仮想マシンに次の更新プログラムが適用されます。

  - Windows 10 および Windows Server 2016 の場合:KB 4343884、 [、2018 年 8 月 30 日-KB4343884 (OS ビルド 14393.2457)](https://support.microsoft.com/en-us/help/4343884/windows-10-update-kb4343884)
  - Windows Server 2012 R2KB 4343891、 [、2018 年 8 月 30 日-KB4343891 (月単位のロールアップのプレビュー)](https://support.microsoft.com/en-us/help/4343891/windows-81-update-kb4343891)

### <a name="video-playback-issues-on-windows-10-version-1709"></a>Windows 10 バージョン 1709 でビデオの再生の問題

この問題は、ユーザーが Windows 10 バージョン 1709 を実行しているリモート コンピューターに接続するときに発生します。 ときに、VMR9 を使用してビデオを再生これらのユーザー (混在レンダラー ビデオ 9) のコーデック、player は黒ウィンドウのみを示しています。

これは、Windows 10 バージョン 1709 の既知の問題です。 この問題は、Windows 10 バージョン 1703 では発生しません。

### <a name="desktop-sharing-issues-on-windows-10"></a>デスクトップの共有の Windows 10 の問題

この問題は、ユーザーがある場合、読み取り専用ユーザーのプロファイル (と関連するレジストリ ハイブ) など、キオスク シナリオで発生します。 このようなユーザーが Windows 10、バージョン 1803 を実行しているリモート コンピューターに接続するときは、自分のデスクトップを共有できません。

この問題を解決するには、4340917、Windows 10 更新プログラムを適用[2018 年 7 月 24 日 — KB4340917 (OS ビルド 17134.191)](https://support.microsoft.com/en-us/help/4340917/windows-10-update-kb4340917)します。

### <a name="performance-issues-when-mixing-versions-of-windows-10-if-nla-is-disabled"></a>NLA が無効になっている場合は、Windows 10 のバージョンが混在する場合のパフォーマンスの問題

この問題は、NLA が無効になっているし、Windows 10 を実行しているリモート デスクトップ クライアント コンピューターが別のバージョンの Windows 10 を実行するリモート デスクトップに接続するときに発生します。 Windows 10 バージョン 1709 または以前のバージョンを実行するコンピューターでリモート デスクトップ クライアントのユーザーでは、Windows 10、バージョン 1803 以降を実行するリモート デスクトップに接続するときにパフォーマンスが低下が発生します。

これには、Windows 10、バージョン 1803 以降のバージョンに接続するときに、以前のクライアント コンピューターが低速のプロトコルを使用 NLA が無効になっているために発生します。

この問題を解決するには、サポート技術情報の 4340917 を適用[2018 年 7 月 24 日 — KB4340917 (OS ビルド 17134.191)](https://support.microsoft.com/en-us/help/4340917/windows-10-update-kb4340917)します。

### <a name="black-screen-issue"></a>黒い画面の問題

この問題は、Windows 8.0、Windows 8.1、Windows 10 RTM、および Windows Server 2012 R2 で発生します。 ユーザーは、リモート デスクトップでの複数のアプリケーションを起動し、セッションから切断します。 定期的に、ユーザーは、アプリケーションと対話し、もう一度接続を切断するには、リモート デスクトップに再接続します。 ある時点で、ユーザーが再接続するとき、リモート デスクトップ セッションのみを示す黒い画面。 ユーザーは、リモート コンピューターのコンソール (または RDSH サーバー コンソール) からリモート デスクトップ セッションを終了する必要があります。 このアクションでは、アプリケーションが停止します。

この問題を解決するには、必要に応じて次の更新プログラムが適用されます。

  - Windows 8 および Windows Server 2012:KB4103719、 [、2018 年 5 月 17日: KB4103719 (月単位のロールアップのプレビュー)](https://support.microsoft.com/en-us/help/4103719/windows-server-2012-update-kb4103719)
  - Windows 8.1 および Windows Server 2012 R2:KB4103724、 [、2018 年 5 月 17日: KB4103724 (月単位のロールアップのプレビュー)](https://support.microsoft.com/en-us/help/4103724/windows-81-update-kb4103724) kb 4284863、 [、2018 年 6 月 21 日-KB4284863 (月単位のロールアップのプレビュー)](https://support.microsoft.com/en-us/help/4284863/windows-81-update-kb4284863)
  - Windows 10:KB4284860 で修正された[2018 年 6 月 12 日 — KB4284860 (OS ビルド 10240.17889)](https://support.microsoft.com/en-us/help/4284860/windows-10-update-kb4284860)
