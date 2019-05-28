---
ms.assetid: 4deff06a-d0ef-4e5a-9701-5911ba667201
title: AD FS の迅速な復元ツール
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 04/01/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: a831154a8b1e84f5ed879375980882e208c33d73
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66190352"
---
# <a name="ad-fs-rapid-restore-tool"></a>AD FS の迅速な復元ツール

## <a name="overview"></a>概要
今すぐ AD FS は、AD FS ファームを設定して高可用性実現されます。 一部の組織し 1 台のサーバーの AD FS デプロイする方法、複数の AD FS サーバーとネットワーク負荷も一部ことができますが、インフラストラクチャを分散する必要がなくなりますサービス保証場合に復元できる迅速に問題があります。
新しい AD FS の迅速な復元ツールは、完全バックアップとオペレーティング システムまたはシステム状態の復元を必要とせずに AD FS のデータを復元する方法を提供します。 Azure またはオンプレミスの場所には、AD FS 構成をエクスポートするのには、新しいツールを使用できます。  再作成または AD FS 環境を複製する、新しい AD FS のインストールに、エクスポートされたデータを適用できます。 

## <a name="scenarios"></a>シナリオ
次のシナリオでは、AD FS の迅速な復元ツールを使用できます。

1. 問題の発生後、AD FS 機能を迅速に復元します。
    - ツールを使用して、オンラインの AD FS サーバーの代わりに迅速にデプロイされる AD FS の場合は、コールド スタンバイ インストールを作成するには
2. 同一のテストおよび運用環境をデプロイします。
    - ツールを使用して、すばやく検証済みのテスト構成を運用環境に配置またはテスト環境で AD FS の運用環境の正確なコピーをすばやく作成するには

## <a name="what-is-backed-up"></a>バックアップの対象
ツールは、次の AD FS 構成をバックアップします。
    
- AD FS 構成データベース (SQL または WID)
- 構成ファイルを (AD FS のフォルダーにあります)
- トークンの署名と証明書と秘密キー (から Active Directory DKM コンテナー) を暗号化解除を自動的に生成されます。
- SSL 証明書とそのいずれかの外部で登録した (トークンの署名、トークン暗号化解除およびサービスの通信) の証明書と対応する秘密キー (注: 秘密キーをエクスポート可能にする必要があり、スクリプトを実行しているユーザーはそれらにアクセスする権限が必要)
- カスタム認証プロバイダー、属性ストア、およびローカルの要求プロバイダーの一覧は、インストールされているを信頼します。

