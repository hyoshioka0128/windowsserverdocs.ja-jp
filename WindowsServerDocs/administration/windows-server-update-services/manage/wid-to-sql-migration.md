---
title: (Windows Internal Database) から WSUS データベースを移行する WID to SQL
description: Windows Server Update Service (WSUS) のトピックでは、SQL Server のローカルまたはリモート インスタンスに Windows Internal Database インスタンスから、WSUS データベース (SUSDB) を移行する方法。
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-wsus
ms.tgt_pltfrm: na
ms.topic: get-started article
ms.assetid: 90e3464c-49d8-4861-96db-ee6f8a09g7dr
author: coreyp-at-msft
ms.author: coreyp
manager: dougkim
ms.date: 07/25/2018
ms.openlocfilehash: 9015bbc54a4c4bda0f691b79dbb7d3ba8ddbc4a1
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66439894"
---
>適用対象:Windows Server 2012、Windows Server 2012 R2、Windows Server 2016

# <a name="migrating-the-wsus-database-from-wid-to-sql"></a>WID から SQL への WSUS データベースの移行

SQL Server のローカルまたはリモート インスタンスに、Windows Internal Database インスタンスからの WSUS データベース (SUSDB) に移行するのに、次の手順を使用します。

## <a name="prerequisites"></a>前提条件

- SQL インスタンス。 既定値は、この**MSSQLServer**またはカスタムのインスタンス。
- SQL Server Management Studio
- WID の役割がインストールされた WSUS
- IIS (これが通常含まれる WSUS サーバー マネージャーからインストールする場合)。 インストールされていない、する必要があります。

## <a name="migrating-the-wsus-database"></a>WSUS データベースを移行します。

### <a name="stop-the-iis-and-wsus-services-on-the-wsus-server"></a>WSUS サーバーで IIS と WSUS サービスを停止します。

(管理者特権で)、PowerShell から次のコマンドを実行します。

```powershell
    Stop-Service IISADMIN
    Stop-Service WsusService
```

### <a name="detach-susdb-from-the-windows-internal-database"></a>SUSDB Windows 内部データベースからのデタッチします。

#### <a name="using-sql-management-studio"></a>SQL Management Studio を使用します。

1. 右クリックして**SUSDB** - &gt; **タスク** - &gt;クリックして**デタッチ**: ![image1](images/image1.png)
2. 確認**既存の接続を削除** をクリック**OK** (アクティブな接続が存在しない場合は省略可能)。
    ![image2](images/image2.png)

#### <a name="using-command-prompt"></a>コマンド プロンプトを使用

