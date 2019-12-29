---
title: CAPolicy.inf ファイルを準備する
description: Capolicy.inf には、Active Directory 証明書サービス (AD CS) をインストールするとき、または CA 証明書を更新するときに使用されるさまざまな設定が含まれています。
manager: alanth
ms.topic: article
ms.assetid: 65b36794-bb09-4c1b-a2e7-8fc780893d97
ms.prod: windows-server
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 2af3a621991627addb94238e84cceb357fb47731
ms.sourcegitcommit: b7f55949f166554614f581c9ddcef5a82fa00625
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/18/2019
ms.locfileid: "72588085"
---
# <a name="capolicyinf-syntax"></a>Capolicy.inf 構文
>   適用対象: Windows Server (半期チャネル)、Windows Server 2016

Capolicy.inf は、ルート CA 証明書およびルート CA によって発行されたすべての証明書に適用される拡張機能、制約、およびその他の構成設定を定義する構成ファイルです。 ルート CA のセットアップルーチンを開始する前に、Capolicy.inf ファイルをホストサーバーにインストールする必要があります。 ルート CA のセキュリティ制限を変更する場合は、ルート証明書を更新する必要があり、更新プロセスを開始する前に、更新された Capolicy.inf ファイルをサーバーにインストールする必要があります。

Capolicy.inf は次のとおりです。

-   管理者によって手動で作成および定義された

-   ルートと下位の CA 証明書の作成中に使用されます

-   署名 CA で定義され、証明書 (要求が付与されている CA ではなく) に署名して発行します。

Capolicy.inf ファイルを作成したら、ADCS をインストールする前に、または CA 証明書を更新する前に、サーバーの **% systemroot%** フォルダーにコピーする必要があります。

Capolicy.inf を使用すると、さまざまな CA 属性とオプションを指定して構成することができます。 次のセクションでは、特定のニーズに合わせて .inf ファイルを作成するためのすべてのオプションについて説明します。

## <a name="capolicyinf-file-structure"></a>Capolicy.inf ファイル構造

.Inf ファイルの構造を記述するには、次の用語を使用します。

-   _Section_ –は、キーの論理グループを対象とするファイルの領域です。 .Inf ファイル内のセクション名は、角かっこで囲まれて表示されます。 すべてではなく、多くのセクションが証明書の拡張機能を構成するために使用されます。

-   _キー_ –エントリの名前であり、等号の左側に表示されます。

-   _Value_ –パラメーターであり、等号の右側に表示されます。

次の例では、 **[Version]** がセクション、 **Signature**がキー、 **"\$Windows NT \$"** が値です。

以下に例を示します。

```PowerShell
[Version]                     #section
Signature="$Windows NT$"      #key=value
```

###  <a name="version"></a>バージョン

ファイルを .inf ファイルとして識別します。 バージョンは唯一の必須セクションであり、Capolicy.inf ファイルの先頭にある必要があります。

###  <a name="policystatementextension"></a>PolicyStatementExtension

組織によって定義されているポリシーと、そのポリシーが省略可能か必須かを示します。 複数のポリシーは、コンマで区切られます。 これらの名前は、特定の展開のコンテキストで意味があります。または、これらのポリシーの存在を確認するカスタムアプリケーションに関連しています。

定義されたポリシーごとに、その特定のポリシーの設定を定義するセクションが必要です。 ポリシーごとに、ユーザー定義オブジェクト識別子 (OID) と、ポリシーステートメントとして表示するテキストか、ポリシーステートメントへの URL ポインターを指定する必要があります。 URL は、HTTP、FTP、または LDAP URL の形式にすることができます。

ポリシーステートメントに説明用のテキストを使用する場合、Capolicy.inf の次の3行は次のようになります。

```
[InternalPolicy]
OID=1.1.1.1.1.1.1
Notice=”Legal policy statement text”
```

CA ポリシーステートメントをホストする URL を使用する場合、次の3行は次のようになります。

```
[InternalPolicy]
OID=1.1.1.1.1.1.2
URL=https://pki.wingtiptoys.com/policies/legalpolicy.asp
```

さらに:

-   複数の URL と注意事項のキーがサポートされています。

-   同じポリシーセクションの注意と URL キーがサポートされています。

-   スペースを含む Url、またはスペースを含むテキストは、引用符で囲む必要があります。 これは、表示されているセクションに関係なく、 **URL**キーに当てはまります。

ポリシーセクション内の複数の通知と Url の例は次のようになります。

```
[InternalPolicy]
OID=1.1.1.1.1.1.1
URL=https://pki.wingtiptoys.com/policies/legalpolicy.asp
URL=ftp://ftp.wingtiptoys.com/pki/policies/legalpolicy.asp
Notice=”Legal policy statement text”
```

### <a name="crldistributionpoint"></a>CRLDistributionPoint

Capolicy.inf で、ルート CA 証明書の CRL 配布ポイント (Cdp) を指定できます。  CA をインストールした後、発行された各証明書に CA に含まれる CDP Url を構成できます。 ルート CA 証明書は、Capolicy.inf ファイルのこのセクションで指定されている Url を示しています。 

