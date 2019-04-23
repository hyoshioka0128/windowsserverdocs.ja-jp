---
title: Windows Server 2016 へのドメイン コントローラーのアップグレード
description: このドキュメントは、Windows Server 2012 R2 から Windows Server 2016 にアップグレードする方法を説明します
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: fe6fb196c996d4d95c6b58d1ab77591602e143d9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59868423"
---
# <a name="upgrade-domain-controllers-to-windows-server-2016"></a>Windows Server 2016 へのドメイン コントローラーのアップグレード

適用先:Windows Server 2016

このトピックでは、Windows Server 2016 での Active Directory Domain Services に関する背景情報を提供し、Windows Server 2012 または Windows Server 2012 R2 からドメイン コント ローラーをアップグレードするプロセスについて説明します。 

## <a name="pre-requisites"></a>前提条件
ドメインをアップグレードすることをお勧めの方法は、新しいバージョンの Windows Server を実行し、必要に応じて古いドメイン コントローラの降格するドメイン コント ローラーに昇格します。 この方法は、既存のドメイン コントローラーのオペレーティング システムをアップグレードする方法としてお勧めします。 この一覧は、新しいバージョンの Windows Server を実行するドメイン コント ローラーを昇格する前にする一般的な手順について説明します。 

1.  対象サーバーがシステム要件を満たしていることを確認します。 
2.  アプリケーションの互換性を確認します。 
3.  Windows Server 2016 への移行の推奨事項を確認します。 
4.  セキュリティ設定を確認します。 詳細については、次を参照してください。[非推奨の機能および動作変更は、Windows Server 2016 での AD DS に関連する](../../../get-started\deprecated-features.md)します。 
5.  インストールを実行するコンピューターから対象サーバーに接続できることを確認します。 
6.  必要な操作マスターの役割を使用できることを確認します。 
    - インストールを実行するマシンを既存のドメインまたはフォレストで Windows Server 2016 を実行する最初の DC をインストールするにはへの接続を必要があります、**スキーマ マスター** adprep/forestprep およびインフラストラクチャ マスターを実行するにはadprep/domainprep を実行します。 
    - フォレスト スキーマが既に拡張されているドメイン内で最初の DC をインストールする場合は、インフラストラクチャ マスターへの接続のみが必要になります。 
    - インストールまたは既存のフォレストでドメインを削除する、接続する必要があります、**ドメイン名前付けマスタ**します。 
    - 任意のドメイン コント ローラーのインストールへの接続も必要です、 **RID マスターします。** 
    - 既存のフォレスト内で最初の読み取り専用のドメイン コントローラーをインストールするには、各アプリケーション ディレクトリ パーティション (ドメインでない名前付けコンテキスト (NDNC) とも呼ばれます) について、インフラストラクチャ マスターへの接続が必要です。 

### <a name="installation-steps-and-required-administrative-levels"></a>インストール手順と必要な管理レベル
次の表は、アップグレードの手順と次の手順を実行するアクセス許可の要件の概要

|インストール操作|資格情報の要件|
| ----- | ----- |
|新しいフォレストをインストールする|対象サーバーのローカル Administrator|
|既存のフォレスト内に新しいドメインをインストールする|Enterprise Admins|
|既存ドメイン内に追加 DC をインストールする|Domain Admins|
|adprep /forestprep を実行する|Schema Admins、Enterprise Admins、Domain Admins|
|adprep /domainprep を実行する|Domain Admins|
|adprep /domainprep /gpprep を実行する|Domain Admins|
|adprep /rodcprep を実行する|Enterprise Admins|

Windows Server 2016 の新機能の詳細については、次を参照してください。 [Windows Server 2016 の新](../../../get-started/what-s-new-in-windows-server-2016.md)します。



## <a name="supported-in-place-upgrade-paths"></a>サポートされる一括アップグレード パス
64 ビット バージョンの Windows Server 2012 または Windows Server 2012 R2 を実行するドメイン コント ローラーは、Windows Server 2016 にアップグレードできます。 Windows Server 2016 でのみ、64 ビット バージョンであるために、のみの 64 ビット バージョンのアップグレードはサポートされています。

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

