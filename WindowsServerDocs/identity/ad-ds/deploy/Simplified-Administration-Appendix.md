---
ms.assetid: c911d6c6-98c6-4532-b1db-5724e1ceb96c
title: "簡略化された管理の付録"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 5de7431d0f3fe9a078432b11a63ce996d3abe447
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="simplified-administration-appendix"></a>簡略化された管理の付録

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

  
-   [サーバー マネージャーの追加のサーバー] ダイアログ ボックス (Active Directory)](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_AddServers)  
  
-   [サーバー マネージャーのリモート サーバーの状態](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_ServerMgrStatus)  
  
-   [Windows PowerShell モジュールの読み込み](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_PSLoadModule)  
  
-   [以前のオペレーティング システムの発行の修正プログラムを削除します。](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_Rid)  
  
-   [Ntdsutil.exe インストール メディアの変更](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_IFM)  
  
## <a name="BKMK_AddServers"></a>サーバー マネージャーの追加のサーバー] ダイアログ ボックス (Active Directory)  

**サーバーの追加**ダイアログ ボックスでは、ワイルドカードを使用して、オペレーティング システムおよび場所は、サーバーでは、Active Directory を検索します。 ダイアログ ボックスでは、完全修飾ドメイン名またはプレフィックス名で DNS クエリを使用することもできます。 これらの検索は、.NET、つまり、サーバー マネージャーでの接続のドメイン コントローラーは、Windows Server 2003 にも実行できますが、SOAP を介して AD 管理ゲートウェイに対する AD Windows PowerShell いないによって実装され、ネイティブの DNS および LDAP プロトコルを使用します。 プロビジョニングのためのサーバー名を持つファイルをインポートすることもできます。  
  
Active Directory の検索は、次の LDAP フィルターを使用します。  
  
```  
(&(ObjectCategory=computer)  
  
(&(ObjectCategory=computer)(cn=dc*)(OperatingSystemVersion=6.2*))  
  
(&(ObjectCategory=computer)(OperatingSystemVersion=6.1*))  
  
(&(ObjectCategory=computer)(OperatingSystemVersion=6.0*))  
  
(&(ObjectCategory=computer)(|(OperatingSystemVersion=5.2*)(OperatingSystemVersion=5.1*)))  
  
```  
  
Active Directory の検索では、次の属性が返されます。  
  
```  
( dnsHostName )( operatingSystem )( cn )  
  
```  
  
## <a name="BKMK_ServerMgrStatus"></a>サーバー マネージャーのリモート サーバーの状態  
サーバー マネージャーでは、アドレス ルーティング プロトコルを使用してリモート サーバーのユーザー補助をテストします。 プール内にある場合でも、ARP 要求に応答していないすべてのサーバーは表示されません。  
  
ARP 応答する場合、DCOM と WMI 接続行われますサーバーにステータス情報を返すため。 RPC、DCOM、および WMI がない場合到達可能なサーバー マネージャーは、サーバーを完全に管理することはできません。  
  
## <a name="BKMK_PSLoadModule"></a>Windows PowerShell モジュールの読み込み  
Windows PowerShell 3.0 では、動的モジュールの読み込みを実装します。 使用して、**Import-module**コマンドレットは通常必要ありません。代わりに、単に、コマンドレット、エイリアス、または関数を呼び出すと、モジュールが読み込まれます。  
  
読み込まれたモジュールを表示するを使用して、**Get-module**コマンドレット。  
  
```  
Get-Module  
  
```  
  
![簡略化された管理](media/Simplified-Administration-Appendix/ADDS_PSGetModule.gif)  
  
インストールされているすべてのモジュールがエクスポートされた関数とコマンドレットを参照してくださいを使用します。  
  
```  
Get-Module -ListAvailable  
  
```  
  
使用するためのメインのケース、**モジュールのインポート**コマンドにアクセスする必要がある場合、"AD:"、Windows PowerShell 仮想ドライブが既に読み込まれて、モジュールです。 たとえば、次のコマンドを使用します。  
  
```  
import-module activedirectory  
cd ad:  
dir  
  
```  
  
## <a name="BKMK_Rid"></a>以前のオペレーティング システムの発行の修正プログラムを削除します。  
参照してください[更新プログラムが検出し、Windows Server 2008 R2 を実行しているドメイン コントローラーでグローバル RID プールの過剰消費を防ぐために使用可能な](https://support.microsoft.com/kb/2618669)します。  
  
## <a name="BKMK_IFM"></a>Ntdsutil.exe インストール メディアからの変更します。  
Windows Server 2012 では、次の 2 つの追加オプションを追加、Ntdsutil.exe コマンド ライン ツールを**IFM (IFM メディアの作成)**メニュー。 これらによって、エクスポートした NTDS.DIT はデータベース ファイルです。 ディスク領域が非常に高価でできない場合は、これは、IFM を作成する時間を節約できます。  
  
次の表では、次の 2 つの新しいメニュー項目について説明します。  
  
|||  
|-|-|  
|メニュー項目|説明|  
|完全 NoDefrag %s を作成します|完全 AD DC または %s のフォルダーに/ad LDS インスタンスの最適化を行わずに IFM メディアを作成します。|  
|Sysvol の全 NoDefrag %s を作成します|SYSVOL と %s のフォルダーに完全 AD DC の最適化を行わずに IFM メディアを作成します。|  
  
![簡略化された管理](media/Simplified-Administration-Appendix/ADDS_PSIFM.png)  
  
![簡略化された管理](media/Simplified-Administration-Appendix/ADDS_PSIFMComplete.gif)  
  


