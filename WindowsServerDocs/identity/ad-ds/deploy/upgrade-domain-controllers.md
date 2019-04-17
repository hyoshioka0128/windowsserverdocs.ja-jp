---
title: "ドメイン コント ローラーを Windows Server 2016 にアップグレードします。"
description: "このドキュメントは、Windows Server 2012 R2 から Windows Server 2016 にアップグレードする方法を説明します。"
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 187972c2f44a4d7f91b1b3ac1c905529564cfa6d
ms.sourcegitcommit: f748c6c4ce700b0787ffdd1fca620c21c4331fd2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/21/2017
---
# <a name="upgrade-domain-controllers-to-windows-server-2016"></a>ドメイン コント ローラーを Windows Server 2016 にアップグレードします。

Windows Server 2016 の適用対象:

このトピックでは、Windows Server 2016 での Active Directory ドメイン サービスに関する背景情報を提供し、Windows Server 2012 または Windows Server 2012 R2 からドメイン コント ローラーをアップグレードするプロセスについて説明します。 

## <a name="pre-requisites"></a>前提条件
ドメインをアップグレードすることをお勧めは新しいバージョンの Windows Server を実行し、必要に応じて古いドメイン コントローラの降格するドメイン コント ローラーに昇格することです。 そのメソッドは、既存のドメイン コント ローラーのオペレーティング システムをアップグレードすることをお勧めします。 この一覧は、新しいバージョンの Windows Server を実行するドメイン コント ローラーを昇格する前に実行する一般的な手順について説明します。 

1.  ターゲット サーバーは、システム要件を満たしていることを確認します。 
2.  アプリケーションの互換性を確認します。 
3.  Windows Server 2016 に移るための推奨事項を確認します。 
4.  セキュリティ設定を確認します。 詳細については、次を参照してください。[推奨されなくなった機能および動作変更は、Windows Server 2016 での AD DS に関連する](../../../get-started\deprecated-features.md)します。 
5.  インストールを実行するコンピューターからターゲット サーバーへの接続を確認します。 
6.  必要な操作マスターの役割の可用性を確認します。 
    - 既存のドメインまたはフォレストでの Windows Server 2016 を実行する最初の DC をインストールするには、インストールを実行するコンピューターに接続が必要、**スキーマ マスター** adprep/domainprep を実行するために、adprep/forestprep およびインフラストラクチャ マスターを実行するためにします。 
    - フォレスト スキーマが既に拡張ドメイン内の最初の DC をインストールするには、インフラストラクチャ マスターへの接続のみ必要。 
    - 既存のフォレストにドメインを削除またはをインストールする必要がありますへの接続、**ドメイン名前付けマスタ**します。 
    - 任意のドメイン コント ローラーのインストールへの接続も必要です、 **RID マスターします。** 
    - 既存のフォレスト内の最初の読み取り専用ドメイン コント ローラーをインストールする場合はの各アプリケーション ディレクトリ パーティション、ドメインでない名前付けコンテキストまたは NDNC とも呼ばれる、インフラストラクチャ マスターへの接続をする必要があります。 

### <a name="installation-steps-and-required-administrative-levels"></a>インストール手順を実行し、必要な管理レベル
次の表に、アップグレードの手順を実行し、次の手順を実行するアクセス許可の要件の概要

|インストールの操作|資格情報の要件|
| ----- | ----- |
|新しいフォレストをインストールします。|ターゲット サーバーのローカル管理者アカウント|
|既存のフォレストに新しいドメインをインストールします。|Enterprise Admins|
|既存のドメインに追加の DC をインストールします。|Domain Admins|
|Adprep/forestprep を実行します。|Schema Admins、Enterprise Admins、Domain Admins|
|Adprep/domainprep を実行します。|Domain Admins|
|Adprep/domainprep/gpprep を実行します。|Domain Admins|
|Adprep/rodcprep を実行します。|Enterprise Admins|

Windows Server 2016 の新機能の追加については、次を参照してください。 [Windows Server 2016 の新着](../../../get-started/what-s-new-in-windows-server-2016.md)します。



## <a name="supported-in-place-upgrade-paths"></a>サポートされる一括アップグレード パス
64 ビット バージョンの Windows Server 2012 または Windows Server 2012 R2 を実行するドメイン コントローラーは、Windows Server 2016 にアップグレードすることができます。 64 ビット バージョンの Windows Server 2016 にのみ基づくものために、64 ビット バージョンのアップグレードのみがサポートされています。