サポートされるアップグレード パスの詳細については、次を参照してください[サポートされるアップグレード パス。](../../../get-started/supported-upgrade-paths.md)

## <a name="adprep-and-domainprep"></a>Adprep および Domainprep
Windows Server 2016 オペレーティング システムに既存のドメイン コント ローラーのインプレース アップグレードを実行している場合は、手動で adprep/forestprep と adprep/domainprep を実行する必要があります。  Adprep/forestprep をフォレストに 1 回だけ実行する必要があります。  Adprep/domainprep をする必要があるドメイン コント ローラーは、Windows Server 2016 にアップグレードするドメインごとに 1 回実行する必要があります。

新しい Windows Server 2016 サーバーを昇格する場合は、これらを手動で実行する必要はありません。  これらは、PowerShell に統合されて、サーバー マネージャーで発生します。

Adprep の実行の詳細については、次を参照してください[Adprep の実行。](https://technet.microsoft.com/library/dd464018.aspx) 


## <a name="functional-level-features-and-requirements"></a>機能レベルの機能と要件
Windows Server 2016 では、Windows Server 2003 フォレストの機能レベルが必要です。 既存の Active Directory フォレストに Windows Server 2016 を実行するドメイン コント ローラーを追加する前に、フォレストの機能レベルが Windows Server 2003 以降である必要があります。 Windows Server 2003 以降を実行するドメイン コントローラーがフォレストに含まれており、フォレストの機能レベルが Windows 2000 のレベルである場合も、インストールがブロックされます。 

Windows 2000 ドメイン コント ローラーは、Windows Server 2016 のドメイン コント ローラーをフォレストに追加する前に削除する必要があります。 この場合、次に示すワークフローを検討してください。 


1. Windows Server 2003 以降を実行するドメイン コントローラーをインストールします。 これらのドメイン コントローラーは、Windows Server の評価版に展開できます。 この手順では、前提条件として、そのオペレーティング システム リリースの adprep.exe を実行している必要もあります。 
2.  Windows 2000 ドメイン コントローラーを削除します。 具体的には、Windows Server 2000 ドメイン コントローラーをドメインから正常に降格するか強制的に削除し、Active Directory ユーザーとコンピューターを使用して、削除されたすべてのドメイン コントローラーのドメイン コントローラー アカウントを削除します。 
3.  フォレストの機能レベルを Windows Server 2003 以上に昇格します。 
4.  Windows Server 2016 を実行するドメイン コント ローラーをインストールします。 
5.  以前のバージョンの Windows Server を実行するドメイン コントローラーを削除することはできません。 

### <a name="rolling-back-functional-levels"></a>機能レベルをロールバックしています

フォレストの機能レベル (FFL) を特定の値に設定した後、ロールバックするか、次の例外が、フォレストの機能レベルを低くことはできません。 

- Windows Server 2012 R2 FFL からアップグレードする場合は、Windows Server 2012 R2 に下げることができます。 
- Windows Server 2008 R2 FFL からアップグレードする場合は、Windows Server 2008 R2 に下げることができます。

ドメインの機能レベルを特定の値に設定した後は、ロールバックするか、例外を次のドメイン機能レベルを下げることはできません。 

- Windows Server 2016 へのドメイン機能レベルを上げるし、フォレストの機能レベルが Windows Server 2012 またはそれ以下の場合は、ドメインの機能レベルのロールのオプションを Windows Server 2012 または Windows Server 2012 R2 

低い機能レベルで使用できる機能の詳細については、「 [AD DS の機能レベルとは](../active-directory-functional-levels.md)」を参照してください。 
 
## <a name="ad-ds-interoperability-with-other-server-roles-and-windows-operating-systems"></a>他のサーバー役割および Windows オペレーティング システムとの AD DS の相互運用性
AD DS は、次の Windows オペレーティング システムではサポートされません。 


- Windows MultiPoint Server 
- Windows Server 2016 Essentials 

次のサーバー役割または役割サービスを実行するサーバーに、AD DS をインストールすることはできません。 

- Microsoft Hyper-V Server 2016
- リモート デスクトップ接続ブローカー 

## <a name="administration-of-windows-server-2016-servers"></a>Windows Server 2016 サーバーの管理
Windows 10 用のリモート サーバー管理ツールを使用すると、ドメイン コント ローラーと Windows Server 2016 を実行している他のサーバーを管理できます。 Windows 10 を実行しているコンピューターでは、Windows Server 2016 リモート サーバー管理ツールを実行できます。 

## <a name="step-by-step-for-upgrading-to-windows-server-2016"></a>Windows Server 2016 にアップグレードするためのステップ バイ ステップ
次は、Contoso のフォレストを Windows Server 2012 R2 から Windows Server 2016 にアップグレードの単純な例です。

![アップグレード](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade1.png)

1.  新しい Windows Server 2016 をフォレストに参加させます。 入力を求められたら再起動します。 
![アップグレード](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade2.png)
2.  ドメイン管理者アカウントで新しい Windows Server 2016 にサインインします。
3.  **サーバー マネージャー****追加の役割と機能の**、インストール**Active Directory Domain Services**新しい Windows Server 2016 でします。 Adprep が 2012 R2 のフォレストとドメインに自動的に実行されます。
![アップグレード](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade3.png) 
4.  **サーバー マネージャー**を黄色の三角形をクリックし、ドロップダウン リストから次のようにクリックします。**サーバーのドメイン コント ローラーに昇格させる**します。 
![アップグレード](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade4.png)
5.  **配置構成**画面で、**ドメイン コント ローラーを既存のフォレストに追加**し、次へ をクリックします。 
![アップグレード](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade5.png)
6.  **ドメイン コント ローラー オプション**画面で、入力、**ディレクトリ サービス復元モード (DSRM)** パスワードをクリックします [次へ]。 
7.  画面の残りの部分をクリックして**次**します。 
8.  **の前提条件チェック**画面で、**インストール**します。 再起動が完了することがもう一度サインインします。
9.  Windows Server 2012 R2 サーバー上で**サーバー マネージャー**、[ツール] を選択**Active Directory Module for Windows PowerShell**します。 
![アップグレード](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade6.png)
10. PowerShell では、windows は、FSMO の役割を移動するのに移動 ADDirectoryServerOperationMasterRole を使用します。 各 - OperationMasterRole の名前を入力または番号を使用してロールを指定できます。 詳細については、次を参照してください[移動 ADDirectoryServerOperationMasterRole。](https://technet.microsoft.com/library/hh852302.aspx)

   ``` powershell
   Move-ADDirectoryServerOperationMasterRole -Identity "DC-W2K16" -OperationMasterRole 0,1,2,3,4
   ```

   ![アップグレード](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade7.png)</br>
11. Windows Server 2016 サーバーに移動して、役割が移動されたことを確認**サーバー マネージャー****ツール**、 **Active Directory Module for Windows PowerShell**。 使用して、`Get-ADDomain`と`Get-ADForest`FSMO の役割所有者を表示するコマンドレットです。
![アップグレード](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade8.png)
![アップグレード](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade9.png)
12. 降格し、Windows Server 2012 R2 のドメイン コント ローラーを削除します。 Dc を降格する方法の詳細については、次を参照してください[を降格するドメイン コント ローラーとドメイン。](../../ad-ds/deploy/Demoting-Domain-Controllers-and-Domains--Level-200-.md)
13. サーバーを降格し、削除すると、フォレストの機能と Windows Server 2016 のドメイン機能レベルを上げることができます。


## <a name="next-steps"></a>次の手順
-   [新しい Active Directory ドメインではサービスのインストールと削除](../../ad-ds/deploy/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal.md)  
-   [Active Directory Domain Services インストール&#40;レベル 100&#41;](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md)     
-   [Windows Server 2016 の機能レベル](../../ad-ds/Windows-Server-2016-Functional-Levels.md)  
