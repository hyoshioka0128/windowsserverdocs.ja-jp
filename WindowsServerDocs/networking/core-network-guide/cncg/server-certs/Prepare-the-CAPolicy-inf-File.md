---
title: CAPolicy.inf ファイルを準備します。
description: CAPolicy.inf には、Active Directory 証明書サービス (AD CS) をインストールする場合、または CA を更新するときに使用されるさまざまな設定が含まれています。証明書。
manager: alanth
ms.topic: article
ms.assetid: 65b36794-bb09-4c1b-a2e7-8fc780893d97
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 9618d4abe512b487f4f22ffde85a052c1c52ef22
ms.sourcegitcommit: fb4e2ace2e0a29e0f6b028f1cb945cab6aa6ee2c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/05/2018
---
# <a name="capolicyinf-syntax"></a>CAPolicy.inf の構文
>   適用対象: Windows Server (半期チャネル)、Windows Server 2016

CAPolicy.inf では、拡張機能、制約、およびその他のルート CA 証明書とルート CA によって発行されたすべての証明書に適用される構成設定を定義する構成ファイル。 CAPolicy.inf ファイルは、セットアップ ルーチンのルート CA を開始する前に、ホスト サーバーにインストールする必要があります。 ルート CA のセキュリティの制限を変更できますが、ルート証明書を更新する必要があり、更新された CAPolicy.inf ファイルは更新プロセスを開始する前に、サーバーにインストールする必要があります。

CAPolicy.inf に示します。

-   作成され、管理者が手動で定義されています。

-   ルートと下位 CA 証明書を作成する際に使用率

-   サインインして (いない、要求が与えられている CA) 証明書の発行の署名の CA で定義されています。

コピーする必要があります、CAPolicy.inf ファイルを作成した後、**%systemroot%** ad CS をインストールまたは CA 証明書を更新する前に、サーバーのフォルダーです。

CAPolicy.inf を指定し、さまざまな CA 属性とオプションを構成できます。 次のセクションでは、特定のニーズに合わせて調整 .inf ファイルを作成するためのすべてのオプションについて説明します。

## <a name="capolicyinf-file-structure"></a>CAPolicy.inf ファイルの構造

.Inf ファイル構造を記述する次の用語が使用されます。

-   _セクション_– キーの論理グループをカバーするファイルの領域です。 セクション名の .inf ファイルでは、角かっこで表示されるによって識別されます。 すべてではなく、多くのセクションでは、証明書の拡張機能の構成に使用されます。

-   _キー_ – エントリの名前し、等号 (=) の左側に表示されます。

-   _値_– パラメーターし、等号 (=) の右側に表示されます。

、次の例で**[バージョン]** ] セクションでは、**署名**、キーと**"\ $ Windows NT \ $"**値です。

例:

```PowerShell
[Version]                     #section
Signature="$Windows NT$"      #key=value
```

###  <a name="version"></a>バージョン

.Inf ファイルとして、ファイルを識別します。 バージョンは、唯一要求セクション、CAPolicy.inf ファイルの先頭にある必要があります。

###  <a name="policystatementextension"></a>PolicyStatementExtension

組織によって定義されているポリシーの一覧はオプションか必須かどうか。 複数のポリシーは、コンマで区切られます。 名前は、これらのポリシーの有無をチェックするカスタム アプリケーションとの関連または特定の展開のコンテキストで意味を持ちます。

各ポリシーを定義すると、その特定のポリシーの設定を定義するセクション必要があります。 各ポリシーについて、ユーザー定義のオブジェクト識別子 (OID) を提供する必要があり、テキストとして表示するポリシー ステートメントまたはポリシー ステートメントへの URL のポインター。 URL は、HTTP、FTP、または LDAP URL の形式であることができます。

ポリシー ステートメントにわかりやすいテキストがある場合は、し、次の 3 行 CAPolicy.inf のようになります。

```
[InternalPolicy]
OID=1.1.1.1.1.1.1
Notice=”Legal policy statement text”
```

CA のポリシー ステートメントをホストする URL を使用しようとする場合、次の 3 行代わりにようになります。

```
[InternalPolicy]
OID=1.1.1.1.1.1.2
URL=http://pki.wingtiptoys.com/policies/legalpolicy.asp
```

さらに：

-   複数の URL とキーがサポートされます。

-   同じポリシー] セクションで、通知と URL のキーがサポートされます。

-   Url をスペースまたはスペースを含むテキストは、引用符で囲む必要があります。 場合は true。これは、**URL**キー、それが表示されるセクションに関係なく。

複数の通知とポリシー] セクションで Url の例のようになります。

```
[InternalPolicy]
OID=1.1.1.1.1.1.1
URL=http://pki.wingtiptoys.com/policies/legalpolicy.asp
URL=ftp://ftp.wingtiptoys.com/pki/policies/legalpolicy.asp
Notice=”Legal policy statement text”
```

