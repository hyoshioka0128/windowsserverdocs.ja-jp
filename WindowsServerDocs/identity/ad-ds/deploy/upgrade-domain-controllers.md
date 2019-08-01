---
title: Windows Server 2016 へのドメイン コントローラーのアップグレード
description: このドキュメントでは、Windows Server 2012 R2 から Windows Server 2016 にアップグレードする方法について説明します。
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 3e144a09c99d9b72d623956e868b3f573962ed94
ms.sourcegitcommit: 67833e36b8b2c6194a1426a974c5ad9c859fa4c9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/19/2019
ms.locfileid: "68329638"
---
# <a name="upgrade-domain-controllers-to-windows-server-2016"></a>Windows Server 2016 へのドメイン コントローラーのアップグレード

適用先:Windows Server

このトピックでは、Windows Server 2016 の Active Directory Domain Services に関する背景情報と、Windows Server 2012 または Windows Server 2012 R2 からドメインコントローラーをアップグレードするプロセスについて説明します。

## <a name="pre-requisites"></a>前提条件

ドメインをアップグレードする場合は、新しいバージョンの Windows Server を実行するドメインコントローラーを昇格させ、必要に応じて古いドメインコントローラーを降格する方法をお勧めします。 この方法は、既存のドメイン コントローラーのオペレーティング システムをアップグレードする方法としてお勧めします。 この一覧では、新しいバージョンの Windows Server を実行するドメインコントローラーを昇格する前に実行する一般的な手順について説明します。

1. 対象サーバーがシステム要件を満たしていることを確認します。
1. アプリケーションの互換性を確認します。
1. Windows Server 2016 への移行に関する推奨事項を確認する
1. セキュリティ設定を確認します。 詳細については、「 [Windows Server 2016 の AD DS に関連する非推奨の機能と動作の変更](../../../get-started/deprecated-features.md)」を参照してください。
1. インストールを実行するコンピューターから対象サーバーに接続できることを確認します。
1. 必要な操作マスターの役割を使用できることを確認します。
   - 既存のドメインおよびフォレストで Windows Server 2016 を実行する最初の DC をインストールするには、インストールを実行するコンピューターが**スキーママスター**に接続して、adprep/forestprep とインフラストラクチャマスターを実行し、adprep/を実行する必要があります。domainprep.
   - フォレストスキーマが既に拡張されているドメインに最初の DC をインストールするには、**インフラストラクチャマスター**への接続のみが必要です。
   - 既存のフォレスト内のドメインをインストールまたは削除するには、**ドメイン名前付けマスター**への接続が必要です。
   - ドメインコントローラーのインストールでは、 **RID マスター**への接続も必要です。
   - 最初の読み取り専用ドメインコントローラーを既存のフォレストにインストールする場合は、各アプリケーションディレクトリパーティションの**インフラストラクチャマスター**への接続が必要です。これは、非ドメイン名前付けコンテキストまたは ndnc とも呼ばれます。

### <a name="installation-steps-and-required-administrative-levels"></a>インストール手順と必要な管理レベル

次の表に、アップグレード手順の概要と、これらの手順を完了するためのアクセス許可の要件を示します。

|インストール操作|資格情報の要件|
| ----- | ----- |
|新しいフォレストをインストールする|対象サーバーのローカル Administrator|
|既存のフォレスト内に新しいドメインをインストールする|Enterprise Admins|
|既存ドメイン内に追加 DC をインストールする|Domain Admins|
|adprep /forestprep を実行する|Schema Admins、Enterprise Admins、Domain Admins|
|adprep /domainprep を実行する|Domain Admins|
|adprep /domainprep /gpprep を実行する|Domain Admins|
|adprep /rodcprep を実行する|Enterprise Admins|

Windows Server 2016 の新機能の詳細については、「 [Windows server 2016](../../../get-started/what-s-new-in-windows-server-2016.md)の新機能」を参照してください。

## <a name="supported-in-place-upgrade-paths"></a>サポートされる一括アップグレード パス

Windows Server 2012 または Windows Server 2012 R2 の64ビットバージョンを実行するドメインコントローラーは、Windows Server 2016 にアップグレードできます。 Windows Server 2016 には64ビットバージョンのみが含まれているため、64ビットバージョンのアップグレードのみがサポートされます。