```
[CRLDistributionPoint]
URL=http://pki.wingtiptoys.com/cdp/WingtipToysRootCA.crl
```

このセクションに関する追加情報を次に示します。
-   対応
    - HTTP 
    - ファイルの Url
    - LDAP Url 
    - 複数の Url
   
    >[!IMPORTANT]
    >では、HTTPS Url はサポートされていません。

-   引用符は、Url をスペースで囲む必要があります。

-   Url が指定されていない場合 (つまり、 **[CRLDistributionPoint]** セクションがファイルに存在していても空の場合)、CRL 配布ポイントの拡張機能はルート CA 証明書から除外されます。 これは通常、ルート CA を設定するときに推奨されます。 Windows はルート CA 証明書に対して失効確認を実行しないため、CDP 拡張機能はルート CA 証明書では不要です。

-    CA は、たとえば、クライアントが HTTP 経由で取得した web サイトのフォルダーを表す共有に、ファイル UNC に発行できます。

-   ルート CA を設定する場合、またはルート CA 証明書を更新する場合にのみ、このセクションを使用します。 CA は、下位 CA CDP 拡張機能を決定します。
   

### <a name="authorityinformationaccess"></a>AuthorityInformationAccess

ルート CA 証明書の場合は、Capolicy.inf で機関情報アクセスポイントを指定できます。

```
[AuthorityInformationAccess]
URL=http://pki.wingtiptoys.com/Public/myCA.crt
```

機関情報アクセスセクションの追加の注意事項:

-   複数の Url がサポートされています。

-   HTTP、FTP、LDAP、およびファイルの Url がサポートされています。 HTTPS Url はサポートされていません。

-   このセクションは、ルート CA を設定する場合、またはルート CA 証明書を更新する場合にのみ使用されます。 下位 CA の AIA 拡張機能は、下位 CA の証明書を発行した CA によって決定されます。

-   スペースを含む Url は引用符で囲む必要があります。

-   Url が指定されていない場合 (つまり、 **[AuthorityInformationAccess]** セクションがファイルに存在していても空の場合)、証明機関情報アクセス拡張機能はルート CA 証明書から除外されます。 ここでも、ルート CA 証明書の場合は、証明書へのリンクによって参照される必要があるルート CA より上位の権限がないため、この設定が推奨されます。

### <a name="certsrv_server"></a>certsrv_Server

Capolicy.inf のもう1つのオプションセクションは [certsrv_server] で、更新またはインストールされる CA の更新キーの長さ、更新の有効期間、および証明書失効リスト (CRL) の有効期間を指定するために使用されます。 このセクションのキーは必要ありません。 これらの設定の多くには、ほとんどのニーズに十分な既定値があり、Capolicy.inf ファイルから単純に省略できます。 また、これらの設定の多くは、CA のインストール後に変更することもできます。

例は次のようになります。

```
[certsrv_server]
RenewalKeyLength=2048
RenewalValidityPeriod=Years
RenewalValidityPeriodUnits=5
CRLPeriod=Days
CRLPeriodUnits=2
CRLDeltaPeriod=Hours
CRLDeltaPeriodUnits=4
ClockSkewMinutes=20
LoadDefaultTemplates=True
AlternateSignatureAlgorithm=0
ForceUTF8=0
EnableKeyCounting=0
```

**RenewalKeyLength**は、更新に対してのみキーサイズを設定します。 これは、CA 証明書の更新時に新しいキーペアが生成された場合にのみ使用されます。 最初の CA 証明書のキーサイズは、CA がインストールされるときに設定されます。

新しいキーのペアで CA 証明書を更新するときに、キーの長さを増減することができます。 たとえば、ルート CA キーのサイズを4096バイト以上に設定している場合、2048バイトのキーサイズのみをサポートする Java アプリまたはネットワークデバイスがあることを検出します。 サイズを増減するかどうかにかかわらず、その CA によって発行されたすべての証明書を再発行する必要があります。

**RenewalValidityPeriod**と**RenewalValidityPeriodUnits**は、古いルート ca 証明書を更新するときに、新しいルート ca 証明書の有効期間を確立します。 ルート CA にのみ適用されます。 下位 CA の証明書の有効期間は、その上位の証明書の有効期間によって決まります。 RenewalValidityPeriod には、時間、日、週、月、年の値を指定できます。

**CRLPeriod**と**CRLPeriodUnits**は、base CRL の有効期間を確立します。 **CRLPeriod**には、時間、日、週、月、年の値を指定できます。

**CRLDeltaPeriod**と**CRLDeltaPeriodUnits**は、delta CRL の有効期間を確立します。 **CRLDeltaPeriod**には、時間、日、週、月、年の値を指定できます。

これらの各設定は、CA がインストールされた後で構成できます。

```
Certutil -setreg CACRLPeriod Weeks
Certutil -setreg CACRLPeriodUnits 1
Certutil -setreg CACRLDeltaPeriod Days
Certutil -setreg CACRLDeltaPeriodUnits 1
```

