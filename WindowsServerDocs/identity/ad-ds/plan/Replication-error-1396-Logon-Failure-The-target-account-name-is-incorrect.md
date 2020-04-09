---
ms.assetid: 399a8bbe-3375-4bb0-b55b-5f46e7050028
title: 'レプリケーション エラー 1396。ログオン エラー: 対象のアカウント名は間違っています'
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: b608066f3fd9d2f6c2bd86194e816f4c9665d6c1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80822075"
---
# <a name="replication-error-1396-logon-failure-the-target-account-name-is-incorrect"></a>レプリケーション エラー 1396。ログオン エラー: 対象のアカウント名は間違っています

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012


<developerConceptualDocument xmlns="https://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="https://www.w3.org/1999/xlink" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="https://ddue.schemas.microsoft.com/authoring/2003/5 http://clixdevr3.blob.core.windows.net/ddueschema/developer.xsd"> <introduction>
    <para>この記事では、Active Directory レプリケーションが Win32 エラー1396で失敗した場合の現象と原因、および解決方法について説明します。 &quot;ログオンエラー: ターゲットアカウント名が正しくありません。&quot; </para>
    <list class="bullet"> <listItem>
        <para>
          <link xlink:href="d3a01966-74c9-4c49-ba11-354b9acf7519#BKMK_Symptoms">現象</link>
        </para>
      </listItem> <listItem>
        <para>
          
の<link xlink:href="d3a01966-74c9-4c49-ba11-354b9acf7519#BKMK_Causes">原因</link>        </para>
      </listItem> <listItem>
        <para>
          <link xlink:href="d3a01966-74c9-4c49-ba11-354b9acf7519#BKMK_Resolutions">解決策</link>
        </para>
      </listItem>
    </list>
  </introduction>
  <section address="BKMK_Symptoms">
    <title>現象</title>
    <content>
      <para />
      <list class="ordered">