|使用しているエディション|アップグレード先のエディション|
| ----- | ----- |
|Windows Server 2012 Standard|Windows Server 2016 Standard または Datacenter|
|Windows Server 2012 Datacenter|Windows Server 2016 Datacenter|
|Windows Server 2012 R2 Standard|Windows Server 2016 Standard または Datacenter|
|Windows Server 2012 R2 Datacenter|Windows Server 2016 Datacenter|
|Windows Server 2012 R2 Essentials|Windows Server 2016 Essentials|
|Windows Storage Server 2012 Standard|Windows Storage Server 2016 Standard|
|Windows Storage Server 2012 Workgroup|Windows Storage Server 2016 Workgroup|
|Windows Storage Server 2012 R2 Standard|Windows Storage Server 2016 Standard|
|Windows Storage Server 2012 R2 Workgroup|Windows Storage Server 2016 Workgroup|

サポートされているアップグレードパスの詳細については、「[サポートされるアップグレードパス](../../../get-started/supported-upgrade-paths.md)」を参照してください。

## <a name="adprep-and-domainprep"></a>Adprep および Domainprep

既存のドメインコントローラーを Windows Server 2016 オペレーティングシステムにインプレースアップグレードする場合は、adprep/forestprep と adprep/domainprep を手動で実行する必要があります。  Adprep/forestprep は、フォレスト内で1回だけ実行する必要があります。  Adprep/domainprep は、Windows Server 2016 にアップグレードするドメインコントローラーが存在する各ドメインで1回実行する必要があります。

新しい Windows Server 2016 サーバーを昇格する場合は、手動で実行する必要はありません。  これらは、PowerShell とサーバーマネージャーのエクスペリエンスに統合されています。

