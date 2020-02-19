---
ms.assetid: 4deff06a-d0ef-4e5a-9701-5911ba667201
title: AD FS の迅速な復元ツール
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/02/2019
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 2570aae52da2925a62dd6c9262af325fb5461fff
ms.sourcegitcommit: 2a15de216edde8b8e240a4aa679dc6d470e4159e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77465266"
---
# <a name="ad-fs-rapid-restore-tool"></a>AD FS の迅速な復元ツール

## <a name="overview"></a>概要
現在 AD FS は、AD FS ファームを設定することによって高可用性になっています。 組織によっては、1台のサーバー AD FS 展開する方法が必要になることがあります。これにより、複数の AD FS サーバーおよびネットワーク負荷分散インフラストラクチャが不要になり、問題が発生した場合でもサービスを迅速に復元できることが保証されます。
新しい AD FS 迅速な復元ツールを使用すると、オペレーティングシステムまたはシステム状態の完全バックアップと復元を必要とすることなく、AD FS データを復元することができます。 新しいツールを使用して、AD FS 構成を Azure またはオンプレミスの場所にエクスポートできます。  その後、エクスポートしたデータを新しい AD FS インストールに適用し、AD FS 環境の再作成または複製を行うことができます。 

## <a name="scenarios"></a>シナリオ
AD FS 高速復元ツールは、次のシナリオで使用できます。

1. 問題の発生後に AD FS 機能を迅速に復元する
    - ツールを使用して、オンライン AD FS サーバーの代わりに迅速に展開できるコールドスタンバイインストール AD FS を作成します。
2. 同一のテスト環境と運用環境をデプロイする
    - ツールを使用すると、テスト環境で実稼働 AD FS の正確なコピーをすばやく作成したり、検証済みのテスト構成を運用環境にすばやく配置したりすることが可能です。
3. SQL ベースの構成から WID への移行またはその逆の移行
    - このツールを使用して、SQL ベースのファーム構成から WID へ、またはその逆方向に移動します。 


>[!NOTE] 
>SQL マージレプリケーションまたは Always on 可用性グループを使用している場合、高速復元ツールはサポートされていません。 代替手段として、SQL ベースのバックアップと SSL 証明書のバックアップを使用することをお勧めします。

## <a name="what-is-backed-up"></a>バックアップ対象
ツールは、次の AD FS 構成をバックアップします。
    
- 構成データベースの AD FS (SQL または WID)
- 構成ファイル (AD FS フォルダーにあります)
- 証明書と秘密キーの署名と暗号化解除を自動的に生成したトークン (Active Directory DKM コンテナーから)
- SSL 証明書と外部に登録された証明書 (トークンの署名、トークンの暗号化とサービス通信)、および対応する秘密キー (注: 秘密キーはエクスポート可能である必要があり、スクリプトを実行するユーザーにはアクセス許可が必要です)
- インストールされているカスタム認証プロバイダー、属性ストア、およびローカル要求プロバイダー信頼の一覧。