## <a name="how-to-use-the-tool"></a>ツールを使用する方法
最初に、[ダウンロード](https://go.microsoft.com/fwlink/?LinkId=825646)し、AD FS サーバーに、MSI をインストールします。  

PowerShell プロンプトから次のコマンドを実行します。

```powershell
import-module 'C:\Program Files (x86)\ADFS Rapid Recreation Tool\ADFSRapidRecreationTool.dll'
```

>[!NOTE] 
>Windows 統合 Database (WID) を使用している場合は、このツールをプライマリ AD FS サーバーで実行する必要があります。  使用することができます、`Get-AdfsSyncProperties`を確認するかどうか、サーバーがプライマリ サーバーの PowerShell コマンドレット。

### <a name="system-requirements"></a>システム要件

- このツールは、Windows Server 2012 R2 以降の AD FS に対して機能します。 
- 必要な .NET framework は、少なくとも 4.0 です。 
- バックアップと同じバージョンの AD FS サーバーで復元を実行する必要があり、AD FS サービス アカウントとして同じ Active Directory アカウントを使用しています。

## <a name="create-a-backup"></a>バックアップを作成します。
バックアップを作成するには、バックアップ ADFS コマンドレットを使用します。 このコマンドレットは、AD FS の構成、データベース、SSL 証明書などをバックアップします。 

ユーザーは、このコマンドレットを実行する、少なくともローカル管理者であるがします。 (既定の AD FS の構成で必要)、Active Directory DKM コンテナーをバックアップするには、ユーザーがドメイン管理者である、AD FS サービス アカウントの資格情報を渡す必要があるか DKM コンテナーにアクセスします。  ユーザーがドメイン管理者である必要があるかどうか、またはコンテナーへのアクセス許可がある gMSA アカウントを使用している場合gMSA 資格情報を提供することはできません。 

バックアップ「adfsBackup_ID_Date 時間」のパターンに従って名前が付けられます。 バージョン番号、日付、およびバックアップの実行時間が含まれます。
コマンドレットは、次のパラメーターを受け取ります。
    
パラメーター セット

![AD FS の迅速な復元ツール](media/AD-FS-Rapid-Restore-Tool/parameter1.png)

### <a name="detailed-description"></a>詳細な説明

- **BackupDKM** -既定の構成 (署名と暗号化解除証明書は自動的に生成されたトークン) で AD FS のキーを格納する Active Directory DKM コンテナーをバックアップします。 これは、AD ツール 'ldifde' を使用して、AD コンテナーとそのすべてのサブツリーをエクスポートします。

- -**StorageType&lt;文字列&gt;** -ユーザーが使用するストレージの種類。 "FileSystem"は、ユーザーがローカルまたはネットワークの"Azure"は、ユーザーが、ユーザーは、バックアップを実行するときに Azure ストレージ コンテナーに格納する、ファイル システム バックアップの場所を選択することを示しますまたはでフォルダーに格納することを示します、。クラウド。 Azure を使用して、コマンドレットに Azure ストレージ資格情報を渡します。 ストレージの資格情報には、アカウント名とキーが含まれています。 さらはコンテナー名で渡すもする必要があります。 コンテナーが存在しない場合は、バックアップ中に作成されます。 使用するファイル システム ストレージのパスを与える必要があります。 そのディレクトリでは、バックアップごとに新しいディレクトリが作成されます。 作成した各ディレクトリは、バックアップ ファイルが格納されます。 

- **EncryptionPassword&lt;文字列&gt;** -格納する前にすべてのバックアップ ファイルの暗号化に使用するパスワード

- **AzureConnectionCredentials &lt;pscredential&gt;**  -アカウント名と、Azure ストレージ アカウントのキー

- **AzureStorageContainer&lt;文字列&gt;** -ストレージ コンテナーを Azure でのバックアップの格納

- **StoragePath&lt;文字列&gt;** -場所、バックアップに格納されます

- **ServiceAccountCredential &lt;pscredential&gt;**  -現在実行されている AD FS サービスに使用されるサービス アカウントを指定します。 このパラメーターは、DKM のバックアップをユーザーが希望の場合にのみ必要またはドメイン管理者でないと、コンテナーの内容へのアクセスはありません。 

- **BackupComment &lt;string[]&gt;**  -HYPER-V でチェックポイントの名前付けの概念に似ています、復元中に表示されるバックアップに関する情報の文字列。 既定値は空の文字列

 
## <a name="backup-examples"></a>バックアップの例
AD FS 迅速な復元ツールを使用するためのバックアップの例を次に示します。

### <a name="backup-the-ad-fs-configuration-with-the-dkm-to-the-file-system-and-has-access-to-the-dkm-container-contents-either-domain-admin-or-delegated"></a>ファイル システムに、DKM での AD FS 構成をバックアップして、DKM コンテナーの内容にアクセスする (いずれかのドメイン管理者または代理)

```powershell
Backup-ADFS -StorageType "FileSystem" -StoragePath "C:\Users\administrator\testExport\" -EncryptionPassword "password" -BackupComment "Clean Install of ADFS (FS)" -BackupDKM
```
 
### <a name="backup-the-ad-fs-configuration-with-the-dkm-to-the-file-system-with-the-service-account-credential-running-as-local-admin"></a>ローカル管理者として実行して、サービス アカウント資格情報でファイル システムに、DKM で、バックアップ、AD FS の構成

```powershell
Backup-ADFS -StorageType "FileSystem" -StoragePath "C:\Users\administrator\testExport\" -EncryptionPassword "password" -BackupComment "Clean Install of ADFS (FS)" -BackupDKM -ServiceAccountCredential $cred
```

### <a name="backup-the-ad-fs-configuration-without-the-dkm-to-the-azure-storage-container"></a>Azure ストレージ コンテナー DKM なしの AD FS 構成をバックアップします。

```powershell
Backup-ADFS -StorageType "Azure" -AzureConnectionCredentials $cred -AzureStorageContainer "adfsbackups"  -EncryptionPassword "password" -BackupComment "Clean Install of ADFS"
```

### <a name="backup-the-ad-fs-configuration-without-the-dkm-to-the-file-system"></a>ファイル システムに DKM なしの AD FS 構成をバックアップします。

```powershell   
Backup-ADFS -StorageType "FileSystem" -StoragePath "C:\Users\administrator\testExport\" -EncryptionPassword "password" -BackupComment "Clean Install of ADFS (FS)"
```

## <a name="restore-from-backup"></a>バックアップから復元します。
新しい AD FS のインストールにバックアップ ADFS を使用して作成、構成を適用するには、復元 ADFS コマンドレットを使用します。

このコマンドレットは、コマンドレットを使用して、新しい AD FS ファームを作成します。`Install-AdfsFarm`し、AD FS の構成、データベース、証明書などを復元します。サーバーで AD FS の役割がインストールされていない場合、コマンドレットによってインストールされます。  コマンドレットは、既存のバックアップの復元場所を確認し、日付/時刻の引用したものと、バックアップに、ユーザーが接続されている可能性がありますが任意のバックアップ コメントに基づいて、適切なバックアップを選択するよう求めます。 異なるフェデレーション サービス名を持つ複数の AD FS 構成がある場合は、まず適切な AD FS 構成を選択する、ユーザーが求めします。
ユーザーは、このコマンドレットを実行するローカルおよびドメインの両方の管理者であるがします。


>[!NOTE] 
>AD FS の迅速な回復ツールを使用する前に、サーバーがバックアップを復元する前に、ドメインに参加していることを確認します。 

コマンドレットは、次のパラメーターを受け取ります。 

![AD FS の迅速な復元ツール](media/AD-FS-Rapid-Restore-Tool/parameter2.png)

### <a name="detailed-description"></a>詳細な説明

- **StorageType&lt;文字列&gt;** -ユーザーが使用するストレージの種類。
 "FileSystem"は、ユーザーがローカルのフォルダーに保存するか、ネットワーク上の"Azure"を示す、ユーザーが Azure ストレージ コンテナーに格納することを示します

- **DecryptionPassword&lt;文字列&gt;** -すべてのバックアップ ファイルの暗号化に使用されたパスワード 

- **AzureConnectionCredentials &lt;pscredential&gt;**  -アカウント名と、Azure ストレージ アカウントのキー

- **AzureStorageContainer&lt;文字列&gt;** -ストレージ コンテナーを Azure でのバックアップの格納

- **StoragePath&lt;文字列&gt;** -場所、バックアップに格納されます

- **ADFSName&lt;文字列&gt;**  -してバックアップを復元することは、フェデレーションの名前。 これが指定されていない場合は、その 1 つだけのフェデレーション サービス名が使用されます。 ある場合は、複数のフェデレーション サービスが、場所にバックアップし、ユーザーはバックアップ フェデレーション サービスのいずれかを選択するように求められます。

- **ServiceAccountCredential &lt; pscredential &gt;**  -新しい AD FS サービスが復元中に使用されるサービス アカウントを指定します 

- **GroupServiceAccountIdentifier&lt;文字列&gt;** -ユーザーが復元される新しい AD FS サービスを使用する、GMSA します。 既定では、どちらが指定される場合、バックアップをアカウント名が使用 GMSA で、ユーザーがサービス アカウントに配置するように求め、その他の場合

- **DBConnectionString&lt;文字列&gt;** が渡す必要があります、SQL 接続文字列または型 WID WID. をし、ユーザーは、復元、異なる DB を使用するなどの場合 -

- **Force &lt;bool&gt;**  -バックアップを選択した後、ツールがあります、画面の指示をスキップ

- **RestoreDKM &lt;bool&gt;**  - ad DKM コンテナーを復元すると、新しい AD 場合に設定する必要があり、DKM が最初にバックアップされました。

## <a name="restore-examples"></a>Restore の例

### <a name="restore-the-ad-fs-configuration-without-the-dkm-from-the-azure-storage-container"></a>Azure ストレージ コンテナーから、DKM なしの AD FS 構成を復元します。

```powershell
Restore-ADFS -StorageType "Azure" -AzureConnectionCredential $cred -DecryptionPassword "password" -AzureStorageContainer "adfsbackups"
```

### <a name="restore-the-ad-fs-configuration-without-the-dkm-from-the-file-system"></a>ファイル システムから、DKM なしの AD FS 構成を復元します。
 
```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\uSERS\administrator\testExport\" -DecryptionPassword "password"
```

### <a name="restore-the-ad-fs-configuration-with-the-dkm-to-the-file-system"></a>ファイル システムに、DKM で AD FS 構成を復元します。 
 
```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\uSERS\administrator\testExport\" -DecryptionPassword "password" -RestoreDKM
```

### <a name="restore-the-ad-fs-configuration-to-wid"></a>WID を AD FS の構成を復元します。

```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\uSERS\administrator\testExport\" -DecryptionPassword "password" -DBConnectionString "WID"
``` 

### <a name="restore-the-ad-fs-configuration-to-sql"></a>To SQL、AD FS の構成を復元します。

```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\uSERS\administrator\testExport\" -DecryptionPassword "password" -DBConnectionString "Data Source=TESTMACHINE\SQLEXPRESS; Integrated Security=True"
```

### <a name="restores-the-ad-fs-configuration-with-the-specified-gmsa"></a>指定した GMSA を使用して AD FS 構成を復元します。

```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\uSERS\administrator\testExport\" -DecryptionPassword "password" -GroupServiceAccountIdentifier "mangupd1\adfsgmsa$"
```
### <a name="restore-the-ad-fs-configuration-with-the-specified-service-account-creds"></a>指定されたサービス アカウントの資格情報を使用して AD FS 構成を復元します。

```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\uSERS\administrator\testExport\" -DecryptionPassword "password" -ServiceAccountCredential $cred
```

## <a name="encryption-information"></a>暗号化情報
すべてのバックアップ データは、クラウドにプッシュすること、またはファイル システムに格納する前に暗号化されます。  

バックアップの一環として作成される各ドキュメントは、aes-256 で暗号化されます。 ツールに渡されるパスワードは、Rfc2898DeriveBytes クラスを使用して新しいパスワードを生成するパスフレーズとして使用されます。 

RngCryptoServiceProvider を使用して、AES および Rfc2898DeriveBytes クラスによって使用される salt を生成します。 

## <a name="log-files"></a>ログ ファイル
バックアップまたは復元が実行されるたびにログ ファイルが作成されます。 これらは、次の場所で見つかんだことができます。

- **%localappdata%\ADFSRapidRecreationTool**

>[!NOTE]
> 追加の認証プロバイダーの概要を含む PostRestore_Instructions ファイルが作成される可能性がある復元を実行するには、属性を格納し、ローカルの要求プロバイダー信頼と AD FS サービスを開始する前に手動でインストールする場合。

## <a name="version-release-history"></a>バージョン リリース履歴

### <a name="version-10810"></a>バージョン:1.0.81.0
リリース:2019 年 4 月

**修正された問題:**


- 証明書のバックアップと復元のバグの修正
- 別のトレース情報をログ ファイル


### <a name="version-10750"></a>バージョン:1.0.75.0
リリース:2018 年 8 月

**修正された問題:**
* -BackupDKM スイッチを使用する場合は、バックアップ ADFS を更新します。  現在のコンテキストで DKM コンテナーへのアクセスを持つかどうか、ツールが決定されます。  場合は、ドメイン管理者特権またはサービス アカウントの資格情報のいずれかには不要です。  これによりを明示的に資格情報を提供することや、ドメイン管理者アカウントとして実行されているバックアップを自動化できます。

### <a name="version-10730"></a>バージョン:1.0.73.0
リリース:2018 年 8 月

**修正された問題:**
* アプリケーションは、FIPS 準拠するように、暗号化アルゴリズムを更新します。
    
    >[!NOTE]
    > 古いバックアップは、FIPS コンプライアンスに従って暗号化アルゴリズムが変更されたのため、新しいバージョンでは機能しません
    
* マージ レプリケーションを使用する SQL クラスターのサポートを追加します。

### <a name="version-10720"></a>バージョン:1.0.72.0
リリース:2018 年 7 月

**修正された問題:**

   - バグの修正:固定します。インプレース アップグレードをサポートするための MSI インストーラー 

### <a name="10180"></a>1.0.18.0
リリース:2018 年 7 月

**修正された問題:**

   - バグを修正: に特殊文字があるサービス アカウントのパスワードの処理 (つまり、'&')
   - バグを修正: Microsoft.IdentityServer.Servicehost.exe.config が別のプロセスによって使用されているため、復元に失敗


### <a name="1000"></a>1.0.0.0
リリース日。2016 年 10 月

AD FS 迅速な復元ツールの最初のリリース