|このエディションを実行している: 場合|これらのエディションにアップグレードすることができます。|
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

サポートされるアップグレード パスに関する詳細については、次を参照してください[サポートされるアップグレード パス。](../../../get-started/supported-upgrade-paths.md)

## <a name="adprep-and-domainprep"></a>Adprep およびドメインの準備
Windows Server 2016 オペレーティング システムに既存のドメイン コント ローラーのインプレース アップグレードを実行する場合は、手動で adprep/forestprep と adprep/domainprep を実行する必要があります。  Adprep/forestprep は、フォレスト内に 1 回だけ実行する必要があります。  Adprep/domainprep を Windows Server 2016 にアップグレードしているドメイン コント ローラーがあるドメインごとに 1 回実行する必要があります。

新しい Windows Server 2016 サーバーを昇格する場合は、これらを手動で実行する必要はありません。  これらは、PowerShell に統合されてし、サーバー マネージャーのエクスペリエンスします。

Adprep の実行の詳細については、次を参照してください[Adprep の実行。](https://technet.microsoft.com/library/dd464018.aspx) 


## <a name="functional-level-features-and-requirements"></a>機能レベルの機能と要件
Windows Server 2016 では、Windows Server 2003 フォレストの機能レベルが必要です。 つまり、既存の Active Directory フォレストに Windows Server 2016 を実行するドメイン コント ローラーを追加する前に、フォレストの機能レベルが Windows Server 2003 以降である必要があります。 Windows Server 2003 を実行するドメイン コント ローラーがフォレストに含まれている場合か、後で、フォレストの機能が、レベルが Windows 2000、インストールがブロックされてもします。 

Windows 2000 ドメイン コント ローラーは、Windows Server 2016 ドメイン コント ローラーをフォレストに追加する前に削除する必要があります。 この場合は、次のワークフローを検討してください。 


1. またはを実行する Windows Server 2003 以降のドメイン コント ローラーをインストールします。 Windows Server の評価版では、これらのドメイン コント ローラーを展開できます。 この手順では、前提条件としてそのオペレーティング システム リリースのための adprep.exe の実行も必要です。 
2.  Windows 2000 ドメイン コント ローラーを削除します。 具体的には、正常に降格か、ドメインと使用されている Active Directory ユーザーとすべての削除されたドメイン コント ローラーのドメイン コント ローラー アカウントを削除するコンピューターから Windows Server 2000 ドメイン コント ローラーを強制的に削除します。 
3.  フォレストの機能レベルを Windows Server 2003 以上を生成します。 
4.  Windows Server 2016 を実行するドメイン コント ローラーをインストールします。 
5.  以前のバージョンの Windows Server を実行するドメイン コント ローラーを削除します。 

### <a name="rolling-back-functional-levels"></a>機能レベルをロールバックします。

フォレストの機能レベル (FFL) を特定の値に設定した後は、ロールバックまたは次の例外を除き、フォレストの機能レベルを下げることはできません。 

- Windows Server 2012 R2 FFL からアップグレードする場合は、Windows Server 2012 R2 に下げることができます。 
- Windows Server 2008 R2 FFL からアップグレードする場合は、Windows Server 2008 R2 に下げることができます。

ドメインの機能レベルを特定の値に設定した後は、ロールバックまたは次の例外を除き、ドメインの機能レベルを下げることはできません。 

- ドメインの機能レベルをロールバックのオプションが Windows Server 2012 または Windows Server 2012 R2 に戻すときに、Windows Server 2016 へのドメイン機能レベルを上げるし、フォレストの機能レベルが Windows Server 2012 またはそれ以下の場合は、 

低い機能レベルで使用可能な機能の詳細については、次を参照してください。[について Active Directory ドメイン サービス (AD DS) の機能レベル](../active-directory-functional-levels.md)します。 
 
## <a name="ad-ds-interoperability-with-other-server-roles-and-windows-operating-systems"></a>その他のサーバーの役割と Windows オペレーティング システムと AD DS の相互運用
AD DS は、次の Windows オペレーティング システムでサポートされていません。 


- Windows MultiPoint Server 
- Windows Server 2016 Essentials 

次のサーバーの役割または役割サービスを実行しているサーバーで AD DS をインストールすることはできません。 

- Microsoft HYPER-V Server 2016
- リモート デスクトップ接続ブローカー 

## <a name="administration-of-windows-server-2016-servers"></a>Windows Server 2016 サーバーの管理
Windows 10 用のリモート サーバー管理ツールを使用すると、ドメイン コント ローラーと Windows Server 2016 を実行している他のサーバーを管理できます。 Windows 10 を実行しているコンピューターでは、Windows Server 2016 リモート サーバー管理ツールを実行できます。 

## <a name="step-by-step-for-upgrading-to-windows-server-2016"></a>Windows Server 2016 へのアップグレードの詳細な手順
Windows Server 2012 R2 から Windows Server 2016 に Contoso のフォレストをアップグレードする場合の簡単な例を次に示します。

![アップグレード](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade1.png)

1.  新しい Windows Server 2016 をフォレストに参加します。 表示されたら再起動します。 
![アップグレード](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade2.png)
2.  ドメイン管理者アカウントを使用して新しい Windows Server 2016 にサインインします。
3.  **サーバー マネージャー**[**追加の役割と機能**、インストール**Active Directory Domain Services**新しい Windows Server 2016 でします。 2012 R2 のフォレストとドメインで adprep が自動的に実行されます。
![アップグレード](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade3.png) 
4.  **サーバー マネージャー**、黄色の三角形をクリックし、ドロップダウン リストから次のようにクリックします。**サーバーをドメイン コント ローラーに昇格**します。 
![アップグレード](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade4.png)
5.  **展開構成**画面で、**ドメイン コント ローラーを既存のフォレストに追加**し、[次へ] をクリックします。 
![アップグレード](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade5.png)
6.  **ドメイン コント ローラー オプション**画面で、入力、**ディレクトリ サービス復元モード (DSRM)**パスワードとをクリックして [次へ]。 
7.  残りの画面をクリックして**次**します。 
8.  **の前提条件チェック**画面で、[**インストール**します。 再起動が完了することができますにもう一度サインインします。
9.  Windows Server 2012 R2 サーバーで、[**サーバー マネージャー**、[ツール] を選択**Active Directory 用 Windows PowerShell モジュール**します。 
![アップグレード](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade6.png)
10. PowerShell ウィンドウを使用して移動 ADDirectoryServerOperationMasterRole FSMO の役割を移動します。 各 - OperationMasterRole の名前を入力するか、番号を使用して役割を指定します。 番号。 詳細については、次を参照してください[移動 ADDirectoryServerOperationMasterRole。](https://technet.microsoft.com/library/hh852302.aspx)

``` powershell
Move-ADDirectoryServerOperationMasterRole -Identity "DC-W2K16" -OperationMasterRole 0,1,2,3,4
```

![アップグレード](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade7.png)</br>
11. Windows Server 2016 サーバーに移動して、役割が移動されたことを確認**サーバー マネージャー**[**ツール**[ **Active Directory 用 Windows PowerShell モジュール**します。 使用して、`Get-ADDomain`と`Get-ADForest`FSMO の役割所有者を表示するコマンドレットです。
![のアップグレード] (media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade8.png)
![アップグレード](media/Upgrade-Domain-Controllers-to-Windows-Server-2016/upgrade9.png)
12. 降格し、Windows Server 2012 R2 ドメイン コント ローラーを削除します。 Dc を降格する方法の詳細については、次を参照してください[を降格するドメイン コント ローラーとドメイン。](../../ad-ds/deploy/Demoting-Domain-Controllers-and-Domains--Level-200-.md)
13. サーバーを降格し、削除した後、フォレストの機能と Windows Server 2016 へのドメイン機能レベルを上げることができます。


## <a name="next-steps"></a>次の手順
-   [新機能の Active Directory ドメイン サービスのインストールと削除](../../ad-ds/deploy/What-s-New-in-Active-Directory-Domain-Services-Installation-and-Removal.md)  
-   [Active Directory ドメイン サービス (&) #40; をインストールします。Level 100 & #41 です。](../../ad-ds/deploy/Install-Active-Directory-Domain-Services--Level-100-.md)     
-   [Windows Server 2016 の機能レベル](../../ad-ds/Windows-Server-2016-Functional-Levels.md)  