<listItem><para>Active Directory のレプリケーションテストが失敗したことを示すエラー 1396: ログオンに失敗しました: ターゲットアカウント名が正しくありません。&quot;</para><code>Testing server: &lt;Site name&gt;&lt;DC Name&gt;
Starting test: Replications
[Replications Check,&lt;DC Name&gt;] A recent replication attempt failed:
From &lt;source DC&gt; to &lt;destination DC&gt;
Naming Context: CN=&lt;DN path of naming context&gt;
<codeFeaturedElement>The replication generated an error (1396):
Logon Failure: The target account name is incorrect.</codeFeaturedElement>
The failure occurred at &lt;date&gt; &lt;time&gt;.
The last success occurred at &lt;date&gt; &lt;time&gt;.
XX failures have occurred since the last success</code></listItem><listItem><para>REPADMIN.EXE は、最後のレプリケーションの試行がステータス1396で失敗したことを報告します。</para><para>1396ステータスを一般的に示す REPADMIN コマンドには、次のようなものがあります。</para><table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11"><tbody><tr><TD><list class="bullet"><listItem><para>REPADMIN/ADD</para></listItem><listItem><para>REPADMIN/REPLSUM</para></listItem><listItem><para>REPADMIN/REHOST</para></listItem><listItem><para>REPADMIN/SHOWVECTOR/LATENCY</para></listItem></list></TD><TD><list class="bullet"><listItem><para>REPADMIN/SHOWREPS</para></listItem><listItem><para>REPADMIN/SHOWREPL</para></listItem><listItem><para>REPADMIN/SYNCALL</para></listItem></list></TD></tr></tbody></table><para>&quot;REPADMIN&quot;/SHOWREPS からのサンプル出力は、CONTOSO-DC2 から CONTOSO-DC1 への入力方向のレプリケーションを示していますが、&quot;ログオンエラーが発生しています。ターゲットアカウント名が正しくありません。&quot; エラーを次に示します。</para><code>Default-First-Site-NameCONTOSO-DC1
DSA Options: IS_GC 
Site Options: (none)
DSA object GUID: b6dc8589-7e00-4a5d-b688-045aef63ec01
DSA invocationID: b6dc8589-7e00-4a5d-b688-045aef63ec01
==== INBOUND NEIGHBORS ======================================
DC=contoso,DC=com
Default-First-Site-NameCONTOSO-DC2 via RPC
DSA object GUID: 74fbe06c-932c-46b5-831b-af9e31f496b2
Last attempt @ &lt;date&gt; &lt;time&gt; failed, <codeFeaturedElement>result 1396 (0x574):
Logon Failure: The target account name is incorrect.</codeFeaturedElement>
&lt;#&gt; consecutive failure(s).
Last success @ &lt;date&gt; &lt;time&gt;.
</code></listItem><listItem><para>Active Directory サイトおよびサービスの [<ui>今すぐレプリケート</ui>] コマンドを実行すると &quot;ログオンエラーが返されます。発信先アカウント名が正しくありません。&quot;</para><para>ソース DC からの接続オブジェクトを右クリックし、[<ui>今すぐレプリケート</ui>] を選択すると &quot;ログオンエラーが発生する: ターゲットアカウント名が正しくありません。画面上のエラーメッセージを&quot; 次に示します。</para><para>ダイアログのタイトルのテキスト:</para><para>今すぐレプリケート</para><para>ダイアログメッセージのテキスト: </para><para>名前付けコンテキストを同期しようとしたときに次のエラーが発生しました。ドメインコントローラー &lt;ソース DC&gt; からドメインコントローラー &lt;宛先 DC&gt;への DNS パスの&gt; を &lt;ます。ログオンエラー: ターゲットアカウント名が正しくありません。 この操作は続行されません。 </para></listItem><listItem><para>1396状態の NTDS KCC、NTDS General、または Microsoft-Windows ActiveDirectory_DomainService イベントは、イベントビューアーのディレクトリサービスログに記録されます。</para><para>1396状態を一般的に示す Active Directory イベントは次のとおりです。</para><table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11"><thead><tr><TD><para>イベント ID</para></TD><TD><para>イベント ソース</para></TD><TD><para>イベントの文字列</para></TD></tr></thead><tbody><tr><TD><para>1125</para></TD><TD><para>Microsoft-Windows-ActiveDirectory_DomainService</para></TD><TD><para>Active Directory ドメインサービスインストールウィザード (Dcpromo) は、次のドメインコントローラーとの接続を確立できませんでした。</para></TD></tr><tr><TD><para>1645</para><para>このイベントは、3つの部分から構成される SPN を一覧表示します。</para></TD><TD><para>NTDS レプリケーション</para></TD><TD><para>Active Directory は、宛先ドメイン コントローラの要求されたサービス プリンシパル名 (SPN) が、SPN を解決するキー配布センター (KDC) ドメイン コントローラ上で登録されていないため、認証済みのリモート プロシージャ コール (RPC) を別のドメイン コントローラに対して実行しませんでした。</para></TD></tr><tr><TD><para>1655</para></TD><TD><para>Microsoft-Windows-ActiveDirectory_DomainService</para></TD><TD><para>Active Directory Domain Services が次のグローバルカタログと通信しようとしましたが、試行は失敗しました。</para></TD></tr><tr><TD><para>2847</para></TD><TD><para>Microsoft-Windows-ActiveDirectory_DomainService</para></TD><TD><para>知識整合性チェッカーは、ローカルの読み取り専用ディレクトリサービスのレプリケーション接続を検出し、次のディレクトリサービスインスタンスでリモートで更新しようとしました。 操作に失敗しました。 再試行されます。</para></TD></tr><tr><TD><para>1925</para></TD><TD><para>NTDS KCC</para></TD><TD><para>次の書き込み可能なディレクトリ パーティションのレプリケーション リンクを確立できませんでした。</para></TD></tr><tr><TD><para>1926</para></TD><TD><para>NTDS KCC</para></TD><TD><para>失敗した次のパラメーターを使用して、読み取り専用のディレクトリ パーティションへのレプリケーション リンクを確立するために試行します。</para></TD></tr><tr><TD><para>5781</para></TD><TD><para>ネット</para></TD><TD><para> サーバーの名前を DNS に登録できません。</para></TD></tr></tbody></table></listItem><listItem><para>DCPROMO がスクリーンエラーで失敗する</para><para>ダイアログのタイトルのテキスト:</para><para>Active Directory のインストールに失敗しました</para><para>ダイアログメッセージのテキスト:</para><para>サーバー ReplicationSourceDC.contoso.com で、ディレクトリサービスが CN = NTDS 設定、CN = Server、cn = Servers、CN = Site、CN = Sites、CN = Configuration、DC = contoso、DC = com のサーバーオブジェクトを作成できなかったため、操作に失敗しました。 </para><para>指定されたネットワーク資格情報に、レプリカを追加するための十分なアクセス権があることを確認してください。 </para><para>
&quot;ログオンエラー: ターゲットアカウント名が正しくありません。 &quot;</para><para>この場合、イベント ID 1645、1168、および1125は、昇格されているサーバーにログ記録されます。</para></listItem><listItem><para><embeddedLabel>Net use</embeddedLabel>を使用してドライブをマップする:</para><code>C:&gt;net use z: &lt;server_name&gt;c$
System error 1396 has occurred.
Logon Failure: The target account name is incorrect.</code><para>この場合、サーバーはイベント ID 333 をシステムイベントログに記録し、SQL Server などのアプリケーションに対して大量の仮想メモリを使用することもできます。</para></listItem><listItem><para>DC 時刻が正しくありません。</para></listItem><listItem><para>RODC の krbtgt アカウントを復元した後、削除された KDC は RODC で開始されません。 たとえば、復元後にエラー1396が表示されます。 </para><para>
イベント ID 1645 が RODC に記録されます。 </para><para>
また、Dcdiag は RODC krbtgt アカウントを更新できないというエラーを報告します。 </para></listItem>
</list>
    </content>
  </section>
  <section address="BKMK_Causes">
    <content>の
    <title>原因</title>
      <para />
      <list class="ordered">
        <listItem>
          <para>SPN は、Kerberos を使用した認証を試みているクライアントの代わりに KDC によって検索されたグローバルカタログに存在しません。</para>
          <para>Active Directory レプリケーションのコンテキストでは、Kerberos クライアントは宛先 DC です。 SPN 参照を実行する KDC は、宛先 DC 自体である可能性がありますが、リモート DC である可能性があります。</para>
        </listItem>
        <listItem>
          <para>参照されているサービスプリンシパル名を含むユーザーまたはサービスアカウントは、送信先 DC のレプリケートを試行したときに KDC によって検索されたグローバルカタログに存在しません。</para>
          <para>Active Directory レプリケーションのコンテキストでは、ソース DC コンピューターアカウントが、受信レプリケーションを実行する宛先 DC に代わって DC によって検索されるグローバルカタログに存在しません。</para>
        </listItem>
        <listItem>
          <para>宛先 DC にソース Dc ドメインの LSA シークレットがありません。</para>
        </listItem>
        <listItem>
          <para>参照されている SPN は、ソース DC とは別のコンピューターアカウントに存在します。</para>
        </listItem>
      </list>
    </content>
  </section>
  <section address="BKMK_Resolutions">
      <list class="ordered">
        <listItem>
    <content>
    <title>解像度</title>
          <para>宛先 DC の NTDS レプリケーションイベント1645のディレクトリサービスイベントログを確認し、次の点に注意してください。</para>
          <para>宛先 DC の名前</para>
          <para>参照されている SPN (ソース Dc NTDS 設定オブジェクトの E3514235-4B06-11D1-AB04-00C04FC2DCD2/&lt;オブジェクト guid&gt;/&lt;ターゲットドメイン&amp;amp; gt;.&amp;amp; lt; tld&amp;amp; gt; @&lt;ターゲットドメイン&gt;の tld&lt;&gt;</para>
          <para>宛先 DC によって使用されている KDC</para>
        </listItem>
        <listItem>
          <para>手順 1. で確認した KDC のコンソールから、次のように入力します。 </para>
          <code>nltest /dsgetdc &lt;forest root DNS domain name &gt; /gc</code>
          <para>レプリケーションが失敗し、移行先 DC で1396エラーが発生した直後に、NLTEST locator テストを実行します。 </para>
          <para>これにより、KDC が SPN 参照に対して実行している GC が識別されます。 </para>
          <para>KDC によって検索される GC は、Microsoft-Windows-ActiveDirectory_DomainService イベント1655でキャプチャされることもあります。</para>
        </listItem>
        <listItem>
          <para>手順 2. で検出されたグローバルカタログの手順1で検出された SPN を検索します。</para>
          <code>C:&gt;repadmin /showattr Server_Name DC=corp,DC=contoso,dc=com &lt;GC used by KDC&gt; &lt;DN path of forest root domain&gt; /filter:&quot;(serviceprincipalname=&lt;SPN cited in the NTDS Replication event 1645&gt;)&quot; /gc /subtree /atts:cn,serviceprincipalname</code>
          <para>または</para>
          <code>C:&gt;dsquery * forestroot -scope subtree -filter &quot;(serviceprincipalname=E3514235-4B06-11D1-AB04-00C04FC2DCD2/65cead9f-4949-46a3-a49a-f1fbfe13d2b3*)&quot; -attr * -s Server_Name.europe.corp.contoso.com</code>
          <para>SPN のホストオブジェクトが存在することを確認します。</para>
          <para>オブジェクトが MY.CNF または conflict で破損しているか、または lost and found コンテナーに存在するかを含め、ホストオブジェクトの DN パスを確認します。</para>
          <para>ソース dc Active Directory レプリケーション SPN が、ソース Dc コンピューターアカウントにのみ登録されていることを確認します。</para>
          <para>レプリケーション SPN がない場合は、ソース DC がそれ自体に SPN を登録しているかどうか、および単純なレプリケーションの待機時間またはレプリケーションエラーのために KDC で使用される GC に SPN が存在していないかどうかを確認します。</para>
        </listItem>
        <listItem>
          <para>セキュリティで保護されたチャネルの正常性と信頼の正常性を確認します。</para>
        </listItem>
      </list>
    </content>
  </section>
  <relatedTopics>
    <externalLink>
      <linkText>エラー1396で失敗した Active Directory 操作のトラブルシューティング: ログオンエラー: ターゲットアカウント名が正しく</linkText>ありません。
      <linkUri><a href="https://support.microsoft.com/kb/2183411/en-gb" data-raw-source="https://support.microsoft.com/kb/2183411/en-gb">https://support.microsoft.com/kb/2183411/en-gb</a></linkUri> 
    </externalLink>
  </relatedTopics>
</developerConceptualDocument>


