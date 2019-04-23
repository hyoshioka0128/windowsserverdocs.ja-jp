---
ms.assetid: 399a8bbe-3375-4bb0-b55b-5f46e7050028
title: 'レプリケーション エラー 1396。ログオン エラー: 対象のアカウント名は間違っています'
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: ef3da06dd348b804f538d37cafbfabdd8bf45beb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59844503"
---
# <a name="replication-error-1396-logon-failure-the-target-account-name-is-incorrect"></a>レプリケーション エラー 1396。ログオン エラー: 対象のアカウント名は間違っています

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012


<developerConceptualDocument xmlns="https://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="https://www.w3.org/1999/xlink" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="https://ddue.schemas.microsoft.com/authoring/2003/5 http://clixdevr3.blob.core.windows.net/ddueschema/developer.xsd"> <introduction>
    <para>この記事に説明します、現象、原因と Win32 エラー 1396 で失敗する Active Directory レプリケーションの解決方法。"ログオン失敗。対象のアカウント名が正しくありません。" </para>
    <list class="bullet">
      <listItem>
        <para>
          <link xlink:href="d3a01966-74c9-4c49-ba11-354b9acf7519#BKMK_Symptoms">現象</link>
        </para>
      </listItem> <listItem>
        <para>
          <link xlink:href="d3a01966-74c9-4c49-ba11-354b9acf7519#BKMK_Causes">エラーの原因</link>
        </para>
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
<listItem><para>Active Directory レプリケーションのテストが失敗しましたエラー 1396 DCDIAG レポート:ログオン エラー:対象のアカウント名が正しくありません。"</para><code>Testing server: &lt;Site name&gt;&lt;DC Name&gt;
Starting test: Replications
[Replications Check,&lt;DC Name&gt;] A recent replication attempt failed:
From &lt;source DC&gt; to &lt;destination DC&gt;
Naming Context: CN=&lt;DN path of naming context&gt;
<codeFeaturedElement>The replication generated an error (1396):
Logon Failure: The target account name is incorrect.</codeFeaturedElement>
The failure occurred at &lt;date&gt; &lt;time&gt;.
The last success occurred at &lt;date&gt; &lt;time&gt;.
XX failures have occurred since the last success</code></listItem><listItem><para>REPADMIN します。実行可能ファイルは、ステータス 1396 の最後のレプリケーションの試行が失敗したことを報告します。</para><para>REPADMIN のコマンドをよくが示されている 1396 状態が含まれますが、これらに限定されません。</para><table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11"><tbody><tr><TD><list class="bullet"><listItem><para>REPADMIN/ADD</para></listItem><listItem><para>REPADMIN/REPLSUM</para></listItem><listItem><para>REPADMIN かかる</para></listItem><listItem><para>REPADMIN/SHOWVECTOR/LATENCY</para></listItem></list></TD><TD><list class="bullet"><listItem><para>REPADMIN/SHOWREPS</para></listItem><listItem><para>REPADMIN/SHOWREPL</para></listItem><listItem><para>REPADMIN/SYNCALL</para></listItem></list></TD></tr></tbody></table><para>CONTOSO DC1 で失敗に contoso-dc2 から入力方向のレプリケーションを表す"REPADMIN/SHOWREPS"からの出力のサンプル、"ログオン エラー。対象のアカウント名が正しくありません。" エラーを次に示します。</para><code>Default-First-Site-NameCONTOSO-DC1
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
</code></listItem><listItem><para><ui>今すぐレプリケート</ui>Active Directory サイトとサービスでのコマンドを返します"ログオン エラー。対象のアカウント名が正しくありません。"</para><para>ソース DC からの接続オブジェクトを右クリックし、選択<ui>今すぐレプリケート</ui>が失敗し"ログオン エラー。対象のアカウント名が正しくありません。" 画面に表示されるエラー メッセージが次に示します。</para><para>ダイアログ タイトルのテキスト:</para><para>今すぐレプリケートします。</para><para>ダイアログ メッセージ テキスト: </para><para>名前付けコンテキストの同期中に、次のエラーが発生した&lt;パーティションの DNS パス&gt;ドメイン コント ローラーから&lt;DC をソース&gt;ドメイン コント ローラーに&lt;レプリケート先 DC&gt;:ログオン エラー:対象のアカウント名が正しくありません。 この操作は続行されません。 </para></listItem><listItem><para>1396 ステータスの NTDS KCC、NTDS 一般または Microsoft-Windows-ActiveDirectory_DomainService イベントは、イベント ビューアーで、ディレクトリ サービス ログに記録されます。</para><para>よく 1396 状態が示されている active Directory のイベントが含まれますが、これらに限定されません。</para><table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11"><thead><tr><TD><para>イベント ID</para></TD><TD><para>イベント ソース</para></TD><TD><para>イベントの文字列</para></TD></tr></thead><tbody><tr><TD><para>1125</para></TD><TD><para>Microsoft-Windows-ActiveDirectory_DomainService</para></TD><TD><para>Active Directory ドメイン サービス インストール ウィザード (Dcpromo) は、次のドメイン コント ローラーとの接続を確立できませんでした。</para></TD></tr><tr><TD><para>1645</para><para>このイベントは、3 つの部分の SPN を一覧表示します。</para></TD><TD><para>NTDS レプリケーション</para></TD><TD><para>Active Directory は、宛先ドメイン コントローラの要求されたサービス プリンシパル名 (SPN) が、SPN を解決するキー配布センター (KDC) ドメイン コントローラ上で登録されていないため、認証済みのリモート プロシージャ コール (RPC) を別のドメイン コントローラに対して実行しませんでした。</para></TD></tr><tr><TD><para>1655</para></TD><TD><para>Microsoft-Windows-ActiveDirectory_DomainService</para></TD><TD><para>Active Directory Domain Services は、次のグローバル カタログと通信しようとして、試行が成功しなかった。</para></TD></tr><tr><TD><para>2847</para></TD><TD><para>Microsoft-Windows-ActiveDirectory_DomainService</para></TD><TD><para>知識整合性チェッカーには、読み取り専用のローカル ディレクトリ サービスのレプリケーション接続があり、次のディレクトリ サービス インスタンスにリモートで更新しようとしています。 操作に失敗しました。 これは再試行されます。</para></TD></tr><tr><TD><para>1925</para></TD><TD><para>NTDS KCC</para></TD><TD><para>次の書き込み可能なディレクトリ パーティションのレプリケーション リンクを確立できませんでした。</para></TD></tr><tr><TD><para>1926</para></TD><TD><para>NTDS KCC</para></TD><TD><para>失敗した次のパラメーターを使用して、読み取り専用のディレクトリ パーティションへのレプリケーション リンクを確立するために試行します。</para></TD></tr><tr><TD><para>5781</para></TD><TD><para>NETLOGON</para></TD><TD><para> サーバーは、DNS での名前を登録することはできません。</para></TD></tr></tbody></table></listItem><listItem><para>画面に表示されるエラーで失敗の DCPROMO</para><para>ダイアログ タイトルのテキスト:</para><para>Active Directory インストールに失敗しました</para><para>ダイアログ メッセージ テキスト:</para><para>操作が失敗しました。ディレクトリ サービスは、CN をサーバー オブジェクトを作成できませんでした NTDS Settings, CN = ServerBeingPromoted、CN = Servers, CN = サイト、CN = Sites, CN = Configuration, DC = contoso, DC = サーバー ReplicationSourceDC.contoso.com で com を = です。 </para><para>ネットワーク資格情報が提供されているレプリカを追加する十分なアクセス権があることを確認してください。 </para><para>
"ログオン失敗。対象のアカウント名が正しくありません。 "</para><para>ここでは、イベント ID 1645、1168、および 1125 が昇格されるサーバーにログオンされます。</para></listItem><listItem><para>ドライブを使用してマップ<embeddedLabel>net</embeddedLabel>:</para><code>C:&gt;net use z: &lt;server_name&gt;c$
System error 1396 has occurred.
Logon Failure: The target account name is incorrect.</code><para>この場合、システム イベント ログでイベント ID 333 もログ記録、サーバーと SQL Server などのアプリケーションに、大量の仮想メモリを使用します。</para></listItem><listItem><para>DC の時刻が正しくありません。</para></listItem><listItem><para>KDC は開始されません RODC の krbtgt アカウントの復元後の RODC で、削除されている必要があります。 たとえば、復元後エラー 1396 が表示されます。 </para><para>
イベント ID 1645 は RODC に記録されます。 </para><para>
Dcdiag は、RODC の krbtgt アカウントを更新できないエラーも報告されます。 </para></listItem>
</list>
    </content>
  </section>
  <section address="BKMK_Causes">
    <title>エラーの原因</title>
    <content>
      <para />
      <list class="ordered">
        <listItem>
          <para>SPN が Kerberos を使用して認証を試みると、クライアントに代わって、KDC によって検索されるグローバル カタログに存在しません。</para>
          <para>Active Directory レプリケーションのコンテキストでの Kerberos クライアントは DC では、SPN の参照を実行する KDC の変換先は、宛先 DC 自体では可能性がありますが、リモート DC 可能性があります。</para>
        </listItem>
        <listItem>
          <para>ユーザーまたはサービス アカウントが参照されるサービス プリンシパル名を含む送信先 DC にレプリケートしようとしています。 代わりに KDC によって検索されるグローバル カタログにありません。</para>
          <para>Active Directory レプリケーションのコンテキストで、ソース DC のコンピューター アカウントが実行する入力方向のレプリケート先 DC レプリケーションの代わりに、DC によって検索されるグローバル カタログにありません。</para>
        </listItem>
        <listItem>
          <para>レプリケート先 DC には、ソース Dc のドメインの LSA シークレットが不足しています。</para>
        </listItem>
        <listItem>
          <para>参照される SPN は、ソース DC の別のコンピューター アカウントに存在します。</para>
        </listItem>
      </list>
    </content>
  </section>
  <section address="BKMK_Resolutions">
    <title>解決策</title>
    <content>
      <list class="ordered">
        <listItem>
          <para>NTDS レプリケーション イベント 1645 のレプリケート先 DC 上のディレクトリ サービス イベント ログを確認し、次に注意してください。</para>
          <para>レプリケート先 DC の名前</para>
          <para>参照されている SPN (E3514235-4B06-11D1-AB04-00C04FC2DCD2/&lt;オブジェクト ソース ドメイン コント ローラーの NTDS 設定オブジェクトの guid&gt;/&lt;ターゲット ドメイン&gt;.&lt;tld&gt;@&lt;ターゲット ドメイン&gt;.&lt;tld&gt;</para>
          <para>レプリケート先 DC によって使用されている KDC</para>
        </listItem>
        <listItem>
          <para>手順 1. で識別される、KDC のコンソールで、次のように入力します。 </para>
          <code>nltest /dsgetdc &lt;forest root DNS domain name &gt; /gc</code>
          <para>レプリケート先 DC に 1396 エラーで失敗したレプリケーションの試行の直後 NLTEST ロケーター テストを実行します。 </para>
          <para>これは、KDC がに対する SPN の参照を実行しているその GC を特定します。 </para>
          <para>KDC によって検索される GC は、Microsoft-Windows-ActiveDirectory_DomainService イベント 1655 もキャプチャする可能性があります。</para>
        </listItem>
        <listItem>
          <para>手順 1 では、手順 2. で発見されたグローバル カタログで検出された SPN が検索されます。</para>
          <code>C:&gt;repadmin /showattr Server_Name DC=corp,DC=contoso,dc=com &lt;GC used by KDC&gt; &lt;DN path of forest root domain&gt; /filter:"(serviceprincipalname=&lt;SPN cited in the NTDS Replication event 1645&gt;)" /gc /subtree /atts:cn,serviceprincipalname</code>
          <para>または</para>
          <code>C:&gt;dsquery * forestroot -scope subtree -filter "(serviceprincipalname=E3514235-4B06-11D1-AB04-00C04FC2DCD2/65cead9f-4949-46a3-a49a-f1fbfe13d2b3*)" -attr * -s Server_Name.europe.corp.contoso.com</code>
          <para>SPN のホスト オブジェクトが存在することを確認します。</para>
          <para>ホスト オブジェクトは CNF/競合が破損または lost and found コンテナに存在するかどうかなどされているオブジェクトの DN パスを確認します。</para>
          <para>ソース Dc のコンピューター アカウントでのみ、ソース Dc の Active Directory レプリケーション SPN が登録されていることを確認します。</para>
          <para>レプリケーションの SPN がない場合は、ソース DC には、それ自体とその SPN が登録した場合と、SPN が単純なレプリケーションの待機時間またはレプリケーションの障害によって KDC で使用される、GC に不足しているかどうかを決定します。</para>
        </listItem>
        <listItem>
          <para>セキュリティで保護されたチャネルの状態を確認し、正常性を信頼します。</para>
        </listItem>
      </list>
    </content>
  </section>
  <relatedTopics>
    <externalLink>
      <linkText>エラー 1396 で失敗する Active Directory 操作のトラブルシューティング。ログオン エラー:対象のアカウント名が正しくありません。</linkText>
      <linkUri>https://support.microsoft.com/kb/2183411/en-gb</linkUri>
    </externalLink>
  </relatedTopics>
</developerConceptualDocument>


