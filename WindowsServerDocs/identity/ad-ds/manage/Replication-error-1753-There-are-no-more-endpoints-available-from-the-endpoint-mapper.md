---
ms.assetid: 0f21951c-b1bf-43bb-a329-bbb40c58c876
title: レプリケーション エラー 1753。エンドポイント マッパーから使用できるエンドポイントはこれ以上ありません
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: e429c87a2194ecfaf02c3d6c579eda75293250d4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827513"
---
# <a name="replication-error-1753-there-are-no-more-endpoints-available-from-the-endpoint-mapper"></a>レプリケーション エラー 1753。エンドポイント マッパーから使用できるエンドポイントはこれ以上ありません

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012


<developerConceptualDocument xmlns="https://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="https://www.w3.org/1999/xlink" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="https://ddue.schemas.microsoft.com/authoring/2003/5 http://clixdevr3.blob.core.windows.net/ddueschema/developer.xsd"> <introduction>
    <para>このトピックでは、現象、原因、および Active Directory レプリケーション エラー 8524 DSA 操作は DNS 参照エラーのため続行できませんを解決する方法について説明します。</para>
    <list class="bullet">
      <listItem>
        <para>
          <link xlink:href="f7022f0d-0099-410c-8178-c654e624bc42#BKMK_Symptoms">現象</link>
        </para>
      </listItem> <listItem>
        <para>
          <link xlink:href="f7022f0d-0099-410c-8178-c654e624bc42#BKMK_Cause">原因</link>
        </para>
      </listItem> <listItem>
        <para>
          <link xlink:href="f7022f0d-0099-410c-8178-c654e624bc42#BKMK_Resolutions">解決策</link>
        </para>
      </listItem> <listItem>
        <para>
          <link xlink:href="f7022f0d-0099-410c-8178-c654e624bc42#BKMK_MoreInfo">詳細については</link>
        </para>
      </listItem>
    </list>
  </introduction>
  <section address="BKMK_Symptoms">
    <title>現象</title>
    <content>
      <para>この記事は、現象、原因を説明し、解像度が 1753 の Win32 エラーで失敗する Active Directory 操作の手順します。「があるエンドポイントのエンドポイント マッパーから使用できる。」</para>
      <list class="ordered">
        <listItem>
          <para>接続のテスト、Active Directory レプリケーションのテストまたは KnowsOfRoleHolders テストが失敗しました。 エラー 1753 DCDIAG レポート:「があるエンドポイントのエンドポイント マッパーから使用できる。」</para>
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
<listItem><para>REPADMIN します。EXE では、そのレプリケーションの試行が失敗しました状態 1753 をレポートします。</para><para>REPADMIN のコマンドをよくが示されている 1753 のステータスが含まれますが、これらに限定されません。</para><table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11"><tbody><tr><TD><list class="bullet"><listItem><para>REPADMIN/REPLSUM</para></listItem><listItem><para>REPADMIN/SHOWREPL</para></listItem></list></TD><TD><list class="bullet"><listItem><para>REPADMIN/SHOWREPS</para></listItem><listItem><para>REPADMIN/SYNCALL</para></listItem></list></TD></tr></tbody></table><para>"REPADMIN/SHOWREPS"が「レプリケーション アクセスが拒否されました」エラーで失敗を CONTOSO DC1 に contoso-dc2 から入力方向のレプリケーションを表すからの出力例は、以下に示します。</para><code>Default-First-Site-NameCONTOSO-DC1
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

