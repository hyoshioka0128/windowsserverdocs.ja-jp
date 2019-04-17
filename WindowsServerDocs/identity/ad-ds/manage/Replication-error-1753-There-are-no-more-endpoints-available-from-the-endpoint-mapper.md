---
ms.assetid: 0f21951c-b1bf-43bb-a329-bbb40c58c876
title: "レプリケーション エラー 1753。エンドポイント マッパーから使用できるエンドポイントは"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 0e7412f5edc6c206888551fdc250883b5c0ced3e
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="replication-error-1753-there-are-no-more-endpoints-available-from-the-endpoint-mapper"></a>レプリケーション エラー 1753。エンドポイント マッパーから使用できるエンドポイントは

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012


<developerConceptualDocument xmlns="https://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="https://www.w3.org/1999/xlink" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="https://ddue.schemas.microsoft.com/authoring/2003/5 http://clixdevr3.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>このトピックでは、現象、原因、および Active Directory レプリケーション エラー 8524 DSA 操作は DNS 参照エラーのため続行できませんを解決する方法について説明します。</para>
    <list class="bullet">
      <listItem><para><link xlink:href="f7022f0d-0099-410c-8178-c654e624bc42#BKMK_Symptoms">現象</link></para></listItem><listItem><para><link xlink:href="f7022f0d-0099-410c-8178-c654e624bc42#BKMK_Cause">原因</link></para></listItem><listItem><para><link xlink:href="f7022f0d-0099-410c-8178-c654e624bc42#BKMK_Resolutions">解像度</link></para></listItem><listItem><para><link xlink:href="f7022f0d-0099-410c-8178-c654e624bc42#BKMK_MoreInfo">詳細</link></para></listItem>
    </list>
  </introduction>
  <section address="BKMK_Symptoms">
    <title>現象</title>
    <content>
      <para>現象、原因を説明し、解像度 Win32 エラー 1753 で失敗する Active Directory 操作の手順を実行します"があるエンドポイントはこれ以上ないエンドポイント マッパーから使用できる。"。</para>
      <list class="ordered">
        <listItem>
          <para>接続のテスト、Active Directory レプリケーションのテストまたは KnowsOfRoleHolders テストが失敗したエラー 1753 DCDIAG レポート:"があるエンドポイントはこれ以上ないエンドポイント マッパーから使用できる。"。</para>
          <code>Testing server: &lt;site&gt;&lt;DC Name&gt;
Starting test: Connectivity
* Active Directory LDAP Services Check
* Active Directory RPC Services Check
[&lt;DC Name&gt;] <codeFeaturedElement>DsBindWithSpnEx() failed with error 1753,
There are no more endpoints available from the endpoint mapper..</codeFeaturedElement>
Printing RPC Extended Error Info:
Error Record 1, ProcessID is &lt;process ID&gt; (DcDiag) 
System Time is: &lt;date&gt; &lt;time&gt;
Generating component is 2 (RPC runtime)
Status is 1753: There are no more endpoints available from the endpoint mapper. Detection location is 500
NumberOfParameters is 4
Unicode string: ncacn_ip_tcp
Unicode string: &lt;source DC object GUID&gt;._msdcs.contoso.com
Long val: -481213899
Long val: 65537
Error Record 2, ProcessID is 700 (DcDiag) 
System Time is: &lt;date&gt; &lt;time&gt;
Generating component is 2 (RPC runtime)
<codeFeaturedElement>Status is 1753: There are no more endpoints available from the endpoint mapper.</codeFeaturedElement>
NumberOfParameters is 1
Unicode string: 1025
[Replications Check,&lt;DC Name&gt;] A recent replication attempt failed:
From &lt;source DC&gt; to &lt;destination DC&gt;
Naming Context: &lt;DN path of directory partition&gt;
The replication generated an error <codeFeaturedElement>(1753):
There are no more endpoints available from the endpoint mapper.</codeFeaturedElement> 
The failure occurred at &lt;date&gt; &lt;time&gt;.
The last success occurred at &lt;date&gt; &lt;time&gt;.
3 failures have occurred since the last success.
The directory on &lt;DC name&gt; is in the process.
of starting up or shutting down, and is not available.
Verify machine is not hung during boot.
</code>
        </listItem>
