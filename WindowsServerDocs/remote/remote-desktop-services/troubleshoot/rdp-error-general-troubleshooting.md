---
title: リモート デスクトップ接続の一般的なトラブルシューティング
description: リモートデスクトップ接続での "クラスが登録されていません" エラーのトラブルシューティング。
ms.reviewer: rklemen
ms.topic: troubleshooting
author: kaushika-msft
manager: dcscontentpm
ms.author: delhan
ms.date: 07/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: 03c3c8daa8dc4bea0e03ed285a98401f91cdf1cb
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857215"
---
# <a name="general-remote-desktop-connection-troubleshooting"></a>リモート デスクトップ接続の一般的なトラブルシューティング

リモート デスクトップ クライアントがリモート デスクトップに接続できず、しかし原因の特定に役立つメッセージや他の症状が提供されない場合は、以下の手順を使用します。

## <a name="check-the-status-of-the-rdp-protocol"></a>RDP プロトコルの状態を確認する

### <a name="check-the-status-of-the-rdp-protocol-on-a-local-computer"></a>ローカル コンピューターで RDP プロトコルの状態を確認する

ローカル コンピューターで RDP プロトコルの状態を確認および変更するには、「[リモート デスクトップを有効にする方法](https://docs.microsoft.com/windows-server/remote/remote-desktop-services/clients/remote-desktop-allow-access#how-to-enable-remote-desktop)」をご覧ください。

> [!NOTE]  
> リモート デスクトップのオプションを利用できない場合は、「[ローカル コンピューターでグループ ポリシー オブジェクト (GPO) が RDP をブロックしているかどうかを確認する](#check-whether-a-group-policy-object-gpo-is-blocking-rdp-on-a-local-computer)」をご覧ください。

### <a name="check-the-status-of-the-rdp-protocol-on-a-remote-computer"></a>リモート コンピューターで RDP プロトコルの状態を確認する

> [!IMPORTANT]  
> このセクションの手順には、慎重に従ってください。 レジストリに正しくない変更を加えると、重大な問題が発生する可能性があります。 レジストリの変更を開始する前に、[レジストリをバックアップ](https://support.microsoft.com/help/322756)して、何らかの問題が発生した場合に復元できるようにします。

リモート コンピューターで RDP プロトコルの状態を確認して変更するには、ネットワーク レジストリ接続を使います。

1. 最初に、 **[スタート]** メニューに移動し、 **[ファイル名を指定して実行]** を選択します。 表示されるテキストボックスに「**regedt32**」と入力します。
2. レジストリ エディターで、 **[ファイル]** 、 **[ネットワーク レジストリへの接続]** の順に選択します。
3. **[コンピューターの選択]** ダイアログ ボックスで、リモート コンピューターの名前を入力し、 **[名前の確認]** を選択してから、 **[OK]** を選択します。
4. **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server** に移動します。  
   ![fDenyTSConnections エントリが示されているレジストリ エディター](../media/troubleshoot-remote-desktop-connections/RegEntry_fDenyTSConnections.png)
   - **fDenyTSConnections** キーの値が **0** の場合、RDP は有効になっています。
   - **fDenyTSConnections** キーの値が **1** の場合、RDP は無効になっています。
5. RDP を有効にするには、**fDenyTSConnections** の値を **1** から **0** に変更します。

### <a name="check-whether-a-group-policy-object-gpo-is-blocking-rdp-on-a-local-computer"></a>ローカル コンピューターでグループ ポリシー オブジェクト (GPO) が RDP をブロックしているかどうかを確認する

ユーザー インターフェイスで RDP を有効にできない場合、または変更した後で **fDenyTSConnections** の値が **1** に戻る場合は、GPO によってコンピューター レベルの設定がオーバーライドされている可能性があります。

ローカル コンピューターでのグループ ポリシーの構成を確認するには、管理者としてコマンド プロンプト ウィンドウを開き、次のコマンドを入力します。

```cmd
gpresult /H c:\gpresult.html
```

このコマンドの終了後、gpresult.html を開きます。 **[コンピューターの構成] > [管理用テンプレート] > [Windows コンポーネント] > [リモート デスクトップ サービス] > [リモート デスクトップ セッション ホスト] > [接続]** で、 **[ユーザーがリモート デスクトップ サービスを使ってリモート接続することを許可する]** ポリシーを探します。

- このポリシーの設定が **[有効]** である場合、グループ ポリシーでは RDP 接続はブロックされていません。
- このポリシー設定が **[無効]** である場合は、 **[優勢な GPO]** を確認します。 これが、RDP 接続をブロックしている GPO です。
  ![ドメイン レベルの GPO の **RDP ブロック** で RDP が無効になっている gpresult.html のセグメントの例。](../media/troubleshoot-remote-desktop-connections/GPResult_RDSH_Connections_GP.png)
   
  ![**ローカル グループ ポリシー** で RDP が無効になっている gpresult.html のセグメントの例。](../media/troubleshoot-remote-desktop-connections/GPResult_RDSH_Connections_LGP.png)

### <a name="check-whether-a-gpo-is-blocking-rdp-on-a-remote-computer"></a>リモート コンピューターで GPO によって RDP がブロックされているかどうかを確認する

リモート コンピューターでグループ ポリシーの構成を確認するためのコマンドは、ローカル コンピューターの場合とほぼ同じです。

```cmd
gpresult /S <computer name> /H c:\gpresult-<computer name>.html
```

このコマンドによって生成されるファイル (**gpresult-<\<コンピューター名\>>.html**) では、ローカル コンピューター バージョン (**gpresult.html**) と同じ情報の形式が使われます。

### <a name="modifying-a-blocking-gpo"></a>ブロックしている GPO を変更する

グループ ポリシー オブジェクト エディター (GPE) およびグループ ポリシー管理コンソール (GPM) で、これらの設定を変更することができます。 グループ ポリシーの使い方について詳しくは、「[Advanced Group Policy Management](https://docs.microsoft.com/microsoft-desktop-optimization-pack/agpm/)」(高度なグループ ポリシーの管理) をご覧ください。

ブロックしているポリシーを変更するには、次のいずれかの方法を使います。

- GPE で、適切なレベルの GPO (ローカル、ドメインなど) にアクセスし、 **[コンピューターの構成]**  >  **[管理用テンプレート]**  >  **[Windows コンポーネント]**  >  **[リモート デスクトップ サービス]**  >  **[リモート デスクトップ セッション ホスト]**  >  **[接続]**  >  **[ユーザーがリモート デスクトップ サービスを使ってリモート接続することを許可する]** に移動します。  
   1. ポリシーを **[有効]** または **[未構成]** に設定します。
   2. 影響を受けるコンピューターで、管理者としてコマンド プロンプト ウィンドウを開き、**gpupdate /force** コマンドを実行します。
- GPM で、影響を受けるコンピューターにブロック ポリシーを適用している組織単位 (OU) に移動し、OU からこのポリシーを削除します。

## <a name="check-the-status-of-the-rdp-services"></a>RDP サービスの状態を確認する

ローカル (クライアント) コンピューターとリモート (ターゲット) コンピューターの両方で、次のサービスが実行されている必要があります。

- リモート デスクトップ サービス (TermService)
- リモート デスクトップ サービス ユーザー モード ポート リダイレクター (UmRdpService)

サービス MMC スナップインを使って、ローカル環境またはリモート環境のサービスを管理できます。 PowerShell を使用して、ローカル環境またはリモート環境 (リモート PowerShell コマンドレットを受け付けるようにリモート コンピューターが構成されている場合) のサービスを管理することもできます。

![サービス MMC スナップインでのリモート デスクトップ サービス。 既定のサービス設定は変更しないでください。](../media/troubleshoot-remote-desktop-connections/RDSServiceStatus.png)

いずれかのコンピューターで、1 つまたは両方のサービスが実行されていない場合は、開始します。

> [!NOTE]  
> リモート デスクトップ サービス サービスを開始する場合、 **[はい]** をクリックすると、リモート デスクトップ サービス ユーザー モード ポート リダイレクター サービスが自動的に再起動します。

## <a name="check-that-the-rdp-listener-is-functioning"></a>RDP リスナーが機能していることを確認する

> [!IMPORTANT]  
> このセクションの手順には、慎重に従ってください。 レジストリに正しくない変更を加えると、重大な問題が発生する可能性があります。 レジストリの変更を開始する前に、[レジストリをバックアップ](https://support.microsoft.com/help/322756)して、何らかの問題が発生した場合に復元できるようにします。

### <a name="check-the-status-of-the-rdp-listener"></a>RDP リスナーの状態を確認する

この手順では、管理者アクセス許可を持つ PowerShell インスタンスを使います。 ローカル コンピューターでは、管理者アクセス許可を持つコマンド プロンプトを使うこともできます。 ただし、この手順では、ローカルとリモートの両方で同じコマンドレットが動作するため、PowerShell を使います。

1. リモート コンピューターに接続するために、次のコマンドレットを実行します。

   ```powershell
   Enter-PSSession -ComputerName <computer name>
   ```

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
   1. 既存のレジストリ エントリをバックアップするには、次のコマンドレットを入力します。  
   
      ```powershell  
      cmd /c 'reg export "HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-tcp" C:\Rdp-tcp-backup.reg'   
      ```  
   

   2. 既存のレジストリ エントリを削除するには、次のコマンドレットを入力します。  
   
      ```powershell  
      Remove-Item -path 'HKLM:\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-tcp' -Recurse -Force  
      ```
   
   3. 新しいレジストリ エントリをインポートしてサービスを再起動するには、次のコマンドレットを入力します。  
   
      ```powershell  
      cmd /c 'regedit /s c:\<filename>.reg'  
      Restart-Service TermService -Force  
      ```
      
      \<filename\> は、エクスポートした .reg ファイルの名前に置き換えます。

6. 再びリモート デスクトップ接続を試みて、構成をテストします。 まだ接続できない場合は、影響を受けるコンピューターを再起動します。
7. それでも接続できない場合は、[RDP の自己署名証明書の状態を確認](#check-the-status-of-the-rdp-self-signed-certificate)します。

### <a name="check-the-status-of-the-rdp-self-signed-certificate"></a>RDP の自己署名証明書の状態を確認する

1. まだ接続できない場合は、証明書 MMC スナップインを開きます。 管理する証明書ストアの選択を求めるメッセージが表示されたら、 **[コンピューター アカウント]** を選択し、影響を受けるコンピューターを選択します。
2. **[証明書]** フォルダーの **[リモート デスクトップ]** で、RDP 自己署名証明書を削除します。 
    ![MMC 証明書スナップインでのリモート デスクトップ証明書。](../media/troubleshoot-remote-desktop-connections/MMCCert_Delete.png)
3. 影響を受けるコンピューターで、リモート デスクトップ サービスのサービスを再起動します。
4. 証明書スナップインを最新の情報に更新します。
5. RDP 自己署名証明書が再作成されていない場合は、[MachineKeys フォルダーのアクセス許可を確認](#check-the-permissions-of-the-machinekeys-folder)します。

### <a name="check-the-permissions-of-the-machinekeys-folder"></a>MachineKeys フォルダーのアクセス許可を確認する

1. 影響を受けるコンピューターでエクスプローラーを開き、**C:\\ProgramData\\Microsoft\\Crypto\\RSA\\** に移動します。
2. **MachineKeys** を右クリックし、 **[プロパティ]** 、 **[セキュリティ]** 、 **[詳細設定]** の順に選択します。
3. 次のアクセス許可が構成されていることを確認します。
      - Builtin\\Administrators: フル コントロール
      - Everyone: 読み取り、書き込み

## <a name="check-the-rdp-listener-port"></a>RDP リスナー ポートを確認する

ローカル (クライアント) コンピューターとリモート (ターゲット) コンピューターの両方で、RDP リスナーがポート 3389 でリッスンしている必要があります。 他のアプリケーションがこのポートを使っていてはなりません。

> [!IMPORTANT]  
> このセクションの手順には、慎重に従ってください。 レジストリに正しくない変更を加えると、重大な問題が発生する可能性があります。 レジストリの変更を開始する前に、[レジストリをバックアップ](https://support.microsoft.com/help/322756)して、何らかの問題が発生した場合に復元できるようにします。

RDP ポートを確認または変更するには、レジストリ エディターを使います。

1. [スタート] メニューに移動し、 **[ファイル名を指定して実行]** を選択して、表示されるテキストボックスに「**regedt32**」と入力します。
      - リモート コンピューターに接続するには、 **[ファイル]** 、 **[ネットワーク レジストリへの接続]** の順に選択します。
      - **[コンピューターの選択]** ダイアログ ボックスで、リモート コンピューターの名前を入力し、 **[名前の確認]** を選択してから、 **[OK]** を選択します。
2. レジストリを開き、**HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Control\\Terminal Server\\WinStations\\\<listener\>** に移動します。 
    ![RDP プロトコルの PortNumber サブキー。](../media/troubleshoot-remote-desktop-connections/RegEntry_PortNumber.png)
3. **PortNumber** の値が **3389** 以外の場合は、**3389** に変更します。 
   > [!IMPORTANT]  
    > 別のポートを使ってリモート デスクトップ サービスを動作させることができます。 ただし、このようにすることはお勧めしません。 この記事では、その種類の構成のトラブルシューティング方法については説明しません。
4. ポート番号を変更した後、リモート デスクトップ サービスのサービスを再起動します。

### <a name="check-that-another-application-isnt-trying-to-use-the-same-port"></a>別のアプリケーションが同じポートを使おうとしていないことを確認する

この手順では、管理者アクセス許可を持つ PowerShell インスタンスを使います。 ローカル コンピューターでは、管理者アクセス許可を持つコマンド プロンプトを使うこともできます。 ただし、この手順では、ローカルとリモートで同じコマンドレットが動作するため、PowerShell を使います。

1. PowerShell ウィンドウを開きます。 リモート コンピューターに接続するには、「**Enter-PSSession -ComputerName <\<コンピューター名\>>** 」と入力します。
2. 次のコマンドを入力します。  
   
     ```powershell  
    cmd /c 'netstat -ano | find "3389"'  
    ```
  
    ![netstat コマンドでは、ポートおよびそれをリッスンしているサービスのリストが生成されます。](../media/troubleshoot-remote-desktop-connections/WPS_netstat.png)
3. 状態が「**LISTENING**」の TCP ポート 3389 (または割り当てられた RDP ポート) のエントリを探します。 
    > [!NOTE]  
   > そのポートを使用しているプロセスまたはサービスのプロセス ID (PID) が、[PID] 列の下に表示されます。
4. ポート 3389 (または、割り当てられている RDP ポート) を使っているアプリケーションを確認するには、次のコマンドを入力します。  
   
     ```powershell  
    cmd /c 'tasklist /svc | find "<pid listening on 3389>"'  
    ```  
  
    ![tasklist コマンドでは、特定のプロセスの詳細が報告されます。](../media/troubleshoot-remote-desktop-connections/WPS_tasklist.png)
5. ポートに関連付けられている PID 番号 (**netstat** の出力からの情報) のエントリを探します。 その PID に関連付けられているサービスまたはプロセスが、右側の列に表示されます。
6. リモート デスクトップ サービス (TermServ.exe) 以外のアプリケーションまたはサービスによってそのポートが使われている場合は、次のいずれかの方法を使って競合を解決できます。
      - 他のアプリケーションまたはサービスを、別のポートを使うように構成します (推奨)。
      - 他のアプリケーションまたはサービスをアンインストールします。
      - 別のポートを使うように RDP を構成した後、リモート デスクトップ サービスのサービスを再起動します (推奨されません)。

### <a name="check-whether-a-firewall-is-blocking-the-rdp-port"></a>ファイアウォールで RDP ポートがブロックされているかどうかを確認する

ポート 3389 を使って、影響を受けるコンピューターに到達できるかどうかをテストするには、**psping** ツールを使います。

1. 影響を受けていない別のコンピューターにアクセスし、<https://live.sysinternals.com/psping.exe> から **psping** をダウンロードします。
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
