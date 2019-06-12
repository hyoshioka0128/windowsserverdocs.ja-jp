---
title: CAPolicy.inf ファイルを準備する
description: CAPolicy.inf には、Active Directory 証明書サービス (AD CS) をインストールする場合、または CA の証明書を更新するときに使用されるさまざまな設定が含まれています。
manager: alanth
ms.topic: article
ms.assetid: 65b36794-bb09-4c1b-a2e7-8fc780893d97
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 19a87df7c4f165d3b0e6c5add4bc40ff97cc87cb
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446461"
---
# <a name="capolicyinf-syntax"></a>CAPolicy.inf の構文
>   適用先:Windows Server 2016 の Windows Server (半期チャネル)

CAPolicy.inf では、拡張機能、制約、および他のルート CA 証明書とルート CA によって発行されたすべての証明書に適用される構成設定を定義する構成ファイルを示します。 CAPolicy.inf ファイルは、セットアップ ルーチンのルート CA を開始する前に、ホスト サーバーにインストールする必要があります。 ルート CA に対するセキュリティ制限を変更すると、ルート証明書を更新する必要があり、更新された CAPolicy.inf ファイルは、更新手続きを開始する前に、サーバーにインストールする必要があります。

CAPolicy.inf に示します。

-   作成され、管理者によって手動で定義されています。

-   ルートと下位の CA 証明書の作成時に使用率

-   署名 CA 署名および (いない要求が与えられている CA) 証明書を発行場所で定義されています。

コピーする必要があります、CAPolicy.inf ファイルを作成すると、 **%systemroot%** ADCS をインストールまたは CA の証明書を更新する前に、サーバーのフォルダー。

CAPolicy.inf を使うとを指定し、さまざまな CA 属性とオプションを構成できます。 次のセクションでは、特定のニーズに合わせて、.inf ファイルを作成するためのすべてのオプションについて説明します。

## <a name="capolicyinf-file-structure"></a>CAPolicy.inf ファイルの構造

次の用語は、.inf ファイルの構造の記述に使用されます。

-   _セクション_– キーの論理グループをカバーするファイルの領域です。 .Inf ファイルでセクション名は、角かっこで表示されるによって識別されます。 すべてではなく、多くのセクションでは、証明書の拡張機能の構成に使用されます。

-   _キー_ – エントリの名前を指定し、等号 (=) の左側に表示されます。

-   _値_– は、パラメーターであり、等号の右側に表示されます。

次の例で **[バージョン]** セクション**署名**、キーと **"\$Windows NT\$"** 値です。

以下に例を示します。

```PowerShell
[Version]                     #section
Signature="$Windows NT$"      #key=value
```

###  <a name="version"></a>バージョン

.Inf ファイルとしてファイルを識別します。 バージョンは、唯一要求セクションは、CAPolicy.inf ファイルの先頭にある必要があります。

###  <a name="policystatementextension"></a>PolicyStatementExtension

組織で定義されているポリシーの一覧は省略可能または必須かどうか。 複数のポリシーは、コンマで区切られます。 名前は、コンテキストの特定の展開、またはこれらのポリシーの有無を確認するカスタム アプリケーションとの関連で意味を持ちます。

各ポリシーを定義すると、セクションの特定のポリシー設定を定義する必要があります。 各ポリシーについて、ユーザー定義のオブジェクト識別子 (OID) を提供する必要があると、テキストとして表示するポリシー ステートメントまたはポリシー ステートメントへの URL ポインター。 URL は、HTTP、FTP、LDAP URL の形式で指定できます。

ポリシー ステートメントにわかりやすいテキストがある場合は、CAPolicy.inf の次の 3 つの行はのようになります。

```
[InternalPolicy]
OID=1.1.1.1.1.1.1
Notice=”Legal policy statement text”
```

URL を使用して、CA のポリシー ステートメントをホストする場合は、し、次の 3 行は代わりにようになります。

```
[InternalPolicy]
OID=1.1.1.1.1.1.2
URL=https://pki.wingtiptoys.com/policies/legalpolicy.asp
```

さらに:

-   複数の URL とキーがサポートされています。

-   同じポリシー セクションで、通知、および URL のキーがサポートされています。

-   スペースを含む Url またはスペースを含むテキストを引用符で囲む必要があります。 場合は true。 これは、 **URL**キーが表示されるセクションに関係なく、します。

複数の通知とポリシー セクションで Url の例は、ようになります。

```
[InternalPolicy]
OID=1.1.1.1.1.1.1
URL=https://pki.wingtiptoys.com/policies/legalpolicy.asp
URL=ftp://ftp.wingtiptoys.com/pki/policies/legalpolicy.asp
Notice=”Legal policy statement text”
```

