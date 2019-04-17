---
title: "SQL Server と Windows Server 2016 の AD FS へのアップグレード"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 70f279bf-aea1-4f4f-9ab3-e9157233e267
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 034d4f1f8d81cf105ba94bff34b180555702acde
ms.sourcegitcommit: 33c1f4965cd2eed7d384a096cfa5c883467b16a4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/02/2017
---
# <a name="upgrading-to-ad-fs-in-windows-server-2016-with-sql-server"></a>SQL Server と Windows Server 2016 の AD FS へのアップグレード

>Windows Server 2016 の適用対象:


## <a name="moving-from-a-windows-server-2012-r2-ad-fs-farm-to-a-windows-server-2016-ad-fs-farm"></a>Windows Server 2012 R2 AD FS ファームから Windows Server 2016 の AD FS ファームへの移行  
次のドキュメントでは、AD FS データベース用 SQL Server を使用しているときに、Windows Server 2016 での AD FS に、AD FS Windows Server 2012 R2 ファームをアップグレードする方法を示します。  

### <a name="upgrading-ad-fs-to-windows-server-2016-fbl"></a>AD FS を Windows Server 2016 FBL にアップグレードします。  
Windows Server 2016 の AD FS では、ファームの動作レベルの機能 (FBL) です。   この機能は、ファーム全体で AD FS ファームを使用できる機能を決定します。   既定では、Windows Server 2012 R2 AD FS ファームで FBL は Windows Server 2012 R2 FBL します。  

Windows Server 2012 R2 のファームに追加できる Windows Server 2016 の AD FS サーバーと Windows Server 2012 R2 として同じ FBL で動作します。  この方法で動作している Windows Server 2016 の AD FS サーバーがある場合は、ファームを「混在させること」と言います。  ただし、しないことができます、FBL が Windows Server 2016 に発生するまでの Windows Server 2016 の新機能を利用します。  混在ファームの場合。  

-   管理者は、新しい、既存の Windows Server 2012 R2 ファームにフェデレーション サーバーを Windows Server 2016 で追加できます。  その結果、ファーム「混在モード」では、Windows Server 2012 R2 ファームレベルの動作の動作します。  ファーム全体で一貫した動作を確認するには、Windows Server 2016 の新機能を構成またはこのモードで使用することはできません。  

-   すべての Windows Server 2012 R2 フェデレーション サーバーは、混在モード ファームから削除されているし、WID ファームの場合 Windows Serve 2016 の新しいフェデレーション サーバーのいずれかに昇格されているプライマリ ノードの役割、管理者は、Windows Server 2012 R2 から Windows Server 2016 への FBL を増やすことができます。  その結果、新しい AD FS Windows Server 2016 機能し、構成して使用できます。  

-   その結果の混在ファームの機能、AD FS Windows Server 2012 R2 の Windows Server 2016 にアップグレードすると考えている組織は、まったく新しいファームを展開する必要はありません、エクスポートし、構成データをインポートします。  代わりに、それがオンライン中に、既存のファームに Windows Server 2016 のノードを追加できのみ FBL 上げるに関連する比較的短いダウンタイムが発生することができます。  

ファームが混在モードで、AD FS ファームがないことの新機能または Windows Server 2016 での AD FS で導入された機能対応に注意してください。  これは、新機能を試したい組織これができない、FBL が発生するまでことを意味します。  その場合は、組織が、FBL rasing する前に新しい機能をテストしようとして、これを行うに個別のファームを展開する必要があります。  

残りの部分は、ドキュメントが Windows Server 2012 R2 環境に Windows Server 2016 のフェデレーション サーバーを追加して、Windows Server 2016 に FBL を発生させるための手順を提供します。  次の手順は、次のアーキテクチャの図で説明されているテスト環境で実行されました。  

> [!NOTE]  
> Windows Server 2016 FBL AD FS に移動するにはすべての Windows 2012 R2 ノードを削除する必要があります。  Windows Server 2016 への Windows Server 2012 R2 の OS のアップグレードし、2016年ノードになることがあるだけできません。  それを削除 2016年の新しいノードを置き換える必要があります。  

