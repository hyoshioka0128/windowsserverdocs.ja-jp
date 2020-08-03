---
ms.assetid: c911d6c6-98c6-4532-b1db-5724e1ceb96c
title: '付録: 管理の簡素化'
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: c92f2633bea6def335ab50f93f0c95b48b9677b0
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2020
ms.locfileid: "87519439"
---
# <a name="simplified-administration-appendix"></a>付録: 管理の簡素化

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

-   [サーバー マネージャーの追加のサーバー] ダイアログ ボックス (Active Directory)](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_AddServers)

-   [サーバー マネージャーのリモート サーバーの状態](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_ServerMgrStatus)

-   [Windows PowerShell モジュールの読み込み](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_PSLoadModule)

-   [以前のオペレーティング システムの発行の修正プログラムを削除します。](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_Rid)

-   [Ntdsutil.exe インストール メディアからの変更します。](../../ad-ds/deploy/Simplified-Administration-Appendix.md#BKMK_IFM)

## <a name="server-manager-add-servers-dialog-active-directory"></a><a name="BKMK_AddServers"></a>サーバー マネージャーの追加のサーバー] ダイアログ ボックス (Active Directory)

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

## <a name="server-manager-remote-server-status"></a><a name="BKMK_ServerMgrStatus"></a>サーバー マネージャーのリモート サーバーの状態
サーバー マネージャーでは、アドレス ルーティング プロトコルを使用してリモート サーバーのユーザー補助をテストします。 プール内にある場合でも、ARP 要求に応答していないすべてのサーバーは表示されません。

ARP 応答があった場合、DCOM と WMI に接続できるサーバーにステータス情報を返します。 場合 RPC、DCOM、および WMI では、到達可能なサーバー マネージャーは、サーバーを完全に管理することはできません。

## <a name="windows-powershell-module-loading"></a><a name="BKMK_PSLoadModule"></a>Windows PowerShell モジュールの読み込み
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

使用するためのメインのケース、 **モジュールのインポート** コマンドにアクセスする必要がある場合、"AD:"、Windows PowerShell 仮想ドライブが既に読み込まれて、モジュールです。 たとえば、次のコマンドを使用します。

```
import-module activedirectory
cd ad:
dir

```

## <a name="rid-issuance-hotfixes-for-previous-operating-systems"></a><a name="BKMK_Rid"></a>以前のオペレーティング システムの発行の修正プログラムを削除します。
参照してください [を検出し、Windows Server 2008 R2 を実行しているドメイン コント ローラーでグローバル RID プールの過剰消費を防ぐ更新プログラムがある](https://support.microsoft.com/kb/2618669)です。

## <a name="ntdsutilexe-install-from-media-changes"></a><a name="BKMK_IFM"></a>Ntdsutil.exe インストール メディアからの変更します。
Windows Server 2012 は、Ntdsutil.exe コマンド ライン ツールを 2 つの追加のオプションを追加、 **IFM (IFM メディアの作成)** メニュー。 これらによって、エクスポートされた NTDS のオフラインでの最適化を実行せずに IFM ストアを作成できます。DIT のデータベース ファイルです。 ディスク領域が非常に高価でできない場合は、これは、IFM を作成する時間を保存します。

次の表では、2 つの新しいメニュー項目について説明します。

|メニュー項目|説明|
|--|--|
|完全 NoDefrag %s を作成します。|AD のフル DC または %s のフォルダーに/AD LDS インスタンスの最適化を行わずに IFM メディアを作成します。|
|Sysvol の全 NoDefrag %s を作成します。|SYSVOL と %s のフォルダーに完全 AD DC の最適化を行わずに IFM メディアを作成します。|

![管理の簡略化](media/Simplified-Administration-Appendix/ADDS_PSIFM.png)

![管理の簡略化](media/Simplified-Administration-Appendix/ADDS_PSIFMComplete.gif)