<listItem><para>REPADMIN します。EXE では、その複製が失敗の状態 1753 をレポートします。</para><para>よく 1753 状態が示されている REPADMIN コマンドが含まれますが、これらに限定されません。</para><table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11"><tbody><tr><TD><list class="bullet"><listItem><para>REPADMIN/REPLSUM</para></listItem><listItem><para>REPADMIN/SHOWREPL</para></listItem></list></TD><TD><list class="bullet"><listItem><para>REPADMIN/SHOWREPS</para></listItem><listItem><para>REPADMIN/SYNCALL</para></listItem></list></TD></tr></tbody></table><para>"REPADMIN/SHOWREPS"を表す「レプリケーション アクセスが拒否されました」エラーで CONTOSO DC1 が失敗する CONTOSO DC2 からの入力方向のレプリケーションが次に示すからの出力の例:</para><code>Default-First-Site-NameCONTOSO-DC1
DSA Options: IS_GC 
Site Options: (none)
DSA object GUID: b6dc8589-7e00-4a5d-b688-045aef63ec01
DSA invocationID: b6dc8589-7e00-4a5d-b688-045aef63ec01
==== INBOUND NEIGHBORS ======================================
DC=contoso,DC=com
Default-First-Site-NameCONTOSO-DC2 via RPC
DSA object GUID: 74fbe06c-932c-46b5-831b-af9e31f496b2
Last attempt @ &lt;date&gt; &lt;time&gt; failed, <codeFeaturedElement>result 1753 (0x6d9):
There are no more endpoints available from the endpoint mapper.</codeFeaturedElement>
&lt;#&gt; consecutive failure(s).
Last success @ &lt;date&gt; &lt;time&gt;.

</code></listItem><listItem><para>、<ui>レプリケーション トポロジの確認</ui>Active Directory サイトとサービスでのコマンドは、「があるエンドポイントはこれ以上ないエンドポイント マッパーから使用可能な」を返します</para><para>ソース ドメイン コントローラーからの接続オブジェクトを右クリックし、選択<ui>レプリケーション トポロジの確認</ui>「があるエンドポイントはこれ以上ないエンドポイント マッパーから使用可能な」で失敗します。画面に表示されるエラー メッセージを次に示します:</para><para>ダイアログのタイトル テキスト: レプリケーション トポロジの確認</para><para>ダイアログ メッセージ テキスト: </para><para>ドメイン コントローラーに接続しているときに、次のエラーが発生しました: エンドポイントがあるエンドポイント マッパーから使用できます。</para></listItem><listItem><para>、<ui>今すぐレプリケート</ui>Active Directory サイトとサービスでのコマンドは、「があるエンドポイントはこれ以上ないエンドポイント マッパーから使用可能な」を返します</para><para>ソース ドメイン コントローラーからの接続オブジェクトを右クリックし、選択<ui>今すぐレプリケート</ui>「があるエンドポイントはこれ以上ないエンドポイント マッパーから使用可能な」で失敗します。画面に表示されるエラー メッセージを次に示します:</para><para>ダイアログのタイトル テキスト: 今すぐレプリケート</para><para>ダイアログ メッセージ テキスト: 名前付けコンテキストを同期するときに、次のエラーが発生した&lt;% のディレクトリ パーティション名&gt;ドメイン コントローラーから&lt;ソース DC&gt;ドメイン コントローラーに&lt;宛先 DC&gt;:</para><para>

