---
ms.assetid: 0fd7b6aa-3e50-45a3-a3a6-56982844363e
title: "イベント ID 2088 - レプリケーションが成功したで DNS 参照エラーが発生しました"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 4f223f075775f942f83a1962da28a77e85e89aa0
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="event-id-2088-dns-lookup-failure-occurred-with-replication-success"></a>イベント ID 2088: レプリケーションが成功したで DNS 参照エラーが発生しました

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

    
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

無効な DNS の構成をメンバーのコンピューター、ドメイン コントローラーまたはログオン認証やネットワーク リソースへのアクセスなど、この Active Directory ドメイン サービス フォレスト内のアプリケーション サーバーの重要なその他の操作に影響する可能性があります。 

このドメイン コントローラーが DNS を使用して、ソース ドメイン コントローラーの IP アドレスを解決できるようにすぐにこの DNS 構成-エラーを解決する必要があります。 

代替サーバーの名前: DC1 失敗している DNS ホスト名: 4a8717eb-8e58-456 c-995a-c92e4add7e8e._msdcs. contoso.com 

注: 既定では、最大 10 個の DNS エラーが表示、12 時間を指定した期間に 10 個を超えるエラーが発生した場合でもされます。  個々 のエラー イベントをログに次の診断レジストリ値 1 に設定します。 

レジストリのパス: HKLM\System\CurrentControlSet\Services\NTDS\Diagnostics\22 DS RPC クライアント 

ユーザーの操作: 

1) ソース ドメイン コントローラーが不要になった場合に機能しているかのオペレーティング システムを別のコンピューター名で再インストールしたまたは NTDSDSA は ntdsutil.exe を使用して、ソース ドメイン コントローラーのメタデータを削除オブジェクト GUID 216498 サポート技術情報の記事で説明する手順を使用します。 

2) ソース ドメイン コントローラーが、Active Directory が実行されていることを確認」と入力して、ネットワークでアクセス可能な"「net view \\&lt;ソース DC 名&gt;"または"ping&lt;ソース DC 名&gt;"します。 

3) Verify that the source domain controller is using a valid DNS server for DNS services, and that the source domain controller's host record and CNAME record are correctly registered, using the DNS Enhanced version of DCDIAG.EXE available on https://www.microsoft.com/dns 

dcdiag/test: dns 

4) DCDIAG.EXE は、次のように、移行先のドメイン コントローラーの本体でコマンドします。 

dcdiag/test: dns 

5) For further analysis of DNS error failures see KB 824449: https://support.microsoft.com/?kbid=824449 

追加のデータ エラー値: 11004 要求された名前が有効ですが、要求された種類のデータが見つかりません。</code>
  </introduction>
  <section>
    <title>診断</title>
    <content>
      <para>DNS の構成の不備または DNS データの伝達の遅延が原因で DNS エイリアス (CNAME) リソース レコードを使用して、ソース ドメイン コントローラー名を解決するのにはエラーをすることができます。</para>
    </content>
  </section>
  <section>
    <title>解像度</title>
    <content>
      <para>」の説明に従って DNS のテストの続行"<link xlink:href="85b1d179-f53e-4f95-b0b8-5b1c096a8076">イベント ID 2087: DNS 参照エラーが原因でレプリケーションが失敗する</link>."</para>
    </content>
  </section>
  <relatedTopics />
</developerConceptualDocument>