次のアーキテクチャ図を検証し、次の手順を記録するために使用されたセットアップを示します。

![アーキテクチャ](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/arch.png) 


#### <a name="join-the-windows-2016-ad-fs-server-to-the-ad-fs-farm"></a>AD FS ファームを Windows 2016 の AD FS サーバーを参加させる

1.  Windows Server 2016 でサーバー マネージャーのインストール、Active Directory フェデレーション サービスの役割を使用してください。  

2.  AD FS 構成ウィザードを使用して、、既存の AD FS ファームを新しい Windows Server 2016 サーバーを参加させます。  **ようこそ**画面をクリックして**次**します。
 ![ファームに参加します。](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/configure1.png)  
3.  **Active Directory ドメイン サービスに接続する**] 画面で、s**管理者アカウントを指定**フェデレーション サービス構成を実行して、[アクセス許可を持つ**次**します。
4.  **指定ファーム**画面で、SQL サーバーとインスタンスの名前を入力し、クリックして**次**します。
![ファームに参加します。](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/configure3.png)
5.  **SSL 証明書の指定**画面で、証明書を指定して] をクリックして**次**します。
![ファームに参加します。](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/configure4.png)
6.  **サービス アカウントの指定**画面で、サービス アカウントを指定して] をクリックして**次**します。 
7.  **オプションの確認**画面で、オプションを確認、] をクリックし、**次**します。 
8.  **の前提条件チェック**画面ことを確認してすべての前提条件チェックの経過した] をクリックして**構成**します。
9.  **結果**画面で、そのサーバーが正常に構成されていることを確認して] をクリックして**閉じる**します。
 
   
#### <a name="remove-the-windows-server-2012-r2-ad-fs-server"></a>Windows Server 2012 R2 AD FS サーバーを削除します。

>[!NOTE]
>セット AdfsSyncProperties を使用して、プライマリ AD FS サーバーを設定する必要がありません-データベースとして SQL を使用する場合の役割。  これは、この構成ではプライマリのすべてのノードと見なされるためです。

1.  サーバー マネージャーの使用中の Windows Server 2012 R2 AD FS サーバーで**役割の削除と機能**下にある**管理**します。 
![サーバーを削除します。](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/remove1.png)
2.  **開始する前に**画面で、[**次**します。
3.  **サーバーの選択**] 画面で、] をクリックして**次**します。
4.  **サーバーの役割**画面で、横にチェック ボックスをオフ**Active Directory フェデレーション サービス**] をクリック**次**します。
![サーバーを削除します。](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/remove2.png)
5.  **機能**] 画面で、] をクリックして**次**します。
6.  **確認**] 画面で、をクリックして**削除**します。
7.  これが完了すると、サーバーを再起動します。
     
#### <a name="raise-the-farm-behavior-level-fbl"></a>(FBL) ファーム動作レベルを上げる
この手順の前に、Active Directory 環境での forestprep と domainprep を実行していることと、Active Directory が、Windows Server 2016 スキーマであることを確認する必要があります。  このドキュメントでは、Windows 2016 ドメイン コント ローラーの概要し、AD のインストール時に実行されたために、これらを実行する必要がありませんでした。

1. 今すぐ Windows Server 2016 サーバーで PowerShell を開き、次を実行します。**$cred = Get-credential**とヒットを入力します。
2. SQL Server に管理者特権を持つ資格情報を入力します。
3. 今すぐ PowerShell では、次を入力します: **Invoke AdfsFarmBehaviorLevelRaise-$cred に資格情報**
2. 入力を求め、入力**Y**します。これにより、レベルを上げることが開始されます。  これが完了すると、FBL 正常が生成されます。  
![更新プログラムを終了します。](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/finish1.png)
3. これで、AD FS の管理に移動した場合は、Windows Server 2016 の AD FS で追加された新しいノードが表示されます。  
4. 同様に、PowerShell コマンドレットを使用することができます。 現在 FBL を表示するには、Get-AdfsFarmInformation します。  
![更新プログラムを終了します。](media/Upgrading-to-AD-FS-in-Windows-Server-2016-SQL/finish2.png)