</code></listItem><listItem><para><ui>レプリケーション トポロジの確認</ui>Active Directory サイトとサービスでのコマンドは、「があるエンドポイントのエンドポイント マッパーから使用できる」を返します。</para><para>ソース DC からの接続オブジェクトを右クリックし、選択<ui>レプリケーション トポロジの確認</ui>「があるエンドポイントのエンドポイント マッパーから使用できる」で失敗する。 画面に表示されるエラー メッセージが次に示します。</para><para>ダイアログ タイトルのテキスト:レプリケーション トポロジを確認します。</para><para>ダイアログ メッセージ テキスト: </para><para>ドメイン コント ローラーに接続するときに、次のエラーが発生しました。エンドポイントはエンドポイント マッパーから使用できます。</para></listItem><listItem><para><ui>今すぐレプリケート</ui>Active Directory サイトとサービスでのコマンドは、「があるエンドポイントのエンドポイント マッパーから使用できる」を返します。</para><para>ソース DC からの接続オブジェクトを右クリックし、選択<ui>今すぐレプリケート</ui>「があるエンドポイントのエンドポイント マッパーから使用できる」で失敗する。 画面に表示されるエラー メッセージが次に示します。</para><para>ダイアログ タイトルのテキスト:今すぐレプリケートします。</para><para>ダイアログ メッセージ テキスト:名前付けコンテキストの同期中に、次のエラーが発生した&lt;% ディレクトリ パーティション名 %&gt;ドメイン コント ローラーから&lt;ソース DC&gt;ドメイン コント ローラーに&lt;宛先 DC&gt;:</para><para>

エンドポイントはエンドポイント マッパーから使用できます。</para><para>操作は続行されません。</para></listItem><listItem><para>-2146893022 ステータスの NTDS KCC、NTDS 一般または Microsoft-Windows-ActiveDirectory_DomainService イベントは、イベント ビューアーで、ディレクトリ サービス ログに記録されます。</para><para>よく-2146893022 状態が示されている active Directory のイベントが含まれますが、これらに限定されません。</para><table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11"><thead><tr><TD><para>イベント ID</para></TD><TD><para>イベント ソース</para></TD><TD><para>イベントの文字列</para></TD></tr></thead><tbody><tr><TD><para>1655</para></TD><TD><para>NTDS 全般</para></TD><TD><para>Active Directory は、次のグローバル カタログと通信しようとして、試行が成功しなかった場合。</para></TD></tr><tr><TD><para>1925</para></TD><TD><para>NTDS KCC</para></TD><TD><para>次の書き込み可能なディレクトリ パーティションのレプリケーション リンクを確立できませんでした。</para></TD></tr><tr><TD><para>1265</para></TD><TD><para>NTDS KCC</para></TD><TD><para>知識整合性チェッカー (KCC) によって、次のディレクトリ パーティションとソース ドメイン コントローラのレプリケーション合意の追加に失敗しました。</para></TD></tr></tbody></table></listItem>
</list>
    </content>
  </section>
  <section address="BKMK_Cause">
    <title>原因</title>
    <content>
      <para>次の図は、手順 7. で、クライアント アプリケーションに、RPC クライアントからのデータの受け渡しを手順 1. で RPC エンドポイント マッパー (EPM) とサーバー アプリケーションの登録で開始 RPC ワークフローを示しています。 </para>
      <para>&lt;ADDS_RPCWorkflow&gt;</para>
      <para>手順 1 ~ 7 のマップを次の操作:</para>
      <list class="ordered">
        <listItem>
          <para>RPC エンドポイント マッパー (EPM) とそのエンドポイントを登録するサーバー アプリ </para>
        </listItem>
        <listItem>
          <para>クライアントが、RPC 呼び出しを行う (、ユーザーに代わって OS またはアプリケーションが開始した操作) </para>
        </listItem>
        <listItem>
          <para>クライアント側 RPC がターゲット コンピューター EPM と、クライアント呼び出しを完了するエンドポイントを要求 </para>
        </listItem>
        <listItem>
          <para>エンドポイントを持つサーバー マシンの EPM 応答 </para>
        </listItem>
        <listItem>
          <para>クライアント側 RPC サーバー アプリを接続します。 </para>
        </listItem>
        <listItem>
          <para>サーバー アプリの呼び出しの実行、RPC クライアントに結果を返します </para>
        </listItem>
        <listItem>
          <para>クライアント側 RPC は、クライアント アプリに結果を渡します</para>
        </listItem>
      </list>
      <para>エラー 1753 年は、手順 3 と 4 の間での障害によって生成されます。 具体的には、エラー 1753 年は、RPC クライアント (レプリケート先 DC) がポート 135 で RPC サーバー (ソース DC) にお問い合わせくださいできましたが、RPC サーバー (ソース DC) で EPM 関心のある RPC アプリケーションを見つけることができませんでしたとサーバー側でエラー 1753 年が返されることを意味します。 1753 エラーの存在は、RPC クライアント (レプリケート先 DC) が、ネットワーク経由での RPC サーバー (AD レプリケーション ソース DC) からサーバー側のエラー応答を受信したことを示します。 </para>
      <para>1753 エラーの特定の根本原因は次のとおりです。 </para>
      <list class="ordered">
        <listItem>
          <para>サーバー アプリを起動していない (つまり「詳細」の図の上にある手順 1 がまったく試行されなかった)。</para>
        </listItem>
        <listItem>
          <para>サーバー アプリの開始が、RPC エンドポイント マッパー (つまり手順 1 で上記の「詳細」図が試行されたが失敗しました) を登録できないの初期化中に何らかの障害が発生しました。</para>
        </listItem>
        <listItem>
          <para>サーバー アプリが開始されましたが、亡くなった後。 (つまり手順 1 上の「詳細」図でが正常に完了したが取り消された後で、サーバーが亡くなったため。)</para>
        </listItem>
        <listItem>
          <para>サーバー アプリは、(意図的なものが 3 に似ていますそのエンドポイントを手動で登録解除。 とんでもないことがには含まれて完全を期すのため)。</para>
        </listItem>
        <listItem>
          <para>(レプリケート先 DC) の RPC クライアントは接続名を DNS、WINS、またはホスト/Lmhosts ファイルで IP の割り当てエラーのためのものよりも、別の RPC サーバーです。</para>
        </listItem>
      </list>
      <para>エラー 1753 の原因ではありません。 </para>
      <list class="bullet">
        <listItem>
          <para>ポート 135 で RPC クライアント (レプリケート先 DC) および RPC サーバー (ソース DC) 間のネットワーク接続がないです。</para>
        </listItem>
        <listItem>
          <para>RPC サーバー (ソース DC) 間のネットワーク接続が不足しているエフェメラル ポート経由でポート 135 と RPC クライアント (レプリケート先 DC) を使用します。 </para>
        </listItem>
        <listItem>
          <para>パスワードの不一致またはソース DC で Kerberos の暗号化されたパケットの暗号化を解除することができません。 </para>
        </listItem>
      </list>
      <para> </para>
    </content>
  </section>
  <section address="BKMK_Resolutions">
    <title>解決策</title>
    <content>
      <list class="ordered">
        <listItem>
          <para>
            <embeddedLabel>エンドポイント マッパーにそのサービスを登録するサービスが開始されたことを確認します。</embeddedLabel>
          </para>
          <para>Windows 2000 と Windows Server 2003 Dc: ソース DC を通常モードになっていることを確認します。 </para>
          <para>