### <a name="crldistributionpoint"></a>CRLDistributionPoint

CAPolicy.inf でのルート CA 証明書の CRL 配布ポイント (Cdp) を指定できます。 CA をインストールした後は、発行された各証明書の CA を含む CDP Url を構成できます。 ルート CA 証明書自体では、CAPolicy.inf ファイルのこのセクションで指定されている Url が含まれています。

```
[CRLDistributionPoint]
URL=http://pki.wingtiptoys.com/cdp/WingtipToysRootCA.crl
```

このセクションでに関する追加情報:

-   複数の Url がサポートされます。

-   HTTP、FTP、および LDAP Url がサポートされます。 HTTPS Url を指定することはできません。

-   このセクションではルート CA を設定するか、ルート CA 証明書を更新する場合にのみ使用します。 下位の CA の CDP 拡張機能は、下位 CA の証明書を発行する CA によって決定されます。

-   スペースを含む Url は、引用符で囲む必要があります。

-   Url を指定しない場合: は場合、**[CRLDistributionPoint]** – セクションで、ファイルが存在するが、空、ルート CA 証明書の CRL 配布ポイントの拡張子を省略するとします。 これは、ルート CA をセットアップするときに通常が望ましい方法です。 Windows では、失効 CDP 拡張機能は、ルート CA 証明書で不要なため、ルート CA 証明書のチェックは実行されません。

### <a name="authorityinformationaccess"></a>AuthorityInformationAccess

CAPolicy.inf のルート CA 証明書の機関情報アクセス ポイントを指定できます。

```
[AuthorityInformationAccess]
URL=http://pki.wingtiptoys.com/Public/myCA.crt
```

機関情報アクセス] セクションでいくつか追加の注記:

-   複数の Url がサポートされます。

-   HTTP、FTP、LDAP、およびファイルの Url がサポートされます。 HTTPS Url を指定することはできません。

-   このセクションではルート CA を設定またはルート CA 証明書を更新する場合にのみ使用します。 下位の CA の AIA 拡張機能は、下位 CA の証明書を発行した CA によって決定されます。

-   スペースを含む Url は、引用符で囲む必要があります。

-   Url を指定しない場合: は場合、**[AuthorityInformationAccess]** – セクションで、ファイルが存在するが、空、ルート CA 証明書の CRL 配布ポイントの拡張子を省略するとします。 もう一度、ルート CA の証明書へのリンクが参照する必要がありますをよりも高い権限がないため、ルート CA 証明書の場合、優先設定になります。

### <a name="certsrvserver"></a>certsrv_Server

CAPolicy.inf の別の省略可能なセクションは、certsrv_server される CA のキーの長さを更新、更新の有効期間、および証明書失効リスト (CRL) の有効期間を指定するために使用されます。更新されたりインストールします。 このセクションでキーが必要です。 これらの設定の多くがある既定値はほとんどのニーズに十分に対応し、単に CAPolicy.inf ファイルから省略できます。 また、CA をインストールした後、このこれらの設定の多くを変更できます。

例のようになります。

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

**RenewalKeyLength**のみの更新のキーのサイズを設定します。 これは、CA 証明書の更新中に新しいキーのペアが生成されたときにのみ使用されます。 最初の CA 証明書のキーのサイズは、CA のインストール時に設定されます。

新しいキーのペアで CA 証明書を更新するには、キーの長さでするか増加または減少ことができます。 たとえば、ルート CA キーのサイズの 4,096 バイト以上に設定したことを検出する場合がある Java アプリやキーのサイズを 2048 バイトのみをサポートするネットワーク デバイス。 増加するか、または、サイズを小さくするかどうかは、その CA によって発行されたすべての証明書を再発行する必要があります。

**RenewalValidityPeriod**と**RenewalValidityPeriodUnits**古いルート CA 証明書を更新するときに、新しいルート CA 証明書の有効期間を確立します。 ルート CA にのみ適用されます。 下位 CA の証明書の有効期間は、上位によって決定されます。 RenewalValidityPeriod は、次の値を持つことができます。時間、日、週、月、および年間です。

**CRLPeriod**と**CRLPeriodUnits** base CRL の有効期間を確立します。 **CRLPeriod**、次の値を持つことができます。時間、日、週、月、および年間です。

**CRLDeltaPeriod**と**CRLDeltaPeriodUnits** delta CRL の有効期間を確立します。 **CRLDeltaPeriod**、次の値を持つことができます。時間、日、週、月、および年間です。

CA をインストールした後、これらの設定を構成できます。

