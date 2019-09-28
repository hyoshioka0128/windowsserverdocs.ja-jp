---
ms.assetid: 0fd7b6aa-3e50-45a3-a3a6-56982844363e
title: イベント ID 2088-レプリケーションの成功時に DNS 参照エラーが発生しました
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: d51cbcc93a8decbcb72a1e91854a09345507511d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71368913"
---
# <a name="event-id-2088-dns-lookup-failure-occurred-with-replication-success"></a>イベント ID 2088:レプリケーションの成功時に DNS 参照エラーが発生しました

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

    
    <developerConceptualDocument xmlns="https://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="https://www.w3.org/1999/xlink" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="https://ddue.schemas.microsoft.com/authoring/2003/5 http://clixdevr3.blob.core.windows.net/ddueschema/developer.xsd">
      <introduction>
    <para>When a destination domain controller running Windows Server 2003 with Service Pack 1 (SP1) receives Event ID 2088 in the Directory Service event log, attempts to resolve the globally unique identifier (GUID) in the alias (CNAME) resource record to an IP address for the source domain controller failed. However, the destination domain controller tried other means to resolve the name and succeeded by using either the fully qualified domain name (FQDN) or the NetBIOS name of the source domain controller. Although replication was successful, the Domain Name System (DNS) problem should be diagnosed and resolved. </para>
    <para>The following is an example of the event text: </para>
    <code>Log Name: Directory Service

    Source: Microsoft-Windows-ActiveDirectory_DomainService
    Date: 3/15/2008  9:20:11 AM
    Event ID: 2088
    Task Category: DS RPC Client 
    Level: Warning
    Keywords: Classic
    User: ANONYMOUS LOGON
    Computer: DC3.contoso.com
    Description:
    Active Directory could not use DNS to resolve the IP address of the 
    source domain controller listed below. To maintain the consistency 
    of Security groups, group policy, users and computers and their passwords, 
    Active Directory Domain Services successfully replicated using the NetBIOS 
    or fully qualified computer name of the source domain controller. 

無効な DNS 構成は、ログオン認証やネットワークリソースへのアクセスなど、この Active Directory Domain Services フォレスト内のメンバーコンピューター、ドメインコントローラー、またはアプリケーションサーバーに対する他の重要な操作に影響を与える可能性があります。 

このドメインコントローラーが DNS を使用してソースドメインコントローラーの IP アドレスを解決できるように、この DNS 構成エラーを直ちに解決する必要があります。 

代替サーバー名:DC1 失敗した DNS ホスト名:4a8717eb-8e58-456c-995a-c92e4add7e8e. contoso .com 

注: 既定では、10個を超えるエラーが発生した場合でも、12時間以内に最大10個の DNS エラーのみが表示されます。  個々のエラーイベントをすべてログに記録するには、次の診断レジストリ値を1に設定します。 

レジストリパス:HKLM\System\CurrentControlSet\Services\NTDS\Diagnostics\22 DS RPC クライアント 

ユーザーの操作: 

1) ソースドメインコントローラーが機能しなくなった場合、または別のコンピューター名または NTDSDSA オブジェクト GUID を使用してそのオペレーティングシステムが再インストールされている場合は、「MSKB」の記事に記載されている手順を使用して、ソースドメインコントローラーのメタデータを ntdsutil.exe で削除します。216498。 

2) ソースドメインコントローラが Active Directory 実行されていて、ネットワーク上でアクセス可能であることを確認します。「net view \\ @ no__t-1source DC name @ no__t」または「ping &lt;source DC name @ no__t」と入力します。 

3) ソースドメインコントローラが DNS サービスに有効な DNS サーバーを使用しており、ソースドメインコントローラのホストレコードと CNAME レコードが正しく登録されていることを確認します。これには、DNS 拡張バージョンの DCDIAG を使用します。実行可能ファイル <https://www.microsoft.com/dns> 

dcdiag/test: dns 

4) この宛先ドメインコントローラが dns 拡張バージョンの DCDIAG を実行して、DNS サービスに対して有効な DNS サーバーを使用していることを確認してください。次のように、移行先ドメインコントローラーのコンソールで EXE コマンドを実行します。 

dcdiag/test: dns 

5) DNS エラーエラーの詳細な分析については、「KB 824449: <https://support.microsoft.com/?kbid=824449>」を参照してください。 

追加のデータ エラー値:11004要求された名前は有効ですが、要求された種類のデータが見つかりませんでした @ no__t-0 </introduction>
  <section>
    <title>Diagnosis @ no__t @ no__t @ no__t @<para>Dns のエイリアス (CNAME) リソースレコードを使用してソースドメインコントローラー名を解決できない場合は、dns のデータ伝達の誤りまたは遅延が原因である可能性があります。</para>
    </content>
  </section>
  <section>
    <title>Resolution @ no__t @ no__t @ no__t @<para>@No__t-0 @ no__t-1 イベント ID 2087 の説明に従って、DNS テストを続行します。DNS 参照のエラーにより、レプリケーションが失敗しました @ no__t-0。 &quot;</para>
    </content>
  </section>
  <relatedTopics />
</developerConceptualDocument>


