---
title: DNS に関連するライセンス認証の問題のトラブルシューティングに関するガイドライン
ms.topic: article
ms.date: 09/10/2019
ms.technology: server-general
author: Teresa-Motiv
ms.author: v-tea
ms.localizationpriority: medium
ms.openlocfilehash: 6cd94e997deaaf358c72793e6ff35d51a9ab3df6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80826186"
---
# <a name="guidelines-for-troubleshooting-dns-related-activation-issues"></a>DNS に関連するライセンス認証の問題のトラブルシューティングに関するガイドライン

次の条件の 1 つ以上に該当する場合は、これらの方法のいくつかを使用する必要があります。

- ボリューム ライセンス メディアと&nbsp;ボリューム ライセンス汎用プロダクトキーを使用して、次のいずれかのオペレーティング システムをインストールします。
   - Windows Server 2019
   - Windows Server 2016
   - Windows Server 2012 R2
   - Windows Server 2012
   - Windows Server 2008 R2
   - Windows Server 2008
   - Windows 10
   - Windows 8.1
   - Windows 8
- ライセンス認証ウィザードから KMS ホスト コンピューターに接続できません。

クライアント システムをライセンス認証しようとすると、ライセンス認証ウィザードでは、DNS を使用して KMS ソフトウェアを実行している対応するコンピューターが検索されます。 ウィザードで DNS が照会され、KMS ホスト コンピューターの DNS エントリが見つからない場合、ウィザードからはエラーが報告されます。   

<a id="list"></a>次の一覧を確認し、お客様の状況に合った方法を見つけてください。