Windows Server 2008 または Windows Server 2008 R2: ソース DC のコンソールで、サービス スナップイン (services.msc) を起動し、いることを確認、 <embeddedLabel>Active Directory Domain Services</embeddedLabel>サービスが実行されています。 </para>
        </listItem>
        <listItem>
          <para>
            <embeddedLabel>目的の RPC サーバー (ソース DC) に接続されている RPC クライアント (レプリケート先 DC) を確認します。</embeddedLabel>
          </para>
          <para>一般的な Active Directory フォレスト内のすべての Dc では、_msdcs でドメイン コント ローラーの CNAME レコードを登録します。&lt;フォレスト ルート ドメイン&gt;フォレスト内にあるどのドメインに関係なく、DNS ゾーンです。 派生した DC の CNAME レコードは、 <embeddedLabel>objectGUID</embeddedLabel>各ドメイン コント ローラーの NTDS 設定オブジェクトの属性です。 </para>
          <para>レプリケーション ベースの操作を実行するときに、レプリケート先 DC は、ソース Dc の CNAME レコードに DNS を照会します。 CNAME レコードには、ソース Dc の IP アドレスを派生するために使用するソース DC の完全修飾コンピューター名が含まれています。 DNS クライアントのキャッシュ参照を使用してホスト/LMHost ファイルを参照して、ホスト A/AAAA は、DNS または WINS に記録します。 </para>
          <para>NTDS 設定オブジェクトを古いし、DNS、WINS、ホストおよび LMHOST ファイル内の不適切な名前対 IP マッピングが原因で、不適切な RPC サーバー (ソース DC) に接続するには、RPC クライアント (レプリケート先 DC)。 さらに、不適切な名前対 IP マッピングと、インストールされている目的 (この場合 Active Directory のロール) の RPC クライアント (レプリケート先 DC)、RPC サーバー アプリケーションをもしていないコンピューターに接続する場合があります。 (例: DC2 用の古いホスト レコードが DC3 またはのメンバー コンピューターの IP アドレスが含まれています)。 </para>
          <para>Active Directory の Dc のコピー先に存在するソース DC の objectGUID がソースの Active Directory のドメイン コント ローラーのコピーに格納されているソース DC の objectGUID と一致することを確認します。 不一致がある場合、ntds 設定オブジェクトの repadmin/showobjmeta を使用して、ソース ドメイン コント ローラーの昇格の最後に対応するいずれかを確認する (ヒント: NTDS 設定オブジェクトの作成の昇格の最後の日付に対して/showobjmeta から日の日付のタイムスタンプを比較しますソース Dc dcpromo.log ファイルです。 最後の変更を使用して、/、DCPROMO の日付を作成する必要があります。ログ ファイル自体) です。 オブジェクトの Guid が同一でない場合、レプリケート先 DC の可能性が高いの CNAME レコードが IP のマッピングに無効な名前のホスト レコードを指しますソース DC の古い NTDS 設定オブジェクトがあります。 </para>
          <para>レプリケート先 DC の実行する DNS サーバーを決定する IPCONFIG/ALL DC が名前解決を使用して移行先。</para>
          <code>c:&gt;ipconfig /all</code>
          <para>レプリケート先 DC のソース Dc の完全修飾 DC の CNAME レコードに対する NSLOOKUP を実行します。</para>
          <code>c:&gt;nslookup -type=cname &lt;fully qualified cname of source DC&gt; &lt;destination DCs primary DNS Server IP &gt;