```
Certutil -setreg CACRLPeriod Weeks
Certutil -setreg CACRLPeriodUnits 1
Certutil -setreg CACRLDeltaPeriod Days
Certutil -setreg CACRLDeltaPeriodUnits 1
```

有効にするすべての変更を Active Directory 証明書サービスを再起動してください。

**LoadDefaultTemplates**エンタープライズ CA のインストール中にのみ適用されます。 この設定は、いずれかの True または False (または 1 または 0)、既定のテンプレートのいずれかに設定されている CA を決定します。

CA の既定のインストールで、既定の証明書テンプレートのサブセットは証明機関スナップインで証明書テンプレート フォルダーに追加されます。 これはこと、役割がインストールされた後に、AD CS サービスが開始するとすぐに、ユーザーまたはコンピューターのための十分なアクセス許可ですぐに登録に使用できる証明書を意味します。

いない LoadDefaultTemplates 設定を既定のテンプレートがエンタープライズ CA に追加されることを防ぐために使用できるように、すぐに、CA のインストール後に、すべての証明書を発行することがあります。 CA 上で構成されているテンプレートがない場合し、そのことができますない証明書を発行します。

**AlternateSignatureAlgorithm** CA 証明書と証明書の要求の両方の PKCS\ #1 V2.1 署名の形式をサポートするために CA を構成します。 CA の CA 証明書のルートで 1 に設定すると、PKCS\ #1 V2.1 署名の形式が含まれます。 設定すると、下位の CA、下位 CA は作成証明書の要求を PKCS\ #1 V2.1 署名の形式が含まれています。

**ForceUTF8**、既定値を変更識別名を utf-8 が相対識別名 (Rdn) でサブジェクトと発行者のエンコードします。 のみこれら Rdn、RFC によってディレクトリ文字列型が影響を受けるように定義されているような utf-8 をサポートします。 たとえば、RDN ドメイン コンポーネント (DC) の Country RDN (C) のみがサポートを印刷可能な文字列としてエンコード中に IA5 または utf-8 でエンコードをサポートします。 ForceUTF8 ディレクティブは、DC RDN はそのために影響が C RDN には影響しません。

**EnableKeyCounting**カウンターを増分します CA の署名キーを使用するたびに、CA を構成します。 ハードウェア セキュリティ モジュール (HSM) およびキーのカウントをサポートする、関連付けられている暗号化サービス プロバイダー (CSP) がない限り、この設定を有効にしないでください。 Microsoft Strong CSP も、Microsoft ソフトウェア キー格納プロバイダー (KSP) サポート キーをカウントします。


## <a name="create-the-capolicyinf-file"></a>CAPolicy.inf ファイルを作成します。

AD CS をインストールする前に、特定の設定、展開の CAPolicy.inf ファイルを構成します。

**前提条件:** Administrators グループのメンバーがあります。

1.  AD CS では、Windows PowerShell を開き、インストールを計画しているコンピューターで次のように入力します。**メモ帳 c:.inf**し、Enter キーを押します。

2.  新しいファイルを作成するのにメッセージが表示されたら、] をクリックして**はい**します。

3.  ファイルの内容に応じて、次を入力します。
   ```
   [Version]  
    Signature="$Windows NT$"  
    [PolicyStatementExtension]  
    Policies=InternalPolicy  
    [InternalPolicy]  
    OID=1.2.3.4.1455.67.89.5  
    Notice="Legal Policy Statement"  
    URL=http://pki.corp.contoso.com/pki/cps.txt  
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
1.  をクリックして**ファイル**、] をクリックし、**名前を付けて保存**します。

2.  %Systemroot% フォルダーに移動します。

3.  次のことを確認します。

    -   **ファイル名**に設定されている**CAPolicy.inf**

    -   **ファイルの種類**に設定されている**すべてのファイル**

    -   **エンコード**は**ANSI**

4.  をクリックして**保存**します。

5.  ファイルを上書きするメッセージが表示されたら、] をクリックして**はい**します。

    ![CAPolicy.inf ファイルの名前を付けて保存場所](../../../media/Prepare-the-CAPolicy-inf-File/001-SaveCAPolicyORCA1.gif)

    >   [!CAUTION]  
    >   必ず、inf 拡張子を付けて CAPolicy.inf を保存してください。 具体的には入力しないでください場合**.inf**上記のオプションを選択とファイルの名前の末尾には、ファイルをテキスト ファイルとして保存されますおよび CA のインストール中には使用されません。

6.  メモ帳を閉じます。

>   [!IMPORTANT]  
>   CAPolicy.inf で確認できます URL を指定する行があるhttp://pki.corp.contoso.com/pki/cps.txtします。 CAPolicy.inf の内部ポリシー] セクションが認証実施規定 (CPS) の場所を指定する方法の例として示されています。 このガイドで指示された場合しない証明書の実施規定 (CPS) を作成します。