### <a name="crldistributionpoint"></a>CRLDistributionPoint

Capolicy.inf のルート CA 証明書の CRL 配布ポイント (Cdp) を指定できます。  CA をインストールした後は、発行された各証明書に CA を含む CDP Url を構成することができます。 ルート CA 証明書は、CAPolicy.inf ファイルのこのセクションで指定された Url を示します。 

```
[CRLDistributionPoint]
URL=http://pki.wingtiptoys.com/cdp/WingtipToysRootCA.crl
```

このセクションに関する追加情報:
-   サポートされています。
    - HTTP 
    - ファイルの Url
    - LDAP Url 
    - 複数の Url
   
    >[!IMPORTANT]
    >HTTPS の Url はサポートされません。

-   引用符は、スペースを含む Url を囲む必要があります。

-   Url を指定しない場合: これは場合、 **[CRLDistributionPoint]** – セクションがファイルに存在しますが、空、機関情報アクセス拡張機能はルート CA 証明書から省略されます。 これは、ルート CA をセットアップするときに、通常は適しています。 Windows では、失効 CDP 拡張機能はルート CA 証明書で余分なので、ルート CA の証明書の確認は実行されません。

-    CA は、web サイトが HTTP 経由でクライアントを取得する場所のフォルダーを表す共有などのファイルの UNC を発行できます。

-   このセクションを設定するルート CA またはルート CA 証明書を更新する場合にのみ使用します。 CA は、下位の CA の CDP 拡張機能を決定します。
   

### <a name="authorityinformationaccess"></a>AuthorityInformationAccess

ルート CA 証明書の CAPolicy.inf では、機関情報アクセス ポイントを指定できます。

```
[AuthorityInformationAccess]
URL=http://pki.wingtiptoys.com/Public/myCA.crt
```

追加の機関情報アクセス セクションの注意事項:

-   複数の Url がサポートされています。

-   HTTP、FTP、LDAP およびファイルの Url がサポートされています。 HTTPS Url がサポートされていません。

-   このセクションでは、ルート CA を設定するルート CA 証明書を更新する場合にのみ使用されます。 下位の CA の AIA 拡張機能は、下位 CA の証明書を発行した CA によって決定されます。

-   スペースを含む Url は、引用符で囲む必要があります。

-   Url を指定しない場合: これは場合、 **[AuthorityInformationAccess]** – セクションがファイルに存在しますが、空では、ルート CA 証明書の CRL 配布ポイント拡張機能を省略するとします。 ここでも、これになりますルート CA 証明書の場合、優先設定ルート CA の証明書へのリンクを参照する必要がありますをより高い権限がありません。

### <a name="certsrvserver"></a>certsrv_Server

CAPolicy.inf のもう 1 つの省略可能なセクションが certsrv_server を使用して、キーの長さを更新、更新の有効期間、および証明書失効リスト (CRL) の有効期間を指定されている CA のインストールまたは更新します。 このセクションではキーが必要です。 これらの設定の多くは、CAPolicy.inf ファイルから単に省略できますが、ほとんどのニーズのための十分なを既定値を指定します。 または、CA がインストールされた後、この設定の多くを変更できます。

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

**RenewalKeyLength**更新のみのキーのサイズを設定します。 これは、CA 証明書の更新中に新しいキー ペアが生成された場合にのみ使用されます。 最初の CA 証明書のキーのサイズは、CA がインストールされているときに設定されます。

新しいキーのペアで CA 証明書を更新する場合に、キーの長さは、いずれかの増加または減少します。 たとえば、ルート CA キーのサイズは 4096 バイト以上のバージョンに設定し、を検出する場合がある Java アプリ、またはキーのサイズが 2048 バイトのみをサポートするネットワーク デバイス。 サイズを増減するかどうかは、その CA によって発行されたすべての証明書を再発行する必要があります。

**RenewalValidityPeriod**と**RenewalValidityPeriodUnits**古いルート CA 証明書を更新するときに、新しいルート CA 証明書の有効期間を確立します。 ルート CA にのみ適用されます。 下位 CA の証明書の有効期間は、その優れたによって決定されます。 RenewalValidityPeriod には、次の値を持つことができます。時間、日、週、月、および年です。

**CRLPeriod**と**CRLPeriodUnits** base CRL の有効期間に設定します。 **CRLPeriod**次の値を持つことができます。時間、日、週、月、および年です。