c:&gt;nslookup -type=cname &lt;fully qualified cname of source DC&gt; &lt;destination DCs secondary DNS Server IP&gt;</code>
          <para>NSLOOKUP によって返される IP アドレスがホスト名を「所有」していることを確認/ソース DC のセキュリティ id。</para>

          <code>C:&gt;NBTSTAT -A &lt;IP address returned by NSLOOKUP in the step above&gt;</code>
          <para>または</para>
          <para>ソース DC のコンソールにログインし、コマンド プロンプトから"IPCONFIG"を実行し、ソース DC が上記の NSLOOKUP コマンドによって返される IP アドレスを所有していることを確認します</para>
          <para>古い/重複するホストで DNS の IP のマッピングを確認してください。</para>
          <code>NSLOOKUP -type=hostname &lt;single label hostname of source DC&gt; &lt;primary DNS Server IP on destination DC&gt;
NSLOOKUP -type=hostname &lt;single label hostname of source DC&gt; &lt;secondary DNS Server IP on destination DC&gt;

NSLOOKUP -type=hostname &lt;fully qualified computer name of source DC&gt; &lt;primary DNS Server IP on destination DC&gt;
NSLOOKUP -type=hostname &lt;fully qualified computer name of source DC&gt; &lt;secondary DNS Server IP on dest. DC&gt;</code>
<para>無効な IP アドレスは、ホスト レコードに存在する場合は、DNS の清掃を有効にして正しく構成されているかどうかを調査します。 </para><para>上のテストまたはネットワークのトレースが無効な IP アドレスを返す名前クエリを表示されない場合は、ホスト ファイル、LMHOSTS ファイルおよび WINS サーバーに古いエントリを検討してください。 DNS サーバーが WINS フォールバック名前解決を実行して構成することも注意してください。</para>
</listItem>
        <listItem>
          <para>
            <embeddedLabel>RPC サーバー (ソース DC) 上のエンドポイント マッパー (Active Directory などで) サーバー アプリケーションが登録されていることを確認します。</embeddedLabel>
          </para>
          <para>Active Directory では、よく知られていると、動的に登録されているポートの組み合わせを使用します。 このテーブルには、よく知られているポートと Active Directory ドメイン コント ローラーによって使用されるプロトコルが一覧表示します。</para>
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
                  <para>x</para>
                </TD>
                <TD>
                  <para>x</para>
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
                  <para>x</para>
                </TD>
                <TD>
                  <para>x</para>
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
                  <para>x</para>
                </TD>
                <TD>
                  <para>x</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>Microsoft-DS</para>
                </TD>
                <TD>
                  <para>445</para>
                </TD>
                <TD>
                  <para>x</para>
                </TD>
                <TD>
                  <para>x</para>
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
                  <para>x</para>
                </TD>
                <TD>
                  <para>x</para>
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
                  <para>x</para>
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
                  <para>x</para>
                </TD>
                <TD>
                  <para />
                </TD>
              </tr>
            </tbody>
          </table>
          <para>既知のポートは、エンドポイント マッパーに登録されていません。 </para>
          <para>Active Directory と他のアプリケーションも、RPC のエフェメラル ポートの範囲で動的に割り当てられたポートを受信するサービスを登録します。 1024 ~ 5000 Windows 2000 および Windows Server 2003 コンピューター上での TCP ポートとポート 49152 と 65535 の範囲を Windows Server 2008 および Windows Server 2008 R2 コンピューターの間で、このような RPC サーバー アプリケーションが動的に割り当てられます。 RPC ポート レプリケーションで使用されるには、ハード コーディングされたに記載の手順を使用して、レジストリで<externalLink><linkText>サポート技術情報記事 224196</linkText><linkUri>https://support.microsoft.com/kb/224196</linkUri></externalLink>します。 Active Directory は、ハード コーディングされたポートを使用する、EPM 構成されている場合に登録し続けます。 </para>
          <para>関心のある RPC サーバー アプリケーションが RPC サーバー (ソース DC の AD レプリケーションの場合)、RPC エンドポイント マッパーで自身に登録を確認します。 </para>
          <para>このタスクを実行する方法がいくつかがインストールして、管理特権のコマンド プロンプトからのソース DC の構文を使用してコンソールに PORTQRY を実行する 1 つです。 </para>
          <code>c:\&gt;portquery -n &lt;source DC&gt; -e 135 &gt;file.txt</code>
          <para>Portqry の出力では、「MS NT ディレクトリ DRS インターフェイス」を動的に登録されているポート番号に注意してください。 (UUID =... 351) の、 <embeddedLabel>ncacn_ip_tcp プロトコル</embeddedLabel>します。 次のスニペットは、Windows Server 2008 R2 の DC と UUID から portquery 出力の例を示していますで具体的には Active Directory で使用されるプロトコルのペアが強調表示/<embeddedLabel>太字</embeddedLabel>: </para>
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
          <para>このエラーを解決するその他の考えられる方法:</para>
          <list class="ordered">
            <listItem>
              <para>ソース DC が通常モードで起動されると、ソース DC で OS と DC ロールを完全に開始したことを確認します。</para>
            </listItem>
            <listItem>
              <para>Active Directory ドメイン サービスが実行されていることを確認します。 サービスは、現在停止しているか、既定のスタートアップの値で構成されていません場合、は、既定のスタートアップの値にリセットし、変更されたドメイン コント ローラーを再起動操作を再試行します。</para>
            </listItem>
            <listItem>
              <para>RPC サービスと RPC ロケーターのスタートアップの値とサービスの状態が、RPC クライアント (レプリケート先 DC) および RPC サーバー (ソース DC) の OS バージョンに対して正しいことを確認します。 サービスは、現在停止しているか、既定のスタートアップの値で構成されていません場合、は、既定のスタートアップの値にリセットし、変更されたドメイン コント ローラーを再起動操作を再試行します。</para>
              <para>さらに、サービス コンテキストが、次の表に示す既定の設定と一致することを確認します。</para>
              <table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11">
                <thead>
                  <tr>
                    <TD>
                      <para>サービス</para>
                    </TD>
                    <TD>
                      <para>Windows Server 2003 およびそれ以降、既定の状態 (スタートアップの種類) </para>
                    </TD>
                    <TD>
                      <para>Windows Server 2000 では、既定の状態 (スタートアップの種類)</para>
                    </TD>
                  </tr>
                </thead>
                <tbody>
                  <tr>
                    <TD>
                      <para>リモート プロシージャ コール</para>
                    </TD>
                    <TD>
                      <para>開始 (自動)</para>
                    </TD>
                    <TD>
                      <para>開始 (自動)</para>
                    </TD>
                  </tr>
                  <tr>
                    <TD>
                      <para>リモート プロシージャ コールのロケーター</para>
                    </TD>
                    <TD>
                      <para>Null または停止 (手動)</para>
                    </TD>
                    <TD>
                      <para>開始 (自動)</para>
                    </TD>
                  </tr>
                </tbody>
              </table>
            </listItem>
            <listItem>
              <para>動的ポートの範囲のサイズが制限されていないことを確認します。 RPC ポートの範囲を列挙するために Windows Server 2008 および Windows Server 2008 R2 の NETSH 構文は、以下に示します。</para>
              <code>&gt;netsh int ipv4 show dynamicport tcp