変更を有効にするには、必ず Active Directory 証明書サービスを再起動してください。

**Loaddefaulttemplates**は、エンタープライズ CA のインストール中にのみ適用されます。 この設定 (True または False (または1または 0)) は、CA が既定のテンプレートを使用して構成されているかどうかを示します。

CA の既定のインストールでは、既定の証明書テンプレートのサブセットが、証明機関スナップインの [証明書テンプレート] フォルダーに追加されます。 これは、役割がインストールされた後、AD CS サービスが開始されるとすぐに、十分なアクセス許可を持つユーザーまたはコンピューターが証明書をすぐに登録できることを意味します。

CA がインストールされた直後に証明書を発行することはできません。そのため、LoadDefaultTemplates 設定を使用して、既定のテンプレートがエンタープライズ CA に追加されないようにすることができます。 CA にテンプレートが構成されていない場合、証明書を発行することはできません。

**AlternateSignatureAlgorithm**は、ca 証明書と証明書要求の両方に対して、PKCS \#1 v1.0 の署名形式をサポートするように ca を構成します。 ルート CA で1に設定すると、CA 証明書には PKCS \#1 v1.0 の署名形式が含められます。 下位 ca で設定されている場合、下位 CA は PKCS \#1 v1.0 の署名形式を含む証明書要求を作成します。

**ForceUTF8**は、件名と発行者の識別名の相対識別名 (RDNs) の既定のエンコードを utf-8 に変更します。 RFC によってディレクトリ文字列型として定義されているものなど、UTF-8 をサポートする RDNs のみが影響を受けます。 たとえば、ドメインコンポーネント (DC) の RDN は、IA5 または UTF-8 としてエンコーディングをサポートしていますが、Country RDN (C) では、エンコード可能な文字列としてエンコードのみがサポートされています。 したがって、ForceUTF8 ディレクティブは DC RDN に影響を与えますが、C RDN には影響しません。

**Enablekeycounting**は、ca の署名キーが使用されるたびに、カウンターをインクリメントするように ca を構成します。 ハードウェアセキュリティモジュール (HSM) と関連する暗号化サービスプロバイダー (CSP) がキーカウントをサポートしていない場合は、この設定を有効にしないでください。 Microsoft の強力な CSP と Microsoft ソフトウェアキー格納プロバイダー (KSP) では、キーカウントはサポートされていません。

## <a name="create-the-capolicyinf-file"></a>Capolicy.inf ファイルを作成する

AD CS をインストールする前に、固有の設定で、展開の CAPolicy.inf ファイルを構成します。

**前提条件:** Administrators グループのメンバーである必要があります。

1. AD CS のインストールを計画しているコンピューターで、Windows PowerShell を開き、「 **notepad c:\** 」と入力して、enter キーを押します。

2. 新しいファイルを作成するかどうかを確認するメッセージが表示されたら、 **[はい]** をクリックします。

3. ファイルに次の内容を入力します。
   ```
   [Version]  
   Signature="$Windows NT$"  
   [PolicyStatementExtension]  
   Policies=InternalPolicy  
   [InternalPolicy]  
   OID=1.2.3.4.1455.67.89.5  
   Notice="Legal Policy Statement"  
   URL=https://pki.corp.contoso.com/pki/cps.txt  
   [Certsrv_Server]  
   RenewalKeyLength=2048  
   RenewalValidityPeriod=Years  
   RenewalValidityPeriodUnits=5  
   CRLPeriod=weeks  
   CRLPeriodUnits=1  
   LoadDefaultTemplates=0  
   AlternateSignatureAlgorithm=1  
   [CRLDistributionPoint]  
   [AuthorityInformationAccess]
   ```
4. **[ファイル]** をクリックし、名前を付け **[て保存]** をクリックします。

5. % Systemroot% フォルダーに移動します。

6. 次の内容を確認します。

   -   **[ファイル名]** が **CAPolicy.inf** に設定されている。

   -   **[ファイルの種類]** が **[すべてのファイル]** に設定されている。

   -   **[文字コード]** が **[ANSI]** に設定されている。

7. **[保存]** をクリックします。

8. ファイルを上書きするかどうかをたずねるメッセージが表示されたら、 **[はい]** をクリックします。

   ![Capolicy.inf ファイルの場所として保存します。](../../../media/Prepare-the-CAPolicy-inf-File/001-SaveCAPolicyORCA1.gif)

   > [!CAUTION]
   >   拡張子 inf を付けて CAPolicy.inf を保存してください。 ファイル名の末尾に **.inf** を指定しないで上記のオプションを選択した場合、ファイルはテキスト ファイルとして保存され、CA のインストール時に使用されなくなります。

9. メモ帳を閉じます。

> [!IMPORTANT]
>   Capolicy.inf で、 https://pki.corp.contoso.com/pki/cps.txt URL を指定する行があることを確認できます。 この CAPolicy.inf の InternalPolicy セクションは、認証実施規定 (CPS) の場所を指定する方法の例として示されています。 このガイドでは、証明書作成ステートメント (CPS) を作成するように指示されていません。
