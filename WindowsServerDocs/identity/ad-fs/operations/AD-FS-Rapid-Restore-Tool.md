---
ms.assetid: 4deff06a-d0ef-4e5a-9701-5911ba667201
title: "AD FS の迅速な復元ツール"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 02/20/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: cd1cc8dab07288ba73c507bc551f089bb79502bc
ms.sourcegitcommit: 36d7b1dfd7da8e9f303d007a628e76149de000f2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/21/2018
---
# <a name="ad-fs-rapid-restore-tool"></a>AD FS の迅速な復元ツール

>適用対象: Windows Server 2016、Windows Server 2012 R2

## <a name="overview"></a>概要
今日、AD FS ファームをセットアップで AD FS を高可用性されます。 一部の組織はなどのような単一のサーバーの AD FS の展開方法を複数の AD FS サーバーおよびネットワーク負荷分散の一部が解決しないときに、インフラストラクチャの必要性を排除するサービスを提供する保証を復元できます迅速に問題がある場合。
新しい AD FS の迅速な復元ツールは、完全バックアップとオペレーティング システムまたはシステム状態の復元を必要とせず、AD FS のデータを復元する方法を説明します。 Azure するのにか、内部設置型の場所には、AD FS 構成をエクスポートするのには、新しいツールを使用できます。  再作成または AD FS 環境を複製するは、エクスポートされたデータを新規の AD FS のインストールに適用できます。 

## <a name="scenarios"></a>シナリオ
AD FS の迅速な復元ツールは、次のシナリオで使用できます。

1. 問題の発生後、AD FS 機能を簡単に復元します。
    - ツールを使用して、オンラインの AD FS サーバーの代わりに迅速に展開されている AD FS のコールド スタンバイ インストールを作成するには
2. 同じテスト環境と実稼働環境を展開します。
    - すばやく展開する検証テスト構成を運用環境またはテスト環境で AD FS の運用の正確なコピーをすばやく作成ツールを使用します。

## <a name="what-is-backed-up"></a>バックアップの対象
ツールは、次の AD FS 構成をバックアップします。
    
- AD FS 構成データベース (SQL または WID)
- 構成ファイル (AD FS のフォルダーにあります)
- トークンの署名と証明書と秘密キー (Active Directory DKM コンテナー) からの暗号化を解除を自動的に生成されます。
- SSL 証明書と、外部で登録した (トークン署名、トークン暗号化解除とサービスの通信) の証明書と対応する秘密キー (注: 秘密キーをエクスポート可能にする必要があり、スクリプトを実行しているユーザーにアクセスする権限が必要)
- カスタム認証プロバイダー、属性ストア、およびローカルの要求プロバイダーの一覧は、インストールされているを信頼します。

