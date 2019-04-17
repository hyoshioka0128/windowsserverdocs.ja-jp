---
title: サーバー証明書の展開の計画
description: このトピックの「802.1 X ワイヤードおよびワイヤレス展開の証明書をサーバーのデプロイ ガイドの一部である
manager: brianlic
ms.topic: article
ms.assetid: 7eb746e0-1046-4123-b532-77d5683ded44
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: eacfa404da91d14a7a7328646c2320be8220000c
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="server-certificate-deployment-planning"></a>サーバー証明書の展開の計画

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

サーバー証明書を展開する前に、次の項目を計画する必要があります。  
  
-   [基本的なサーバー構成を計画します。](#bkmk_basic)  
  
-   [ドメイン アクセスを計画します。](#bkmk_domain)  
  
-   [Web サーバー上の仮想ディレクトリの名前と場所を計画します。](#bkmk_virtual)  
  
-   [Web サーバーの DNS エイリアス (CNAME) レコードを計画します。](#bkmk_cname)  
  
-   [CAPolicy.inf の構成を計画します。](#bkmk_capolicy)  
  
-   [CA1 で CDP および AIA 拡張機能の構成を計画します。](#bkmk_cdp)  
  
-   [CA と Web サーバーの間でコピー操作を計画します。](#bkmk_copy)  
  
-   [CA 上でサーバー証明書テンプレートの構成を計画します。](#bkmk_template)  
  
## <a name="bkmk_basic"></a>基本的なサーバー構成を計画します。  
証明機関と Web サーバーとして使用する計画しているコンピューターで Windows Server 2016 をインストールした後、コンピューターの名前を変更を割り当てると、ローカル コンピューターの静的 IP アドレスを構成してください。  
  
詳細については、Windows Server 2016 を参照してください。[コア ネットワーク ガイド](../../../core-network-guide/Core-Network-Guide.md)します。  
  
## <a name="bkmk_domain"></a>ドメイン アクセスを計画します。  
ドメインにログオンするには、コンピューターがドメイン メンバー コンピューターをする必要があり、ログオンを試みる前に AD DS でユーザー アカウントを作成する必要があります。 さらに、このガイドのほとんどの手順では、ユーザー アカウントが Active Directory ユーザーとコンピューターの Enterprise Admins グループまたは Domain Admins グループのメンバーを適切なグループ メンバーシップを持つアカウントを使用して CA にログオンする必要がありますのでが必要です。  
  
詳細については、Windows Server 2016 を参照してください。[コア ネットワーク ガイド](../../../core-network-guide/Core-Network-Guide.md)します。  
  
## <a name="bkmk_virtual"></a>Web サーバー上の仮想ディレクトリの名前と場所を計画します。  
CRL と他のコンピューターに CA 証明書にアクセスを提供するには、Web サーバー上の仮想ディレクトリにこれらの項目を格納する必要があります。 このガイドでは、仮想ディレクトリは、Web サーバー WEB1 上にあります。 このフォルダーは、「c:」ドライブあるし、、"pki"をという名前 展開に適切なフォルダーの場所で、Web サーバー上の仮想ディレクトリを検索できます。  
  
## <a name="bkmk_cname"></a>Web サーバーの DNS エイリアス (CNAME) レコードを計画します。  
エイリアス (CNAME) リソース レコードは正規名リソース レコードと呼ばれることもあります。 これらのレコードと容易をファイル転送プロトコル (FTP) サーバーと同じコンピューター上の Web サーバーの両方のホストとしてこのような管理を行うには、1 つのホストを指す複数の名前を使用することができます。 たとえば、よく知られたサーバー名 (ftp、www など) では、これらのサービスをホストするドメイン ネーム システム (DNS) ホスト名、WEB1 などのサーバー コンピューターにマップするエイリアス (CNAME) リソース レコードを使用して、登録されます。  
  
このガイドでは、証明機関 (CA) の証明書失効リスト (CRL) をホストする Web サーバーを構成するための指示を提供します。 FTP または Web サイトをホストするように、他の目的の Web サーバーを使用する可能性がありますも、ためには、Web サーバーの DNS でエイリアス リソース レコードを作成することをお勧めします。 このガイドで CNAME レコードが、"pki"をという名前が、展開に適切な名前を選択することができます。  
  
## <a name="bkmk_capolicy"></a>CAPolicy.inf の構成を計画します。  
AD CS をインストールする前に、展開に適切な情報を使用して CA の CAPolicy.inf を構成する必要があります。 CAPolicy.inf ファイルには、次の情報が含まれています。  
  
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
```  
このファイルの次の項目を計画する必要があります。  
  
-   **URL**します。 例 CAPolicy.inf ファイルの URL の値が**http://pki.corp.contoso.com/pki/cps.txt**します。 これは、このガイド内の Web サーバーが WEB1 という名前は、pki の DNS の CNAME リソース レコードを持つためです。 Web サーバーも corp.contoso.com ドメインに参加しています。 さらに、証明書失効リストが格納されている"pki"という名前の Web サーバーでは仮想ディレクトリが存在します。 ドメイン内、Web サーバー上の仮想ディレクトリには、CAPolicy.inf ファイルのポイントで URL の指定した値を確認します。  
  
-   **RenewalKeyLength**します。 Windows Server 2012 で AD CS の既定の更新のキーの長さは 2048 です。 選択したキーの長さを使用する予定のアプリケーションとの互換性を提供しながらできるだけ長くする必要があります。  
  
-   **RenewalValidityPeriodUnits**します。 CAPolicy.inf ファイルの例では、5 年の RenewalValidityPeriodUnits 値があります。 これは、CA の想定される存続期間が約 10 年であるためです。 RenewalValidityPeriodUnits の値は、CA または登録できるようにする対象となる年間の最大数の全体的な有効期間を反映する必要があります。  
  
-   **CRLPeriodUnits**します。 CAPolicy.inf ファイルの例では、1 の CRLPeriodUnits 値があります。 これは、このガイドで証明書失効リストの例の更新間隔が 1 週間であるためです。 この設定で指定した間隔の値は必要があります、CRL を格納する Web サーバーの仮想ディレクトリを CA の CRL を公開し、認証プロセスであるコンピューターへのアクセス権を提供します。  
  
-   **AlternateSignatureAlgorithm**します。 この CAPolicy.inf では、別の署名形式を実装することで、強化されたセキュリティ メカニズムを実装します。 この CA から証明書を必要とする Windows XP クライアントがある場合は、この設定を実装しないでください。  
  
後で、公開キー インフラストラクチャにすべての下位 Ca を追加する予定がないと、すべての下位 Ca の追加できないようにする場合は、値を 0 CAPolicy.inf ファイルに PathLength キーを追加できます。 このキーを追加するにコピーし、次のコード ファイルに貼り付けます。  
  
```  
[BasicConstraintsExtension]  
PathLength=0  
Critical=Yes  
```  
  
> [!IMPORTANT]  
> そのための特別な理由がない限り、CAPolicy.inf ファイルにその他の設定を変更することは推奨されません。  
  
## <a name="bkmk_cdp"></a>CA1 で CDP および AIA 拡張機能の構成を計画します。  
CA1 で証明書失効リスト (CRL) 配布ポイント (CDP) および機関情報アクセス (AIA) の設定を構成するときに、Web サーバーとドメイン名の名前が必要です。 証明書失効リスト (CRL) および証明機関の証明書が格納されている Web サーバーで作成した仮想ディレクトリの名前も必要があります。  
  
この展開の手順の中に入力する必要があります CDP の場所には、形式があります。  
      
    `http:\/\/*DNSAlias\(CNAME\)RecordName*.*Domain*.com\/*VirtualDirectoryName*\/<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl.`  
      
たとえば、WEB1 という名前の Web サーバーは、DNS、Web サーバーの CNAME レコード エイリアスは"pki"場合は、ドメイン corp.contoso.com、および仮想ディレクトリの名前は pki、CDP の場所は。  
      
    `http:\/\/pki.corp.contoso.com\/pki\/<CaName><CRLNameSuffix><DeltaCRLAllowed>.crl`  
      
入力する必要があります AIA の場所には、形式があります。  
      
    `http:\/\/*DNSAlias\(CNAME\)RecordName*.*Domain*.com\/*VirtualDirectoryName*\/<ServerDNSName>\_<CaName><CertificateName>.crt.`  
      
たとえば、WEB1 という名前の Web サーバーは、DNS、Web サーバーの CNAME レコード エイリアスは"pki"場合は、ドメイン corp.contoso.com、および仮想ディレクトリの名前は pki、AIA の場所は。  
      
    `http:\/\/pki.corp.contoso.com\/pki\/<ServerDNSName>\_<CaName><CertificateName>.crt`  
      
## <a name="bkmk_copy"></a>CA と Web サーバーの間でコピー操作を計画します。  
CRL と CA 証明書を発行 CA から Web サーバーの仮想ディレクトリに、CA の CDP および AIA の場所を構成した後は、certutil-crl コマンドを実行できます。 [CA プロパティによって正しいパスを構成することを確認**拡張機能:** ] タブのこのガイドの手順に従って、このコマンドを実行する前にします。 さらに、エンタープライズ CA 証明書を Web サーバーにコピーする必要があります既に Web サーバー上の仮想ディレクトリを作成して共有フォルダーとしてフォルダーを構成します。  
  
## <a name="bkmk_template"></a>CA 上でサーバー証明書テンプレートの構成を計画します。  
自動登録サーバーの証明書を展開するには、という名前の証明書テンプレートをコピーする必要があります**RAS および IAS サーバー**します。 既定では、このコピーの名前は**コピーの RAS および IAS サーバー**します。 このテンプレートのコピーの名前を変更する場合は、この展開の手順の中に使用する名前を計画します。  
  
> [!NOTE]  
> 最後の 3 つの展開セクションでは、このガイドを使用するサーバーでは、グループ ポリシーの更新は、サーバー証明書の自動登録を構成して、サーバーに CA から有効なサーバー証明書が受信したことを確認する - するには、追加の計画手順は不要です。  
  


