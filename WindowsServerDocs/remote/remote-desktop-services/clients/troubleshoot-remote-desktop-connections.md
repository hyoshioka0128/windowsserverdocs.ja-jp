---
title: リモート デスクトップ接続のトラブルシューティング
description: 現象別のトラブルシューティング手順
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
ms.openlocfilehash: c6ce719ffa24cfc6704348c17548fe5cf33d9271
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67284146"
---
# <a name="troubleshooting-remote-desktop-connections"></a>リモート デスクトップ接続のトラブルシューティング
リモート デスクトップ サービス (RDS) の最も一般的ないくつかの問題に関する簡単な説明については、「[Frequently asked questions about the Remote Desktop clients](https://review.docs.microsoft.com/en-us/windows-server/remote/remote-desktop-services/clients/remote-desktop-client-faq)」 (リモート デスクトップ クライアントについてよく寄せられる質問) をご覧ください。 この記事では、接続の問題のトラブルシューティングに対するさらに高度ないくつかのアプローチについて説明します。 これらの手順の多くは、1 台の物理コンピューターが別の物理コンピューターに接続しているような単純な構成、またはさらに複雑な構成のどちらのトラブルシューティングにも適用されます。 一部の手順は、複雑なマルチユーザー シナリオでのみ発生する問題に対処します。 リモート デスクトップのコンポーネントおよびそれらの連動方法について詳しくは、「[リモート デスクトップ サービスのアーキテクチャ](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/desktop-hosting-logical-architecture)」をご覧ください。

> [!NOTE]  
> この記事で説明されている手順の多くでは、複数のコンピューターにアクセスする必要があり、そのうちの一部はリモートでのアクセスが必要な場合があります。 リモート管理ツールとその構成方法について詳しくは、「[Windows オペレーティング システムのリモート サーバー管理ツール (RSAT)](https://support.microsoft.com/en-us/help/2693643/remote-server-administration-tools-rsat-for-windows-operating-systems)」をご覧ください。

次の一覧では、発生している現象の種類を示します。

- [リモート デスクトップ クライアントはリモート デスクトップに接続できないが、特定の現象やメッセージはない (一般的なトラブルシューティング手順)](#no-specific-symptoms-or-messages-general-troubleshooting-steps)
- [リモート デスクトップ クライアントはリモート デスクトップに接続できず、"クラスが登録されていません" というメッセージを受け取る](#client-cannot-connect-class-not-registered)
- [リモート デスクトップ クライアントはリモート デスクトップに接続できず、"使用可能なライセンスがありません" または "セキュリティ エラー" というメッセージを受け取る](#client-cannot-connect-no-licenses-available)
- [ユーザーは、"アクセス拒否" というメッセージを受け取るか、または資格情報を 2 回入力する必要がある](#user-cannot-authenticate-or-must-authenticate-twice)
- [接続時に、"Remote Desktop Service is currently busy" (リモート デスクトップ サービスは現在ビジー状態です) というメッセージを受け取る](#on-connecting-user-receives-remote-desktop-service-is-currently-busy-message)
- [リモート デスクトップ クライアントが切断され、同じセッションに再接続できない](#rd-client-disconnects-and-cannot-reconnect-to-the-same-session)
- [ユーザーがワイヤレス ネットワーク経由でリモート ラップトップに接続した後、ラップトップがネットワークから切断される](#remote-laptop-disconnects-from-wireless-network)。
- [ユーザー エクスペリエンスのパフォーマンスの低下、またはリモート アプリケーションの問題](#user-experiences-poor-performance-or-application-problems)

> [!NOTE]  
> 現在の RDP 切断コードの一覧については、「[ExtendedDisconnectReasonCode enumeration](https://docs.microsoft.com/windows/desktop/TermServ/extendeddisconnectreasoncode)」 (ExtendedDisconnectReasonCode 列挙型) をご覧ください。 

## <a name="no-specific-symptoms-or-messages-general-troubleshooting-steps"></a>特定の現象またはメッセージがない (一般的なトラブルシューティング手順)

リモート デスクトップ クライアントがリモート デスクトップに接続できず、しかし原因の特定に役立つメッセージや他の症状が提供されない場合は、以下の手順を使います。 この種の問題の最も一般的な原因の多くを解決するには、以下の方法を使います。

- [RDP プロトコルの状態を確認する](#check-the-status-of-the-rdp-protocol)
- [RDP サービスの状態を確認する](#check-the-status-of-the-rdp-services)
- [RDP リスナーが機能していることを確認する](#check-that-the-rdp-listener-is-functioning)
- [RDP リスナー ポートを確認する](#check-the-rdp-listener-port)

### <a name="check-the-status-of-the-rdp-protocol"></a>RDP プロトコルの状態を確認する

#### <a name="check-the-status-of-the-rdp-protocol-on-a-local-computer"></a>ローカル コンピューターで RDP プロトコルの状態を確認する

ローカル コンピューターで RDP プロトコルの状態を確認および変更するには、「[リモート デスクトップを有効にする方法](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/clients/remote-desktop-allow-access#how-to-enable-remote-desktop)」をご覧ください。

> [!NOTE]  
> リモート デスクトップのオプションを利用できない場合は、「[ローカル コンピューターでグループ ポリシー オブジェクト (GPO) が RDP をブロックしているかどうかを確認する](#check-whether-a-group-policy-object-gpo-is-blocking-rdp-on-a-local-computer)」をご覧ください。

#### <a name="check-the-status-of-the-rdp-protocol-on-a-remote-computer"></a>リモート コンピューターで RDP プロトコルの状態を確認する

> [!IMPORTANT]  
> 慎重にこのセクションの手順に従います。 誤ってレジストリを変更すると、重大な問題が発生する可能性があります。 変更する前に、問題が発生した場合に[復元するためにレジストリをバックアップ](https://support.microsoft.com/en-us/help/322756%22%20target=%22_self%22)します。

リモート コンピューターで RDP プロトコルの状態を確認して変更するには、ネットワーク レジストリ接続を使います。

1. **[スタート]** を選択し、 **[ファイル名を指定して実行]** を選択して、「**regedt32**」と入力します。
2. レジストリ エディターで、 **[ファイル]** 、 **[ネットワーク レジストリへの接続]** の順に選択します。
3. **[コンピューターの選択]** ダイアログ ボックスで、リモート コンピューターの名前を入力し、 **[名前の確認]** を選択してから、 **[OK]** を選択します。
4. **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server** に移動します。  
   ![fDenyTSConnections エントリが示されているレジストリ エディター](../media/troubleshoot-remote-desktop-connections/RegEntry_fDenyTSConnections.png)
   - **fDenyTSConnections** キーの値が **0** の場合、RDP は有効になっています
   - **fDenyTSConnections** キーの値が **1** の場合、RDP は無効になっています
5. RDP を有効にするには、**fDenyTSConnections** の値を **1** から **0** に変更します。

#### <a name="check-whether-a-group-policy-object-gpo-is-blocking-rdp-on-a-local-computer"></a>ローカル コンピューターでグループ ポリシー オブジェクト (GPO) が RDP をブロックしているかどうかを確認する

ユーザー インターフェイスで RDP を有効にできない場合、または変更した後で **fDenyTSConnections** の値が **1** に戻る場合は、GPO によってコンピューター レベルの設定がオーバーライドされている可能性があります。

ローカル コンピューターでのグループ ポリシーの構成を確認するには、管理者としてコマンド プロンプト ウィンドウを開き、次のコマンドを入力します。
```
gpresult /H c:\gpresult.html
```
このコマンドの終了後、gpresult.html を開きます。 **[コンピューターの構成] > [管理用テンプレート] > [Windows コンポーネント] > [リモート デスクトップ サービス] > [リモート デスクトップ セッション ホスト] > [接続]** で、 **[ユーザーがリモート デスクトップ サービスを使ってリモート接続することを許可する]** ポリシーを探します。

- このポリシーの設定が **[有効]** である場合、グループ ポリシーでは RDP 接続はブロックされていません。
- このポリシー設定が **[無効]** である場合は、 **[優勢な GPO]** を確認します。 これが、RDP 接続をブロックしている GPO です。
  ![ドメイン レベルの GPO の **RDP ブロック** で RDP が無効になっている gpresult.html のセグメントの例。](../media/troubleshoot-remote-desktop-connections/GPResult_RDSH_Connections_GP.png)
   
  ![**ローカル グループ ポリシー** で RDP が無効になっている gpresult.html のセグメントの例。](../media/troubleshoot-remote-desktop-connections/GPResult_RDSH_Connections_LGP.png)

#### <a name="check-whether-a-gpo-is-blocking-rdp-on-a-remote-computer"></a>リモート コンピューターで GPO によって RDP がブロックされているかどうかを確認する

リモート コンピューターでグループ ポリシーの構成を確認するためのコマンドは、ローカル コンピューターの場合とほぼ同じです。
```
gpresult /S <computer name> /H c:\gpresult-<computer name>.html
```
このコマンドによって生成されるファイル (**gpresult-<\<コンピューター名\>>.html**) では、ローカル コンピューター バージョン (**gpresult.html**) と同じ情報の形式が使われます。

#### <a name="modifying-a-blocking-gpo"></a>ブロックしている GPO を変更する

グループ ポリシー オブジェクト エディター (GPE) およびグループ ポリシー管理コンソール (GPM) で、これらの設定を変更することができます。 グループ ポリシーの使い方について詳しくは、「[Advanced Group Policy Management](https://docs.microsoft.com/microsoft-desktop-optimization-pack/agpm/)」(高度なグループ ポリシーの管理) をご覧ください。

ブロックしているポリシーを変更するには、次のいずれかの方法を使います。

- GPE で、適切なレベルの GPO (ローカル、ドメインなど) にアクセスし、 **[コンピューターの構成] > [管理用テンプレート] > [Windows コンポーネント] > [リモート デスクトップ サービス] > [リモート デスクトップ セッション ホスト] > [接続]** > **[ユーザーがリモート デスクトップ サービスを使ってリモート接続することを許可する]** に移動します。  
   1. ポリシーを **[有効]** または **[未構成]** に設定します。
   2. 影響を受けるコンピューターで、管理者としてコマンド プロンプト ウィンドウを開き、**gpupdate /force** コマンドを実行します。
- GPM で、影響を受けるコンピューターにブロック ポリシーを適用している OU に移動し、OU からポリシーを削除します。

### <a name="check-the-status-of-the-rdp-services"></a>RDP サービスの状態を確認する

ローカル (クライアント) コンピューターとリモート (ターゲット) コンピューターの両方で、次のサービスが実行されている必要があります。

- リモート デスクトップ サービス (TermService)
- リモート デスクトップ サービス ユーザー モード ポート リダイレクター (UmRdpService)

サービス MMC スナップインを使って、ローカル環境またはリモート環境のサービスを管理できます。 ローカル環境またはリモート環境 (リモート PowerShell コマンドを受け付けるようにリモート コンピューターが構成されている場合) で PowerShell を使うこともできます。

![サービス MMC スナップインでのリモート デスクトップ サービス。 既定のサービス設定は変更しないでください。](../media/troubleshoot-remote-desktop-connections/RDSServiceStatus.png)

いずれかのコンピューターで、1 つまたは両方のサービスが実行されていない場合は、開始します。

> [!NOTE]  
> リモート デスクトップ サービス サービスを開始する場合、 **[はい]** をクリックすると、リモート デスクトップ サービス ユーザー モード ポート リダイレクター サービスが自動的に再起動します。

### <a name="check-that-the-rdp-listener-is-functioning"></a>RDP リスナーが機能していることを確認する

> [!IMPORTANT]  
> 慎重にこのセクションの手順に従います。 誤ってレジストリを変更すると、重大な問題が発生する可能性があります。 変更する前に、問題が発生した場合に[復元するためにレジストリをバックアップ](https://support.microsoft.com/en-us/help/322756%22%20target=%22_self%22)します。

#### <a name="check-the-status-of-the-rdp-listener"></a>RDP リスナーの状態を確認する

この手順では、管理者アクセス許可を持つ PowerShell インスタンスを使います。 ローカル コンピューターでは、管理者アクセス許可を持つコマンド プロンプトを使うこともできます。 ただし、この手順では、ローカルとリモートの両方で同じコマンドが動作するため、PowerShell を使います。

1. PowerShell ウィンドウを開きます。 リモート コンピューターに接続するには、「**Enter-PSSession -ComputerName <\<コンピューター名\>>** 」と入力します。
2. 「**qwinsta**」と入力します。 
    ![qwinsta コマンドでは、コンピューターのポートでリッスンしているプロセスが一覧表示される。](../media/troubleshoot-remote-desktop-connections/WPS_qwinsta.png)
3. リストに **Listen** という状態の **rdp-tcp** が含まれている場合、RDP リスナーは動作しています。 「[RDP リスナー ポートを確認する](#check-the-rdp-listener-port)」に進んでください。 それ以外の場合は、手順 4 に進みます。
4. 動作中のコンピューターから RDP リスナーの構成をエクスポートします。
    1. 影響を受けるコンピューターと同じバージョンのオペレーティング システムが搭載されているコンピューターにサインインし、そのコンピューターのレジストリにアクセスします (たとえば、レジストリ エディターを使用)。
    2. 次のレジストリ エントリに移動します。  
        **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server\\WinStations\\RDP-Tcp**
    3. エントリを .reg ファイルにエクスポートします。 たとえば、レジストリ エディターでエントリを右クリックし、 **[エクスポート]** を選択してから、エクスポートされる設定のファイル名を入力します。
    4. エクスポートした .reg ファイルを、影響を受けるコンピューターにコピーします。
5. RDP リスナーの構成をインポートするには、影響を受けるコンピューターで管理者アクセス許可を持つ PowerShell ウィンドウを開きます (または、PowerShell ウィンドウを開き、影響を受けるコンピューターにリモート接続します)。
   1. 既存のレジストリ エントリをバックアップするには、次のコマンドを入力します。  
   
      ```powershell  
      cmd /c 'reg export "HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-tcp" C:\Rdp-tcp-backup.reg'   
      ```  
   

   2. 既存のレジストリ エントリを削除するには、次のコマンドを入力します。  
   
      ```powershell  
      Remove-Item -path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-tcp' -Recurse -Force  
      ```
   
   3. 新しいレジストリ エントリをインポートしてサービスを再起動するには、次のコマンドを入力します。  
   
      ```powershell  
      cmd /c 'regedit /s c:\<filename>.reg'  
      Restart-Service TermService -Force  
      ```   
      \<filename\> は、エクスポートした .reg ファイルの名前です。
6. 再びリモート デスクトップ接続を試みて、構成をテストします。 まだ接続できない場合は、影響を受けるコンピューターを再起動します。
7. それでも接続できない場合は、[RDP の自己署名証明書の状態を確認](#check-the-status-of-the-rdp-self-signed-certificate)します。

#### <a name="check-the-status-of-the-rdp-self-signed-certificate"></a>RDP の自己署名証明書の状態を確認する

1. まだ接続できない場合は、証明書 MMC スナップインを開きます。 管理する証明書ストアの選択を求めるメッセージが表示されたら、 **[コンピューター アカウント]** を選択し、影響を受けるコンピューターを選択します。
2. **[証明書]** フォルダーの **[リモート デスクトップ]** で、RDP 自己署名証明書を削除します。 
    ![MMC 証明書スナップインでのリモート デスクトップ証明書。](../media/troubleshoot-remote-desktop-connections/MMCCert_Delete.png)
3. 影響を受けるコンピューターで、リモート デスクトップ サービスのサービスを再起動します。
4. 証明書スナップインを最新の情報に更新します。
5. RDP 自己署名証明書が再作成されていない場合は、[MachineKeys フォルダーのアクセス許可を確認](#check-the-permissions-of-the-machinekeys-folder)します。

#### <a name="check-the-permissions-of-the-machinekeys-folder"></a>MachineKeys フォルダーのアクセス許可を確認する

1. 影響を受けるコンピューターでエクスプローラーを開き、**C:\\ProgramData\\Microsoft\\Crypto\\RSA\\** に移動します。
2. **MachineKeys** を右クリックし、 **[プロパティ]** 、 **[セキュリティ]** 、 **[詳細設定]** の順に選択します。
3. 次のアクセス許可が構成されていることを確認します。
      - Builtin\\Administrators: フル コントロール
      - Everyone: 読み取り、書き込み

### <a name="check-the-rdp-listener-port"></a>RDP リスナー ポートを確認する

ローカル (クライアント) コンピューターとリモート (ターゲット) コンピューターの両方で、RDP リスナーがポート 3389 でリッスンしている必要があります。 他のアプリケーションがこのポートを使っていてはなりません。

> [!IMPORTANT]  
> 慎重にこのセクションの手順に従います。 誤ってレジストリを変更すると、重大な問題が発生する可能性があります。 変更する前に、問題が発生した場合に[復元するためにレジストリをバックアップ](https://support.microsoft.com/en-us/help/322756%22%20target=%22_self%22)します。

RDP ポートを確認または変更するには、レジストリ エディターを使います。

1. [スタート] を選択し、 **[ファイル名を指定して実行]** を選択して、「**regedt32**」と入力します。
      - リモート コンピューターに接続するには、 **[ファイル]** 、 **[ネットワーク レジストリへの接続]** の順に選択します。
      - **[コンピューターの選択]** ダイアログ ボックスで、リモート コンピューターの名前を入力し、 **[名前の確認]** を選択してから、 **[OK]** を選択します。
2. レジストリを開き、**HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server\\WinStations\\\<listener\>** に移動します。 
    ![RDP プロトコルの PortNumber サブキー。](../media/troubleshoot-remote-desktop-connections/RegEntry_PortNumber.png)
3. **PortNumber** の値が **3389** 以外の場合は、**3389** に変更します。 
   > [!IMPORTANT]  
    > 別のポートを使ってリモート デスクトップ サービスを動作させることができます。 ただし、このようにすることはお勧めできません。 そのような構成のトラブルシューティングは、この記事の範囲外です。
4. ポート番号を変更した後、リモート デスクトップ サービスのサービスを再起動します。

#### <a name="check-that-another-application-is-not-trying-to-use-the-same-port"></a>別のアプリケーションが同じポートを使おうとしていないことを確認する

この手順では、管理者アクセス許可を持つ PowerShell インスタンスを使います。 ローカル コンピューターでは、管理者アクセス許可を持つコマンド プロンプトを使うこともできます。 ただし、この手順では、ローカルとリモートで同じコマンドが動作するため、PowerShell を使います。

1. PowerShell ウィンドウを開きます。 リモート コンピューターに接続するには、「**Enter-PSSession -ComputerName <\<コンピューター名\>>** 」と入力します。
2. 次のコマンドを入力します。  
   
     ```powershell  
    cmd /c 'netstat -ano | find "3389"'  
    ```
  
    ![netstat コマンドでは、ポートおよびそれをリッスンしているサービスのリストが生成されます。](../media/troubleshoot-remote-desktop-connections/WPS_netstat.png)
3. 3\. 状態が「**LISTENING**」の TCP ポート 3389 (または割り当てられた RDP ポート) のエントリを探します。 
    > [!NOTE]  
   > そのポートを使用しているプロセスまたはサービスの PID (プロセス ID) が [PID] 列の下に表示されます。
4. ポート 3389 (または、割り当てられている RDP ポート) を使っているアプリケーションを確認するには、次のコマンドを入力します。  
   
     ```powershell  
    cmd /c 'tasklist /svc | find "<pid listening on 3389>"'  
    ```  
  
    ![tasklist コマンドでは、特定のプロセスの詳細が報告されます。](../media/troubleshoot-remote-desktop-connections/WPS_tasklist.png)
5. ポートに関連付けられている PID 番号 (**netstat** の出力からの情報) のエントリを探します。 その PID に関連付けられているサービスまたはプロセスが、右側に表示されます。
6. リモート デスクトップ サービス (TermServ.exe) 以外のアプリケーションまたはサービスによってそのポートが使われている場合は、次のいずれかの方法を使って競合を解決できます。
      - 他のアプリケーションまたはサービスを、別のポートを使うように構成します (推奨)。
      - 他のアプリケーションまたはサービスをアンインストールします。
      - 別のポートを使うように RDP を構成した後、リモート デスクトップ サービスのサービスを再起動します (推奨されません)。

#### <a name="check-whether-a-firewall-is-blocking-the-rdp-port"></a>ファイアウォールで RDP ポートがブロックされているかどうかを確認する

ポート 3389 を使って、影響を受けるコンピューターに到達できるかどうかをテストするには、**psping** ツールを使います。

1. 影響を受けるコンピューターとは異なるコンピューターで、<https://live.sysinternals.com/psping.exe> から **psping** をダウンロードします。
2. 管理者としてコマンド プロンプト ウィンドウを開き、**psping** をインストールしたディレクトリに移動して、次のコマンドを入力します。  
   
   ```  
   psping -accepteula <computer IP>:3389  
   ```
   
3. **psping** コマンドの出力で次のような結果を確認します。  
      - **\<コンピューター IP\>** へ接続しています: リモート コンピューターは到達可能です。
      - **(0% 損失)** : すべての接続試行が成功しました。
      - **The remote computer refused the network connection (リモート コンピューターによりネットワーク接続が拒否されました)** : リモート コンピューターは到達不可能です。
      - **(100% 損失)** : すべての接続試行が失敗しました。
1. 複数のコンピューターで **psping** を実行し、影響を受けるコンピューターに接続できるかどうかをテストします。
1. 影響を受けるコンピューターによって、他のすべてのコンピューターからの接続がブロックされるか、他のコンピューターの一部がブロックされるか、または他のコンピューターの 1 つだけかに注意してください。
1. 推奨される次の手順は次のとおりです。
      - ネットワーク管理者と協力して、影響を受けるコンピューターへの RDP トラフィックがネットワークで許可されることを確認します。
      - ソース コンピューターと影響を受けるコンピューターの間にあるすべてのファイアウォール (影響を受けるコンピューター上の Windows ファイアウォールを含む) の構成を調べて、ファイアウォールによって RDP ポートがブロックされているかどうかを確認します。

## <a name="client-cannot-connect-class-not-registered"></a>クライアントが接続できない、"クラスが登録されていません"

Windows 10 バージョン 1709 以降を実行しているクライアントを使ってリモート コンピューターに接続しようとすると、リモート デスクトップ セッション ホスト サーバーで "クラスが登録されていません (0x80040154)" エラー コードを含むメッセージが報告されて、クライアントが接続できないことがあります。

この問題は、接続しようとしているユーザーに必須のユーザー プロファイルがある場合に発生します。 この問題を解決するには、[2018 年 7 月 24 日 — KB4338817 (OS ビルド 16299.579)](https://support.microsoft.com/en-us/help/4338817/windows-10-update-kb4338817) Windows 10 更新プログラムをインストールします。

## <a name="client-cannot-connect-no-licenses-available"></a>クライアントが接続できない、使用可能なライセンスがない

この状況は、RDSH サーバーとリモート デスクトップ ライセンス サーバーを含む展開に当てはまります。

ユーザーでどの状況が発生しているかを明らかにします。

- ライセンスを使用できない、またはライセンス サーバーを使用できないため、セッションが切断されました
- セキュリティ エラーのため、アクセスが拒否されました

ドメイン管理者として RD セッション ホストにサインインし、RD ライセンス診断機能ツールを開きます。 次のようなメッセージを探します。

  - リモート デスクトップ セッション ホスト サーバーの猶予期間が過ぎましたが、RD セッション ホスト サーバーでライセンス サーバーが 1 台も構成されていません。 RD セッション ホスト サーバーにライセンス サーバーが構成されていないと、RD セッション ホスト サーバーへの接続は拒否されます。
  - ライセンス サーバー \<コンピューター名\> は使用できません。 原因としては、ネットワーク接続に問題がある、ライセンス サーバー上でリモート デスクトップ ライセンス サービスが停止している、または RD ライセンスがコンピューターにインストールされていない、の 3 つが考えられます。

これらの問題は、次のユーザー メッセージと関連することがよくあります。

  - このコンピューターで利用できるリモート デスクトップ クライアント アクセス ライセンスがないため、リモート セッションは切断されました。
  - ライセンスを提供するためのリモート デスクトップ ライセンス サーバーがないため、リモート セッションは切断されました。

この場合は、[RD ライセンス サービスを構成](#configure-the-rd-licensing-service)します。

RD ライセンス診断機能ツールで、"RDP プロトコル コンポーネント X.224 により、プロトコル ストリームにエラーが検出され、クライアントが切断されました" のような他の問題が表示される場合は、ライセンスの証明書に影響を与える問題が存在する可能性があります。 そのような問題は、次のようなユーザー メッセージと関連することがよくあります。

Because of a security error, the client could not connect to the Terminal server. After making sure that you are logged on to the network, try connecting to the server again. (セキュリティのエラーのため、クライアントはターミナル サーバーに接続できません。ネットワークにログオンしていることを確認した後、もう一度サーバーに接続してみてください。)

この場合は、[X509 証明書のレジストリ キーを更新](#refresh-the-x509-certificate-registry-keys)します。

### <a name="configure-the-rd-licensing-service"></a>RD ライセンス サービスを構成する

次の手順では、サーバー マネージャーを使って、構成を変更します。 サーバー マネージャーを構成して使用する方法については、「[サーバー マネージャー](https://docs.microsoft.com/windows-server/administration/server-manager/server-manager)」をご覧ください。

1. サーバー マネージャーを開き、 **[リモート デスクトップ サービス]** に移動します。
2. **[展開の概要]** で **[タスク]** を選択した後、 **[Edit Deployment Properties]\(展開のプロパティの編集\)** を選択します。
3. **[RD ライセンス]** を選択し、展開に適したライセンス モードを選択します ( **[接続デバイス数]** または **[接続ユーザー数]** )。
4. RD ライセンス サーバーの完全修飾ドメイン名 (FQDN) を入力し、 **[追加]** を選択します。
5. 複数の RD ライセンス サーバーがある場合は、サーバーごとに手順 4 を繰り返します。 
    ![サーバー マネージャーでの RD ライセンス サーバーの構成オプション。](../media/troubleshoot-remote-desktop-connections/RDLicensing_Configure.png)

### <a name="refresh-the-x509-certificate-registry-keys"></a>X509 証明書のレジストリ キーを更新する

> [!IMPORTANT]  
> 慎重にこのセクションの手順に従います。 誤ってレジストリを変更すると、重大な問題が発生する可能性があります。 変更する前に、問題が発生した場合に[復元するためにレジストリをバックアップ](https://support.microsoft.com/en-us/help/322756%22%20target=%22_self%22)します。

この問題を解決するには、レジストリをバックアップした後、X509 証明書のレジストリ キーを削除し、コンピューターを再起動してから、RD ライセンス サーバーを再びアクティブ化します。 これを行うには、次の手順に従います。

> [!NOTE]  
> RDSH サーバーごとに、次の手順を実行します。

1. レジストリ エディターを開き、**HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server\\RCM** に移動します。
2. [レジストリ] メニューで **[レジストリ ファイルのエクスポート]** を選択します。
3. **[ファイル名]** ボックスに「**exported- Certificate**」と入力し、 **[保存]** を選択します。
4. 次の各値を右クリックして **[削除]** を選択し、 **[はい]** を選択して削除を確認します。  
      - **Certificate**
      - **X509 Certificate**
      - **X509 Certificate ID**
      - **X509 Certificate2**
5. レジストリ エディターを終了し、RDSH サーバーを再起動します。

## <a name="user-cannot-authenticate-or-must-authenticate-twice"></a>ユーザーが認証できない、または 2 回認証する必要がある

ユーザーの認証に影響する可能性のある問題がいくつかあります。 このセクションでは、次の場合を取り上げます。

  - ["制限された種類のログオン" メッセージでユーザーがアクセスを拒否される](#access-denied-restricted-type-of-logon)
  - [イベント 16965 "SAM データベースへのリモート呼び出しが拒否されました" でユーザーまたはアプリケーションがアクセスを拒否される](#access-denied-a-remote-call-to-the-sam-database-has-been-denied)
  - [ユーザーがスマート カードを使用してサインインできない](#a-user-cannot-sign-in-by-using-a-smart-card)
  - [リモート PC がロックされている場合、ユーザーがパスワードを 2 回入力する必要がある](#if-the-remote-pc-is-locked-a-user-needs-to-enter-a-password-twice)
  - [ユーザーがサインインできず、"認証エラー" および "CredSSP 暗号化オラクルの修復" のメッセージを受け取る](#user-cannot-sign-in-and-receives-authentication-error-and-credssp-encryption-oracle-remediation-messages)
  - [クライアント コンピューターを更新した後、一部のユーザーが 2 回サインインする必要がある](#after-you-update-client-computers-some-users-need-to-sign-in-twice)。
  - [複数の RD 接続ブローカーを含む RemoteGuard を使用する展開でユーザーがアクセスを拒否される](#users-are-denied-access-on-a-deployment-that-uses-remote-credential-guard-with-multiple-rd-connection-brokers)

### <a name="access-denied-restricted-type-of-logon"></a>アクセス拒否、制限された種類のログオン

この状況では、Windows 10 のユーザーが Windows 10 または Windows Server 2016 のコンピューターに接続しようとすると、次のメッセージでアクセスを拒否されます。

> リモート デスクトップ接続:  
> 使用できるログオンの種類 (ネットワークまたは対話型) がシステム管理者により制限されています。 サポートが必要な場合は、システム管理者かテクニカル サポートに問い合わせてください。

この問題は、RDP 接続にネットワーク レベル認証 (NLA) が必要であり、ユーザーが **Remote Desktop Users** グループのメンバーではない場合に発生します。 また、**Remote Desktop Users** グループが **[ネットワーク経由でのアクセス]** ユーザー権利に割り当てられていない場合にも、発生する可能性があります。

この問題を解決するには、次のいずれかの手順に従います。

  - [ユーザーのグループ メンバーシップまたはユーザー権利の割り当てを変更します](#modify-the-users-group-membership-or-user-rights-assignment)。
  - NLA をオフにします (非推奨)。
  - Windows 10 以外のリモート デスクトップ クライアントを使います。 たとえば、Windows 7 クライアントではこの問題は発生しません。

#### <a name="modify-the-users-group-membership-or-user-rights-assignment"></a>ユーザーのグループ メンバーシップまたはユーザー権利の割り当てを変更する

この問題の影響を受けるユーザーが 1 人だけの場合、この問題の最も簡単な解決策は、ユーザーを **Remote Desktop Users** グループに追加することです。

ユーザーが既にこのグループのメンバーである場合は (または、複数のグループ メンバーに同じ問題がある場合は)、リモートの Windows 10 または Windows Server 2016 コンピューターでユーザー権利の構成を確認します。

1. グループ ポリシー オブジェクト エディター (GPE) を開き、リモート コンピューターのローカル ポリシーに接続します。
2. **[コンピューターの構成] > [Windows の設定] > [セキュリティ設定] > [ローカル ポリシー] > [ユーザー権利の割り当て]** に移動し、 **[ネットワーク経由でのアクセス]** を右クリックして、 **[プロパティ]** を選択します。
3. **Remote Desktop Users** (または親グループ) のユーザーとグループの一覧を確認します。
4. 一覧に **Remote Desktop Users** (または **Everyone** などの親グループ) が含まれていない場合、それを一覧に追加する必要があります (展開に複数のコンピューターがある場合は、グループ ポリシー オブジェクトを使います)。  
    たとえば、 **[ネットワーク経由でのアクセス]** の既定のメンバーシップには、**Everyone** が含まれています。 展開でグループ ポリシー オブジェクトを使って **Everyone** を削除している場合は、グループ ポリシー オブジェクトを更新して **Remote Desktop Users** を追加することにより、アクセスを復元することが必要な場合があります。

### <a name="access-denied-a-remote-call-to-the-sam-database-has-been-denied"></a>アクセス拒否、SAM データベースへのリモート呼び出しが拒否される

この動作が発生する可能性が最も高いのは、ドメイン コントローラーで Windows Server 2016 以降が実行されていて、ユーザーがカスタマイズされた接続アプリを使って接続しようとした場合です。 具体的には、Active Directory のユーザーのプロファイル情報にアクセスするアプリケーションは、アクセスを拒否されます。

この動作は、Windows に対する変更による結果です。 Windows Server 2012 R2 およびそれより前のバージョンでは、ユーザーがリモート デスクトップにログオンするとき、リモート接続マネージャー (RCM) はドメイン コントローラー (DC) に対し、Active Directory Domain Services (AD DS) 内のユーザー オブジェクト上にあるリモート デスクトップに固有の構成をクエリします。 この情報は、[Active Directory ユーザーとコンピューター] MMC スナップインで、ユーザーのオブジェクト プロパティの [リモート デスクトップ サービスのプロファイル] タブに表示されます。

Windows Server 2016 以降では、RCM は AD DS のユーザー オブジェクトをクエリしなくなっています。 リモート デスクトップ サービスの属性を使っているため、RCM で AD DS をクエリする必要がある場合は、RCM の以前の動作を手動で有効にする必要があります。

> [!IMPORTANT]  
> 慎重にこのセクションの手順に従います。 誤ってレジストリを変更すると、重大な問題が発生する可能性があります。 変更する前に、問題が発生した場合に[復元するためにレジストリをバックアップ](https://support.microsoft.com/en-us/help/322756%22%20target=%22_self%22)します。

RD セッション ホスト サーバーで以前の RCM の動作を有効にするには、次のレジストリ エントリを構成した後、**リモート デスクトップ サービス**のサービスを再起動します。  
  - **HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Policies\\Microsoft\\Windows NT\\Terminal Services**
  - **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server\\WinStations\\\<Winstation name\>\\**  
      - 名前: **fQueryUserConfigFromDC**
      - タイプ: **Reg\_DWORD**
      - 値:**1** (10 進)

RD セッション ホスト サーバー以外のサーバーで以前の RCM の動作を有効にするには、これらのレジストリ エントリと、次の追加レジストリ エントリを構成します (その後、サービスを再起動します)。
  - **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server**

この動作について詳しくは、KB 3200967 「[Windows Server のリモート接続マネージャーへの変更](https://support.microsoft.com/en-us/help/3200967/changes-to-remote-connection-manager-in-windows-server)」をご覧ください。

### <a name="a-user-cannot-sign-in-by-using-a-smart-card"></a>ユーザーがスマート カードを使用してサインインできない

この記事では、ユーザーがスマート カードを使ってリモート デスクトップにサインインできない場合の 3 つの一般的な状況について説明します。  
  - [ユーザーが読み取り専用ドメイン コントローラー (RODC) を使用するブランチ オフィスにサインインできない](#cannot-sign-in-with-a-smart-card-in-a-branch-office-with-a-rodc)
  - [ユーザーが最近更新された Windows Server 2008 SP2 コンピューターにサインインできない](#cannot-sign-in-with-a-smart-card-to-a-windows-server-2008-sp2-computer)
  - [ユーザーが最近更新された Windows コンピューターへのサインインを維持できず、リモート デスクトップ サービスのサービスが応答しなくなる (ハング)](#cannot-stay-signed-in-with-a-smart-card-and-remote-desktop-services-service-hangs)

#### <a name="cannot-sign-in-with-a-smart-card-in-a-branch-office-with-a-rodc"></a>RODC を使用するブランチ オフィスにスマート カードでサインインできない

この問題は、RODC を使うブランチ サイトに RDSH サーバーが含まれる展開で発生します。 RDSH サーバーは、ルート ドメインでホストされます。 ブランチ サイトのユーザーは子ドメインに属し、認証にスマート カードを使います。 RODC はユーザーのパスワードをキャッシュするように構成されています (RODC は **Allowed RODC Password Replication グループ**に属しています)。 ユーザーは、RDSH サーバー上のセッションにサインインしようとすると、次のようなメッセージを受け取ります。"実行しようとしたログオンは無効です。 ユーザー名または認証情報に誤りがあります。"

これは、ルート DC と RODC によるユーザーの資格情報の暗号化の管理方法での既知の問題です。 ルート DC では暗号化キーを使って資格情報が暗号化され、RODC では復号化キーがクライアントに提供されます。 しかし、2 つのキーが一致しません。

この問題を回避するには、RODC でパスワードのキャッシュを無効にするか、またはブランチ サイトに書き込み可能 DC を展開することによって、DC のトポロジを変更することを検討します。 別の方法は、RDSH サーバーをユーザーと同じ子ドメインに移動することです。 もう 1 つの代替案は、スマート カードなしでユーザーがサインインできるようにすることです。 いずれの解決策でも、パフォーマンスまたはセキュリティ レベルの低下が避けられない場合があります。

#### <a name="cannot-sign-in-with-a-smart-card-to-a-windows-server-2008-sp2-computer"></a>Windows Server 2008 SP2 のコンピューターにスマート カードでサインインできない

この問題は、ユーザーが KB4093227 (2018.4B) で更新された Windows Server 2008 SP2 コンピューターにサインインするときに発生します。 ユーザーは、スマート カードを使ってサインインしようとすると、次のようなメッセージでアクセスを拒否されます。"No valid certificates found. Check that the card is inserted correctly and fits tightly.” (有効な証明書が見つかりませんでした。カードが正しく挿入され、密着していることを確認してください。) 同時に、Windows Server コンピューターでは次のアプリケーション イベントが記録されます。"挿入されたスマート カードからデジタル証明書を取得しているときにエラーが発生しました。 署名が無効です。"

この問題を解決するには、KB 4093227 「[Windows Server 2008 における Windows リモート デスクトップ プロトコル (RDP) のサービス拒否の脆弱性を解決するためのセキュリティ更新プログラムについて: 2018 年 4 月 10 日](https://support.microsoft.com/en-us/help/4093227/security-update-for-vulnerabilities-in-windows-server-2008)」の 2018.06 B の再リリースで Windows Server コンピューターを更新してください。

#### <a name="cannot-stay-signed-in-with-a-smart-card-and-remote-desktop-services-service-hangs"></a>スマート カードでのサインインを維持できず、リモート デスクトップ サービスのサービスがハングする

この問題は、ユーザーが KB 4056446 で更新された Windows または Windows Server コンピューターにサインインするときに発生します。 最初、ユーザーはスマート カードを使ってシステムにサインインできる場合がありますが、その後 "SCARD\_E\_NO\_SERVICE" のエラー メッセージを受け取ります。 リモート コンピューターが応答しなくなる可能性があります。

この問題を回避するには、リモート コンピューターを再起動します。

この問題を解決するには、適切な修正プログラムでリモート コンピューターを更新します。

  - Windows Server 2008 SP2: KB 4090928、[Windows leaks handles in the lsm.exe process and smart card applications may display "SCARD\_E\_NO\_SERVICE" errors](https://support.microsoft.com/en-us/help/4090928/scard-e-no-service-errors-when-windows-leaks-handles-in-the-lsm-exe) (Windows の lsm.exe プロセスでハンドルがリークし、スマート カード アプリケーションで "SCARD_E_NO_SERVICE" エラーが表示される場合がある)
  - Windows Server 2012 R2KB 4103724、[2018 年 5 月 17 日 — KB4103724 (マンスリー ロールアップのプレビュー)](https://support.microsoft.com/en-us/help/4103724/windows-81-update-kb4103724)
  - Windows Server 2016 および Windows 10 バージョン 1607: KB 4103720、[2018 年 5 月 17 日 — KB4103720 (OS ビルド 14393.2273)](https://support.microsoft.com/en-us/help/4103720/windows-10-update-kb4103720)

### <a name="if-the-remote-pc-is-locked-a-user-needs-to-enter-a-password-twice"></a>リモート PC がロックされている場合、ユーザーがパスワードを 2 回入力する必要がある

この問題は、RDP 接続に NLA を必要としない展開内の Windows 10 バージョン 1709 が実行されているリモート デスクトップにユーザーが接続しようとしたときに発生する可能性があります。 これらの条件下では、リモート デスクトップがロックされている場合、ユーザーは接続するときに資格情報を 2 回入力する必要があります。

この問題を解決するには、Windows 10 バージョン 1709 コンピューターを KB 4343893、[2018 年 8 月 30 日 — KB4343893 (OS ビルド 16299.637)](https://support.microsoft.com/en-us/help/4343893/windows-10-update-kb4343893) で更新します。

### <a name="user-cannot-sign-in-and-receives-authentication-error-and-credssp-encryption-oracle-remediation-messages"></a>ユーザーがサインインできず、"認証エラー" および "CredSSP 暗号化オラクルの修復" のメッセージを受け取る

ユーザーは、Windows Vista SP2 以降または Windows Server 2008 SP2 以降の任意のバージョンを使ってサインインしようとすると、アクセスを拒否され、次のようなメッセージを受け取ります。

  - 認証エラーが発生しました。 要求された関数はサポートされていません。
  - This could be due to CredSSP encryption oracle remediation (これは、CredSSP 暗号化オラクルの修復のためである可能性があります)

"CredSSP 暗号化オラクルの修復" とは、2018 年の 3 月、4 月、5 月にリリースされた一連のセキュリティ更新プログラムのことです。 CredSSP は、他のアプリケーションに対する認証要求を処理する認証プロバイダーです。 2018 年 3 月 13 日の "3B" およびそれ以降の更新プログラムでは、攻撃者がユーザーの資格情報を中継してターゲット システムでコードを実行する悪用に対処しました。

最初の更新プログラムでは、新しいグループ ポリシー オブジェクトである**暗号化オラクルの修復**のサポートが追加されました。設定できる値は次のとおりです。

  - **Vulnerable (脆弱性あり)** 。 CredSSP を使用するクライアント アプリケーションは安全でないバージョンにフォールバックできますが、この動作はリモート デスクトップを攻撃の危険にさらします。 CredSSP を使用するサービスは、更新されていないクライアントを受け付けます。
  - **Mitigated (軽減済み)** 。 CredSSP を使用するクライアント アプリケーションは安全でないバージョンにフォールバックできませんが、CredSSP を使用するサービスは更新されていないクライアントを受け付けます。
  - **Force Updated Clients (更新されたクライアントを強制する)** 。 CredSSP を使用するクライアント アプリケーションは安全でないバージョンにフォールバックできず、CredSSP を使用するサービスは修正プログラムが適用されていないクライアントを受け付けません。 
    注:この設定は、すべてのリモート ホストが最新バージョンをサポートするようになるまで、展開しないでください。

2018 年 5 月 8 日の更新プログラムでは、**暗号化オラクルの修復**の既定の設定が **Vulnerable (脆弱性あり)** から **Mitigated (軽減済み)** に変更されました。 この変更により、更新プログラムが適用されたリモート デスクトップ クライアントは、適用されていないサーバー (または、更新後に再起動されていないサーバー) に接続できません。 更新プログラムの効果およびそれによってブロックされる通信の種類について詳しくは、KB 4093492 「[CVE-2018-0886 の CredSSP の更新プログラム](https://support.microsoft.com/en-us/help/4093492/credssp-updates-for-cve-2018-0886-march-13-2018)」をご覧ください。

この問題を解決するには、すべてのシステムを完全に更新して再起動します。 更新プログラムの完全な一覧および脆弱性の詳細については、「[CVE-2018-0886 | CredSSP のリモートでコードが実行される脆弱性](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2018-0886)」をご覧ください。

更新が完了するまでこの問題を回避するには、KB 4093492 で許可される接続の種類を確認してください。 可能な代替手段がない場合、次のいずれかの方法を検討できます。

- 影響を受けているクライアント コンピューターで、 **[Encryption Oracle Remediation]\(暗号化オラクルの修復\)** ポリシーを **[Vulnerable]\(脆弱性あり\)** に戻します。
- **[コンピューターの構成] > [管理用テンプレート] > [Windows コンポーネント] > [リモート デスクトップ サービス] > [リモート デスクトップ セッション ホスト] > [セキュリティ]** グループ ポリシー フォルダーで、次のポリシーを変更します。  
  - **[リモート (RDP) 接続に特定のセキュリティ レイヤーの使用を必要とする]** : **[有効]** に設定し、 **[RDP]** を選択します。
  - **[リモート接続にネットワーク レベル認証を使用したユーザー認証を必要とする]** : **[無効]** に設定します。
    > [!IMPORTANT]  
    > これらの変更により、展開のセキュリティが低下します。 使用する場合は、一時的にする必要があります。

グループ ポリシーの使用について詳しくは、「[ブロックしている GPO を変更する](#modifying-a-blocking-gpo)」をご覧ください。

### <a name="after-you-update-client-computers-some-users-need-to-sign-in-twice"></a>クライアント コンピューターを更新した後、一部のユーザーが 2 回サインインする必要がある

一部の Windows 7 または Windows 10 バージョン 1709 のユーザーは、リモート デスクトップ セッションにサインインすると、2 つ目のサインイン画面がすぐに表示されます。 この問題は、クライアント コンピューターに次の更新プログラムが適用されていると発生します。

  - Windows 7: KB 4103718、[2018 年 5 月 8 日 — KB4103718 (マンスリー ロールアップ)](https://support.microsoft.com/en-us/help/4103718/windows-7-update-kb4103718)
  - Windows 10 1709: KB 4103727、[2018 年 5 月 8 日 — KB4103727 (OS ビルド 16299.431)](https://support.microsoft.com/en-us/help/4103727/windows-10-update-kb4103727)

この問題を解決するには、ユーザーが接続するコンピューター (および RDSH または RDVI サーバー) が、2018 年 6 月まで完全に更新されていることを確認します。 これには次の更新プログラムが含まれます。

  - Windows Server 2016: KB 4284880、[2018 年 6 月 12 日 — KB4284880 (OS ビルド 14393.2312)](https://support.microsoft.com/en-us/help/4284880/windows-10-update-kb4284880)
  - Windows Server 2012 R2KB 4284815、[2018 年 6 月 12 日 — KB4284815 (マンスリー ロールアップ)](https://support.microsoft.com/en-us/help/4284815/windows-81-update-kb4284815)
  - Windows Server 2012: KB 4284855、[2018 年 6 月 12 日 — KB4284855 (マンスリー ロールアップ)](https://support.microsoft.com/en-us/help/4284855/windows-server-2012-update-kb4284855)
  - Windows Server 2008 R2:KB 4284826、[2018 年 6 月 12 日 — KB4284826 (マンスリー ロールアップ)](https://support.microsoft.com/en-us/help/4284826/windows-7-update-kb4284826)
  - Windows Server 2008 SP2: KB4056564, [Description of the security update for the CredSSP remote code execution vulnerability in Windows Server 2008, Windows Embedded POSReady 2009, and Windows Embedded Standard 2009:March 13, 2018](https://support.microsoft.com/en-us/help/4056564/security-update-for-vulnerabilities-in-windows-server-2008) (Windows Server 2008、Windows Embedded POSReady 2009、Windows Embedded Standard 2009 での CredSSP リモート コード実行の脆弱性に対するセキュリティ更新プログラムの説明: 2018 年 3 月 13 日)

### <a name="users-are-denied-access-on-a-deployment-that-uses-remote-credential-guard-with-multiple-rd-connection-brokers"></a>複数の RD 接続ブローカーを含む Remote Credential Guard を使用する展開でユーザーがアクセスを拒否される

この問題は、Windows Defender Remote Credential Guard が使われている場合に、複数のリモート デスクトップ接続ブローカーを使用する高可用性の展開で発生します。 ユーザーは、リモート デスクトップにサインインできません。

この問題は、Remote Credential Guard では認証に Kerberos が使われていて、NTLM が制限されるために発生します。 ただし、負荷分散されている高可用性構成の RD 接続ブローカーでは、Kerberos の操作をサポートできません。

負荷分散された RD 接続ブローカーが含まれる高可用性構成を使う必要がある場合は、Remote Credential Guard を無効にすることで、この問題を回避できます。 Windows Defender Remote Credential Guard の管理方法について詳しくは、「[Windows Defender Remote Credential Guard を使用してリモート デスクトップの資格情報を保護する](https://docs.microsoft.com/windows/security/identity-protection/remote-credential-guard#enable-windows-defender-remote-credential-guard)」をご覧ください。

## <a name="on-connecting-user-receives-remote-desktop-service-is-currently-busy-message"></a>接続時に、ユーザーが "Remote Desktop Service is currently busy" (リモート デスクトップ サービスは現在ビジー状態です) というメッセージを受け取る

この問題に対する適切な対応を確認するには、次の手順を使います。

1. リモート デスクトップ サービスのサービスは、応答しなくなりますか (たとえば、リモート デスクトップ クライアントがようこそ画面で "ハング" しているように見える)。  
      - サービスが応答しなくなる場合は、「[RDSH サーバーのメモリの問題](#rdsh-server-memory-issue)」をご覧ください。
      - クライアントは通常どおりサービスとやり取りしているように見える場合は、次の手順に進みます。
2. 1 人または複数のユーザーがリモート デスクトップ セッションを切断した場合、ユーザーは再び接続できますか。  
   - 何人のユーザーがセッションを切断しても引き続きサービスで接続が拒否される場合は、「[RD リスナーの問題](#rd-listener-issue)」をご覧ください。
   - 何人かのユーザーがセッションを切断すると、サービスでの接続の受け付けが始まる場合は、「[接続制限ポリシーを確認する](#check-the-connection-limit-policy)」をご覧ください。

### <a name="rdsh-server-memory-issue"></a>RDSH サーバーのメモリの問題

一部の Windows Server 2012 R2 RDSH サーバーでは、メモリ リークが検出されています。 時間の経過と共に、これらのサーバーでは、リモート デスクトップ接続とローカル コンソール サインインの両方が、次のようなメッセージで拒否されるようになります。

> リモート デスクトップ サービスが現在ビジー状態のため、実行しようとしている操作を完了できません。 しばらくたってからもう一度試してください。 他のユーザーはログオンできます。

また、接続しようとしているリモート デスクトップ クライアントは、応答しなくなります。

この問題を回避するには、RDSH サーバーを再起動します。

この問題を解決するには、KB 4093114、[2018 年 4 月 10 日 — KB4093114 (マンスリー ロールアップ)](file:///C:/Users/v-jesits/AppData/Local/Microsoft/Windows/INetCache/Content.Outlook/FUB8OO45/April%2010,%202018—KB4093114%20(Monthly%20Rollup)) を RDSH サーバーに適用します。

### <a name="rd-listener-issue"></a>RD リスナーの問題

Windows Server 2008 R2 から Windows Server 2012 R2 または Windows Server 2016 に直接アップグレードした一部の RDSH サーバーで問題が確認されています。 リモート デスクトップ クライアントが RDSH サーバーに接続すると、RDSH サーバーによってそのユーザー セッションに対する RD リスナーが作成されます。 影響を受けるサーバーでは RD リスナーのカウントが保持されており、ユーザーが接続すると増やされますが、減らされることはありません。

この問題に対しては、次の方法で対処できます。

  - RDSH サーバーを再起動して、RD リスナーのカウントをリセットします
  - 接続制限ポリシーを変更し、非常に大きな値に設定します。 接続制限ポリシーの管理について詳しくは、「[接続制限ポリシーを確認する](#check-the-connection-limit-policy)」をご覧ください。

この問題を解決するには、次の更新プログラムを RDSH サーバーに適用します。

  - Windows Server 2012 R2KB 4343891、[2018 年 8 月 30 日 — KB4343891 (マンスリー ロールアップのプレビュー)](https://support.microsoft.com/en-us/help/4343891/windows-81-update-kb4343891)
  - Windows Server 2016: KB 4343884、[2018 年 8 月 30 日 — KB4343884 (OS ビルド 14393.2457)](https://support.microsoft.com/en-us/help/4343884/windows-10-update-kb4343884)

### <a name="check-the-connection-limit-policy"></a>接続制限ポリシーを確認する

個々のコンピューター レベルで、またはグループ ポリシー オブジェクト (GPO) を構成することにより、同時リモート デスクトップ接続の数に制限を設定できます。 既定では、制限は設定されていません。

RDSH サーバーで現在の設定を確認し、既存の GPO を特定するには、管理者としてコマンド プロンプト ウィンドウを開き、次のコマンドを入力します。
  
```
gpresult /H c:\gpresult.html
```
   
このコマンドが完了した後、gpresult.html を開き、 **[コンピューターの構成] > [管理用テンプレート] > [Windows コンポーネント] > [リモート デスクトップ サービス] > [リモート デスクトップ セッション ホスト] > [接続]** で、 **[接続数を制限する]** ポリシーを探します。

  - このポリシーの設定が **[無効]** になっている場合、グループ ポリシーでは RDP 接続の数は制限されていません。
  - このポリシー設定が **[有効]** になっている場合は、 **[優勢な GPO]** を確認します。 接続の制限を削除または変更する必要がある場合は、この GPO を編集します。

ポリシーの変更を適用するには、影響を受けるコンピューターでコマンド プロンプト ウィンドウを開き、次のコマンドを入力します。
  
```
gpupdate /force
```
  
## <a name="rd-client-disconnects-and-cannot-reconnect-to-the-same-session"></a>RD クライアントが切断され、同じセッションに再接続できない

リモート デスクトップに対するリモート デスクトップ クライアントの接続が失われた後、クライアントがすぐに再接続できません。 ユーザーは、次のようなエラー メッセージを受け取ります。

  - Because of a security error, the client could not connect to the Terminal server. After making sure that you are logged on to the network, try connecting to the server again. (セキュリティのエラーのため、クライアントはターミナル サーバーに接続できません。ネットワークにログオンしていることを確認した後、もう一度サーバーに接続してみてください。)
  - リモート デスクトップが切断されました。 セキュリティ エラーのため、クライアントはリモート コンピューターに接続できませんでした。 ネットワークにログオンしていることを確認してから接続し直してください。

時間が経つと、リモート デスクトップ クライアントは、リモート デスクトップに再接続されます。 ただし、クライアントは、元のセッションに接続されるのではなく、RDSH サーバーによって新しいセッションに接続されます。 RDSH サーバーを調べると、元のセッションは切断状態になったのではなく、アクティブなままであることがわかります。

**[コンピューターの構成] > [管理用テンプレート] > [Windows コンポーネント] > [リモート デスクトップ サービス] > [リモート デスクトップ セッション ホスト] > [接続]** グループ ポリシー フォルダーで **[キープアライブ接続間隔を構成する]** ポリシーを有効にすることで、この問題を回避できます。 このポリシーを有効にした場合、キープアライブ間隔を入力する必要があります。 キープアライブ間隔で、サーバーがセッション状態を何分ごとに確認するかが決定されます。

この問題の原因は、認証および構成設定の構成の誤りである可能性があります。 これらの設定は、サーバー レベルで、または GPO を使って、構成できます。 グループ ポリシーの設定は、 **[コンピューターの構成] > [管理用テンプレート] > [Windows コンポーネント] > [リモート デスクトップ サービス] > [リモート デスクトップ セッション ホスト] > [セキュリティ]** グループ ポリシー フォルダーで使用できます。

1. 3\. RD セッション ホスト サーバーで、レジストリ エディターを開きます。
2. **[接続]** で、接続の名前を右クリックし、 **[プロパティ]** をクリックします。
3. 接続の **[プロパティ]** ダイアログ ボックスの、 **[全般]** タブの **[セキュリティ]** レイヤーで、セキュリティ メソッドを選択します。
4. **[暗号化レベル]** で、目的のレベルをクリックします。 **[低]** 、 **[クライアント互換]** 、 **[高]** 、または **[FIPS 準拠]** を選択できます。

> [!NOTE]  
>  - クライアントと RD セッション ホスト サーバーの間の通信で最高レベルの暗号化が必要な場合は、[FIPS 準拠] 暗号化を使います。
>  - グループ ポリシーで構成した暗号化レベルの設定により、リモート デスクトップ サービス構成ツールを使用して設定した構成がオーバーライドされます。 また、[[システム暗号化: 暗号化、ハッシュ、署名のための FIPS 準拠アルゴリズムを使う]](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc780081\(v=ws.10\)) ポリシーを有効にした場合、この設定により **[クライアント接続の暗号化レベルを設定する]** ポリシーがオーバーライドされます。 システム暗号化ポリシーは、 **[コンピューターの構成] > [Windows の設定] > [セキュリティ設定] > [ローカル ポリシー] > [セキュリティ オプション]** フォルダーにあります。
>  - 暗号化レベルを変更した場合、新しい暗号化レベルは、ユーザーが次回ログオンした時に有効になります。 1 つのサーバーで複数の暗号化レベルが必要な場合は、複数のネットワーク アダプターをインストールし、各アダプターを個別に構成します。
>  - 対応する秘密キーが証明書にあることを確認するには、リモート デスクトップ サービスの構成で、証明書を表示する接続を右クリックして、 **[全般]** 、 **[編集]** の順に選択し、表示する証明書を選択して、 **[証明書の表示]** を選択します。 **[全般]** タブの下端に、"この証明書に対応する秘密キーを持っています" と表示されるはずです。 また、この情報は、証明書スナップインを使って見ることもできます。
>  - FIPS 準拠の暗号化 ( **[システム暗号化: 暗号化、ハッシュ、署名のための FIPS 準拠アルゴリズムを使う]** ポリシーまたはリモート デスクトップ サーバーの構成の **[FIPS 準拠]** の設定) では、Microsoft 暗号化モジュールを使って、Federal Information Processing Standard (FIPS) 140-1 暗号化アルゴリズムで、クライアントとサーバーの間で送受信されるデータが暗号化および暗号化解除されます。 詳しくは、「[FIPS 140 検証](https://docs.microsoft.com/windows/security/threat-protection/fips-140-validation)」をご覧ください。
>  - **[高]** の設定では、強力な 128 ビット暗号化を使って、クライアントとサーバーの間で送受信されるデータが暗号化されます。
>  - **[クライアント互換]** の設定では、クライアントとサーバーの間で送信されるすべてのデータが、クライアントでサポートされている最高のキー強度で暗号化されます。
>  - **[低]** の設定では、56 ビット暗号化を使って、クライアントからサーバーに送信されるデータが暗号化されます。

## <a name="remote-laptop-disconnects-from-wireless-network"></a>リモート ラップトップがワイヤレス ネットワークから切断される

この問題は、リモート デスクトップ クライアントが 802.1x ワイヤレス ネットワークを使ってラップトップ コンピューターに接続されているときに、発生する可能性があります。 断続的に、ラップトップがワイヤレス ネットワークから切断され、自動的には再接続しません。

これは、ワイヤレス ネットワーク接続に対するネットワーク認証の設定が**ユーザー認証**のときに発生する既知の問題です。

この問題を回避するには、ネットワーク認証の設定を **[ユーザーまたはコンピューターの認証]** または **[コンピューター認証]** に設定します。

 > [!NOTE]  
> 1 台のコンピューターでネットワーク認証の設定を変更するには、[ネットワークと共有センター] コントロール パネルを使って、新しい設定で新しいワイヤレス接続を作成することが必要な場合があります。

GPO を使ってワイヤレス ネットワーク設定を構成する方法について詳しくは、「[ワイヤレス ネットワークを構成する (IEEE 802.11) ポリシー](https://docs.microsoft.com/windows-server/networking/core-network-guide/cncg/wireless/e-wireless-access-deployment#bkmk_policies)」をご覧ください。

## <a name="user-experiences-poor-performance-or-application-problems"></a>ユーザー エクスペリエンスのパフォーマンスの低下、またはアプリケーションの問題

このセクションでは、ユーザーがリモート デスクトップ機能を使うときに発生する可能性があるいくつかの一般的な問題を取り上げます。

  - [Microsoft Azure の新しい仮想マシンに接続するユーザーで断続的に問題が発生する](#intermittent-problems-with-new-microsoft-azure-virtual-machines)。
  - [Windows 10 バージョン 1709 のリモート デスクトップに接続するユーザーでビデオ再生の問題が発生する](#video-playback-issues-on-windows-10-version-1709)。
  - [読み取り専用ユーザー プロファイルを使用するユーザーが Windows 10 のリモート デスクトップに接続すると、デスクトップを共有できない。](#desktop-sharing-issues-on-windows-10)
  - [古いバージョンの Windows 10 を実行するクライアントを使用するユーザーが Windows 10 のリモート デスクトップに接続した場合、NLA が無効になっていると、パフォーマンスが低下する](#performance-issues-when-mixing-versions-of-windows-10-if-nla-is-disabled)
  - [ユーザーがリモート デスクトップ セッションで複数のアプリケーションを実行し、切断と再接続を頻繁に行うと、再接続時に黒い画面が発生する可能性がある。](#black-screen-issue)

### <a name="intermittent-problems-with-new-microsoft-azure-virtual-machines"></a>新しい Microsoft Azure 仮想マシンでの断続的な問題

この問題は、最近プロビジョニングされた仮想マシンに影響します。 ユーザーが仮想マシンに接続した後、リモート デスクトップ セッションでユーザーのすべての設定が正しく読み込まれないことがあります。

この問題を回避するには、仮想マシンから切断し、少なくとも 20 分間待ってから、再接続します。

この問題を解決するには、必要に応じて、次の更新プログラムを仮想マシンに適用します。

  - Windows 10 および Windows Server 2016: KB 4343884、[2018 年 8 月 30 日 — KB4343884 (OS ビルド 14393.2457)](https://support.microsoft.com/en-us/help/4343884/windows-10-update-kb4343884)
  - Windows Server 2012 R2KB 4343891、[2018 年 8 月 30 日 — KB4343891 (マンスリー ロールアップのプレビュー)](https://support.microsoft.com/en-us/help/4343891/windows-81-update-kb4343891)

### <a name="video-playback-issues-on-windows-10-version-1709"></a>Windows 10 バージョン 1709 でのビデオ再生の問題

この問題は、Windows 10 バージョン 1709 が実行されているリモート コンピューターにユーザーが接続すると発生します。 これらのユーザーが VMR9 (Video Mixing Renderer 9) コーデックを使ってビデオを再生すると、プレーヤーに黒いウィンドウだけが表示されます。

これは、Windows 10 バージョン 1709 での既知の問題です。 この問題は、Windows 10 バージョン 1703 では発生しません。

### <a name="desktop-sharing-issues-on-windows-10"></a>Windows 10 でのデスクトップ共有の問題

この問題は、ユーザーがキオスク シナリオのように読み取り専用のユーザー プロファイル (および関連するレジストリ ハイブ) を使用している場合に発生します。 このようなユーザーは、Windows 10 バージョン 1803 が実行されているリモート コンピューターに接続すると、自分のデスクトップを共有できません。

この問題を解決するには、Windows 10 更新プログラム 4340917、[2018 年 7 月 24 日 — KB4340917 (OS ビルド 17134.191)](https://support.microsoft.com/en-us/help/4340917/windows-10-update-kb4340917) を適用します。

### <a name="performance-issues-when-mixing-versions-of-windows-10-if-nla-is-disabled"></a>NLA が無効になっている場合に Windows 10 のバージョンが混在するときのパフォーマンスの問題

この問題は、NLA が無効になっているときに、Windows 10 が実行されているリモート デスクトップ クライアント コンピューターで異なるバージョンの Windows 10 が実行されているリモート デスクトップに接続すると発生します。 Windows 10 バージョン 1709 以前のバージョンが実行されているコンピューターのリモート デスクトップ クライアントのユーザーは、Windows 10 バージョン 1803 以降が実行されているリモート デスクトップに接続すると、パフォーマンスの低下が発生します。

これは、NLA が無効になっていると、古いクライアント コンピューターでは、Windows 10 バージョン 1803 以降に接続するときに、低速のプロトコルが使われるために発生します。

この問題を解決するには、KB 4340917、[2018 年 7 月 24 日 — KB4340917 (OS ビルド 17134.191)](https://support.microsoft.com/en-us/help/4340917/windows-10-update-kb4340917) を適用します。

### <a name="black-screen-issue"></a>黒い画面の問題

この問題は、Windows 8.0、Windows 8.1、Windows 10 RTM、および Windows Server 2012 R2 で発生します。 ユーザーは、リモート デスクトップで複数のアプリケーションを起動した後、セッションから切断します。 ユーザーは、定期的にリモート デスクトップに再接続してアプリケーションと対話し、再び切断します。 ある時点で、ユーザーが再接続すると、リモート デスクトップ セッションに黒い画面だけが表示されます。 ユーザーは、リモート コンピューターのコンソール (または RDSH サーバー コンソール) から、リモート デスクトップ セッションを終了する必要があります。 このアクションで、アプリケーションは停止されます。

この問題を解決するには、必要に応じて次の更新プログラムを適用します。

  - Windows 8 および Windows Server 2012: KB4103719、[2018 年 5 月 17 日 — KB4103719 (マンスリー ロールアップのプレビュー)](https://support.microsoft.com/en-us/help/4103719/windows-server-2012-update-kb4103719)
  - Windows 8.1 および Windows Server 2012 R2: KB4103724、[2018 年 5 月 17 日 — KB4103724 (マンスリー ロールアップのプレビュー)](https://support.microsoft.com/en-us/help/4103724/windows-81-update-kb4103724) および KB 4284863、[2018 年 6 月 21 日 — KB4284863 (マンスリー ロールアップのプレビュー)](https://support.microsoft.com/en-us/help/4284863/windows-81-update-kb4284863)
  - Windows 10:KB4284860、[2018 年 6 月 12 日 — KB4284860 (OS ビルド 10240.17889)](https://support.microsoft.com/en-us/help/4284860/windows-10-update-kb4284860) で修正されました