> [!IMPORTANT]
> 次の手順を使用して Windows Internal Database インスタンスから、WSUS データベース (SUSDB) を切断する方法を表示する、 **sqlcmd**ユーティリティ。 詳細については、 **sqlcmd**ユーティリティを参照してください[sqlcmd ユーティリティ](https://go.microsoft.com/fwlink/?LinkId=81183)します。
> 1. 管理者特権でコマンド プロンプトを開きます
> 2. 使用して Windows Internal Database インスタンスからデタッチ WSUS データベース (SUSDB) には、次の SQL コマンドを実行、 **sqlcmd**ユーティリティ。

```batchfile
        sqlcmd -S \\.\pipe\Microsoft##WID\tsql\query
        use master
        GO
        alter database SUSDB set single_user with rollback immediate
        GO
        sp_detach_db SUSDB
        GO
```

### <a name="copy-the-susdb-files-to-the-sql-server"></a>SUSDB ファイルを SQL Server にコピーします。

1. コピー **SUSDB.mdf**と**SUSDB\_log.ldf** WID データ フォルダーから ( **%systemdrive%** \** * * Windows\WID\Data) SQL インスタンスのデータフォルダー。

> [!TIP]
> たとえば、SQL インスタンスのフォルダーが**C:\Program files \microsoft SQL Server\MSSQL12 します。MSSQLSERVER\MSSQL**、WID データ フォルダーと**C:\Windows\WID\Data、** SUSDB ファイルのコピー **C:\Windows\WID\Data**に**C:\Program files \microsoft SQL Server\MSSQL12. します。MSSQLSERVER\MSSQL\Data**

### <a name="attach-susdb-to-the-sql-instance"></a>SUSDB を SQL インスタンスにアタッチします。

1. **SQL Server Management Studio**下で、**インスタンス**ノードを右クリックして**データベース**、順にクリックします**アタッチ**。
    ![image3](images/image3.png)
2. **データベースのアタッチ**ボックスで、**アタッチするデータベース**、 をクリックして、**追加**ボタンをクリックし、検索、 **SUSDB.mdf**ファイル (からコピーしますWID フォルダー)、順にクリックします**OK**します。
    ![image4](images/image4.png) ![image5](images/image5.png)

> [!TIP]
> これが実行することも Transact-sql を使用します。  参照してください、 [SQL データベースをアタッチするドキュメント](https://docs.microsoft.com/sql/relational-databases/databases/attach-a-database)手順については、します。
>
> 例 (前の例からのパスを使用):
> ```sql
>    USE master;
>    GO
>    CREATE DATABASE SUSDB
>    ON
>        (FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Data\SUSDB.mdf'),
>        (FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Log\SUSDB_Log.ldf')
>        FOR ATTACH;
>    GO
>```

### <a name="verify-sql-server-and-database-logins-and-permissions"></a>SQL Server データベースのログインやアクセス許可を確認します。

#### <a name="sql-server-login-permissions"></a>SQL Server ログイン権限

後、SUSDB をアタッチするには、ことを確認します**NT authority \network SERVICE**次の手順を実行して、SQL Server のインスタンスにログインの権限します。

1. SQL Server Management Studio に移動します。
2. インスタンスを開く
3. クリックして**セキュリティ**
4. クリックして**ログイン**

**NT authority \network SERVICE**アカウントの一覧を表示する必要があります。 そうでない場合は、新しいログイン名を追加することで追加する必要があります。

> [!IMPORTANT]
> 形式で、WSUS サーバーのコンピューター アカウントを一覧表示する SQL インスタンスが WSUS から別のコンピューター上にある場合は、 **[FQDN]\\[WSUSComputerName] $** します。  場合は、次の手順を使用して、追加することができます、置き換える**NT authority \network SERVICE** 、WSUS サーバーのコンピューター アカウントを使用して ( **[FQDN]\\[WSUSComputerName] $** )なります***に加えて***に権限を付与**NT authority \network SERVICE**

##### <a name="adding-nt-authoritynetwork-service-and-granting-it-rights"></a>NT authority \network SERVICE を追加して、許可の権限します。

1. 右クリックして**ログイン**クリック**新しいログインしています.**
    ![image6](images/image6.png)
2. **全般**ページで入力します、**ログイン名**(**NT authority \network SERVICE**)、設定、**既定のデータベース**SUSDB にします。
    ![image7](images/image7.png)
3. **サーバーの役割**ことを確認 ページで、**パブリック**と**sysadmin**が選択されています。
    ![image8](images/image8.png)
4. **ユーザー マッピング**ページ。
    - **このログインにマップされたユーザー**: 選択**SUSDB**
    - **データベース ロールのメンバーシップ。SUSDB**は、次のチェックを確認します。
        - **パブリック**
        - **webService** ![image9](images/image9.png)
5. **[OK]** をクリックします。

表示する必要があります**NT authority \network SERVICE**でログインします。
![image10](images/image10.png)

#### <a name="database-permissions"></a>データベース権限

1. SUSDB を右クリックします。
2. 選択**プロパティ**
3. クリックして**アクセス許可**

**NT authority \network SERVICE**アカウントの一覧を表示する必要があります。

1. そうでない場合は、アカウントを追加します。
2. ログイン名 ボックスでは、次の形式で、WSUS コンピューターを入力します。
    > [**FQDN]\\[WSUSComputerName] $**
3. いることを確認、**既定のデータベース**に設定されている**SUSDB**します。

    > [!TIP]
    > 次の例では、FQDN は**Contosto.com** WSUS マシン名は**WsusMachine**:
    >
    > ![Image11](images/image11.png)

4. **ユーザー マッピング**] ページで、[、 **SUSDB**下データベース **「このログインにマップされたユーザー」**
5. 確認**webservice**下、 **"データベース ロールのメンバーシップ。SUSDB"** : ![image12](images/image12.png)
6. クリックして**OK**設定を保存します。
    > [!NOTE]
    > 変更を有効にする SQL サービスを再起動する必要があります。

### <a name="edit-the-registry-to-point-wsus-to-the-sql-server-instance"></a>WSUS SQL Server のインスタンスにレジストリを編集します。

> [!IMPORTANT]
> 慎重にこのセクションの手順に従います。 誤ってレジストリを変更すると、重大な問題が発生する可能性があります。 変更する前に[復元するためのレジストリをバックアップする](https://support.microsoft.com/en-us/help/322756)問題が発生した場合。

1. **[スタート]** ボタンをクリックし、 **[ファイル名を指定して実行]** をクリックして、「**regedit**」と入力し、 **[OK]** をクリックします。
2. 次のキーを探します。**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\UpdateServices\Server\Setup\SqlServerName**
3. **値**テキスト ボックスに「 **[ServerName]\\[インスタンス名]** をクリックし、 **OK**。 インスタンス名が既定のインスタンスの場合は、入力 **[ServerName]** します。
4. 次のキーを探します。**Hkey_local_machine Services\Server\Setup\Installed ロール Services\UpdateServices WidDatabase** ![image13](images/image13.png)
5. キーの名前を変更 **: UpdateServices データベース** ![image41](images/image14.png)

    > [!NOTE]
    > このキーを更新しない場合**WsusUtil**移行した SQL インスタンスではなく、WID をサービス操作が試行されます。

### <a name="start-the-iis-and-wsus-services-on-the-wsus-server"></a>WSUS サーバーで IIS と WSUS のサービスを開始します。

(管理者特権で)、PowerShell から次のコマンドを実行します。

```powershell
    Start-Service IISADMIN
    Start-Service WsusService
```

> [!NOTE]
> WSUS コンソールを使用している場合は、閉じてから再起動します。

## <a name="uninstalling-the-wid-role-not-recommended"></a>(非推奨)、WID の役割をアンインストールします。

> [!WARNING]
> WID の役割を削除するデータベース フォルダーを削除しても ( **%SystemDrive%\Program \update Services\Database**) WSUSUtil.exe に必要なインストール後のタスク用のスクリプトを格納しています。 WID の役割をアンインストールする場合は、必ずバックアップ、 **%SystemDrive%\Program \update Services\Database**事前フォルダー。

PowerShell を使用します。

```powershell
Uninstall-WindowsFeature -Name 'Windows-Internal-Database'
```

WID ロールが削除された後は、次のレジストリ キーが存在することを確認します。**Hkey_local_machine Services\Server\Setup\Installed ロール Services\UpdateServices データベース**