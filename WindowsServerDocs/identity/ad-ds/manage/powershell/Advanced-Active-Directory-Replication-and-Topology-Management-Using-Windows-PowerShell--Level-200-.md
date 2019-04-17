---
ms.assetid: fe05e52c-cbf8-428b-8176-63407991042f
title: "Active Directory レプリケーションおよびトポロジ管理の Windows PowerShell (レベル 200) を使用して高度な"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 1e05616b4b594ae54fcaa3ec6496c0917ecde38b
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="advanced-active-directory-replication-and-topology-management-using-windows-powershell-level-200"></a>Active Directory レプリケーションおよびトポロジ管理の Windows PowerShell (レベル 200) を使用して高度な

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

このトピックでは、新しい AD DS レプリケーションおよびトポロジ管理コマンドレットの詳細については、について説明し、その他の例を示します。 概要については、次を参照してください。 [Introduction to Active Directory レプリケーションおよびトポロジ管理を使用して Windows PowerShell (&) #40 です。Level 100 & #41 です。](../../../ad-ds/manage/powershell/Introduction-to-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-100-.md).  
  
1.  [概要](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_Intro)  
  
2.  [レプリケーションとメタデータ](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_Repl)  
  
3.  [Get ADReplicationAttributeMetadata](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_ReplAttrMD)  
  
4.  [Get ADReplicationPartnerMetadata](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_PartnerMD)  
  
5.  [Get ADReplicationFailure](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_ReplFail)  
  
6.  [Get-adreplicationqueueoperation および Get-adreplicationuptodatenessvectortable](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_ReplQueue)  
  
7.  [同期 ADObject](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_Sync)  
  
8.  [トポロジ](../../../ad-ds/manage/powershell/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-.md#BKMK_Topo)  
  
## <a name="BKMK_Intro"></a>概要  
Windows Server 2012 では、レプリケーションとフォレスト トポロジを管理する 25 個の新しいコマンドレットでは、Windows PowerShell 用 Active Directory モジュールを拡張します。 これには、前に、された強制的に使用する、汎用**\*-AdObject**名詞または .NET 関数を呼び出す。  
  
すべての Active Directory Windows PowerShell コマンドレットと同様にこの新機能のインストールが必要、 [Active Directory 管理ゲートウェイ サービス](https://www.microsoft.com/download/details.aspx?displaylang=en&id=2852)で少なくとも 1 つのドメイン コント ローラー (可能であれば、すべてのドメイン コント ローラー)。  
  
次の表は、新しいレプリケーションおよびトポロジ コマンドレットが、Active Directory Windows PowerShell モジュールに追加します。  
  
|||  
|-|-|  
|コマンドレット|説明|  
|Get ADReplicationAttributeMetadata|属性のオブジェクトのレプリケーション メタデータを返します|  
|Get ADReplicationConnection|ドメイン コント ローラー接続オブジェクトの詳細を返します|  
|Get ADReplicationFailure|最新のレプリケーション エラーのドメイン コント ローラーを返します|  
|Get ADReplicationPartnerMetadata|ドメイン コント ローラーのレプリケーション構成を返します|  
|Get-adreplicationqueueoperation|現在のレプリケーション キューのバックログを返します|  
|Get ADReplicationSite|サイト情報を返します|  
|Get ADReplicationSiteLink|サイト リンク情報を返します|  
|Get ADReplicationSiteLinkBridge|サイト リンク ブリッジ情報を返します|  
|Get ADReplicationSubnet|AD サブネット情報を返します|  
|Get-adreplicationuptodatenessvectortable|ドメイン コント ローラーの UTD ベクターを返します|  
|Get ADTrust|ドメイン間またはフォレスト間の信頼に関する情報を返します|  
|New-adreplicationsite|新しいサイトを作成します。|  
|新しい ADReplicationSiteLink|新しいサイト リンクを作成します。|  
|新しい ADReplicationSiteLinkBridge|新しいサイト リンク ブリッジを作成します。|  
|新しい ADReplicationSubnet|新しい AD サブネットを作成します。|  
|削除 ADReplicationSite|サイトを削除します。|  
|削除 ADReplicationSiteLink|サイト リンクを削除します。|  
|削除 ADReplicationSiteLinkBridge|サイト リンク ブリッジを削除します。|  
|削除 ADReplicationSubnet|AD サブネットを削除します。|  
|セット ADReplicationConnection|接続を変更します。|  
|セット ADReplicationSite|サイトを変更します。|  
|セット ADReplicationSiteLink|サイト リンクを変更します。|  
|セット ADReplicationSiteLinkBridge|サイト リンク ブリッジを変更します。|  
|セット ADReplicationSubnet|AD サブネットを変更します。|  
|同期 ADObject|1 つのオブジェクトのレプリケーションを強制します|  
  
これらのコマンドレットのほとんどでは、Repadmin.exe で、基準があります。 (表示されていない)、他のコマンドレットは、ダイナミック アクセス制御とグループ管理サービス アカウントなどの機能を処理します。  
  
すべての Active Directory Windows PowerShell コマンドレットの完全な一覧は、次のコマンドを実行します。  
  
```  
Get-command -module ActiveDirectory  
```  
  
すべての Active Directory Windows PowerShell コマンドレットの引数の完全な一覧は、ヘルプを参照します。 例えば：  
  
```  
Get-help New-ADReplicationSite  
  
```  
  
使用して、`Update-Help`コマンドレット ヘルプ ファイルをダウンロードしてインストール  
  
### <a name="BKMK_Repl"></a>レプリケーションとメタデータ  
Repadmin.exe は、正常性と Active Directory レプリケーションの整合性を検証します。 Repadmin.exe には、単純なデータ操作オプションが用意されています - 引数がいくつかサポート CSV 出力では、たとえば - が、オートメーション一般的に必要なテキスト ファイル出力を解析しています。 Windows PowerShell 用 Active Directory モジュールが提供する、返されたデータを実際に制御できるオプションの最初の試行これには、前にスクリプトを作成またはサード パーティ製のツールを使用する必要があります。  
  
さらに、次のコマンドレットは、の新しいパラメーター セットを実装**ターゲット**、**スコープ**、および**EnumerationServer**:  
  
-   **Get ADReplicationFailure**  
  
-   **Get ADReplicationPartnerMetadata**  
  
-   **Get-adreplicationuptodatenessvectortable**  
  
**ターゲット**引数がターゲット サーバー、サイト、ドメイン、またはによって指定されたフォレストを識別する文字列のコンマ区切りのリストを受け入れる、**スコープ**引数。 アスタリスク (\ *) は容認されても、および指定されたスコープ内のすべてのサーバーを意味します。 スコープが指定されていない場合は、現在のユーザーのフォレスト内のすべてのサーバーを意味します。 **スコープ**引数は検索の範囲を指定します。 使用できる値は**サーバー**、**サイト**、**ドメイン**、および**フォレスト**します。 **EnumerationServer**で指定されたドメイン コントローラの一覧を列挙するサーバーを指定**ターゲット**と**スコープ**します。 同じように動作して、**サーバー**引数、指定したサーバーの Active Directory Web サービスを実行する必要があります。  
  
新しいコマンドレットを紹介するには、次のとおりいくつかのサンプル シナリオ repadmin.exe; に示す機能が不可能ですこれらの例を利用すれば、管理者の組み合わせが明らかにします。 コマンドレットのヘルプを特定の使用法の要件を確認します。  
  
### <a name="BKMK_ReplAttrMD"></a>Get ADReplicationAttributeMetadata  
このコマンドレットと同様に**repadmin.exe/showobjmeta**します。 属性が変更された場合、元のドメイン コント ローラー、バージョンおよび USN 情報、および属性データなどのレプリケーション メタデータを返すことができます。 このコマンドレットは、場所を監査し、変更が発生したときに便利です。  
  
Repadmin とは異なり Windows PowerShell では柔軟な検索と出力を制御します。 たとえば、読み取り可能な一覧として注文、Domain Admins オブジェクトのメタデータを出力することができます。  
  
```  
Get-ADReplicationAttributeMetadata -object "cn=domain admins,cn=users,dc=corp,dc=contoso,dc=com" -server dc1.corp.contoso.com -showalllinkedvalues | format-list  
  
```  
  
![powershell を使用した高度な管理](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplAttrMd.png)  
  
または、表形式で、repadmin のようにデータを並べ替えることができます。  
  
```  
Get-ADReplicationAttributeMetadata -object "cn=domain admins,cn=users,dc=corp,dc=contoso,dc=com" -server dc1.corp.contoso.com -showalllinkedvalues | format-table -wrap  
  
```  
  
![powershell を使用した高度な管理](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplAttrMdTable.png)  
  
パイプライン処理によって、オブジェクトのクラス全体のメタデータを取得することができます、 **Get-adobject**コマンドレットすべてのグループなどのフィルターを使用しとを組み合わせることが特定の日付。 パイプラインは、データを渡すための複数のコマンドレット間で使用されるチャネルです。 すべてのグループを表示するには、2012 年 1 月 13 日に何らかの方法で変更。  
  
```  
get-adobject -filter 'objectclass -eq "group"' | Get-ADReplicationAttributeMetadata -server dc1.corp.contoso.com | where-object {$_.lastoriginatingchangetime -like "*1/13/2012*" -and $_.attributename -eq "name"} | format-table object  
```  
  
![powershell を使用した高度な管理](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplAttrMdClass.png)  
  
パイプラインを使用した Windows PowerShell 操作の詳細については、次を参照してください。[パイプ処理と Windows PowerShell でパイプライン](https://technet.microsoft.com/library/ee176927.aspx)します。  
  
またはを調べるにすべてのグループを持つメンバーとして、およびグループが最後に変更されたときに Tony Wang:  
  
```  
get-adobject -filter 'objectclass -eq "group"' | Get-ADReplicationAttributeMetadata -server dc1.corp.contoso.com -showalllinkedvalues | where-object {$_.attributevalue -like "*tony wang*"} | format-table object,LastOriginatingChangeTime,version -auto  
  
```  
  
![powershell を使用した高度な管理](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplAttrMdFilter.png)  
  
または、権限のあるすべてのオブジェクトを検索するを使用して復元システム状態のバックアップ、ドメイン内の人為的に高いバージョンに基づいています。  
  
```  
get-adobject -filter 'objectclass -like "*"' | Get-ADReplicationAttributeMetadata -server dc1.corp.contoso.com | where-object {$_.version -gt "100000" -and $_.attributename -eq "name"} | format-table object,LastOriginatingChangeTime  
```  
  
![powershell を使用した高度な管理](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplAttrMdFilter2.png)  
  
または、すべてのユーザーのメタデータを Microsoft Excel で後で検証 CSV ファイルに送信するには。  
  
```  
get-adobject -filter 'objectclass -eq "user"' | Get-ADReplicationAttributeMetadata -server dc1.corp.contoso.com -showalllinkedvalues | export-csv allgroupmetadata.csv  
```  
  
### <a name="BKMK_PartnerMD"></a>Get ADReplicationPartnerMetadata  
このコマンドレットは、構成とすると、監視、インベントリ作成、またはのトラブルシューティングを行うことが、ドメイン コント ローラーのレプリケーションの状態に関する情報を返します。 Repadmin.exe とは異なり Windows PowerShell を使用することを意味する形式では重要なデータのみを参照してください。  
  
たとえば、1 つのドメイン コント ローラーの読み取り可能なレプリケーションの状態。  
  
```  
Get-ADReplicationPartnerMetadata -target dc1.corp.contoso.com  
```  
  
![powershell を使用した高度な管理](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplPartnerMd.png)  
  
代わりに、前回のドメイン コント ローラー複製の受信し、そのパートナーを表形式で書式設定。  
  
```  
Get-ADReplicationPartnerMetadata -target dc1.corp.contoso.com | format-table lastreplicationattempt,lastreplicationresult,partner -auto  
```  
  
![powershell を使用した高度な管理](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplPartnerMdTable.png)  
  
または、フォレスト内のすべてのドメイン コント ローラーに接続し、表示、何らかの理由が最後に試行されたレプリケーションが失敗しました。  
  
```  
Get-ADReplicationPartnerMetadata -target * -scope server | where {$_.lastreplicationresult -ne "0"} | ft server,lastreplicationattempt,lastreplicationresult,partner -auto  
  
```  
  
![powershell を使用した高度な管理](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplPartnerMdFail.png)  
  
### <a name="BKMK_ReplFail"></a>Get ADReplicationFailure  
レプリケーションで最近のエラーに関する情報を返しますをこのコマンドレットを使用できます。 似ていますが**Repadmin.exe/showreplsum**、もう一度、Windows PowerShell のおかげ制御の詳細と似ています。  
  
たとえば、ドメイン コント ローラーの最新のエラーと接続に失敗したパートナーを返すことができます。  
  
```  
Get-ADReplicationFailure dc1.corp.contoso.com  
```  
  
![powershell を使用した高度な管理](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplFail.png)  
  
または、特定 AD 論理サイト、簡単に表示すると最も重要なデータのみが含まれている順序ですべてのサーバーに対して表示される表形式が返されます。  
  
```  
Get-ADReplicationFailure -scope site -target default-first-site-name | format-table server,firstfailuretime,failurecount,lasterror,partner -auto  
  
```  
  
![powershell を使用した高度な管理](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSGetADReplFailScoped.png)  
  
### <a name="BKMK_ReplQueue"></a>Get-adreplicationqueueoperation および Get-adreplicationuptodatenessvectortable  
これらのコマンドレットの両方のドメイン コント ローラーの側面をさらを返すまで"2、保留中のレプリケーションやバージョン ベクターの情報が含まれます。  
  
### <a name="BKMK_Sync"></a>同期 ADObject  
このコマンドレットは、実行中によく似ています**Repadmin.exe/replsingleobject**します。 問題を修正するには、特に、帯域外レプリケーションが必要な変更を加えると非常に便利です。  
  
たとえば、ユーザーが CEO のユーザー アカウントを削除し、Active Directory のごみ箱に復元しました、当てはまらない場合はすぐにすべてのドメイン コント ローラーにレプリケートします。 多くの場合これを行うすべて、その他のオブジェクトに対する変更の; のレプリケーションを強制なし結局のところ、WAN リンクのオーバー ロードを避けるために、レプリケーション スケジュールがあるためにです。  
  
```  
Get-ADDomainController -filter * | foreach {Sync-ADObject -object "cn=tony wang,cn=users,dc=corp,dc=contoso,dc=com" -source dc1 -destination $_.hostname}  
  
```  
  
![powershell を使用した高度な管理](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSSyncAD.png)  
  
### <a name="BKMK_Topo"></a>トポロジ  
Repadmin.exe は、サイト、サイト リンク、サイト リンク ブリッジ、および接続のようなレプリケーション トポロジに関する情報を返す得意ですが、変更を行う引数の包括的なセットをありません。 実際には、決してしましたを作成し、AD DS トポロジを変更する管理者向けに設計されたスクリプト可能なインボックス Windows のユーティリティ。 一括する必要が Active Directory を変更するように Active Directory は、何百万ものお客様の環境で完成度が高く、論理的な情報が明らかになります。  
  
など、他のユーザーの統合と組み合わせて、新しいブランチ オフィスを迅速に展開した後は、物理的な場所、ネットワークの変更、および新しいキャパシティ要件に基づいて行う 100 サイト変更があります。 変更する場合、Dssites.msc や Adsiedit.msc を使用してではなくを自動化できます。 これは、スプレッドシート形式のネットワークおよび施設のチームが提供されるデータの使用する場合に特に役立ちます。  
  
**取得-Adreplication\ ***コマンドレットは、レプリケーション トポロジに関する情報を返すし、パイプラインをための便利な**設定-Adreplication\ ***コマンドレットに一括でします。 **取得**コマンドレットは、データを変更しないで、データのみを表示または Windows PowerShell を作成するセッション オブジェクトをパイプラインに処理する**設定-Adreplication\ ***コマンドレット。 **新規**と**削除**コマンドレットは、作成または Active Directory トポロジ オブジェクトを削除するのに便利です。  
  
たとえば、CSV ファイルを使用して新しいサイトを作成することができます。  
  
```  
import-csv -path C:\newsites.csv | new-adreplicationsite  
```  
  
![powershell を使用した高度な管理](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSNewSitesCSV.png)  
  
![powershell を使用した高度な管理](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSImportCSV.png)  
  
また、カスタムのレプリケーション間隔とサイト コストを持つ 2 つの既存のサイト間での新しいサイト リンクを作成します。  
  
```  
new-adreplicationsitelink -name "chicago<-->waukegan" -sitesincluded chicago,waukegan -cost 50 -replicationfrequencyinminutes 15  
```  
  
![powershell を使用した高度な管理](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSNewADReplSite.png)  
  
また、フォレスト内のすべてのサイトを検索し、置換その**オプション**サイト間を有効にするフラグで属性の変更の通知を圧縮を使用して最大速度でレプリケートするためには。  
  
```  
get-adreplicationsitelink -filter * | set-adobject -replace @{options=$($_.options -bor 1)}  
```  
  
![powershell を使用した高度な管理](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSNewADReplSiteLink.gif)  
  
> [!IMPORTANT]  
> 設定**-bor 5**もこれらのサイト リンクで圧縮を無効にします。  
  
または、これらの場所の実際のサブネットを含むリストを調整するために、サブネットの割り当てがないすべてのサイトを探します。  
  
```  
get-adreplicationsite -filter * -property subnets | where-object {!$_.subnets -eq "*"} | format-table name  
```  
  
![powershell を使用した高度な管理](media/Advanced-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-200-/ADDS_PSNewADReplSiteFiltrer.png)  
  
## <a name="see-also"></a>参照してください。  
[Active Directory レプリケーションおよびトポロジ管理の Windows PowerShell (&) #40; を使用しての概要Level 100 & #41 です。](../../../ad-ds/manage/powershell/Introduction-to-Active-Directory-Replication-and-Topology-Management-Using-Windows-PowerShell--Level-100-.md)  
  