エンドポイントはエンドポイント マッパーから使用できます。</para><para>、操作は続行されません</para></listItem><listItem><para>-2146893022 ステータスの NTDS KCC、NTDS 一般または Microsoft Windows-activedirectory_domainservice のイベントはイベント ビューアーのディレクトリ サービス ログに記録します。</para><para>よく-2146893022 状態が示されている active Directory のイベントが含まれますが、これらに限定されません。</para><table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11"><thead><tr><TD><para>イベント ID</para></TD><TD><para>イベント ソース</para></TD><TD><para>イベントの文字列</para></TD></tr></thead><tbody><tr><TD><para>1655</para></TD><TD><para>NTDS 全般</para></TD><TD><para>Active Directory は、次のグローバル カタログと通信しようとして、試行が成功しなかった。</para></TD></tr><tr><TD><para>1925</para></TD><TD><para>NTDS KCC</para></TD><TD><para>次の書き込み可能なディレクトリ パーティションのレプリケーション リンクを確立するために失敗しました。</para></TD></tr><tr><TD><para>1265</para></TD><TD><para>NTDS KCC</para></TD><TD><para>知識整合性チェッカー (KCC) によって、次のディレクトリ パーティションとソース ドメイン コントローラーの複製契約の追加に失敗しました。</para></TD></tr></tbody></table></listItem>
</list>
    </content>
  </section>
  <section address="BKMK_Cause">
    <title>原因</title>
    <content>
      <para>次の図は、手順 7. で、クライアント アプリケーションに、RPC クライアントからデータを渡すことを手順 1 で RPC エンドポイント マッパー (EPM) でのサーバー アプリケーションの登録と開始 RPC ワークフローを示しています。</para>
      <para>&lt;ADDS_RPCWorkflow&gt;</para>
      <para>手順 1. ~ 7 マップ、次の操作を:</para>
      <list class="ordered">
        <listItem>
          <para>RPC エンドポイント マッパー (EPM) とそのエンドポイントを登録するサーバー アプリケーション</para>
        </listItem>
        <listItem>
          <para>クライアントは、RPC 呼び出し (、ユーザーに代わって OS やアプリケーション操作を開始しました) </para>
        </listItem>
        <listItem>
          <para>クライアント RPC 連絡先 EPM 対象のコンピューターを側し、クライアントの呼び出しを完了するエンドポイントを求める</para>
        </listItem>
        <listItem>
          <para>サーバー コンピューターの EPM は、エンドポイントで応答</para>
        </listItem>
        <listItem>
          <para>クライアント側 RPC サーバー アプリの連絡先</para>
        </listItem>
        <listItem>
          <para>Server アプリは、呼び出しを実行、RPC クライアントに結果が返さ</para>
        </listItem>
        <listItem>
          <para>クライアント側 RPC クライアント アプリに結果を渡します</para>
        </listItem>
      </list>
      <para>エラー 1753 は手順 3 と 4 間での障害によって生成されます。具体的には、エラー 1753。は、RPC クライアント (レプリケート先 DC) がポート 135 経由の RPC サーバー (ソース DC) にお問い合わせくださいできましたが、RPC サーバー (ソース DC) で EPM 関心のある RPC アプリケーションを見つけることができませんでしたし、サーバー側のエラー 1753 返されることを意味します。1753 エラーの存在は、RPC クライアント (レプリケート先 DC) が、ネットワーク経由での RPC サーバー (AD レプリケーション ソース DC) からサーバー側エラー応答を受信したことを示します。</para>
      <para>1753 エラーの原因として特定の根本原因が考えられます: </para>
      <list class="ordered">
        <listItem>
          <para>、server アプリを起動していない (つまり手順 1 での上にある「詳細」の図は、決して実行しようとしました)。</para>
        </listItem>
        <listItem>
          <para>サーバー アプリの起動が、RPC エンドポイント マッパー (つまり手順 1 上の「詳細」図がしようとしましたが、失敗しました) に登録できない原因となった初期化中に何らかの障害が発生しました。</para>
        </listItem>
        <listItem>
          <para>Server アプリ亡くなりました後は、開始します。(つまり手順 1 上の「詳細」図に、正常に完了しましたは取り消された後で、サーバー亡くなりましたため)。</para>
        </listItem>
        <listItem>
          <para>Server アプリには、そのエンドポイント (意図的なものが 3 に似ています手動で登録されていません。いない可能性がありますが含まれている万全を期しています。)</para>
        </listItem>
        <listItem>
          <para>の RPC クライアント (レプリケート先 DC) よりも、意図した名前を DNS、WINS、またはホスト/Lmhosts ファイル内の IP 割り当てエラーのためのさまざまな RPC サーバーに接続します。</para>
        </listItem>
      </list>
      <para>エラー 1753 が原因ではない: </para>
      <list class="bullet">
        <listItem>
          <para>間のネットワーク接続、RPC クライアント (レプリケート先 DC) と RPC サーバー (ソース DC) 上のポート 135 が不足している</para>
        </listItem>
        <listItem>
          <para>(ソース DC) の RPC サーバー間のネットワーク接続が不足しているポート 135 および RPC クライアント (レプリケート先 DC) を使用して、一時的なポート経由でします。</para>
        </listItem>
        <listItem>
          <para>パスワードが一致しないか、ソース ドメイン コントローラーで Kerberos 暗号化されたパケットの暗号化を解除することができない</para>
        </listItem>
      </list>
      <para></para>
    </content>
  </section>
  <section address="BKMK_Resolutions">
    <title>解決策</title>
    <content>
      <list class="ordered">
        <listItem>
          <para>
            <embeddedLabel>そのサービスのエンドポイント マッパーに登録サービスが開始したことを確認する</embeddedLabel>
          </para>
          <para>Windows 2000 および Windows Server 2003 Dc: ソース ドメイン コントローラーが通常モードになっていることを確認します。</para>
          <para> Windows Server 2008 または Windows Server 2008 R2: ソース DC のコンソールで、サービス マネージャー (services.msc) を開始していることを確認、<embeddedLabel>Active Directory Domain Services</embeddedLabel>サービスが実行されています。</para>
        </listItem>
        <listItem>
          <para>
            <embeddedLabel>RPC クライアント (レプリケート先 DC) (ソース DC)、意図した RPC サーバーに接続されていることを確認</embeddedLabel>
          </para>
          <para>_msdcs にドメイン コントローラー CNAME を記録、一般的な Active Directory フォレスト レジスタですべての Dc です。&lt;フォレスト ルート ドメイン&gt;フォレスト内にあるどのドメインに関係なく、DNS ゾーンです。DC の CNAME レコードはから派生した、<embeddedLabel>objectGUID</embeddedLabel>各ドメイン コントローラーの NTDS 設定オブジェクトの属性です。</para>
          <para>レプリケート先 DC のソース Dc の CNAME レコードの DNS クエリ レプリケーション ベースの操作を実行するとき。CNAME レコードには、ソース Dc の IP アドレスを取得するために使用するソース ドメイン コントローラーの完全修飾コンピューター名が含まれています。DNS クライアント キャッシュの照合を使ってホスト/LMHost ファイル参照では、ホスト A]、[DNS、または WINS で AAAA を記録します。</para>
          <para>古い NTDS 設定オブジェクトと DNS、WINS、ホストおよび LMHOST ファイルに無効な名前-TO-IP マッピング場合 (ソース DC) が誤った RPC サーバーに接続するには、RPC クライアント (レプリケート先 DC) があります。さらに、不正な名前-TO-IP マッピングでは、インストールされている関心 (この場合は、Active Directory ロール) の RPC サーバー アプリケーションもがないコンピューターに接続するには、RPC クライアント (レプリケート先 DC) 可能性があります。(例: DC2 の古いホスト レコードが DC3 またはメンバー コンピューターの IP アドレスが含まれています)。</para>
          <para>ソース Active Directory のドメイン コントローラーのコピー先に存在している DC の objectGUID ソース Dc のコピーの Active Directory に格納されているソース DC の objectGUID を一致することを確認します。不一致がある場合は、repadmin を使用して /showobjmeta ntds 設定オブジェクトをソース ドメイン コントローラーの昇格の最後に対応する 1 つを参照してください (ヒント: NTDS 設定オブジェクトの作成日から、日付スタンプを比較 /showobjmeta に対してソース Dc dcpromo.log ファイルの最後のプロモーション日付。最後の変更]、[DCPROMO.LOG ファイル自体)。オブジェクトの Guid が同一ではない場合、レプリケート先 DC の可能性が高いの CNAME レコードが IP のマッピングに不正な名前のホスト レコードを指しますソース DC の古い NTDS 設定オブジェクトがあります。</para>
          <para>レプリケート先 DC の IPCONFIG/ALL を決定のレプリケート先 DC を使用して DNS サーバーの名前解決を実行します</para>
          <code>c:&gt;ipconfig /all</code>
          <para>レプリケート先 DC の、でソース Dc の完全修飾 DC の CNAME レコードに対する nslookup コマンドを実行:</para>
          <code>c:&gt;nslookup -type=cname &lt;fully qualified cname of source DC&gt; &lt;destination DCs primary DNS Server IP &gt;
c:&gt;nslookup -type=cname &lt;fully qualified cname of source DC&gt; &lt;destination DCs secondary DNS Server IP&gt;</code>
          <para>NSLOOKUP によって返される IP アドレスが、ホスト名を"所有"していることを確認/ソース DC のセキュリティ id:</para>

          <code>C:&gt;NBTSTAT -A &lt;IP address returned by NSLOOKUP in the step above&gt;</code>
          <para>または</para>
          <para>ソース DC のコンソールにログオン。、CMD プロンプトから"IPCONFIG"を実行し、ソース DC が上記の NSLOOKUP コマンドによって返される IP アドレスを所有していることを確認</para>
          <para>古い]、[重複する IP のマッピングを DNS にホストするためのチェック</para>
          <code>NSLOOKUP -type=hostname &lt;single label hostname of source DC&gt; &lt;primary DNS Server IP on destination DC&gt;
NSLOOKUP -type=hostname &lt;single label hostname of source DC&gt; &lt;secondary DNS Server IP on destination DC&gt;

NSLOOKUP -type=hostname &lt;fully qualified computer name of source DC&gt; &lt;primary DNS Server IP on destination DC&gt;
NSLOOKUP -type=hostname &lt;fully qualified computer name of source DC&gt; &lt;secondary DNS Server IP on dest. DC&gt;</code>
<para>ホスト レコードに無効な IP アドレスが存在する場合は、DNS スカベンジングを有効になっていると適切に構成されているかどうかを調査します。</para><para>上記のテストまたはネットワーク トレースが無効な IP アドレスを返す、名前クエリを表示されない場合は、ホスト ファイル、LMHOSTS ファイルおよび WINS サーバーで古いエントリを検討してください。DNS サーバーには WINS フォールバック名前解決を実行するも構成することに注意してください。</para>
</listItem>
        <listItem>
          <para>
            <embeddedLabel>サーバー アプリケーション (Active Directory などで) が、RPC サーバー (ソース DC) 上のエンドポイント マッパーに登録されていることを確認</embeddedLabel>
          </para>
          <para>Active Directory はよく知られていると、動的に登録されているポートの組み合わせを使用します。次の表は、よく知られているポートと Active Directory ドメイン コントローラーで使用されるプロトコルを示します。</para>
          <table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11">
            <thead>
              <tr>
                <TD>
                  <para>RPC サーバー アプリケーション</para>
                </TD>
                <TD>
                  <para>ポート</para>
                </TD>
                <TD>
                  <para>TCP</para>
                </TD>
                <TD>
                  <para>UDP</para>
                </TD>
              </tr>
            </thead>
            <tbody>
              <tr>
                <TD>
                  <para>DNS サーバー</para>
                </TD>
                <TD>
                  <para>53</para>
                </TD>
                <TD>
                  <para>X</para>
                </TD>
                <TD>
                  <para>X</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>Kerberos</para>
                </TD>
                <TD>
                  <para>88</para>
                </TD>
                <TD>
                  <para>X</para>
                </TD>
                <TD>
                  <para>X</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>LDAP サーバー</para>
                </TD>
                <TD>
                  <para>389</para>
                </TD>
                <TD>
                  <para>X</para>
                </TD>
                <TD>
                  <para>X</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>Microsoft DS</para>
                </TD>
                <TD>
                  <para>445</para>
                </TD>
                <TD>
                  <para>X</para>
                </TD>
                <TD>
                  <para>X</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>LDAP SSL</para>
                </TD>
                <TD>
                  <para>636</para>
                </TD>
                <TD>
                  <para>X</para>
                </TD>
                <TD>
                  <para>X</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>グローバル カタログ サーバー</para>
                </TD>
                <TD>
                  <para>3268</para>
                </TD>
                <TD>
                  <para>X</para>
                </TD>
                <TD>
                  <para />
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>グローバル カタログ サーバー</para>
                </TD>
                <TD>
                  <para>3269</para>
                </TD>
                <TD>
                  <para>X</para>
                </TD>
                <TD>
                  <para />
                </TD>
              </tr>
            </tbody>
          </table>
          <para>Well-known ports are NOT registered with the endpoint mapper. </para>
          <para>Active Directory and other applications also register services that receive dynamically assigned ports in the RPC ephemeral port range. Such RPC server applications are dynamically assigned TCP ports between 1024 and 5000 on Windows 2000 and Windows Server 2003 computers and ports between 49152 and 65535 range on Windows Server 2008 and Windows Server 2008 R2 computers. The RPC port used by replication can be hard-coded in the registry using the steps documented in <externalLink><linkText>KB article 224196</linkText><linkUri>https://support.microsoft.com/kb/224196</linkUri></externalLink>. Active Directory continues to register with the EPM when configured to use a hard coded port. </para>
          <para>Verify that the RPC Server application of interest has registered itself with the RPC endpoint mapper on the RPC Server (the source DC in the case of AD replication). </para>
          <para>There are a number of ways to accomplish this task but one is to install and run PORTQRY from an admin privileged CMD prompt on the console of the source DC using the syntax: </para>
          <code>c:\&gt;portquery -n &lt;source DC&gt; -e 135 &gt;file.txt</code>
          <para>In the portqry output, note the port numbers dynamically registered by the "MS NT Directory DRS Interface" (UUID = 351...) for the <embeddedLabel>ncacn_ip_tcp protocol</embeddedLabel>. The snippet below shows sample portquery output from a Windows Server 2008 R2 DC and the UUID / protocol pair specifically used by Active Directory highlighted in <embeddedLabel>bold</embeddedLabel>: </para>
          <code>UUID: e3514235-4b06-11d1-ab04-00c04fc2dcd2 MS NT Directory DRS Interface
ncacn_np:CONTOSO-DC01[\pipe\lsass] 
UUID: e3514235-4b06-11d1-ab04-00c04fc2dcd2 MS NT Directory DRS Interface
ncacn_np:CONTOSO-DC01[\PIPE\protected_storage] 
<codeFeaturedElement>UUID: e3514235-4b06-11d1-ab04-00c04fc2dcd2 MS NT Directory DRS Interface
ncacn_ip_tcp:CONTOSO-DC01[49156]</codeFeaturedElement> 
UUID: e3514235-4b06-11d1-ab04-00c04fc2dcd2 MS NT Directory DRS Interface
ncacn_http:CONTOSO-DC01[49157] 
UUID: e3514235-4b06-11d1-ab04-00c04fc2dcd2 MS NT Directory DRS Interface
ncacn_http:CONTOSO-DC01[6004]</code>
          <para />
        </listItem>
        <listItem>
          <para>Other possible ways to resolve this error:</para>
          <list class="ordered">
            <listItem>
              <para>Verify that the source DC is booted in normal mode and that the OS and DC role on the source DC have fully started.</para>
            </listItem>
            <listItem>
              <para>Verify that the Active Directory Domain Service is running. If the service is currently stopped or was not configured with default startup values, reset the default startup values, reboot the modified DC then retry the operation.</para>
            </listItem>
            <listItem>
              <para>Verify that the startup value and service status for RPC service and RPC Locator is correct for OS version of the RPC Client (destination DC) and RPC Server (source DC). If the service is currently stopped or was not configured with default startup values, reset the default startup values, reboot the modified DC then retry the operation.</para>
              <para>In addition, ensure that the service context matches default settings listed in the following table.</para>
              <table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11">
                <thead>
                  <tr>
                    <TD>
                      <para>サービス</para>
                    </TD>
                    <TD>
                      <para>既定の状態 (スタートアップの種類) Windows Server 2003 以降 </para>
                    </TD>
                    <TD>
                      <para>Windows Server 2000 で既定の状態 (スタートアップの種類)</para>
                    </TD>
                  </tr>
                </thead>
                <tbody>
                  <tr>
                    <TD>
                      <para>リモート プロシージャ コール</para>
                    </TD>
                    <TD>
                      <para>(自動) の開始</para>
                    </TD>
                    <TD>
                      <para>(自動) の開始</para>
                    </TD>
                  </tr>
                  <tr>
                    <TD>
                      <para>リモート プロシージャ コール ロケーター</para>
                    </TD>
                    <TD>
                      <para>Null (手動) を停止しているか</para>
                    </TD>
                    <TD>
                      <para>(自動) の開始</para>
                    </TD>
                  </tr>
                </tbody>
              </table>
            </listItem>
            <listItem>
              <para>Verify that the size of the dynamic port range has not been constrained. The Windows Server 2008 and Windows Server 2008 R2 NETSH syntax to enumerate the RPC port range is shown below:</para>
              <code>&gt;netsh int ipv4 show dynamicport tcp
&gt;netsh int ipv4 show dynamicport udp
&gt;netsh int ipv6 show dynamicport tcp
&gt;netsh int ipv6 show dynamicport udp</code>
            </listItem>
            <listItem>
              <para>Verify that hard coded port definitions defined in KB 224196 fall within the dynamic port range for source DCs OS version.</para>
              <para>Review <externalLink><linkText>KB article 224196</linkText><linkUri>https://support.microsoft.com/kb/224196</linkUri></externalLink> and ensure that the hard coded port falls within the ephemeral port range for the source DC's operating system version.</para>
            </listItem>
            <listItem>
              <para>Verify that the ClientProtocols key exists under HKLM\Software\Microsoft\Rpc and contains the following 5 default values:</para>
              <code>ncacn_http REG_SZ rpcrt4.dll
ncacn_ip_tcp REG_SZ rpcrt4.dll
<codeFeaturedElement>ncacn_nb_tcp REG_SZ rpcrt4.dll</codeFeaturedElement>
ncacn_np REG_SZ rpcrt4.dll
ncacn_ip_udp REG_SZ rpcrt4.dll</code>
            </listItem>
          </list>
        </listItem>
      </list>
    </content>
  </section>
  <section address="BKMK_MoreInfo">
    <title>詳細については</title>
    <content>
      <para>
        <embeddedLabel>マッピング-2146893022 と RPC エラー 1753 原因 IP に不良名の例: 対象のプリンシパル名が正しくない</embeddedLabel>
      </para>
      <para>contoso.com ドメインから成る DC1 および DC2 で IP アドレス x.x.1.1 と x.x.1.2 します。"A"ホスト]、[すべての DC1 用に構成された DNS サーバーに DC2 用の"AAAA"レコードが正しく登録されています。さらに、DC1 上の HOSTS ファイルには、IP アドレス x.x.1.2 へ DC2s の完全修飾ホスト名のマッピングのエントリが含まれています。後で、DC2 の IP アドレスの変更 X.X.1.2 から X.X.1.3 と新しいメンバー コンピューターには、IP アドレス x.x.1.2 を使用してドメインに参加しています。AD レプリケーションによって試行がトリガーされる、<ui>今すぐレプリケート</ui>トレース以下に示すように、エラー 1753 で Active Directory サイトとサービス スナップインでのコマンドが失敗した:</para>
      <code>F# SRC    DEST    Operation 
1 x.x.1.1 x.x.1.2 ARP:Request, x.x.1.1 asks for x.x.1.2
2 x.x.1.2 x.x.1.1 ARP:Response, x.x.1.2 at 00-13-72-28-C8-5E
3 x.x.1.1 x.x.1.2 TCP:Flags=......S., SrcPort=50206, DstPort=DCE endpoint resolution(135)
4 x.x.1.2 x.x.1.1 ARP:Request, x.x.1.2 asks for x.x.1.1
5 x.x.1.1 x.x.1.2 ARP:Response, x.x.1.1 at 00-15-5D-42-2E-00
6 x.x.1.2 x.x.1.1 TCP:Flags=...A..S., SrcPort=DCE endpoint resolution(135)
7 x.x.1.1 x.x.1.2 TCP:Flags=...A...., SrcPort=50206, DstPort=DCE endpoint resolution(135)
8 x.x.1.1 x.x.1.2 MSRPC:c/o Bind: UUID{E1AF8308-5D1F-11C9-91A4-08002B14A0FA} EPT(EPMP) 
9 x.x.1.2 x.x.1.1 MSRPC:c/o Bind Ack: Call=0x2 Assoc Grp=0x5E68 Xmit=0x16D0 Recv=0x16D0 
<codeFeaturedElement>10</codeFeaturedElement> x.x.1.1 x.x.1.2 EPM:Request: ept_map: NDR, DRSR(DRSR) {E3514235-4B06-11D1-AB04-00C04FC2DCD2} [DCE endpoint resolution(135)]
<codeFeaturedElement>11</codeFeaturedElement> x.x.1.2 x.x.1.1 EPM:Response: ept_map: 0x16C9A0D6 - EP_S_NOT_REGISTERED
</code>
      <para>フレームで<embeddedLabel>10</embeddedLabel>、レプリケート先 DC が Active Directory レプリケーションのサービス クラス UUID E351 ポート 135 経由でソース Dc のエンドポイント マッパーを照会しています.</para>
      <para>フレームで<embeddedLabel>11</embeddedLabel>、ソース DC では、この場合はメンバーのコンピューターである場合、DC の役割をホストしていないと、そのため、E351 登録いません.そのローカル EPM でレプリケーション サービスの UUID は「があるエンドポイントはこれ以上ないエンドポイント マッパーから使用可能な」シンボリック エラー 1753 10 進数のエラー、16 進数のエラー 0x6d9 およびわかりやすいエラーにマップする EP_S_NOT_REGISTERED で応答します。</para>
      <para>"MayberryDC"contoso.com ドメインで、レプリカとして IP アドレス x.x.1.2 とメンバーのコンピューターが後で、昇格を取得します。もう一度、<ui>今すぐレプリケート</ui>コマンドを使用してレプリケーションをトリガーが、この時間が失敗し、画面に表示されるエラー「対象のプリンシパル名が正しくありません」。コンピューターがネットワーク アダプターの ip アドレスが割り当てられているアドレス x.x.1.2<placeholder>は</placeholder>、ドメイン コントローラーが通常モードで起動した現在と... E351 が登録されているレプリケーション サービスでは、ローカルの EPM UUID DC2 の名前またはセキュリティ ID を所有していないと、要求できるようになりましたエラーで失敗"対象のプリンシパル名が正しくありません"ように DC1 から Kerberos 要求の暗号化を解除できません。エラーは、10 進数のエラー-2146893022 にマップ/16 進数のエラー 0x80090322 します。</para>
      <para>ホストで古いエントリがこのような無効なホスト-TO-IP マッピングが考えられます lmhost ファイルでは、ホストの A//DNS、または WINS で AAAA 登録します。</para>
      <para>概要: この例は、無効なホスト-TO-IP マッピング (ここではホスト ファイル) の SPN がまだ登録されていないレプリケーションと、ソース DC エラー 1753。返されるので、"ソース"サービスは実行中 (またはその問題に関してもインストールされている)、Active Directory ドメイン サービスに含まれていない DC に解決するレプリケート先 DC が発生したために失敗しました。2 番目のケースで、無効なホスト-TO-IP マッピング (ホスト ファイル) でもう一度の移行先のドメイン コントローラー レプリケーション、SPN が登録されている、E351... DC に接続する原因となったがそのソース別のホスト名とセキュリティ ID 意図されるソース DC より-2146893022 のエラーで、試行が失敗したため: 対象のプリンシパル名が正しくありません。</para>
    </content>
  </section>
  <relatedTopics>
    <externalLink>
      <linkText>Troubleshooting Active Directory operations that fail with error 1753: There are no more endpoints available from the endpoint mapper.</linkText>
      <linkUri>https://support.microsoft.com/kb/2089874</linkUri>
    </externalLink>
<externalLink><linkText>KB article 839880 Troubleshooting RPC Endpoint Mapper errors using the Windows Server 2003 Support Tools from the product CD</linkText><linkUri>https://support.microsoft.com/kb/839880</linkUri></externalLink>
<externalLink><linkText>KB article 832017 Service overview and network port requirements for the Windows Server system</linkText><linkUri>https://support.microsoft.com/kb/832017/</linkUri></externalLink>
<externalLink><linkText>KB article 224196 Restricting Active Directory replication traffic and client RPC traffic to a specific port</linkText><linkUri>https://support.microsoft.com/kb/224196/</linkUri></externalLink>
<externalLink><linkText>KB article 154596 How to configure RPC dynamic port allocation to work with firewalls</linkText><linkUri>https://support.microsoft.com/kb/154596</linkUri></externalLink><externalLink><linkText>How RPC Works</linkText><linkUri>https://msdn.microsoft.com/library/aa373935(VS.85).aspx</linkUri></externalLink><externalLink><linkText>How the Server Prepares for a Connection</linkText><linkUri>https://msdn.microsoft.com/library/aa373938(VS.85).aspx</linkUri></externalLink>
<externalLink><linkText>How the Client Establishes a Connection</linkText><linkUri>https://msdn.microsoft.com/library/aa373937(VS.85).aspx</linkUri></externalLink><externalLink><linkText>Registering the Interface</linkText><linkUri>https://msdn.microsoft.com/library/aa375357(VS.85).aspx</linkUri></externalLink><externalLink><linkText>Making the Server Available on the Network</linkText><linkUri>https://msdn.microsoft.com/library/aa373974(VS.85).aspx</linkUri></externalLink><externalLink><linkText>Registering Endpoints</linkText><linkUri>https://msdn.microsoft.com/library/aa375255(VS.85).aspx</linkUri></externalLink><externalLink><linkText>Listening for Client Calls</linkText><linkUri>https://msdn.microsoft.com/library/aa373966(VS.85).aspx</linkUri></externalLink><externalLink><linkText>How the Client Establishes a Connection</linkText><linkUri>https://msdn.microsoft.com/library/aa373937(VS.85).aspx</linkUri></externalLink><externalLink><linkText>Restricting Active Directory replication traffic and client RPC traffic to a specific port</linkText><linkUri>https://support.microsoft.com/kb/224196</linkUri></externalLink><externalLink><linkText>SPN for a Target DC in AD DS</linkText><linkUri>https://msdn.microsoft.com/library/dd207688(PROT.13).aspx</linkUri></externalLink></relatedTopics>
</developerConceptualDocument>