## <a name="how-to-use-the-tool"></a>ツールを使用する方法
まず、[ダウンロード](https://go.microsoft.com/fwlink/?LinkId=825646)し、AD FS サーバーに、MSI をインストールします。  

>[!NOTE]
>AD FS 迅速な復元ツールは、FIPS 準拠ではないです。

PowerShell プロンプトから次のコマンドを実行します。

```powershell
import-module 'C:\Program Files (x86)\ADFS Rapid Recreation Tool\ADFSRapidRecreationTool.dll'
```

>[!NOTE] 
>Windows 統合 Database (WID) を使用している場合は、このツールをプライマリ AD FS サーバーで実行する必要があります。  使用することができます、 `Get-SyncProperties` PowerShell コマンドレットを確認するかどうか、サーバーがプライマリ サーバーです。

### <a name="system-requirements"></a>システム要件

- このツールは、Windows Server 2012 R2 以降の AD FS では動作します。 
- 必要な .NET framework 4.0 以上です。 
- バックアップと同じバージョンの AD FS サーバーの復元を行う必要があり、AD FS サービス アカウントとして同じ Active Directory アカウントを使用します。

## <a name="create-a-backup"></a>バックアップを作成します。
バックアップを作成するには、バックアップ ADFS コマンドレットを使用します。 このコマンドレットは、AD FS の構成、データベース、SSL 証明書などをバックアップします。 

ユーザーは、このコマンドレットを実行するには、少なくとも、ローカル管理者であります。 (既定の AD FS の構成に必須)、Active Directory DKM コンテナーをバックアップするに、ユーザーは同様に、ドメインの管理者であるが、するか、または AD FS サービス アカウントの資格情報を渡す必要があります。

パターン「adfsBackup_ID_Date Time」に従ってバックアップ名前はします。 バージョン番号、日付と時刻、バックアップが行われたが格納されます。
このコマンドレットは、次のパラメーターを受け取ります。
    
パラメーター セット

![AD FS の迅速な復元ツール](media/AD-FS-Rapid-Restore-Tool/parameter1.png)

### <a name="detailed-description"></a>詳細な説明

- **BackupDKM** -は、既定の構成 (自動的に生成されたトークンの署名と証明書の暗号化を解除) 内の AD FS のキーを含む Active Directory DKM コンテナーをバックアップします。 これは、AD ツール 'ldifde' を使用して、AD コンテナおよびそのすべてのサブツリーをエクスポートします。

- -**StorageType&lt;文字列&gt;** -ユーザーが使用する記憶域の種類。 "FileSystem"は、ユーザーがローカル フォルダーまたは"Azure"は、ユーザーが、ユーザーが、バックアップを行うときに Azure Storage コンテナーに格納する、ファイル システム バックアップの場所を選択することを示します。 ネットワークまたはクラウドに保存することを示します。 使用する Azure、Azure ストレージの資格情報をコマンドレットに渡される必要があります。 記憶域の資格情報には、アカウント名とキーが含まれています。 さらに、コンテナー名もで渡される必要があります。 コンテナーが存在しない場合は、バックアップ中に作成されます。 使用するファイル システム、記憶域パスを付与する必要があります。 そのディレクトリを各バックアップ用に新しいディレクトリが作成されます。 作成される各ディレクトリに作成したバックアップ ファイルが含まれます。 

- **EncryptionPassword&lt;文字列&gt;** -を実行するすべてのバックアップ ファイルを格納する前に暗号化に使用するパスワード

- **AzureConnectionCredentials &lt;pscredential&gt; ** -Azure ストレージ アカウントのキーとアカウントの名前

- **AzureStorageContainer&lt;文字列&gt;** -ストレージ コンテナーが Azure でのバックアップの格納場所

- **StoragePath&lt;文字列&gt;** -場所、バックアップに格納されます

- **ServiceAccountCredential &lt;pscredential&gt; ** -現在実行されている AD FS サービスに使用されるサービス アカウントを指定します。 このパラメーターは、ユーザーは、DKM をバックアップしたい場合にのみ必要、ドメイン管理者ではありません。

- **BackupComment&lt;文字列&gt;** -HYPER-V チェックポイントの名前付けの概念と同様に、復元中に表示されるバックアップに関する情報の文字列です。 既定では、空の文字列

 
## <a name="backup-examples"></a>バックアップの例
AD FS 迅速な復元ツールを使用するためのバックアップの例を次に示します。

### <a name="backup-the-ad-fs-configuration-with-the-dkm-to-the-file-system-while-running-as-the-domain-admin"></a>ドメイン管理者として実行中に、ファイル システムに、DKM での AD FS 構成をバックアップします。

```powershell
Backup-ADFS -StorageType "FileSystem" -StoragePath "C:\Users\administrator\testExport\" -EncryptionPassword "password" -BackupComment "Clean Install of ADFS (FS)" -BackupDKM
```
 
### <a name="backup-the-ad-fs-configuration-with-the-dkm-to-the-file-system-with-the-service-account-credential-running-as-local-admin"></a>ローカル管理者として実行して、サービス アカウント資格情報でファイル システムに、DKM で、バックアップ、AD FS の構成

```powershell
Backup-ADFS -StorageType "FileSystem" -StoragePath "C:\Users\administrator\testExport\" -EncryptionPassword "password" -BackupComment "Clean Install of ADFS (FS)" -BackupDKM -ServiceAccountCredential $cred
```

### <a name="backup-the-ad-fs-configuration-without-the-dkm-to-the-azure-storage-container"></a>Azure Storage コンテナーに DKM ことがなく、AD FS 構成をバックアップします。

```powershell
Backup-ADFS -StorageType "Azure" -AzureConnectionCredentials $cred -AzureStorageContainer "adfsbackups"  -EncryptionPassword "password" -BackupComment "Clean Install of ADFS"
```

### <a name="backup-the-ad-fs-configuration-without-the-dkm-to-the-file-system"></a>ファイル システムに DKM ことがなく、AD FS 構成をバックアップします。

```powershell   
Backup-ADFS -StorageType "FileSystem" -StoragePath "C:\Users\administrator\testExport\" -EncryptionPassword "password" -BackupComment "Clean Install of ADFS (FS)"
```

## <a name="restore-from-backup"></a>バックアップから復元します。
新しい AD FS のインストールにバックアップ ADFS を使用して作成された構成を適用するには、復元 ADFS コマンドレットを使用します。

このコマンドレットは、コマンドレットを使用して新しい AD FS ファームを作成します。`Install-AdfsFarm`され、AD FS の構成、データベース、証明書などを復元します。サーバーで AD FS の役割がインストールされていない場合、コマンドレットによってインストールされます。  コマンドレットは、既存のバックアップの復元場所を確認し、それが取得された日付/時刻と、ユーザーがバックアップに接続されている可能性がありますが任意のバックアップ コメントに基づいて、適切なバックアップを選択するように求めます。 別のフェデレーション サービス名を持つ複数の AD FS 構成がある場合、ユーザーがするように求められます最初に、適切な AD FS 構成を選択します。
ユーザーが、このコマンドレットを実行するローカルおよびドメインの両方の管理者であります。


>[!NOTE] 
>AD FS の迅速な回復ツールを使用して、前に、サーバーが、バックアップを復元する前に、ドメインに参加していることを確認します。 

このコマンドレットは、次のパラメーターを受け取ります。 

![AD FS の迅速な復元ツール](media/AD-FS-Rapid-Restore-Tool/parameter2.png)

### <a name="detailed-description"></a>詳細な説明

- **StorageType&lt;文字列&gt;** -ユーザーが使用する記憶域の種類。
 "FileSystem"は、ユーザーがそのフォルダーをローカルに保存するか、ネットワークで"Azure"を示して、ユーザーが Azure Storage コンテナーに保存することを示します

- **DecryptionPassword&lt;文字列&gt;** -すべてのバックアップ ファイルの暗号化に使用されたパスワード 

- **AzureConnectionCredentials &lt;pscredential&gt; ** -Azure ストレージ アカウントのキーとアカウントの名前

- **AzureStorageContainer&lt;文字列&gt;** -ストレージ コンテナーが Azure でのバックアップの格納場所

- **StoragePath&lt;文字列&gt;** -場所、バックアップに格納されます

- **ADFSName&lt;文字列&gt; ** -がバックアップを復元しようとして、フェデレーションの名前。 これが指定されていないとがある場合は、1 つだけのフェデレーション サービス名をしが使用されます。 ある場合は、1 つ以上のフェデレーション サービスの場所にバックアップし、バックアップ フェデレーション サービスのいずれかを選択するよう求められます。

- **ServiceAccountCredential &lt; pscredential &gt; ** -新しい AD FS サービスの復元中に使用されるサービス アカウントを指定します。 

- **GroupServiceAccountIdentifier&lt;文字列&gt;** -ユーザーが、新しい AD FS サービスの復元中に使用する、GMSA します。 既定では、どちらも指定した場合、バックアップをアカウント名が使用 GMSA、他のサービス アカウントに配置するよう求められますれていた場合

- **DBConnectionString&lt;文字列&gt;** - 場合、ユーザーには、復元操作に異なる DB を使用する必要があります SQL 接続文字列または型ために渡す WID WID. し、

- **Force &lt;bool&gt; ** -バックアップを選択したら、ツールがある可能性がある画面の指示をスキップします。

- **RestoreDKM &lt;bool&gt; ** - AD に DKM コンテナーを復元しようとして、新しい AD 場合に設定する必要があり、DKM が最初にバックアップされました。

## <a name="restore-examples"></a>例を復元します。

### <a name="restore-the-ad-fs-configuration-without-the-dkm-from-the-azure-storage-container"></a>Azure Storage コンテナーから、DKM ことがなく、AD FS 構成を復元します。

```powershell
Restore-ADFS -StorageType "Azure" -AzureConnectionCredential $cred -DecryptionPassword "password" -AzureStorageContainer "adfsbackups"
```

### <a name="restore-the-ad-fs-configuration-without-the-dkm-from-the-file-system"></a>ファイル システムから、DKM ことがなく、AD FS 構成を復元します。
 
```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\uSERS\administrator\testExport\" -DecryptionPassword "password"
```

### <a name="restore-the-ad-fs-configuration-with-the-dkm-to-the-file-system"></a>ファイル システムに、DKM で AD FS 構成を復元します。 
 
```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\uSERS\administrator\testExport\" -DecryptionPassword "password" -RestoreDKM
```

### <a name="restore-the-ad-fs-configuration-to-wid"></a>WID を AD FS 構成を復元します。

```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\uSERS\administrator\testExport\" -DecryptionPassword "password" -DBConnectionString "WID"
``` 

### <a name="restore-the-ad-fs-configuration-to-sql"></a>SQL への AD FS 構成を復元します。

```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\uSERS\administrator\testExport\" -DecryptionPassword "password" -DBConnectionString "Data Source=TESTMACHINE\SQLEXPRESS; Integrated Security=True"
```

### <a name="restores-the-ad-fs-configuration-with-the-specified-gmsa"></a>指定された GMSA を使用して AD FS 構成を復元します。

```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\uSERS\administrator\testExport\" -DecryptionPassword "password" -GroupServiceAccountIdentifier "mangupd1\adfsgmsa$"
```
### <a name="restore-the-ad-fs-configuration-with-the-specified-service-account-creds"></a>指定されたサービス アカウントの資格情報を使用して AD FS 構成を復元します。

```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\uSERS\administrator\testExport\" -DecryptionPassword "password" -ServiceAccountCredential $cred
```

## <a name="encryption-information"></a>暗号化情報
すべてのバックアップ データはクラウドへのプッシュまたはファイル システムにそれを格納する前に暗号化されます。  

バックアップの一環として作成される各ドキュメントは、AES 256 を使用して暗号化されます。 このツールに渡されたパスワードは、Rfc2898DeriveBytes クラスを使用して新しいパスワードを生成するパスフレーズとして使用されます。 

RngCryptoServiceProvider を使用して、AES and Rfc2898DeriveBytes クラスで使用される salt を生成します。 

## <a name="log-files"></a>ログ ファイル
バックアップまたは復元を実行するたびにログ ファイルが作成されます。 これらは、次の場所で見つかんだことができます。

- **%localappdata%\ADFSRapidRecreationTool**

>[!NOTE]
> 追加の認証プロバイダーの概要が含まれている PostRestore_Instructions ファイルが作成される可能性がある復元を実行するには、属性を格納し、ローカルの要求プロバイダー信頼と AD FS サービスを開始する前に手動でインストールするとき。
