---
title: Windows で SMBv1、SMBv2、および SMBv3 を検出、有効化、および無効化する方法
description: Windows のクライアント環境とサーバー環境で、サーバーメッセージブロックプロトコル (SMBv1、SMBv2、および SMBv3) を有効または無効にする方法について説明します。
author: Deland-Han
manager: dcscontentpm
ms.topic: article
ms.author: delhan
ms.date: 12/25/2019
ms.openlocfilehash: dd2f4c6b6bb17231ac04b3344e9a39df2cad79d0
ms.sourcegitcommit: fb808a6fc851a3e5c47e6a7654366145d2f19554
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/12/2020
ms.locfileid: "84740645"
---
# <a name="how-to-detect-enable-and-disable-smbv1-smbv2-and-smbv3-in-windows"></a>Windows で SMBv1、SMBv2、および SMBv3 を検出、有効化、および無効化する方法

## <a name="summary"></a>まとめ

この記事では、SMB クライアントおよびサーバーコンポーネントで、サーバーメッセージブロック (SMB) バージョン 1 (SMBv1)、SMB バージョン 2 (SMBv2)、および SMB バージョン 3 (SMBv3) を有効または無効にする方法について説明します。 

> [!IMPORTANT]
> SMBv2 または SMBv3 を無効にし**ない**ことをお勧めします。 一時的なトラブルシューティングメジャーとして SMBv2 または SMBv3 のみを無効にします。 SMBv2 または SMBv3 は無効のままにしないでください。  

Windows 7 と Windows Server 2008 R2 で SMBv2 を無効にすると、次の機能が非アクティブになります。 
 
- 複合要求-複数の SMB 2 要求を1つのネットワーク要求として送信できます。    
- 読み取りと書き込みが大きい-より高速なネットワークの使用    
- フォルダーとファイルのプロパティのキャッシュ-クライアントはフォルダーとファイルのローカルコピーを保持します。    
- 持続性のあるハンドル-一時的な切断が発生した場合に、接続がサーバーに透過的に再接続することを許可します。    
- 強化されたメッセージ署名-HMAC SHA-256 MD5 をハッシュアルゴリズムと置き換える    
- ファイル共有のスケーラビリティの向上-サーバーごとにユーザー、共有、開いているファイルの数が大幅に増加しました。    
- シンボリックリンクのサポート    
- クライアント oplock リースモデル-クライアントとサーバーの間で転送されるデータを制限し、待機時間の長いネットワークでのパフォーマンスを向上させ、SMB サーバーのスケーラビリティを向上させます。    
- 大きな MTU のサポート-10 gigabye (GB) イーサネットの完全な使用    
- エネルギー効率の向上-サーバーに対してファイルを開いているクライアントをスリープ状態にすることができます。    

Windows 8、Windows 8.1、Windows 10、Windows Server 2012、Windows Server 2012 R2、Windows Server 2016、および Windows Server 2019 では、SMBv3 を無効にすると、次の機能 (および前の一覧に記載されている SMBv2 機能) が非アクティブになります。 
 
- 透過フェールオーバー-メンテナンス中またはフェールオーバー中にクラスターノードを中断することなくクライアントが再接続する    
- Scale Out-すべてのファイルクラスターノード上の共有データへの同時アクセス     
- マルチチャネル-クライアントとサーバーの間で複数のパスを使用できる場合のネットワーク帯域幅とフォールトトレランスの集約  
- SMB ダイレクト–低待機時間と低い CPU 使用率で、非常に高いパフォーマンスを実現する RDMA ネットワークサポートを追加します。    
- 暗号化–エンドツーエンドの暗号化を提供し、信頼されていないネットワークの傍受から保護します。    
- ディレクトリリース-ブランチオフィスのキャッシュによってアプリケーションの応答時間が向上します。    
- パフォーマンスの最適化-小規模なランダム読み取り/書き込み i/o の最適化

##  <a name="more-information"></a>詳細情報

SMBv2 プロトコルは、Windows Vista および Windows Server 2008 で導入されました。

SMBv3 プロトコルは、Windows 8 および Windows Server 2012 で導入されました。

