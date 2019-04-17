---
ms.assetid: 399a8bbe-3375-4bb0-b55b-5f46e7050028
title: "レプリケーション エラー 1396。ログオン エラー、対象のアカウント名が正しくありません。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 84799de26e1260f914d9b959357d5eed6fef62f6
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="replication-error-1396-logon-failure-the-target-account-name-is-incorrect"></a>レプリケーション エラー 1396。ログオン エラー、対象のアカウント名が正しくありません。

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012


<developerConceptualDocument xmlns="https://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="https://www.w3.org/1999/xlink" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="https://ddue.schemas.microsoft.com/authoring/2003/5 http://clixdevr3.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>この記事では、現象について説明原因と Win32 エラー 1396 で失敗している Active Directory レプリケーションの解決方法:"ログオン エラー: 対象のアカウント名が正しくありません"。</para><list class="bullet"><listItem><para><link xlink:href="d3a01966-74c9-4c49-ba11-354b9acf7519#BKMK_Symptoms">現象</link></para></listItem><listItem><para><link xlink:href="d3a01966-74c9-4c49-ba11-354b9acf7519#BKMK_Causes">により</link></para></listItem><listItem><para><link xlink:href="d3a01966-74c9-4c49-ba11-354b9acf7519#BKMK_Resolutions">解像度</link></para></listItem></list>
  </introduction>
  <section address="BKMK_Symptoms">
    <title>現象</title>
    <content>
      <para />
      <list class="ordered">
