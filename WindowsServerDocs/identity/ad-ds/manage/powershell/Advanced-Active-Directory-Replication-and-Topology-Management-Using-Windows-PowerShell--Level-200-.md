---
ms.assetid: fe05e52c-cbf8-428b-8176-63407991042f
title: Advanced Active Directory Replication and Topology Management Using Windows PowerShell (Level 200)
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: eeac84fb4e875ffe31b560bc72190895cd0527bc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402679"
---
# <a name="advanced-active-directory-replication-and-topology-management-using-windows-powershell-level-200"></a>Advanced Active Directory Replication and Topology Management Using Windows PowerShell (Level 200)

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックでは、AD DS のレプリケーションとトポロジを管理するための新しいコマンドレットの詳細を説明し、いくつかの例を示します。 概要については、「 [Windows &#40;PowerShell レベル&#41;100 を使用した Active Directory レプリケーションとトポロジ管理の概要](../../../ad-ds/manage/powershell/Introduction-to-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-100-.md)」を参照してください。  
  
1.  [はじめに](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_Intro)  
  
2.  [レプリケーションとメタデータ](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_Repl)  
  
3.  [ADReplicationAttributeMetadata](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_ReplAttrMD)  
  
4.  [Get-ADReplicationPartnerMetadata](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_PartnerMD)  
  
5.  [Get-ADReplicationFailure](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_ReplFail)  
  
6.  [Get-adreplicationqueueoperation および get-adreplicationuptodatenessvectortable を取得します。](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_ReplQueue)  
  
7.  [Sync-ADObject](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_Sync)  
  
8.  [モジュール](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_Topo)  
  
## <a name="BKMK_Intro"></a>基礎  
Windows Server 2012 では、Windows PowerShell の Active Directory モジュールが拡張され、レプリケーションとフォレスト トポロジを管理するための 25 個の新しいコマンドレットが追加されました。 この前に、汎用 **\*AdObject**の名詞を使用するか、.net 関数を呼び出す必要がありました。  
  
すべての Active Directory Windows PowerShell コマンドレットと同様に、この新しい機能を使用するには、 [Active Directory 管理ゲートウェイ サービス](https://www.microsoft.com/download/details.aspx?displaylang=en&id=2852) を 1 つ以上のドメイン コントローラー (可能であれば、すべてのドメイン コントローラー) にインストールする必要があります。  
  
次の表に、Active Directory Windows PowerShell モジュールに追加された、レプリケーションおよびトポロジに関する新しいコマンドレットの一覧を示します。  
  
|||  
|-|-|  
|コマンドレット|説明|  
|Get-ADReplicationAttributeMetadata|オブジェクトの属性レプリケーション メタデータを返します|  
|Get-ADReplicationConnection|ドメイン コントローラー接続オブジェクトの詳細を返します|  
|Get-ADReplicationFailure|ドメイン コントローラーの最新のレプリケーション エラーを返します|  
|Get-ADReplicationPartnerMetadata|ドメイン コントローラーのレプリケーション構成を返します|  
|Get-ADReplicationQueueOperation|現在のレプリケーション キューのバックログを返します|  
|Get-ADReplicationSite|サイト情報を返します|  
|Get-ADReplicationSiteLink|サイト リンク情報を返します|  
|Get-ADReplicationSiteLinkBridge|サイト リンク ブリッジ情報を返します|  
|Get-ADReplicationSubnet|AD サブネット情報を返します|  
|Get-ADReplicationUpToDatenessVectorTable|ドメイン コントローラーの UTD ベクターを返します|  
|Get-ADTrust|ドメイン間信頼またはフォレスト間信頼に関する情報を返します|  
|New-ADReplicationSite|新しいサイトを作成します|  
|New-ADReplicationSiteLink|新しいサイト リンクを作成します|  
|New-ADReplicationSiteLinkBridge|新しいサイト リンク ブリッジを作成します|  
|New-ADReplicationSubnet|新しい AD サブネットを作成します|  
|Remove-ADReplicationSite|サイトを削除します|  
|Remove-ADReplicationSiteLink|サイト リンクを削除します|  
|Remove-ADReplicationSiteLinkBridge|サイト リンク ブリッジを削除します|  
|Remove-ADReplicationSubnet|AD サブネットを削除します|  
|Set-ADReplicationConnection|接続を変更します|  
|Set-ADReplicationSite|サイトを変更します|  
|Set-ADReplicationSiteLink|サイト リンクを変更します|  
|Set-ADReplicationSiteLinkBridge|サイト リンク ブリッジを変更します|  
|Set-ADReplicationSubnet|AD サブネットを変更します|  
|Sync-ADObject|単一オブジェクトのレプリケーションを強制します|  
  
これらのコマンドレットのほとんどは、Repadmin.exe を基に作成されています。 上記の表にない他のコマンドレットは、ダイナミック アクセス制御やグループの管理されたサービス アカウントのような機能を扱います。  
  
すべての Active Directory Windows PowerShell コマンドレットの一覧を取得するには、次のコマンドを実行します。  
  
```  
Get-command -module ActiveDirectory  
```  
  
すべての Active Directory Windows PowerShell コマンドレットの引数の一覧については、ヘルプを参照してください。 次に、例を示します。  
  
```  
Get-help New-ADReplicationSite  
  
```  
  
ヘルプ ファイルをダウンロードしてインストールするには、`Update-Help` コマンドレットを使用します。  
  
### <a name="BKMK_Repl"></a>レプリケーションとメタデータ  
Repadmin.exe は、Active Directory レプリケーションの正常性と一貫性を検証します。 Repadmin.exe には簡単なデータ操作オプションがあり、たとえば、いくつかの引数では CSV 出力をサポートしていますが、自動処理を行うには、一般にテキスト ファイル出力を通じた解析が必要でした。 Windows PowerShell の Active Directory モジュールが提供するオプションにより、返されるデータを完全に制御できるようになりました。これを行うには、以前はスクリプトを作成するか、サードパーティ製のツールを使用する必要がありました。  
  
さらに、次のコマンドレットでは、新しいパラメーター セットである **Target**、**Scope**、および **EnumerationServer** が実装されています。  
  
-   **Get-ADReplicationFailure**  
  
-   **Get-ADReplicationPartnerMetadata**  
  
-   **Get-adreplicationqueueoperation および get-adreplicationuptodatenessvectortable**  
  
**Target** 引数は、**Scope** 引数で指定されたターゲットのサーバー、サイト、ドメイン、またはフォレストを識別する文字列のコンマ区切り一覧を受け入れます。 アスタリスク (\*) も許容され、指定したスコープ内のすべてのサーバーを意味します。 スコープが指定されていない場合は、現在のユーザーのフォレスト内のすべてのサーバーを意味します。 **Scope** 引数は検索の範囲を指定します。 指定できる値は、 **Server**、 **Site**、 **Domain**、および **Forest**です。 **EnumerationServer** は、 **Target** および **Scope**で指定されたドメイン コントローラーの一覧を列挙するサーバーを指定します。 **Server** 引数と同じように動作し、指定したサーバーで Active Directory Web サービスが実行されている必要があります。  
  
新しいコマンドレットの概要を説明するために、いくつかのサンプル シナリオを通じて repadmin.exe では実行できない機能を示します。これらの例から、コマンドレットで実行できる管理操作を把握することができます。 特定の使用上の要件については、コマンドレットのヘルプを参照してください。  
  
### <a name="BKMK_ReplAttrMD"></a>ADReplicationAttributeMetadata  
このコマンドレットは、**repadmin.exe /showobjmeta** と似ています。 属性の変更日時、発信元のドメイン コントローラー、バージョンおよび USN 情報、属性データなどのレプリケーション メタデータを返すことができます。 このコマンドレットは、変更が発生した場所と時間を監査するのに役立ちます。  
  
Repadmin とは異なり、Windows PowerShell では検索と出力を柔軟に制御することができます。 たとえば、Domain Admins オブジェクトのメタデータを、読みやすい順序に並べた一覧として出力できます。  
  
```  
Get-ADReplicationAttributeMetadata -object "cn=domain admins,cn=users,dc=corp,dc=contoso,dc=com" -server dc1.corp.contoso.com -showalllinkedvalues | format-list  
  
```  
  
![powershell を使用した高度な管理](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplAttrMd.png)  
  
repadmin と同じようにデータを表形式で出力することもできます。  
  
```  
Get-ADReplicationAttributeMetadata -object "cn=domain admins,cn=users,dc=corp,dc=contoso,dc=com" -server dc1.corp.contoso.com -showalllinkedvalues | format-table -wrap  
  
```  
  
![powershell を使用した高度な管理](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplAttrMdTable.png)  
  
オブジェクトのクラス全体のメタデータを取得できます。このためには、**Get-Adobject** コマンドレットですべてのグループなどのフィルターを使用し、パイプラインで結果を渡して、特定の日付と組み合わせます。 パイプラインは、複数のコマンドレット間でデータを渡すときに使用するチャネルです。 2012 年 1 月 13 日に何らかの方法で変更されたグループをすべて表示するには、次のコマンドを実行します。  
  
```  
get-adobject -filter 'objectclass -eq "group"' | Get-ADReplicationAttributeMetadata -server dc1.corp.contoso.com | where-object {$_.lastoriginatingchangetime -like "*1/13/2012*" -and $_.attributename -eq "name"} | format-table object  
```  
  
![powershell を使用した高度な管理](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplAttrMdClass.png)  
  
パイプラインを使用した Windows PowerShell 操作の詳細については、 [Windows PowerShell のパイプ処理とパイプラインに関するページ](https://technet.microsoft.com/library/ee176927.aspx)を参照してください。  
  
メンバーに Tony Wang が含まれるすべてのグループを検索し、それらのグループが最後に変更された日時を表示するには、次のコマンドを実行します。  
  
```  
get-adobject -filter 'objectclass -eq "group"' | Get-ADReplicationAttributeMetadata -server dc1.corp.contoso.com -showalllinkedvalues | where-object {$_.attributevalue -like "*tony wang*"} | format-table object,LastOriginatingChangeTime,version -auto  
  
```  
  
![powershell を使用した高度な管理](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplAttrMdFilter.png)  
  
ドメインのシステム状態バックアップを使用して正式に復元されたすべてのオブジェクトを、意図的に指定された高いバージョン番号に基づいて検索するには、次のコマンドを実行します。  
  
```  
get-adobject -filter 'objectclass -like "*"' | Get-ADReplicationAttributeMetadata -server dc1.corp.contoso.com | where-object {$_.version -gt "100000" -and $_.attributename -eq "name"} | format-table object,LastOriginatingChangeTime  
```  
  
![powershell を使用した高度な管理](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplAttrMdFilter2.png)  
  
すべてのユーザーのメタデータを CSV ファイルに送信し、後から Microsoft Excel で調査できるようにするには、次のコマンドを実行します。  
  
```  
get-adobject -filter 'objectclass -eq "user"' | Get-ADReplicationAttributeMetadata -server dc1.corp.contoso.com -showalllinkedvalues | export-csv allgroupmetadata.csv  
```  
  
### <a name="BKMK_PartnerMD"></a>Get-ADReplicationPartnerMetadata  
このコマンドレットは、ドメイン コントローラーのレプリケーションの構成と状態に関する情報を返すことで、それらの情報の監視、インベントリ作成、トラブルシューティングが可能になります。 Repadmin.exe とは異なり、Windows PowerShell を使用すると、重要なデータのみを希望の形式で表示できます。  
  
たとえば、単一のドメイン コントローラーのレプリケーションの状態を読みやすい形式で表示するには、次のコマンドを実行します。  
  
```  
Get-ADReplicationPartnerMetadata -target dc1.corp.contoso.com  
```  
  
![powershell を使用した高度な管理](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplPartnerMd.png)  
  
ドメイン コントローラーが入力方向に最後にレプリケートされた日時とそのパートナーを表形式で表示するには、次のコマンドを実行します。  
  
```  
Get-ADReplicationPartnerMetadata -target dc1.corp.contoso.com | format-table lastreplicationattempt,lastreplicationresult,partner -auto  
```  
  
![powershell を使用した高度な管理](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplPartnerMdTable.png)  
  
フォレスト内のすべてのドメイン コントローラーに接続し、最後に試行されたレプリケーションが何らかの理由で失敗したドメイン コントローラーを表示するには、次のコマンドを実行します。  
  
```  
Get-ADReplicationPartnerMetadata -target * -scope server | where {$_.lastreplicationresult -ne "0"} | ft server,lastreplicationattempt,lastreplicationresult,partner -auto  
  
```  
  
![powershell を使用した高度な管理](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplPartnerMdFail.png)  
  
### <a name="BKMK_ReplFail"></a>Get-ADReplicationFailure  
このコマンドレットは、最近発生したレプリケーション エラーの情報を返すために使用できます。 **Repadmin.exe /showreplsum**と似ていますが、Windows PowerShell によって細かい制御が可能です。  
  
たとえば、ドメイン コントローラーの最新のエラーや、接続に失敗したパートナーを返すことができます。  
  
```  
Get-ADReplicationFailure dc1.corp.contoso.com  
```  
  
![powershell を使用した高度な管理](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplFail.png)  
  
特定の AD 論理サイトのすべてのサーバーを、最も重要なデータのみが読みやすい順序で表示される表形式で返すには、次のコマンドを実行します。  
  
```  
Get-ADReplicationFailure -scope site -target default-first-site-name | format-table server,firstfailuretime,failurecount,lasterror,partner -auto  
  
```  
  
![powershell を使用した高度な管理](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplFailScoped.png)  
  
### <a name="BKMK_ReplQueue"></a>Get-adreplicationqueueoperation および get-adreplicationuptodatenessvectortable を取得します。  
この 2 つのコマンドレットは、ドメイン コントローラーの最新の状態に関する情報を返します。これには、保留中のレプリケーションやバージョン ベクターの情報が含まれます。  
  
### <a name="BKMK_Sync"></a>Sync-ADObject  
このコマンドレットは、 **Repadmin.exe /replsingleobject**を実行した場合と似ています。 特に問題を修正するために、帯域外レプリケーションが必要な変更を行う際に役立ちます。  
  
たとえば、誰かが CEO のユーザー アカウントを削除してしまい、Active Directory のごみ箱を使用して復元した場合、直ちにすべてのドメイン コントローラーにそれをレプリケートする必要があります。 その際は、変更されている他のすべてのオブジェクトのレプリケーションは適用しないでおく必要があります。WAN リンクに過剰な負荷がかかるのを避けるため、レプリケーション スケジュールが設定されているためです。  
  
```  
Get-ADDomainController -filter * | foreach {Sync-ADObject -object "cn=tony wang,cn=users,dc=corp,dc=contoso,dc=com" -source dc1 -destination $_.hostname}  
  
```  
  
![powershell を使用した高度な管理](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSSyncAD.png)  
  
### <a name="BKMK_Topo"></a>モジュール  
Repadmin.exe は、サイト、サイト リンク、サイト リンク ブリッジ、および接続のようなレプリケーション トポロジに関する情報を返すには便利ですが、変更を加えるための包括的な引数のセットが用意されていません。 実際、AD DS トポロジを作成および変更する管理者向けに特化して設計された、スクリプトが実行可能な付属の Windows ユーティリティはこれまで存在しませんでした。 Active Directory が普及し、非常に多くのカスタマー環境で利用されるようになったことで、Active Directory の論理情報を一括で変更するニーズが高まっています。  
  
たとえば、新しいブランチ オフィスを迅速に展開した後に、他のオフィスとの統合作業だけでなく、物理的な場所、ネットワークの変更、および新しいキャパシティ要件に基づいて、サイトに多数の変更を加えることが必要になる場合があります。 このような場合、Dssites.msc や Adsiedit.msc を使用して変更を加える代わりに、変更作業を自動化することができます。 これは、ネットワークおよび施設のチームから提供されたスプレッドシート形式のデータを使用する場合に特に役立ちます。  
  
**Get adreplication\\** * コマンドレットは、レプリケーショントポロジに関する情報を返します。これは、 **Set adreplication\\** * コマンドレットを一括でパイプライン処理する場合に役立ちます。 **Get**コマンドレットはデータを変更しません。データの表示のみを行うか、または **、設定-adreplication\\** * コマンドレットにパイプライン処理できる Windows PowerShell セッションオブジェクトを作成します。 **New** および **Remove** コマンドレットは、Active Directory トポロジ オブジェクトを作成または削除するのに役立ちます。  
  
たとえば、CSV ファイルを使用して新しいサイトを作成できます。  
  
```  
import-csv -path C:\newsites.csv | new-adreplicationsite  
```  
  
![powershell を使用した高度な管理](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSNewSitesCSV.png)  
  
![powershell を使用した高度な管理](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSImportCSV.png)  
  
カスタムのレプリケーション間隔とサイト コストを使用して、既存の 2 つのサイト間に新しいサイト リンクを作成します。  
  
```  
new-adreplicationsitelink -name "chicago<-->waukegan" -sitesincluded chicago,waukegan -cost 50 -replicationfrequencyinminutes 15  
```  
  
![powershell を使用した高度な管理](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSNewADReplSite.png)  
  
フォレスト内のすべてのサイトを検索し、それらのサイトの **Options** 属性をサイト間変更の通知を有効化するフラグで置き換え、圧縮を使用して最大速度でレプリケートできるようにします。  
  
```  
get-adreplicationsitelink -filter * | set-adobject -replace @{options=$($_.options -bor 1)}  
```  
  
![powershell を使用した高度な管理](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSNewADReplSiteLink.gif)  
  
> [!IMPORTANT]  
> これらのサイト リンクで圧縮を無効化するには、 **-bor 5** を設定します。  
  
サブネットが割り当てられていないサイトをすべて検索し、出力される一覧に基づいて各サイトの場所の実際のサブネットを設定できるようにします。  
  
```  
get-adreplicationsite -filter * -property subnets | where-object {!$_.subnets -eq "*"} | format-table name  
```  
  
![powershell を使用した高度な管理](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSNewADReplSiteFiltrer.png)  
  
## <a name="see-also"></a>参照  
[Windows PowerShell &#40;レベル100を使用した Active Directory レプリケーションとトポロジ管理の概要&#41;](../../../ad-ds/manage/powershell/Introduction-to-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-100-.md)  
  