SMBv2 および SMBv3 機能の機能の詳細については、次の記事を参照してください。

[サーバー メッセージ ブロックの概要](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831795(v=ws.11))

[SMB の新機能](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff625695(v=ws.10))  

## <a name="how-to-gracefully-remove-smb-v1-in-windows-81-windows-10-windows-2012-r2-windows-server-2016-and-windows-server-2019"></a>Windows 8.1、Windows 10、Windows 2012 R2、Windows Server 2016、および Windows Server 2019 で SMB v1 を適切に削除する方法

#### <a name="powershell-methods"></a>PowerShell メソッド

##### <a name="smb-v1-client-and-server"></a>SMB v1 (クライアントとサーバー)

- 識別 

  ```PowerShell
  Get-WindowsFeature FS-SMB1
  ```

- 切り替える 

  ```PowerShell
  Disable-WindowsOptionalFeature -Online -FeatureName smb1protocol
  ```

- 有効にする: 

  ```PowerShell
  Enable-WindowsOptionalFeature -Online -FeatureName smb1protocol
  ```

#### <a name="windows-server-2012-r2-windows-server-2016-windows-server-2019-server-manager-method-for-disabling-smb"></a>Windows Server 2012 R2、Windows Server 2016、Windows Server 2019: サーバーマネージャー SMB を無効にする方法

##### <a name="smb-v1"></a>SMB v1

![サーバーマネージャー-ダッシュボードの方法](media/detect-enable-and-disable-smbv1-v2-v3-1.png)

#### <a name="windows-81-and-windows-10-powershell-method"></a>Windows 8.1 と Windows 10: PowerShell メソッド

##### <a name="smb-v1-protocol"></a>SMB v1 プロトコル

- 識別 
  
  ```PowerShell
  Get-WindowsOptionalFeature –Online –FeatureName SMB1Protocol
  ```

- 切り替える 

  ```PowerShell
  Disable-WindowsOptionalFeature -Online -FeatureName SMB1Protocol
  ```

- 有効にする: 

  ```PowerShell
  Enable-WindowsOptionalFeature -Online -FeatureName SMB1Protocol
  ```

##### <a name="smb-v2v3protocol-only-disables-smb-v2v3-server"></a>SMB v2/v3 プロトコル (SMB v2/v3 サーバーのみを無効にする)

- 識別 
  
  ```PowerShell
  Get-SmbServerConfiguration | Select EnableSMB2Protocol
  ```

- 切り替える 
  
  ```PowerShell
  Set-SmbServerConfiguration –EnableSMB2Protocol $false
  ```

- 有効にする:

  ```PowerShell
  Set-SmbServerConfiguration –EnableSMB2Protocol $true
  ```

#### <a name="windows-81-and-windows-10-add-or-remove-programs-method"></a>Windows 8.1 と Windows 10: プログラムの追加と削除の方法

![プログラムの追加と削除のクライアントメソッド](media/detect-enable-and-disable-smbv1-v2-v3-2.png)

## <a name="how-to-detect-status-enable-and-disable-smb-protocols-on-the-smb-server"></a>SMB サーバーで状態を検出し、SMB プロトコルを有効または無効にする方法

### <a name="for-windows-8-and-windows-server-2012"></a>Windows 8 および Windows Server 2012 の場合

Windows 8 と Windows Server 2012 には、新しい**SMBServerConfiguration** windows PowerShell コマンドレットが導入されています。 コマンドレットを使用すると、サーバーコンポーネントの SMBv1、SMBv2、および SMBv3 プロトコルを有効または無効にすることができます。  

> [!NOTE]   
> Windows 8 または Windows Server 2012 で SMBv2 を有効または無効にすると、SMBv3 も有効または無効になります。 これらのプロトコルは同じスタックを共有するため、この動作が発生します。     

**SMBServerConfiguration**コマンドレットを実行した後に、コンピューターを再起動する必要はありません。 

##### <a name="smb-v1-on-smb-server"></a>Smb サーバー上の SMB v1

- 識別 
  
  ```PowerShell
  Get-SmbServerConfiguration | Select EnableSMB1Protocol
  ```