- KMS ホストをインストールできない場合、または KMS ライセンス認証を使用できない場合は、「[プロダクト キーを MAK に変更する](#change-the-product-key-to-an-mak)」の手順を試してください。
- KMS ホストをインストールして構成する必要がある場合は、「[ライセンス認証するクライアントに合わせて KMS ホストを構成する](#configure-a-kms-host-for-the-clients-to-activate-against)」の手順を実行します。
- クライアントで既存の KMS ホストを見つけられない場合は、次の手順でルーティング構成のトラブルシューティングを行います。 これらの手順は、最も簡単なものから最も複雑なものの順に並べています。
  - [DNS サーバーへの基本的な IP 接続を確認する](#verify-basic-ip-connectivity-to-the-dns-server)
  - [KMS ホストの構成を確認する](#verify-the-configuration-of-the-kms-host)  
  - [ルーティングの問題の種類を特定する](#determine-the-type-of-routing-issue)
  - [DNS 構成を確認する](#verify-the-dns-configuration)
  - [KMS SRV レコードを手動で作成する](#manually-create-a-kms-srv-record)
  - [KMS クライアントに KMS ホストを手動で割り当てる](#manually-assign-a-kms-host-to-a-kms-client)
  - [複数の DNS ドメインに公開するように KMS ホストを構成する](#configure-the-kms-host-to-publish-in-multiple-dns-domains)

## <a name="change-the-product-key-to-an-mak"></a>プロダクト キーを MAK に変更する

KMS ホストをインストールできない場合、または何らかの理由で KMS ライセンス認証を使用できない場合は、プロダクト キーを MAK に変更します。 Windows イメージを Microsoft Developer Network (MSDN) または TechNet からダウンロードした場合、メディアの下に記載されている Stock Keeping Unit (SKU) は、一般にボリューム ライセンスが付与されたメディアであり、表示されているプロダクト キーは MAK キーです。

プロダクト キーを MAK に変更するには、次の手順を実行します。

1. 管理者特権のコマンド プロンプト ウィンドウを開きます。 これを行うには、Windows ロゴ キーを押しながら X キーを押し、 **[コマンド プロンプト]** を右クリックして、 **[管理者として実行]** を選択します。 管理者パスワードまたは確認入力を求められた場合は、パスワードを入力するか、確認入力を行います。
2. コマンド プロンプトで次のコマンドを実行します。
   ```cmd
    slmgr -ipk xxxxx-xxxxx-xxxxx-xxxxx-xxxxx
   ```
   > [!NOTE]
   > **xxxxx-xxxxx-xxxxx-xxxxx-xxxxx** のプレースホルダーは、MAK プロダクト キーを表します。  

[手順の一覧に戻ります。](#list)

## <a name="configure-a-kms-host-for-the-clients-to-activate-against"></a>ライセンス認証するクライアントに合わせて KMS ホストを構成する

KMS ライセンス認証を使用するには、ライセンス認証するクライアントに合わせて KMS ホストを構成する必要があります。 環境に KMS ホストが構成されていない場合は、KMS ホストをインストールし、適切な KMS ホスト キーを使用してライセンス認証します。 KMS ソフトウェアをホストするようにネットワーク上のコンピューターを構成した後、ドメイン ネーム システム (DNS) の設定を公開します。

KMS ホストの構成プロセスの詳細については、「[キー管理サービスによるライセンス認証](https://docs.microsoft.com/windows/deployment/volume-activation/activate-using-key-management-service-vamt)」と「[VAMT のインストールと構成](https://docs.microsoft.com/windows/deployment/volume-activation/install-configure-vamt)」を参照してください。

[手順の一覧に戻ります。](#list)

## <a name="verify-basic-ip-connectivity-to-the-dns-server"></a>DNS サーバーへの基本的な IP 接続を確認する

ping コマンドを使用して、DNS サーバーへの基本的な IP 接続を確認します。 これを行うには、エラーが発生している KMS クライアントと KMS ホスト コンピューターの両方で、次の手順を実行します。

1. 管理者特権のコマンド プロンプト ウィンドウを開きます。
1. コマンド プロンプトで次のコマンドを実行します。
   ```cmd
   ping <DNS_Server_IP_address>
   ```
   > [!NOTE]
   > このコマンドからの出力に "Reply from" という語句が含まれていない場合は、この記事の他の手順を実行する前に解決する必要があるネットワークの問題または DNS の問題があります。 DNS サーバーに対して ping が失敗した場合の TCP/IP の問題のトラブルシューティング方法については、「[TCP/IP の問題に関する高度なトラブルシューティング](https://docs.microsoft.com/windows/client-management/troubleshoot-tcpip)」を参照してください。

[手順の一覧に戻ります。](#list)

## <a name="verify-the-configuration-of-the-kms-host"></a>KMS ホストの構成を確認する

KMS ホスト サーバーのレジストリを調べて、DNS に登録されているかどうかを確認します。 既定で、KMS ホスト サーバーでは、24 時間に 1 回、DNS SRV レコードが動的に登録されます。 
> [!IMPORTANT]
> 慎重にこのセクションの手順に従います。 レジストリを正しく変更しないと、重大な問題が発生する可能性があります。 変更する前に、問題が発生した場合に[復元するためにレジストリをバックアップ](https://support.microsoft.com/help/322756)します。  

この設定を確認するには、次の手順を実行します。
1. レジストリ エディターを起動します。 これを行うには、 **[スタート]** を右クリックし、 **[ファイル名を指定して実行]** を選択して「**regedit**」と入力し、Enter キーを押します。
1. **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\SL** サブキーを見つけて、**DisableDnsPublishing** エントリの値を確認します。 このエントリには、次の有効な値があります。
   - **0** または未定義 (既定値):KMS ホストサーバーで 24 時間ごとに SRV レコードが登録されます。
   - **1**:KMS ホストサーバーでは、自動的に SRV レコードが登録されません。 動的更新がサポートされていない実装の場合は、「[KMS SRV レコードを手動で作成する](#manually-create-a-kms-srv-record)」を参照してください。  
1. **DisableDnsPublishing** エントリがない場合は作成します (型は DWORD です)。 動的登録を許容できる場合は、値を未定義のままにするか、**0** に設定します。

[手順の一覧に戻ります。](#list)

## <a name="determine-the-type-of-routing-issue"></a>ルーティングの問題の種類を特定する

次のコマンドを使用すると、名前解決の問題か SRV レコードの問題かを判断できます。  

1. KMS クライアントで、管理者特権でのコマンド プロンプト ウィンドウを開きます。  
1. コマンド プロンプトで次のコマンドを実行します。
   ```cmd
   cscript \windows\system32\slmgr.vbs -skms <KMS_FQDN>:<port>
   cscript \windows\system32\slmgr.vbs -ato
   ```
   > [!NOTE]
   > このコマンドで、<KMS_FQDN> は KMS ホスト コンピューターの完全修飾ドメイン名 (FQDN) を表し、\<port\> は KMS が使用する TCP ポートを表します。  

   これらのコマンドで問題が解決する場合、これは SRV レコードの問題です。 「[KMS クライアントに KMS ホストを手動で割り当てる](#manually-assign-a-kms-host-to-a-kms-client)」の手順に記載されているコマンドのいずれかを使用して解決できます。  

1. 問題が引き続き発生する場合は、次のコマンドを実行します。
   ```cmd
   cscript \windows\system32\slmgr.vbs -skms <IP Address>:<port>
   cscript \windows\system32\slmgr.vbs -ato
   ```
   > [!NOTE]
   > このコマンドで、\<IP Address\> は KMS ホスト コンピューターの IP アドレスを表し、\<port\> は KMS が使用する TCP ポートを表します。  

   これらのコマンドで問題が解決する場合、最も可能性の高いものは名前解決の問題です。 トラブルシューティングの詳細については、「[DNS 構成を確認する](#verify-the-dns-configuration)」の手順を参照してください。

1. これらのコマンドのいずれでも問題が解決しない場合は、コンピューターのファイアウォール構成を確認します。 KMS クライアントと KMS ホストの間で行われるライセンス認証の通信には 1688 TCP ポートが使用されます。 KMS クライアントと KMS ホストの両方のファイアウォールで、ポート 1688 での通信が許可されている必要があります。

[手順の一覧に戻ります。](#list)

## <a name="verify-the-dns-configuration"></a>DNS 構成を確認する

>[!NOTE]
> 特に明記されていない限り、該当するエラーが発生した KMS クライアントで次の手順を実行します。

1. 管理者特権でのコマンド プロンプト ウィンドウを開きます
1. コマンド プロンプトで次のコマンドを実行します。
   ```cmd
   IPCONFIG /all
   ```
1. コマンドの結果から、次の情報を確認します。
   - KMS クライアント コンピューターの割り当て済み IP アドレス
   - KMS クライアント コンピューターに使用されるプライマリ DNS サーバーの IP アドレス
   - KMS クライアント コンピューターに使用される既定のゲートウェイの IP アドレス
   - KMS クライアント コンピューターに使用される DNS サフィックス検索一覧
1. KMS ホスト SRV レコードが DNS に登録されていることを確認します。 これを行うには、次の手順に従います。  
   1. 管理者特権のコマンド プロンプト ウィンドウを開きます。
   1. コマンド プロンプトで次のコマンドを実行します。
      ```cmd
      nslookup -type=all _vlmcs._tcp>kms.txt
      ```
   1. コマンドで生成された KMS .txt ファイルを開きます。 このファイルには、次のエントリのようなエントリが 1 つ以上含まれています。
       ```
       _vlmcs._tcp.contoso.com SRV service location:
       priority = 0
       weight = 0
       port = 1688 svr hostname = kms-server.contoso.com
       ```
       > [!NOTE]
       > このエントリで、contoso.com は KMS ホストのドメインを表します。
      1. KMS ホストの IP アドレス、ホスト名、ポート、およびドメインを確認します。
      1. これらの **_vlmcs** エントリが存在し、必要な KMS ホスト名が含まれている場合は、「[KMS クライアントに KMS ホストを手動で割り当てる](#manually-assign-a-kms-host-to-a-kms-client)」に進みます。  
      > [!NOTE]
      > [**nslookup**](https://docs.microsoft.com/windows-server/administration/windows-commands/nslookup) コマンドで KMS ホストが検出されても、DNS クライアントで KMS ホストを検出できるとは限りません。 **nslookup** コマンドで KMS ホストが検出されても KMS ホストを使用してライセンス認証できない場合は、プライマリ DNS サフィックスや DNS サフィックスの検索一覧など、他の DNS 設定を確認します。
1. プライマリ DNS サフィックスの検索一覧に、KMS ホストに関連付けられた DNS ドメイン サフィックスが含まれていることを確認します。 検索一覧にこの情報が含まれていない場合は、「[複数の DNS ドメインに公開するように KMS ホストを構成する](#configure-the-kms-host-to-publish-in-multiple-dns-domains)」の手順に進みます。

[手順の一覧に戻ります。](#list)

## <a name="manually-create-a-kms-srv-record"></a>KMS SRV レコードを手動で作成する

Microsoft DNS サーバーを使用する KMS ホストの SRV レコードを手動で作成するには、次の手順を実行します。

1. DNS サーバーで、DNS マネージャを開きます。 DNS マネージャーを開くには、 **[スタート]** を選択し、 **[管理ツール]** を選択してから、 **[DNS]** を選択します。
1. SRV リソース レコードを作成する DNS サーバーを選択します。
1. コンソール ツリーで、 **[前方参照ゾーン]** を展開し、ドメインを右クリックして、 **[その他の新しいレコード]** を選択します。
1. 一覧を下にスクロールし、 **[サービス ロケーション (SRV)]** を選択して、 **[レコードの作成]** を選択します。
1. 次の情報を入力します。
   - サービス: **_VLMCS**
   - プロトコル: **_TCP**
   - ポート番号:**1688**
   - このサービスを提供しているホスト: **&lt;*KMS ホストの FQDN*&gt;**
1. 完了したら、 **[OK]** を選択し、 **[完了]** を選択します。

BIND 9.x 準拠の DNS サーバーを使用する KMS ホストの SRV レコードを手動で作成するには、その DNS サーバーの指示に従って、SRV レコードの次の情報を指定します。

- 名前:&nbsp; **_vlmcs._TCP**
- 種類:&nbsp;**SRV**
- 優先度:**0**
- 重み:**0**
- ポート:**1688**
- ホスト名: **&lt;*KMS ホストの FQDN または A 名*&gt;**

> [!NOTE]
> KMS では、 **[優先度]** または **[重み]** の値は使用されません。 ただし、レコードにはそれらが含まれている必要があります。

KMS の自動公開をサポートするように BIND 9.x 互換の DNS サーバーを構成するには、KMS ホストからのリソース レコードの更新を有効にするように DNS サーバーを構成します。 たとえば、Named.conf または Named.conf.local のゾーン定義に次の行を追加します。

```cmd
allow-update { any; };
```
## <a name="manually-assign-a-kms-host-to-a-kms-client"></a>KMS クライアントに KMS ホストを手動で割り当てる

既定では、KMS クライアントでは自動検出プロセスが使用されます。 このプロセスに従って、KMS クライアントでは、クライアントのメンバーシップ ゾーン内で _vlmcs SRV レコードを公開したサーバーの一覧が DNS に照会されます。 DNS からは、KMS ホストの一覧がランダムな順序で返されます。 クライアントで KMS ホストが選択され、そのホスト上でセッションの確立が試行されます。 この試行が成功すると、クライアントでは KMS ホストの名前がキャッシュされ、次回の更新の試行時にその使用が試行されます。 セッションのセットアップが失敗した場合、クライアントでは別の KMS ホストがランダムに選択されます。 自動検出プロセスを使用することを強くお勧めします。  

ただし、KMS ホストを特定の KMS クライアントに手動で割り当てることができます。 これを行うには、次の手順に従います。

1. KMS クライアントで、管理者特権でのコマンド プロンプト ウィンドウを開きます。
1. 実装に応じて、次のいずれかの手順を実行します。
   - ホストの FQDN を使用して KMS ホストを割り当てるには、次のコマンドを実行します。
     ```cmd
     cscript \windows\system32\slmgr.vbs -skms <KMS_FQDN>:<port>
     ```
   - ホストのバージョン 4 IP アドレスを使用して KMS ホストを割り当てるには、次のコマンドを実行します。
     ```cmd
     cscript \windows\system32\slmgr.vbs -skms <IPv4Address>:<port>
     ```
    - ホストのバージョン 6 IP アドレスを使用して KMS ホストを割り当てるには、次のコマンドを実行します。
      ```cmd
      cscript \windows\system32\slmgr.vbs -skms <IPv6Address>:<port>
      ```
    - ホストの NETBIOS 名を使用して KMS ホストを割り当てるには、次のコマンドを実行します。
      ```cmd
      cscript \windows\system32\slmgr.vbs -skms <NETBIOSName>:<port>
      ```
   - KMS クライアントで自動検出に戻すには、次のコマンドを実行します。
     ```cmd
     cscript \windows\system32\slmgr.vbs -ckms
     ```
     > [!NOTE]
     > これらのコマンドには、次のプレースホルダーが使用されています。
     >- **<KMS_FQDN>** は、KMS ホスト コンピューターの完全修飾ドメイン名 (FQDN) を表します
     >- **\<IPv4Address\>** は、KMS ホスト コンピューターの IP バージョン 4 アドレスを表します
     >- **\<IPv6Address\>** は、KMS ホスト コンピューターの IP バージョン 6 アドレスを表します
     >- **\<NETBIOSName\>** は、KMS ホスト コンピューターの NETBIOS 名を表します
     >- **\<port\>** は、KMS が使用する TCP ポートを表します。  

## <a name="configure-the-kms-host-to-publish-in-multiple-dns-domains"></a>複数の DNS ドメインに公開するように KMS ホストを構成する

> [!IMPORTANT]
> 慎重にこのセクションの手順に従います。 レジストリを正しく変更しないと、重大な問題が発生する可能性があります。 変更する前に、問題が発生した場合に[復元するためにレジストリをバックアップ](https://support.microsoft.com/help/322756)します。

「[KMS クライアントに KMS ホストを手動で割り当てる](#manually-assign-a-kms-host-to-a-kms-client)」で説明されているように、通常、KMS クライアントでは自動検出プロセスを使用して KMS ホストが識別されます。 このプロセスを実行するには、KMS クライアントコンピューターの DNS ゾーン内の _vlmcs SRV レコードを使用できる必要があります。 DNS ゾーンは、コンピューターのプライマリ DNS サフィックス、または次のいずれかに対応します。
- ドメインに参加しているコンピューターの場合、DNS システム (Active Directory Domain Services (AD DS) DNS など) によって割り当てられたコンピューターのドメイン。
- ワークグループ コンピューターの場合、コンピューターのドメインは動的ホスト構成プロトコル (DHCP) によって割り当てられます。 このドメイン名は、Request for Comments (RFC) 2132 で定義されているように、コード値が 15 のオプションによって定義されています。

既定で、KMS ホストでは、KMS ホスト コンピューターのドメインに対応する DNS ゾーンに SRV レコードが登録されます。 たとえば、KMS ホストが contoso.com ドメインに参加しているとします。 このシナリオでは、KMS ホストでは、contoso.com DNS ゾーン以下に _vmlcs SRV レコードが登録されます。 そのため、レコードでは、サービスが VLMCS._TCP.CONTOSO.COM と識別します。

KMS ホストと KMS クライアントが異なる DNS ゾーンを使用している場合、複数の DNS ドメインで SRV レコードを自動的に公開するように KMS ホストを構成する必要があります。 これを行うには、次の手順に従います。

1. KMS ホスト上でレジストリ エディターを起動します。 
1. **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\SL** サブキーを見つけて選択します。
1. **[詳細]** ウィンドウで空白の領域を右クリックし、 **[新規作成]** をクリックして、 **[複数行文字列値]** を選択します。
1. 新しいエントリの名前として、「**DnsDomainPublishList**」と入力します。
1. 新しい **DnsDomainPublishList** エントリを右クリックし、 **[変更]** を選択します。
1. **[複数行文字列の編集]** ダイアログ ボックスで、KMS から公開される各 DNS ドメイン サフィックスを別の行に入力し、 **[OK]** を選択します。
   > [!NOTE]
   > Windows Server 2008 R2 では、**DnsDomainPublishList** の形式が異なります。 詳細については、ボリューム ライセンス認証のテクニカル リファレンス ガイドを参照してください。
1. [サービス] 管理ツールを使用して Software Licensing サービスを再起動します。 この操作で SRV レコードが作成されます。
1. 一般的な方法を使用して、KMS クライアントから、構成した KMS ホストに接続できることを確認します。 KMS クライアントで、名前と IP アドレスの両方で KMS ホストが正しく識別されることを確認します。 これらのいずれかの確認に失敗する場合は、この DNS クライアント リゾルバーの問題を調べます。
1. KMS クライアント上で以前にキャッシュされた KMS ホスト名をクリアするには、KMS クライアントで管理者特権でのコマンド プロンプト ウィンドウを開き、次のコマンドを実行します。
   ```cmd
   cscript C:\Windows\System32\slmgr.vbs -ckms
   ```