Adprep の実行の詳細については、「 [adprep の実行](https://technet.microsoft.com/library/dd464018.aspx)」を参照してください。

## <a name="functional-level-features-and-requirements"></a>機能レベルの機能と要件

Windows Server 2016 には、Windows Server 2003 フォレストの機能レベルが必要です。 つまり、Windows Server 2016 を実行するドメインコントローラーを既存の Active Directory フォレストに追加するには、フォレストの機能レベルが Windows Server 2003 以上である必要があります。 Windows Server 2003 以降を実行するドメイン コントローラーがフォレストに含まれており、フォレストの機能レベルが Windows 2000 のレベルである場合も、インストールがブロックされます。

Windows Server 2016 ドメインコントローラーをフォレストに追加する前に、windows 2000 ドメインコントローラーを削除する必要があります。 この場合、次に示すワークフローを検討してください。

1. Windows Server 2003 以降を実行するドメイン コントローラーをインストールします。 これらのドメイン コントローラーは、Windows Server の評価版に展開できます。 この手順では、前提条件として、そのオペレーティングシステムのリリースに対して adprep.exe を実行する必要もあります。
1. Windows 2000 ドメイン コントローラーを削除します。 具体的には、Windows Server 2000 ドメイン コントローラーをドメインから正常に降格するか強制的に削除し、Active Directory ユーザーとコンピューターを使用して、削除されたすべてのドメイン コントローラーのドメイン コントローラー アカウントを削除します。
1. フォレストの機能レベルを Windows Server 2003 以上に昇格します。
1. Windows Server 2016 を実行するドメインコントローラーをインストールします。
1. 以前のバージョンの Windows Server を実行するドメイン コントローラーを削除することはできません。

### <a name="rolling-back-functional-levels"></a>機能レベルのロールバック

フォレストの機能レベル (FFL) を特定の値に設定した後で、フォレストの機能レベルをロールバックしたり下げたりすることはできません。ただし、次の例外があります。

- Windows Server 2012 R2 FFL からアップグレードする場合は、Windows Server 2012 R2 に戻すことができます。
- Windows Server 2008 R2 FFL からアップグレードする場合は、Windows Server 2008 R2 に戻すことができます。

ドメインの機能レベルを特定の値に設定した後で、ドメインの機能レベルをロールバックしたり下げたりすることはできません。ただし、次の例外があります。

- ドメインの機能レベルを Windows Server 2016 に上げたときに、フォレストの機能レベルが Windows Server 2012 以下である場合は、ドメインの機能レベルを Windows Server 2012 または Windows Server 2012 R2 にロールバックするオプションがあります。

低い機能レベルで使用できる機能の詳細については、「 [AD DS の機能レベルとは](../active-directory-functional-levels.md)」を参照してください。

## <a name="ad-ds-interoperability-with-other-server-roles-and-windows-operating-systems"></a>他のサーバー役割および Windows オペレーティング システムとの AD DS の相互運用性

AD DS は、次の Windows オペレーティング システムではサポートされません。

- Windows MultiPoint Server
- Windows Server 2016 Essentials

次のサーバー役割または役割サービスを実行するサーバーに、AD DS をインストールすることはできません。

- Microsoft Hyper-V Server 2016
- リモート デスクトップ接続ブローカー

## <a name="administration-of-windows-server-2016-servers"></a>Windows Server 2016 サーバーの管理

Windows 10 のリモートサーバー管理ツールを使用して、Windows Server 2016 を実行するドメインコントローラーやその他のサーバーを管理します。 Windows 10 を実行しているコンピューターで Windows Server 2016 リモートサーバー管理ツールを実行することができます。

## <a name="step-by-step-for-upgrading-to-windows-server-2016"></a>Windows Server 2016 へのアップグレード手順

Contoso フォレストを Windows Server 2012 R2 から Windows Server 2016 にアップグレードする簡単な例を次に示します。

![アップグレード](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade1.png)

1. 新しい Windows Server 2016 をフォレストに参加させます。 プロンプトが表示されたら再起動します。

   ![アップグレード](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade2.png)

1. ドメイン管理者アカウントを使用して、新しい Windows Server 2016 にサインインします。
1. **サーバー マネージャー** **追加の役割と機能の**、インストール**Active Directory Domain Services**新しい Windows Server 2016 でします。 これにより、2012 R2 フォレストとドメインで adprep が自動的に実行されます。

   ![アップグレード](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade3.png)

1. **サーバーマネージャー**で、黄色い三角形をクリックし、ドロップダウンから [サーバーを**ドメインコントローラーに昇格する**] をクリックします。

   ![アップグレード](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade4.png)

1. **展開構成** 画面で、**ドメインコントローラーを既存のフォレストに追加する** を選択し、次へ をクリックします。

   ![アップグレード](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade5.png)

1. **[ドメインコントローラーオプション]** 画面で、**ディレクトリサービス復元モード (DSRM)** のパスワードを入力し、[次へ] をクリックします。
1. 画面の残りの部分について、 **[次へ]** をクリックします。
1. **[前提条件の確認]** 画面で、 **[インストール]** をクリックします。 再起動が完了したら、サインインし直すことができます。
1. Windows Server 2012 R2 サーバーの**サーバーマネージャー**の [ツール] で、 **[Windows PowerShell の Active Directory モジュール]** を選択します。

   ![アップグレード](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade6.png)

1. PowerShell ウィンドウで、移動-ADDirectoryServerOperationMasterRole を使用して FSMO の役割を移動します。 各 OperationMasterRole の名前を入力するか、数値を使用してロールを指定できます。 詳細については[、「移動-ADDirectoryServerOperationMasterRole](https://technet.microsoft.com/library/hh852302.aspx) 」を参照してください。

    ``` powershell
    Move-ADDirectoryServerOperationMasterRole -Identity "DC-W2K16" -OperationMasterRole 0,1,2,3,4
    ```

    ![アップグレード](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade7.png)

1. Windows Server 2016 サーバーに移動して、役割が移動されたことを確認**サーバー マネージャー** **ツール**、 **Active Directory Module for Windows PowerShell**。 `Get-ADDomain` および`Get-ADForest`コマンドレットを使用して、FSMO の役割所有者を表示します。

    ![アップグレード](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade8.png)

    ![アップグレード](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade9.png)

1. Windows Server 2012 R2 ドメインコントローラーを降格して削除します。 Dc の降格の詳細については、「[ドメインコントローラーと](../../ad-ds/deploy/Demoting-Domain-Controllers-and-Domains--Level-200-.md)ドメインの降格」を参照してください。
1. サーバーが降格され、削除されると、フォレストの機能レベルとドメインの機能レベルを Windows Server 2016 に上げることができます。

## <a name="next-steps"></a>次の手順

- [Active Directory Domain Services のインストールと削除の新機能](../../ad-ds/deploy/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal.md)
- [Active Directory Domain Services &#40;レベル100のインストール&#41;](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md)
- [Windows Server 2016 の機能レベル](../../ad-ds/Windows-Server-2016-Functional-Levels.md)  