- 切り替える 

  ```PowerShell
  Set-SmbServerConfiguration -EnableSMB1Protocol $false
  ```

- 有効にする: 
  ```PowerShell
  Set-SmbServerConfiguration -EnableSMB1Protocol $true
  ```

詳細については、「 [Microsoft でのサーバーストレージ](https://techcommunity.microsoft.com/t5/Storage-at-Microsoft/Stop-using-SMB1/ba-p/425858)」を参照してください。 
##### <a name="smb-v2v3-on-smb-server"></a>Smb サーバー上の SMB v2/v3

- 識別

  ```PowerShell
  Get-SmbServerConfiguration | Select EnableSMB2Protocol
  ```

- 切り替える 
  
  ```PowerShell
  Set-SmbServerConfiguration -EnableSMB2Protocol $false
  ```

- 有効にする:
  
  ```PowerShell
  Set-SmbServerConfiguration -EnableSMB2Protocol $true
  ```

### <a name="for-windows-7-windows-server-2008-r2-windows-vista-and-windows-server-2008"></a>Windows 7、Windows Server 2008 R2、Windows Vista、および Windows Server 2008 の場合

Windows 7、Windows Server 2008 R2、Windows Vista、または Windows Server 2008 を実行している SMB サーバーで SMB プロトコルを有効または無効にするには、Windows PowerShell またはレジストリエディターを使用します。 

#### <a name="powershell-methods"></a>PowerShell メソッド

> [!NOTE]
> この方法を行うには、powershell 2.0 以降のバージョンが必要です。

##### <a name="smb-v1-on-smb-server"></a>Smb サーバー上の SMB v1

識別

```PowerShell
Get-Item HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters | ForEach-Object {Get-ItemProperty $_.pspath}
```

既定の構成 = 有効 (レジストリキーは作成されません)。そのため、SMB1 値は返されません。

切り替える

```PowerShell
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters" SMB1 -Type DWORD -Value 0 –Force
```

有効にする:  

```PowerShell
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters" SMB1 -Type DWORD -Value 1 –Force
```  

**メモ**これらの変更を行った後、コンピューターを再起動する必要があります。 詳細については、「 [Microsoft でのサーバーストレージ](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/)」を参照してください。 
##### <a name="smb-v2v3-on-smb-server"></a>Smb サーバー上の SMB v2/v3

識別  

```PowerShell
Get-ItemProperty HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters | ForEach-Object {Get-ItemProperty $_.pspath} 
```

切り替える

```PowerShell
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters" SMB2 -Type DWORD -Value 0 –Force  
```

有効にする:

```PowerShell
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters" SMB2 -Type DWORD -Value 1 –Force 
```

> [!NOTE]
> これらの変更を行った後、コンピューターを再起動する必要があります。 

#### <a name="registry-editor"></a>レジストリ エディター

> [!IMPORTANT]
> 慎重にこのセクションの手順に従います。 レジストリを正しく変更しないと、重大な問題が発生する可能性があります。 変更する前に、問題が発生した場合に[復元するためにレジストリをバックアップ](https://support.microsoft.com/help/322756)します。
 
SMB サーバーで SMBv1 を有効または無効にするには、次のレジストリキーを構成します。

2. レジストリ サブキー **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters** を探し、クリックして選択します。

```
Registry entry: SMB1
REG_DWORD: 0 = Disabled
REG_DWORD: 1 = Enabled
Default: 1 = Enabled (No registry key is created)
```

SMB サーバーで SMBv2 を有効または無効にするには、次のレジストリキーを構成します。 

2. レジストリ サブキー **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters** を探し、クリックして選択します。

```
Registry entry: SMB2
REG_DWORD: 0 = Disabled
REG_DWORD: 1 = Enabled
Default: 1 = Enabled (No registry key is created) 
```

> [!NOTE]
> これらの変更を行った後、コンピューターを再起動する必要があります。 

## <a name="how-to-detect-status-enable-and-disable-smb-protocols-on-the-smb-client"></a>SMB クライアントで状態を検出し、SMB プロトコルを有効または無効にする方法

### <a name="for-windows-vista-windows-server-2008-windows-7-windows-server-2008-r2-windows-8-and-windows-server-2012"></a>Windows Vista、Windows Server 2008、Windows 7、Windows Server 2008 R2、Windows 8、および Windows Server 2012 の場合

> [!NOTE]
> Windows 8 または Windows Server 2012 で SMBv2 を有効または無効にすると、SMBv3 も有効または無効になります。 これらのプロトコルは同じスタックを共有するため、この動作が発生します。 

##### <a name="smb-v1-on-smb-client"></a>Smb クライアント上の SMB v1

- Detect
  
  ```cmd
  sc.exe qc lanmanworkstation
  ```

- 切り替える
  
  ```cmd
  sc.exe config lanmanworkstation depend= bowser/mrxsmb20/nsi
  sc.exe config mrxsmb10 start= disabled
  ```

- 有効にする:

  ```cmd
  sc.exe config lanmanworkstation depend= bowser/mrxsmb10/mrxsmb20/nsi
  sc.exe config mrxsmb10 start= auto
  ```

詳細については、「 [Microsoft でのサーバー記憶域](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/)」を参照してください。 
##### <a name="smb-v2v3-on-smb-client"></a>Smb クライアント上の SMB v2/v3

- 識別

  ```cmd
  sc.exe qc lanmanworkstation
  ```

- 切り替える

  ```cmd
  sc.exe config lanmanworkstation depend= bowser/mrxsmb10/nsi
  sc.exe config mrxsmb20 start= disabled 
  ```

- 有効にする:

  ```cmd
  sc.exe config lanmanworkstation depend= bowser/mrxsmb10/mrxsmb20/nsi
  sc.exe config mrxsmb20 start= auto
  ```

> [!NOTE]
> - これらのコマンドは、管理者特権のコマンドプロンプトで実行する必要があります。    
> - これらの変更を行った後、コンピューターを再起動する必要があります。    
 

## <a name="disable-smbv1-server-with-group-policy"></a>グループポリシーで SMBv1 サーバーを無効にする

この手順では、レジストリに次の新しい項目を構成します。

2. レジストリ サブキー **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters** を探し、クリックして選択します。 

- レジストリエントリ: **SMB1** 
- REG_DWORD: **0** = 無効   

グループポリシーを使用してこれを構成するには、次の手順を実行します。
 
1. [**グループ ポリシー管理コンソール**] を開きます。 新しい基本設定項目を含むグループ ポリシー オブジェクト (GPO) を右クリックして、**[編集]** をクリックします。

2. コンソールツリーの [**コンピューターの構成**] の下にある [**基本設定**] フォルダーを展開し、[ **Windows の設定**] フォルダーを展開します。

3. **レジストリ**ノードを右クリックして [**新規作成**] をポイントし、[**レジストリ項目**] を選択します。

   ![レジストリ-新規-レジストリ項目](media/detect-enable-and-disable-smbv1-v2-v3-3.png)    
 
[**新しいレジストリのプロパティ**] ダイアログボックスで、次のように選択します。 
 
- **操作**: 作成    
- **Hive**: HKEY_LOCAL_MACHINE    
- **キーのパス**: SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters    
- **値の名前**: SMB1    
- **値の型**: REG_DWORD    
- **値のデータ**: 0    
 
![[新しいレジストリのプロパティ]-[全般]](media/detect-enable-and-disable-smbv1-v2-v3-4.png)

これにより、SMBv1 サーバーコンポーネントが無効になります。 このグループポリシーは、ドメイン内のすべての必要なワークステーション、サーバー、およびドメインコントローラーに適用する必要があります。

> [!NOTE]
>また、サポートされていないオペレーティングシステムや、Windows XP などの選択した除外を除外するように、  [WMI フィルター](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc947846(v=ws.10))を設定することもできます。

> [!IMPORTANT]
> 以前のバージョンの Windows XP または以前の Linux およびサードパーティ製のシステム (SMBv2 または SMBv3 をサポートしていないシステム) に対してこれらの変更を行う場合は、SMB v1 が無効になっている SYSVOL または他のファイル共有にアクセスする必要があることに注意してください。     

## <a name="disable-smbv1-client-with-group-policy"></a>グループポリシーを使用した SMBv1 クライアントの無効化

SMBv1 クライアントを無効にするには、 **MRxSMB10**の開始を無効にするために、サービスのレジストリキーを更新する必要があります。 **MRxSMB10**の依存関係は、 **LanmanWorkstation**のエントリから削除する必要があります。これにより、最初に**MRxSMB10**を開始することなく、正常に開始できるようになります。

これにより、レジストリ内の次の2つの項目の既定値が更新され、置き換えられます。 

**HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\services\mrxsmb10** 

レジストリエントリ:**開始**REG_DWORD: **4**= 無効

**HKEY_LOCAL_MACHINE \SYSTEM\CurrentControlSet\Services\LanmanWorkstation** 

レジストリエントリ:**依存関係 Onservice** REG_MULTI_SZ: **"ブラウザー"、"MRxSmb20"、"NSI"**   

> [!NOTE]
> 既定で含まれる MRxSMB10 は、依存関係として削除されます。

グループポリシーを使用してこれを構成するには、次の手順を実行します。
 
1. [**グループ ポリシー管理コンソール**] を開きます。 新しい基本設定項目を含むグループ ポリシー オブジェクト (GPO) を右クリックして、**[編集]** をクリックします。

2. コンソールツリーの [**コンピューターの構成**] の下にある [**基本設定**] フォルダーを展開し、[ **Windows の設定**] フォルダーを展開します。

3. **レジストリ**ノードを右クリックして [**新規作成**] をポイントし、[**レジストリ項目**] を選択します。    

4. [**新しいレジストリのプロパティ**] ダイアログボックスで、次のように選択します。 
 
   - **操作**: 更新
   - **Hive**: HKEY_LOCAL_MACHINE
   - **キーのパス**: SYSTEM\CurrentControlSet\services\mrxsmb10
   - **値の名前**: Start
   - **値の型**: REG_DWORD
   - **値のデータ**: 4
 
   ![開始プロパティ-全般](media/detect-enable-and-disable-smbv1-v2-v3-5.png)

5. 次に、無効にしたばかりの**MRxSMB10**に対する依存関係を削除します。

   [**新しいレジストリのプロパティ**] ダイアログボックスで、次のように選択します。 
 
   - **操作**: 置換
   - **Hive**: HKEY_LOCAL_MACHINE
   - **キーのパス**: SYSTEM\CurrentControlSet\Services\LanmanWorkstation
   - **値の名前**: 依存関係 onservice
   - **値の型**: REG_MULTI_SZ 
   - **値のデータ**:
      - ブラウザー
      - MRxSmb20
      - NSI
 
   > [!NOTE]
   > これら3つの文字列には、箇条書きは含まれません (次のスクリーンショットを参照してください)。

   ![依存関係 Onservice のプロパティ](media/detect-enable-and-disable-smbv1-v2-v3-6.png) 

   既定値には、多くのバージョンの Windows の**MRxSMB10**が含まれています。したがって、この複数値の文字列で置き換えることにより、 **LanmanServer**の依存関係として**MRxSMB10**を削除し、4つの既定値から上記の3つの値だけに移動することが有効になります。

   > [!NOTE]
   > グループポリシー管理コンソールを使用する場合は、引用符またはコンマを使用する必要はありません。 個々の行に各エントリを入力するだけです。

6. SMB v1 の無効化を完了するには、対象のシステムを再起動してください。

### <a name="summary"></a>まとめ

すべての設定が同じグループポリシーオブジェクト (GPO) に含まれている場合、グループポリシーの管理には次の設定が表示されます。

![グループポリシー管理エディター-レジストリ](media/detect-enable-and-disable-smbv1-v2-v3-7.png) 

### <a name="testing-and-validation"></a>テストと検証

これらの構成が完了したら、ポリシーをレプリケートして更新できるようにします。 テストに必要な場合は、コマンドプロンプトで**gpupdate/force**を実行し、対象のコンピューターを確認して、レジストリ設定が正しく適用されていることを確認します。 環境内の他のすべてのシステムで SMB v2 と SMB v3 が機能していることを確認します。

> [!NOTE]
> 必ず、ターゲットシステムを再起動してください。
