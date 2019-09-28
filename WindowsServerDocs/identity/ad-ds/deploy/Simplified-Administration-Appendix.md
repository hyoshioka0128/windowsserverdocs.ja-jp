---
ms.assetid: c911d6c6-98c6-4532-b1db-5724e1ceb96c
title: '付録: 管理の簡素化'
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: ffc2849fa5e18f7984814d6187cf83d68566409b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71369644"
---
# <a name="simplified-administration-appendix"></a>付録: 管理の簡素化

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

  
-   [サーバーマネージャーサーバーの追加 ダイアログ (Active Directory)](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_AddServers)  
  
-   [リモートサーバーの状態のサーバーマネージャー](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_ServerMgrStatus)  
  
-   [Windows PowerShell モジュールの読み込み](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_PSLoadModule)  
  
-   [以前のオペレーティングシステムの RID 発行修正プログラム](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_Rid)  
  
-   [Ntdsutil.exe メディアの変更からのインストール](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_IFM)  
  
## <a name="BKMK_AddServers"></a>サーバーマネージャーサーバーの追加 ダイアログ (Active Directory)  

**サーバーの追加** ダイアログ ボックスでは、ワイルドカードを使用してオペレーティング システム、および場所は、サーバーでは、Active Directory を検索します。 ダイアログ ボックスでは、完全修飾ドメイン名またはプレフィックス名で DNS クエリを使用することもできます。 これらの検索では、.NET、つまり、サーバー マネージャーでの接続のドメイン コント ローラーは、Windows Server 2003 にも実行できますが、SOAP を介して AD 管理ゲートウェイに対する AD Windows PowerShell ではなくによって実装され、ネイティブの DNS および LDAP プロトコルを使用します。 プロビジョニングのためのサーバー名を持つファイルをインポートすることもできます。  
  
Active Directory の検索では、次の LDAP フィルターを使用します。  
  
```  
(&(ObjectCategory=computer)  
  
(&(ObjectCategory=computer)(cn=dc*)(OperatingSystemVersion=6.2*))  
  
(&(ObjectCategory=computer)(OperatingSystemVersion=6.1*))  
  
(&(ObjectCategory=computer)(OperatingSystemVersion=6.0*))  
  
(&(ObjectCategory=computer)(|(OperatingSystemVersion=5.2*)(OperatingSystemVersion=5.1*)))  
  
```  
  
Active Directory の検索には、次の属性が返されます。  
  
```  
( dnsHostName )( operatingSystem )( cn )  
  
```  
  
## <a name="BKMK_ServerMgrStatus"></a>リモートサーバーの状態のサーバーマネージャー  
サーバー マネージャーでは、アドレス ルーティング プロトコルを使用してリモート サーバーのユーザー補助をテストします。 プール内にある場合でも、ARP 要求に応答していないすべてのサーバーは表示されません。  
  
ARP 応答があった場合、DCOM と WMI に接続できるサーバーにステータス情報を返します。 場合 RPC、DCOM、および WMI では、到達可能なサーバー マネージャーは、サーバーを完全に管理することはできません。  
  
## <a name="BKMK_PSLoadModule"></a>Windows PowerShell モジュールの読み込み  
Windows PowerShell 3.0 では、動的モジュールの読み込みを実装します。 使用して、 **Import-module** コマンドレットは通常必要なくなりました。 代わりに、単に、コマンドレット、エイリアス、または関数を呼び出すモジュールを読み込みます。  
  
読み込まれたモジュールを表示するを使用して、 **Get-module** コマンドレットです。  
  
```  
Get-Module  
  
```  
  
![管理の簡略化](media/Simplified-Administration-Appendix/ADDS_PSGetModule.gif)  
  
そのエクスポートされた関数とコマンドレットにインストールされているすべてのモジュールを表示するには、次のコマンドを使用します。  
  
```  
Get-Module -ListAvailable  
  
```  
  
**[モジュールのインポート]** コマンドを使用する場合の主な例は、"AD:" にアクセスする必要がある場合です。Windows PowerShell 仮想ドライブと、モジュールが既に読み込まれているものはありません。 たとえば、次のコマンドを使用します。  
  
```  
import-module activedirectory  
cd ad:  
dir  
  
```  
  
## <a name="BKMK_Rid"></a>以前のオペレーティングシステムの RID 発行修正プログラム  
参照してください [を検出し、Windows Server 2008 R2 を実行しているドメイン コント ローラーでグローバル RID プールの過剰消費を防ぐ更新プログラムがある](https://support.microsoft.com/kb/2618669)です。  
  
## <a name="BKMK_IFM"></a>Ntdsutil.exe メディアの変更からのインストール  
Windows Server 2012 は、Ntdsutil.exe コマンド ライン ツールを 2 つの追加のオプションを追加、 **IFM (IFM メディアの作成)** メニュー。 これらによって、エクスポートされた NTDS のオフラインでの最適化を実行せずに IFM ストアを作成できます。DIT のデータベース ファイルです。 ディスク領域が非常に高価でできない場合は、これは、IFM を作成する時間を保存します。  
  
次の表では、2 つの新しいメニュー項目について説明します。  
  
|||  
|-|-|  
|メニュー項目|説明|  
|完全 NoDefrag %s を作成します。|AD のフル DC または %s のフォルダーに/AD LDS インスタンスの最適化を行わずに IFM メディアを作成します。|  
|Sysvol の全 NoDefrag %s を作成します。|SYSVOL と %s のフォルダーに完全 AD DC の最適化を行わずに IFM メディアを作成します。|  
  
![管理の簡略化](media/Simplified-Administration-Appendix/ADDS_PSIFM.png)  
  
![管理の簡略化](media/Simplified-Administration-Appendix/ADDS_PSIFMComplete.gif)  
  