## <a name="how-to-use-the-tool"></a>ツールの使用方法
まず、AD FS サーバーに MSI を[ダウンロード](https://go.microsoft.com/fwlink/?LinkId=825646)してインストールします。  

PowerShell プロンプトから次のコマンドを実行します。

```powershell
import-module 'C:\Program Files (x86)\ADFS Rapid Recreation Tool\ADFSRapidRecreationTool.dll'
```

>[!NOTE] 
>Windows 統合データベース (WID) を使用している場合は、プライマリ AD FS サーバーでこのツールを実行する必要があります。  `Get-AdfsSyncProperties` PowerShell コマンドレットを使用して、オンになっているサーバーがプライマリサーバーであるかどうかを判断できます。

### <a name="system-requirements"></a>システム要件

- このツールは、Windows Server 2012 R2 以降の AD FS に使用できます。 
- 必要な .NET framework は、少なくとも4.0 です。 
- 復元は、バックアップと同じバージョンの AD FS サーバーで実行する必要があり、AD FS サービスアカウントと同じ Active Directory アカウントを使用します。

## <a name="create-a-backup"></a>バックアップを作成する
バックアップを作成するには、バックアップ-ADFS コマンドレットを使用します。 このコマンドレットは、AD FS の構成、データベース、SSL 証明書などをバックアップします。 

このコマンドレットを実行するには、ユーザーは少なくともローカル管理者である必要があります。 Active Directory DKM コンテナー (既定の AD FS 構成で必要) をバックアップするには、ユーザーがドメイン管理者であるか、AD FS サービスアカウントの資格情報を渡す必要があります。または、DKM コンテナーへのアクセス権を持っている必要があります。  GMSA アカウントを使用している場合は、ユーザーがドメイン管理者であるか、コンテナーに対するアクセス許可を持っている必要があります。gMSA 資格情報を指定することはできません。 

バックアップは、"adfsBackup_ID_Date" のパターンに従って名前が付けられます。 これには、バックアップが実行された日付と時刻のバージョン番号が含まれます。
コマンドレットは、次のパラメーターを受け取ります。
    
パラメーターセット

![AD FS の迅速な復元ツール](media/AD-FS-Rapid-Restore-Tool/parameter1.png)

### <a name="detailed-description"></a>詳細な説明

- **Backupdkm** -既定の構成で AD FS キーを含む Active Directory DKM コンテナーをバックアップします (自動的に生成されたトークンの署名と暗号化解除の証明書)。 Ad ツールの "ldifde" を使用して、AD コンテナーとそのすべてのサブツリーをエクスポートします。

- -**Storagetype &lt;string&gt;** -ユーザーが使用しようとしているストレージの種類。 "FileSystem" は、ユーザーがバックアップを実行したときに、ユーザーがバックアップの場所 (ファイルシステムまたは) を選択したときに、ユーザーがローカルまたはネットワーク "Azure Azure Storage" 内のフォルダーに保存することを示していることを示します。クラウド. Azure を使用するには、Azure Storage 資格情報をコマンドレットに渡す必要があります。 ストレージ資格情報には、アカウント名とキーが含まれています。 さらに、コンテナー名も渡す必要があります。 コンテナーが存在しない場合は、バックアップ中に作成されます。 ファイルシステムを使用するには、ストレージパスを指定する必要があります。 そのディレクトリでは、バックアップごとに新しいディレクトリが作成されます。 作成される各ディレクトリには、バックアップされたファイルが含まれます。 

- **Encryptionpassword &lt;string&gt;** -保存する前にすべてのバックアップファイルを暗号化するために使用されるパスワード

- **Azureconnectioncredentials &lt;pscredential&gt;** -Azure ストレージアカウントのアカウント名とキー

- **Azurestoragecontainer &lt;string&gt;** -バックアップが Azure に格納されるストレージコンテナー

- **Storagepath &lt;string&gt;** -バックアップが格納される場所

- **Serviceaccountcredential &lt;pscredential&gt;** -現在実行中の AD FS サービスに使用されているサービスアカウントを指定します。 このパラメーターは、ユーザーが DKM をバックアップする必要があり、ドメイン管理者ではない場合、またはコンテナーの内容にアクセスできない場合にのみ必要です。 

- **Backupcomment &lt;string []&gt;** -復元中に表示されるバックアップに関する情報文字列。 hyper-v チェックポイントの名前付けの概念と同様です。 既定値は空の文字列です。

 
## <a name="backup-examples"></a>バックアップの例
AD FS 迅速な復元ツールを使用するためのバックアップ例を次に示します。

### <a name="backup-the-ad-fs-configuration-with-the-dkm-to-the-file-system-and-has-access-to-the-dkm-container-contents-either-domain-admin-or-delegated"></a>DKM を使用して AD FS 構成をファイルシステムにバックアップし、DKM コンテナーの内容 (ドメイン管理者または委任) にアクセスできるようにします。

```powershell
Backup-ADFS -StorageType "FileSystem" -StoragePath "C:\Users\administrator\testExport\" -EncryptionPassword "password" -BackupComment "Clean Install of ADFS (FS)" -BackupDKM
```
 
### <a name="backup-the-ad-fs-configuration-with-the-dkm-to-the-file-system-with-the-service-account-credential-running-as-local-admin"></a>ローカル管理者として実行されているサービスアカウントの資格情報を使用して、DKM を使用して AD FS 構成をファイルシステムにバックアップします。

```powershell
Backup-ADFS -StorageType "FileSystem" -StoragePath "C:\Users\administrator\testExport\" -EncryptionPassword "password" -BackupComment "Clean Install of ADFS (FS)" -BackupDKM -ServiceAccountCredential $cred
```

### <a name="backup-the-ad-fs-configuration-without-the-dkm-to-the-azure-storage-container"></a>Azure Storage コンテナーに DKM を指定せずに AD FS 構成をバックアップします。

```powershell
Backup-ADFS -StorageType "Azure" -AzureConnectionCredentials $cred -AzureStorageContainer "adfsbackups"  -EncryptionPassword "password" -BackupComment "Clean Install of ADFS"
```

### <a name="backup-the-ad-fs-configuration-without-the-dkm-to-the-file-system"></a>ファイルシステムに DKM を指定せずに AD FS 構成をバックアップする

```powershell   
Backup-ADFS -StorageType "FileSystem" -StoragePath "C:\Users\administrator\testExport\" -EncryptionPassword "password" -BackupComment "Clean Install of ADFS (FS)"
```

## <a name="restore-from-backup"></a>バックアップからの復元
バックアップ-ADFS を使用して作成された構成を新しい AD FS インストールに適用するには、Restore-ADFS コマンドレットを使用します。

このコマンドレットは、コマンドレット `Install-AdfsFarm` を使用して新しい AD FS ファームを作成し、AD FS 構成、データベース、証明書などを復元します。 AD FS の役割がサーバーにインストールされていない場合は、コマンドレットによってインストールされます。  コマンドレットは、既存のバックアップの復元場所を確認し、実行された日時と、ユーザーがバックアップにアタッチした可能性のあるバックアップコメントに基づいて、適切なバックアップを選択するようユーザーに指示します。 フェデレーションサービス名が異なる複数の AD FS 構成がある場合、ユーザーは最初に適切な AD FS 構成を選択するように求められます。
このコマンドレットを実行するには、ユーザーがローカルとドメインの両方の管理者である必要があります。


>[!NOTE] 
>AD FS 迅速な回復ツールを使用する前に、バックアップを復元する前に、サーバーがドメインに参加していることを確認してください。 

コマンドレットは、次のパラメーターを受け取ります。 

![AD FS の迅速な復元ツール](media/AD-FS-Rapid-Restore-Tool/parameter2.png)

### <a name="detailed-description"></a>詳細な説明

- **Storagetype &lt;string&gt;** -ユーザーが使用するストレージの種類。
 "FileSystem" は、ユーザーがローカルまたはネットワーク "Azure" 内のフォルダーに保存することを示します。これは、ユーザーが Azure Storage コンテナーに保存することを示します。

- **DecryptionPassword &lt;string&gt;** -バックアップされたすべてのファイルを暗号化するために使用されたパスワード 

- **Azureconnectioncredentials &lt;pscredential&gt;** -Azure ストレージアカウントのアカウント名とキー

- **Azurestoragecontainer &lt;string&gt;** -バックアップが Azure に格納されるストレージコンテナー

- **Storagepath &lt;string&gt;** -バックアップが格納される場所

- **ADFSName &lt; string &gt;** -バックアップされ、復元されるフェデレーションの名前。 これが指定されておらず、フェデレーションサービス名が1つしかない場合は、その名前が使用されます。 複数のフェデレーションサービスがその場所にバックアップされている場合、ユーザーはバックアップされたフェデレーションサービスの1つを選択するように求められます。

- **Serviceaccountcredential &lt; pscredential &gt;** -復元する新しい AD FS サービスに使用するサービスアカウントを指定します 

- **GroupServiceAccountIdentifier &lt;string&gt;** -復元する新しい AD FS サービスにユーザーが使用する必要がある GMSA。 既定では、どちらも指定されていない場合は、バックアップされたアカウント名が使用されます (GMSA の場合)。それ以外の場合は、ユーザーはサービスアカウントを入力するように求められます。

- **Dbconnectionstring &lt;文字列&gt;** -ユーザーが復元に別の DB を使用する場合は、WID の SQL 接続文字列または wid の種類を渡す必要があります。

- **&lt;ブール&gt;を強制**する-バックアップを選択した後に、ツールが持つ可能性のあるプロンプトをスキップします。

- **Restoredkm &lt;bool&gt;** -dkm コンテナーを AD に復元します。新しい ad に移動し、dkm が最初にバックアップされた場合は、これを設定する必要があります。

## <a name="restore-examples"></a>復元の例

### <a name="restore-the-ad-fs-configuration-without-the-dkm-from-the-azure-storage-container"></a>Azure Storage コンテナーから DKM を使用せずに AD FS 構成を復元する

```powershell
Restore-ADFS -StorageType "Azure" -AzureConnectionCredential $cred -DecryptionPassword "password" -AzureStorageContainer "adfsbackups"
```

### <a name="restore-the-ad-fs-configuration-without-the-dkm-from-the-file-system"></a>ファイルシステムから DKM を使用せずに AD FS 構成を復元する
 
```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\Users\administrator\testExport\" -DecryptionPassword "password"
```

### <a name="restore-the-ad-fs-configuration-with-the-dkm-to-the-file-system"></a>DKM を使用して AD FS 構成をファイルシステムに復元する 
 
```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\Users\administrator\testExport\" -DecryptionPassword "password" -RestoreDKM
```

### <a name="restore-the-ad-fs-configuration-to-wid"></a>AD FS 構成を WID に復元する

```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\Users\administrator\testExport\" -DecryptionPassword "password" -DBConnectionString "WID"
``` 

### <a name="restore-the-ad-fs-configuration-to-sql"></a>AD FS 構成を SQL に復元する

```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\Users\administrator\testExport\" -DecryptionPassword "password" -DBConnectionString "Data Source=TESTMACHINE\SQLEXPRESS; Integrated Security=True"
```

### <a name="restores-the-ad-fs-configuration-with-the-specified-gmsa"></a>指定した GMSA を使用して AD FS の構成を復元します。

```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\Users\administrator\testExport\" -DecryptionPassword "password" -GroupServiceAccountIdentifier "mangupd1\adfsgmsa$"
```
### <a name="restore-the-ad-fs-configuration-with-the-specified-service-account-creds"></a>指定されたサービスアカウントの資格情報を使用して AD FS 構成を復元します

```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\Users\administrator\testExport\" -DecryptionPassword "password" -ServiceAccountCredential $cred
```

## <a name="encryption-information"></a>暗号化情報
すべてのバックアップデータは、クラウドにプッシュされる前、またはファイルシステムに格納される前に暗号化されます。  

バックアップの一部として作成された各ドキュメントは、AES-256 を使用して暗号化されます。 ツールに渡されるパスワードは、Rfc2898DeriveBytes クラスを使用して新しいパスワードを生成するためのパスフレーズとして使用されます。 

RngCryptoServiceProvider は、AES と Rfc2898DeriveBytes クラスで使用される salt を生成するために使用されます。 

## <a name="log-files"></a>ログ ファイル
バックアップまたは復元が実行されるたびに、ログファイルが作成されます。 これらは次の場所にあります。

- **%localappdata%\ADFSRapidRecreationTool**

>[!NOTE]
> 復元を実行すると、AD FS サービスを開始する前に手動でインストールする追加の認証プロバイダー、属性ストア、およびローカル要求プロバイダー信頼の概要を含む PostRestore_Instructions ファイルが作成される場合があります。

## <a name="version-release-history"></a>バージョンのリリース履歴

### <a name="version-10820"></a>バージョン1.0.82.0
リリース: 2019 年7月

**修正済みの問題:**
- LDAP エスケープ文字を含む AD FS サービスアカウント名のバグ修正


### <a name="version-10810"></a>バージョン: 1.0.81.0
リリース: 2019 年4月

**修正済みの問題:**


- 証明書のバックアップと復元のバグ修正
- ログファイルへの追加のトレース情報


### <a name="version-10750"></a>バージョン: 1.0.75.0
リリース: 2018 年8月

**修正済みの問題:**
* バックアップの更新-BackupDKM スイッチを使用する場合の ADFS。  ツールは、現在のコンテキストが DKM コンテナーにアクセスできるかどうかを判断します。  その場合は、ドメイン管理者特権またはサービスアカウント資格情報は必要ありません。  これにより、資格情報を明示的に指定したり、ドメイン管理者アカウントとして実行したりすることなく、自動バックアップを実行できます。

### <a name="version-10730"></a>バージョン: 1.0.73.0
リリース: 2018 年8月

**修正済みの問題:**
* アプリケーションが FIPS に準拠するように暗号化アルゴリズムを更新する
    
    >[!NOTE]
    > FIPS 準拠に従って暗号化アルゴリズムが変更されたため、古いバックアップは新しいバージョンで動作しません
    
* マージレプリケーションを使用する SQL クラスターのサポートを追加する

### <a name="version-10720"></a>バージョン: 1.0.72.0
リリース: 2018 年7月

**修正済みの問題:**

   - バグの修正: を修正します。インプレースアップグレードをサポートするための MSI インストーラー 

### <a name="10180"></a>1.0.18.0
リリース: 2018 年7月

**修正済みの問題:**

   - バグの修正: 特殊文字が含まれているサービスアカウントのパスワードを処理する (ie、' & ')
   - バグの修正: 別のプロセスによって使用されているため、復元は失敗します。


### <a name="1000"></a>1.0.0.0
リリース日: 2016 年10月

AD FS 迅速な復元ツールの最初のリリース