&gt;netsh int ipv4 show dynamicport udp
&gt;netsh int ipv6 show dynamicport tcp
&gt;netsh int ipv6 show dynamicport udp</code>
            </listItem>
            <listItem>
              <para>ソース Dc OS バージョンの KB 224196 で定義されているハード コーディングされたポートの定義が動的ポートの範囲内にあることを確認します。</para>
              <para>レビュー <externalLink><linkText>サポート技術情報記事 224196</linkText> <linkUri> https://support.microsoft.com/kb/224196 </linkUri> </externalLink>をハード コーディングされたポートがソース DC のオペレーティング システムのバージョンの一時的なポート範囲に収まることを確認してください。</para>
            </listItem>
            <listItem>
              <para>ClientProtocols キーが HKLM\Software\Microsoft\Rpc 下が存在し、次の 5 つの既定値を含むことを確認します。</para>
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
        <embeddedLabel>マッピング-2146893022 と RPC エラー 1753 原因となる IP に不適切な名前の例: 対象のプリンシパル名が正しくありません</embeddedLabel>
      </para>
      <para>DC1 と DC2 の IP アドレス x.x.1.1 と x.x.1.2 contoso.com ドメインで構成されます。 ホストの"A"]、[DC1 用に構成された DNS サーバーのすべてに DC2 用の"AAAA"レコードが正しく登録されています。 さらに、DC1 上の HOSTS ファイルには、IP アドレス x.x.1.2 DC2s の完全修飾ホスト名にマップのエントリが含まれています。 後で、DC2 の IP アドレスの変更 X.X.1.2 から X.X.1.3、新しいメンバーのコンピューターには、IP アドレス x.x.1.2 を使用してドメインに参加しています。 AD レプリケーションの試行がによってトリガーされる、<ui>今すぐレプリケート</ui>トレースを次に示すように、エラー 1753 で Active Directory サイトとサービス スナップインでのコマンドが失敗しました。</para>
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
      <para>フレームで<embeddedLabel>10</embeddedLabel>、レプリケート先 DC は、Active Directory のレプリケーションのサービス クラスの UUID E351 ポート 135 を介してソース Dc のエンドポイント マッパーを照会しています. </para>
      <para>フレームで<embeddedLabel>11</embeddedLabel>、このソース DC では、まだ DC ロールをホストしないと、そのため、E351 登録いないメンバー コンピューターの場合.レプリケーション サービスの UUID をそのローカル EPM では、「は」エンドポイントのエンドポイント マッパーから使用できるシンボリック エラー エラー 1753 年の 10 進数、16 進数のエラー 0x6d9 およびフレンドリ エラーにマップする EP_S_NOT_REGISTERED で応答します。</para>
      <para>後で、IP アドレス x.x.1.2 でメンバー コンピューターは、レプリカ、contoso.com ドメイン内には、"MayberryDC"として昇格を取得します。 もう一度、<ui>今すぐレプリケート</ui>コマンドを使用して、レプリケーション トリガーしますが、この時間に失敗します、画面に表示されるエラー「ターゲットのプリンシパル名が正しくありません」。 コンピューターがネットワーク アダプターの ip アドレスが割り当てられているアドレス x.x.1.2<placeholder>は</placeholder>ドメイン コント ローラーが通常モードで起動した現在および、E351 が登録しています.レプリケーション サービスがそのローカル EPM で UUID が DC2 の名またはセキュリティ id を所有していないと、要求ようになりましたエラーで失敗する「ターゲットのプリンシパル名が正しくありません」ためには、DC1 から Kerberos 要求を復号化できません。 エラーに 10 進数のエラー-2146893022 マップ/エラー 0x80090322 を 16 進数します。 </para>
      <para>このような無効なホストと IP マッピングがホストに古いエントリが考えられます lmhost ファイルでは、ホスト A//、DNS または WINS に AAAA 登録します。 </para>
      <para>概要:(このケースでホスト ファイル) に無効なホストと IP マッピングには、そのため、レプリケーションの「ソース」サービスは実行中 (またはさらに言えばもインストールされている) Active Directory Domain Services に含まれていない DC を解決するのにはレプリケート先 DC が発生したため、この例が失敗しましたSPN がまだ登録されていないと、ソース DC が 1753 のエラーを返しました。 2 番目のケースでは、(ホスト ファイル) にもう一度無効なホストと IP マッピングが原因で、移行先ドメイン コント ローラー、E351 が登録されている DC に接続する.レプリケーション SPN が、そのソースは、エラー-2146893022 で、試行が失敗したため、別のホスト名とセキュリティ id を目的のソース DC にありました。対象のプリンシパル名が正しくありません。</para>
    </content>
  </section>
  <relatedTopics>
    <externalLink>
      <linkText>1753 年のエラーで失敗する Active Directory 操作のトラブルシューティング。エンドポイントはエンドポイント マッパーから使用できます。</linkText> 
      <linkUri> https://support.microsoft.com/kb/2089874 </linkUri> 
    </externalLink> 
<externalLink> <linkText>KB 記事の製品CDからWindowsServer2003サポートツールを使用してトラブルシューティングするRPCエンドポイントマッパーエラーの839880</linkText> <linkUri> https://support.microsoft.com/kb/839880 </linkUri> </externalLink> 
<externalLink> <linkText>832017 サービス概要およびネットワーク ポートの要件の Windows サーバー システムの記事 KB</linkText> <linkUri>https://support.microsoft.com/kb/832017/ </linkUri> </externalLink> 
<externalLink> <linkText>KB 記事 224196 の制限の Active Directory レプリケーションのトラフィックとクライアントの RPC トラフィック特定のポートに</linkText><linkUri> https://support.microsoft.com/kb/224196/ </linkUri> </externalLink> 
<externalLink><linkText>サポート技術情報記事 154596 ファイアウォールで動作する RPC 動的ポート割り当てを構成する方法</linkText><linkUri> https://support.microsoft.com/kb/154596 </linkUri> </externalLink> <externalLink> <linkText>RPC のしくみ</linkText><linkUri>https://msdn.microsoft.com/library/aa373935(VS.85).aspx</linkUri></externalLink><externalLink><linkText>接続のサーバーの準備</linkText><linkUri> https://msdn.microsoft.com/library/aa373938(VS.85).aspx </linkUri> </externalLink> 
<externalLink><linkText>クライアントによる接続の確立</linkText><linkUri> https://msdn.microsoft.com/library/aa373937(VS.85).aspx </linkUri> </externalLink><externalLink> <linkText>、インターフェイスを登録する</linkText><linkUri>https://msdn.microsoft.com/library/aa375357(VS.85).aspx</linkUri></externalLink><externalLink><linkText>サーバーネットワーク上で利用</linkText><linkUri>https://msdn.microsoft.com/library/aa373974(VS.85).aspx</linkUri></externalLink><externalLink><linkText>エンドポイントを登録する</linkText><linkUri>https://msdn.microsoft.com/library/aa375255(VS.85).aspx </linkUri> </externalLink> <externalLink><linkText>クライアント呼び出しのリッスン</linkText><linkUri> https://msdn.microsoft.com/library/aa373966(VS.85).aspx </linkUri> </externalLink><externalLink><linkText>クライアントによる接続の確立</linkText><linkUri>https://msdn.microsoft.com/library/aa373937(VS.85).aspx</linkUri></externalLink><externalLink><linkText>を制限します。Active Directory のレプリケーション トラフィックとクライアント RPC トラフィック特定のポートを</linkText><linkUri>https://support.microsoft.com/kb/224196</linkUri></externalLink><externalLink><linkText>でターゲット DC の SPNAD DS</linkText><linkUri>https://msdn.microsoft.com/library/dd207688(PROT.13).aspx</linkUri></externalLink></relatedTopics>
</developerConceptualDocument>