**CRLDeltaPeriod**と**CRLDeltaPeriodUnits** delta CRL の有効期間を確立します。 **CRLDeltaPeriod**次の値を持つことができます。時間、日、週、月、および年です。

CA がインストールされている後に、これらの各設定を構成することができます。

```
Certutil -setreg CACRLPeriod Weeks
Certutil -setreg CACRLPeriodUnits 1
Certutil -setreg CACRLDeltaPeriod Days
Certutil -setreg CACRLDeltaPeriodUnits 1
```

変更を有効にする Active の Directory 証明書サービスを再起動してください。

**LoadDefaultTemplates**エンタープライズ CA のインストール中にのみ適用されます。 この設定は、いずれかの True または False (または 1 または 0) は、既定のテンプレートのいずれかに設定されている CA によって決まります。

CA の既定のインストールでは、既定の証明書テンプレートのサブセットは、証明機関スナップインで証明書テンプレートのフォルダーに追加されます。 つまり、こと、役割がインストールされた後に、AD CS サービスが開始するとすぐにユーザーまたは十分なアクセス許可を持つコンピューターはすぐに証明書を登録します。

LoadDefaultTemplates 設定は、既定のテンプレートがエンタープライズ CA に追加されていることを防ぐために使用できるように、CA がインストールされた後すぐにすべての証明書を発行しない可能性があります。 CA で構成されているテンプレートがない場合、そのことができますありません証明書を発行します。

**AlternateSignatureAlgorithm** 、PKCS をサポートするために CA を構成します。\#、CA 証明書と証明書の要求の 1 の V2.1 署名形式。 ルート CA を 1 に設定すると、CA 証明書は、PKCS\#1 V2.1 署名形式。 下位 CA を設定すると、下位の CA を含む、PKCS 証明書の要求を作成します\#1 V2.1 署名形式。

**ForceUTF8**既定値を変更する utf-8 名を識別するサブジェクトと発行者の相対識別名 (Rdn) のエンコードします。 のみそれら Rdn 影響を受ける、RFC でのディレクトリの文字列型として定義されているものなど、utf-8 をサポートします。 たとえば、RDN ドメイン コンポーネント (DC) には、Country RDN (C) のみがサポートされますが、印刷可能な文字列としてエンコード IA5 または utf-8 としてエンコードをサポートします。 ForceUTF8 ディレクティブは、DC の RDN はそのために影響が C の RDN には影響しません。

**EnableKeyCounting** CA の署名キーが使用されるたびにカウンターをインクリメントする CA を構成します。 ハードウェア セキュリティ モジュール (HSM) とキーのカウントをサポートする、関連付けられている暗号化サービス プロバイダー (CSP) がない限り、この設定を無効にします。 Microsoft の厳密な CSP も Microsoft ソフトウェア キー格納プロバイダー (KSP) のサポート キー カウントします。


## <a name="create-the-capolicyinf-file"></a>CAPolicy.inf ファイルを作成します。

AD CS をインストールする前に、固有の設定で、展開の CAPolicy.inf ファイルを構成します。

**前提条件:** Administrators グループのメンバーがあります。

1. Windows PowerShell を開き、AD CS のインストールを計画しているコンピューターで「**メモ帳 c:\CAPolicy.inf** ENTER キーを押します。

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
4. クリックして**ファイル**、 をクリックし、**名前を付けて保存**します。

5. %Systemroot% フォルダーに移動します。

6. 次の内容を確認します。

   -   **[ファイル名]** が **CAPolicy.inf** に設定されている。

   -   **[ファイルの種類]** が **[すべてのファイル]** に設定されている。

   -   **[文字コード]** が **[ANSI]** に設定されている。

7. **[保存]** をクリックします。

8. ファイルを上書きするかどうかをたずねるメッセージが表示されたら、 **[はい]** をクリックします。

   ![CAPolicy.inf ファイルの名前を付けて保存場所](../../../media/Prepare-the-CAPolicy-inf-File/001-SaveCAPolicyORCA1.gif)

   > [!CAUTION]
   >   拡張子 inf を付けて CAPolicy.inf を保存してください。 ファイル名の末尾に **.inf** を指定しないで上記のオプションを選択した場合、ファイルはテキスト ファイルとして保存され、CA のインストール時に使用されなくなります。

9. メモ帳を閉じます。

> [!IMPORTANT]
>   CAPolicy.inf をで URL を指定する行があるを参照できます https://pki.corp.contoso.com/pki/cps.txtします。 この CAPolicy.inf の InternalPolicy セクションは、認証実施規定 (CPS) の場所を指定する方法の例として示されています。 このガイドでは、認証実施規定 (CPS) を作成する指示されたされません。