<listItem><para>テストの Active Directory レプリケーション エラー 1396 失敗しました DCDIAG レポート: ログオン エラー: 対象のアカウント名が正しくありません"。</para><code>Testing server: &lt;Site name&gt;&lt;DC Name&gt;
Starting test: Replications
[Replications Check,&lt;DC Name&gt;] A recent replication attempt failed:
From &lt;source DC&gt; to &lt;destination DC&gt;
Naming Context: CN=&lt;DN path of naming context&gt;
<codeFeaturedElement>The replication generated an error (1396):
Logon Failure: The target account name is incorrect.</codeFeaturedElement>
The failure occurred at &lt;date&gt; &lt;time&gt;.
The last success occurred at &lt;date&gt; &lt;time&gt;.
XX failures have occurred since the last success</code></listItem><listItem><para>REPADMIN します。EXE は、1396 の状態と前回の複製の試行が失敗したことをレポートします。</para><para>よく 1396 状態が示されている REPADMIN コマンドが含まれますが、これらに限定されません。</para><table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11"><tbody><tr><TD><list class="bullet"><listItem><para>REPADMIN/ADD</para></listItem><listItem><para>REPADMIN/REPLSUM</para></listItem><listItem><para>REPADMIN かかる</para></listItem><listItem><para>REPADMIN /SHOWVECTOR/LATENCY</para></listItem></list></TD><TD><list class="bullet"><listItem><para>REPADMIN/SHOWREPS</para></listItem><listItem><para>REPADMIN/SHOWREPL</para></listItem><listItem><para>REPADMIN/SYNCALL</para></listItem></list></TD></tr></tbody></table><para>"REPADMIN/SHOWREPS"CONTOSO DC1 で失敗しているに CONTOSO DC2 からの入力方向のレプリケーションを表すからの出力サンプル、"ログオン エラー: 対象のアカウント名が正しくありません"エラーを次に示します::</para><code>Default-First-Site-NameCONTOSO-DC1
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
</code></listItem><listItem><para>、<ui>今すぐレプリケート</ui>Active Directory サイトとサービスでのコマンドを返します"ログオン エラー: 対象のアカウント名が正しくありません。"。</para><para>ソース ドメイン コントローラーからの接続オブジェクトを右クリックし、選択<ui>今すぐレプリケート</ui>が失敗し、"ログオン エラー: 対象のアカウント名が正しくありません"。画面に表示されるエラー メッセージを次に示します:</para><para>ダイアログのタイトル テキスト:</para><para>今すぐレプリケート</para><para>ダイアログ メッセージ テキスト: </para><para>名前付けコンテキストを同期するときに、次のエラーが発生しました&lt;パーティションの DNS パス&gt;ドメイン コントローラーから&lt;DC をソース&gt;ドメイン コントローラーに&lt;レプリケート先 DC&gt;: ログオン エラー: 対象のアカウント名が正しくありません。この操作は続行されません。</para></listItem><listItem><para>1396 ステータスの NTDS KCC、NTDS 一般または Microsoft Windows-activedirectory_domainservice のイベントはイベント ビューアーのディレクトリ サービス ログに記録します。</para><para>よく 1396 状態が示されている active Directory のイベントが含まれますが、これらに限定されません。</para><table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11"><thead><tr><TD><para>イベント ID</para></TD><TD><para>イベント ソース</para></TD><TD><para>イベントの文字列</para></TD></tr></thead><tbody><tr><TD><para>1125</para></TD><TD><para>Microsoft Windows-activedirectory_domainservice</para></TD><TD><para>Active Directory ドメイン サービス インストール ウィザード (Dcpromo) は、次のドメイン コントローラと接続を確立できませんでした。</para></TD></tr><tr><TD><para>1645</para><para>このイベントは、3 部構成 SPN を示します。</para></TD><TD><para>NTDS レプリケーション</para></TD><TD><para>Active Directory は、SPN を解決するキー配布センター (KDC) ドメイン コントローラーで、移行先のドメイン コントローラーの目的のサービス プリンシパル名 (SPN) が登録されていないために、認証済みのリモート プロシージャ コール (RPC) を別のドメイン コントローラに対して実行できませんでした。</para></TD></tr><tr><TD><para>1655</para></TD><TD><para>Microsoft Windows-activedirectory_domainservice</para></TD><TD><para>Active Directory ドメイン サービスは、次のグローバル カタログと通信しようとして、試行が成功しなかった。</para></TD></tr><tr><TD><para>2847</para></TD><TD><para>Microsoft Windows-activedirectory_domainservice</para></TD><TD><para>知識整合性チェッカーでは、読み取り専用のローカル ディレクトリ サービスのレプリケーション接続を配置し、次のディレクトリ サービス インスタンス上のリモートに更新しようとします。 操作に失敗しました。 再試行されます。</para></TD></tr><tr><TD><para>1925</para></TD><TD><para>NTDS KCC</para></TD><TD><para>次の書き込み可能なディレクトリ パーティションのレプリケーション リンクを確立するために失敗しました。</para></TD></tr><tr><TD><para>1926</para></TD><TD><para>NTDS KCC</para></TD><TD><para>失敗した次のパラメーターを使用して、読み取り専用のディレクトリ パーティションへのレプリケーション リンクを確立するために試行します。</para></TD></tr><tr><TD><para>5781</para></TD><TD><para>NETLOGON</para></TD><TD><para> サーバーは、DNS での名前を登録することはできません。</para></TD></tr></tbody></table></listItem><listItem><para>DCPROMO が画面に表示されるエラーで失敗</para><para>ダイアログのタイトル テキスト:</para><para>Active Directory インストールに失敗しました</para><para>ダイアログ メッセージ テキスト:</para><para>ため操作に失敗しました: cn サーバー オブジェクトを作成できませんでした: ディレクトリ サービス NTDS 設定、CN = ServerBeingPromoted、CN = Servers, CN = サイト、CN = Sites, CN = Configuration, DC = contoso, DC = サーバー ReplicationSourceDC.contoso.com で com を = します。</para><para>指定されたネットワーク資格情報は、レプリカを追加するための十分なアクセス権を持ちますを確認してください。</para><para> "ログオン エラー: 対象のアカウント名が正しくありません"。</para><para>ここでは、イベント ID 1645、1168、および 1125 ログに記録される昇格されるサーバー。</para></listItem><listItem><para>を使用してドライブをマップ<embeddedLabel>net</embeddedLabel>:</para><code>C:&gt;net use z: &lt;server_name&gt;c$
System error 1396 has occurred.
Logon Failure: The target account name is incorrect.</code><para>この場合、システム イベント ログにイベント ID 333 をログもサーバーのことができ、SQL Server などのアプリケーションの高い仮想メモリ量を使用します。</para></listItem><listItem><para>、DC の時間が正しくありません。</para></listItem><listItem><para>、KDC は起動しません RODC の krbtgt アカウントの復元後に、RODC は、削除されたためです。たとえば、復元後にエラー 1396 が表示されます。</para><para>イベント ID 1645 が RODC にログオンします。</para><para> Dcdiag も RODC krbtgt アカウントを更新できないことがエラーをレポートします。</para></listItem>
</list>
    </content>
  </section>
  <section address="BKMK_Causes">
    <title>により</title>
    <content>
      <para />
      <list class="ordered">
        <listItem>
          <para>SPN が Kerberos を使用して認証を試みると、クライアントの代わりに KDC によって検索されるグローバル カタログに存在しません。</para>
          <para>Active Directory レプリケーションのコンテキストでの Kerberos クライアントはレプリケート先 DC、KDC の SPN の検索を実行する可能性があります、レプリケート先 DC 自体がリモート DC がある可能性があります。</para>
        </listItem>
        <listItem>
          <para>に代わってレプリケート先 DC をレプリケートしようとすると、KDC によって検索グローバル カタログのプリンシパル名がされている検索サービスを含める必要があります、ユーザーまたはサービス アカウントが存在しません。</para>
          <para>Active Directory レプリケーションのコンテキストでは、ソース DC のコンピューター アカウントは、グローバル カタログを実行する入力方向のレプリケーションをレプリケート先 DC の代わりに、DC で検索に存在しません。</para>
        </listItem>
        <listItem>
          <para>レプリケート先 DC が Dc にソース ドメインの LSA シークレットがありません。</para>
        </listItem>
        <listItem>
          <para>ルックアップされている、SPN がソース ドメイン コントローラー以外の別のコンピューター アカウントに存在します。</para>
        </listItem>
      </list>
    </content>
  </section>
  <section address="BKMK_Resolutions">
    <title>解決策</title>
    <content>
      <list class="ordered">
        <listItem>
          <para>NTDS レプリケーション イベント 1645 のレプリケート先 DC でディレクトリ サービス イベント ログを確認し、次に注意してください:</para>
          <para>レプリケート先 DC の名前</para>
          <para>ルックアップの SPN がされている (E3514235-4B06-11D1-AB04-00C04FC2DCD2/&lt;オブジェクトのソース ドメイン コントローラーの NTDS 設定オブジェクトの guid&gt;/&lt;ターゲット ドメイン&gt;.&lt;tld&gt;@&lt;ターゲット ドメイン&gt;します。&lt;tld&gt;</para>
          <para>レプリケート先 DC によって使用されている、KDC</para>
        </listItem>
        <listItem>
          <para>手順 1 で識別される、KDC のコンソールから、入力: </para>
          <code>nltest /dsgetdc &lt;forest root DNS domain name &gt; /gc</code>
          <para>すぐ後にレプリケーションをしようとレプリケート先 DC で 1396 エラーで失敗する NLTEST ロケーター テストを実行します。</para>
          <para>これに対して SPN lookup KDC を実行しているその GC を識別する必要があります。</para>
          <para>KDC によって検索される、GC は、Microsoft Windows-activedirectory_domainservice のイベント 1655 でもキャプチャ可能性があります。</para>
        </listItem>
        <listItem>
          <para>手順 2 で検出されたグローバル カタログに手順 1 で検出された SPN を検索します。</para>
          <code>C:&gt;repadmin /showattr Server_Name DC=corp,DC=contoso,dc=com &lt;GC used by KDC&gt; &lt;DN path of forest root domain&gt; /filter:"(serviceprincipalname=&lt;SPN cited in the NTDS Replication event 1645&gt;)" /gc /subtree /atts:cn,serviceprincipalname</code>
          <para>または</para>
          <code>C:&gt;dsquery * forestroot -scope subtree -filter "(serviceprincipalname=E3514235-4B06-11D1-AB04-00C04FC2DCD2/65cead9f-4949-46a3-a49a-f1fbfe13d2b3*)" -attr * -s Server_Name.europe.corp.contoso.com</code>
          <para>SPN の場合は、そのホスト オブジェクトが存在することを確認します。</para>
          <para>DN パス、ホスト オブジェクトを含めるため、オブジェクトが CNF]、[競合の破損または lost and found コンテナに存在するかどうかを確認します。</para>
          <para>ソース Dc のコンピューター アカウントでのみ、ソース Dc Active Directory レプリケーションの SPN が登録されていることを確認します。</para>
          <para>レプリケーション SPN が存在しない場合は、ソース DC が、それ自体とその SPN を登録済みの場合と SPN が KDC 単純なレプリケーションの潜在期間またはレプリケーションに失敗した原因で使用される、GC に不足しているかどうかを決定します。</para>
        </listItem>
        <listItem>
          <para>セキュリティで保護されたチャネルのヘルスを確認し、正常性を信頼します。</para>
        </listItem>
      </list>
    </content>
  </section>
  <relatedTopics>
    <externalLink>
      <linkText>エラー 1396 で失敗する Active Directory のトラブルシューティング操作: ログオン エラー: 対象のアカウント名が正しくありません。</linkText>
      <linkUri>https://support.microsoft.com/kb/2183411/en-gb</linkUri>
    </externalLink>
  </relatedTopics>
</developerConceptualDocument>


