---
ms.assetid: 0fd7b6aa-3e50-45a3-a3a6-56982844363e
title: イベント ID 2088 - レプリケーションが成功した DNS 参照エラーが発生しました
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: e0c5e838290a8ebf33f0f7891dc10f8b00e5bcba
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66442651"
---
# <a name="event-id-2088-dns-lookup-failure-occurred-with-replication-success"></a>イベント ID 2088:レプリケーションが成功した DNS 参照エラーが発生しました

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

無効な DNS 構成をメンバーのコンピューター、ドメイン コント ローラーまたはログオン認証およびネットワーク リソースへのアクセスを含め、この Active Directory Domain Services フォレスト内のアプリケーション サーバー上の他の重要な操作に影響する可能性があります。 

このドメイン コント ローラーが DNS を使用して、ソース ドメイン コント ローラーの IP アドレスを解決できるようにすぐにこの DNS 構成エラーを解決する必要があります。 

別のサーバー名:DC1 の失敗した DNS ホスト名:4a8717eb-8e58-456c-995a-c92e4add7e8e._msdcs.contoso.com 

注: 既定では、10 個を超えるエラーが発生した場合でも、最大 10 個の DNS エラーは、12 時間内に表示されます。  個々 のエラー イベントをログに記録するには、レジストリ値、次の診断を設定、1。 

レジストリ パス:HKLM\System\CurrentControlSet\Services\NTDS\Diagnostics\22 DS RPC Client 

ユーザーの操作: 

1) ソース ドメイン コント ローラーが指定されていない場合に機能しているか、そのオペレーティング システムを別のコンピューター名で再インストールまたは NTDSDSA は ntdsutil.exe を使用してソース ドメイン コント ローラーのメタデータを削除オブジェクト GUID、サポート技術情報の記事で説明する手順を使用します。文書番号 216498 します。 

2) ソース ドメイン コント ローラーが Active Directory を実行しているが」と入力して、ネットワーク上でアクセス可能であることを確認"ビューを net \\&lt;ソース DC 名&gt;"または"ping&lt;ソース DC 名&gt;"。 

3) ソース ドメイン コント ローラーを使用している有効な DNS サーバーの DNS サービス、およびソース ドメイン コント ローラーのホスト レコードと CNAME レコードは、正しく登録確認、DCDIAG の DNS が強化されたバージョンを使用して。EXE でご確認いただけます <https://www.microsoft.com/dns> 

dcdiag/test:dns 

4) DCDIAG の DNS が強化されたバージョンを実行して、DNS サービスのこの変換先のドメイン コント ローラーは有効な DNS サーバーを使用することを確認します。次のように、移行先ドメイン コント ローラーのコンソールでのコマンドを実行可能ファイル: 

dcdiag/test:dns 

5) DNS エラーのエラーの詳細な分析は、KB 824449 を参照してください。 <https://support.microsoft.com/?kbid=824449> 

追加のデータ エラー値:11004、要求された名前が有効では、要求された型のデータが見つかりません</code> </introduction>
  <section>
    <title>診断</title>
    <content>
      <para>Dns エイリアス (CNAME) リソース レコードを使用して、ソース ドメイン コント ローラー名を解決するのにはエラーは、DNS の構成の誤りや DNS データの伝達の遅延が原因でことができます。</para>
    </content>
  </section>
  <section>
    <title>解決方法</title>
    <content>
      <para>DNS のテスト」の説明に従って進める&quot;<link xlink:href="85b1d179-f53e-4f95-b0b8-5b1c096a8076">イベント ID 2087。DNS ルックアップの失敗のレプリケーションが失敗する原因となった</link>します。&quot;</para>
    </content>
  </section>
  <relatedTopics />
</developerConceptualDocument>


