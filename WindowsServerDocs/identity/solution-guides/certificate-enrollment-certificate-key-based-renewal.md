---
title: カスタムポートで証明書キーに基づく更新の証明書の登録 Web サービスを構成する
description: ''
author: Deland-Han
ms.author: delhan
manager: dcscontentpm
ms.date: 11/12/2019
ms.topic: article
ms.prod: windows-server
ms.openlocfilehash: 3d3d08d6abe9daa571dd7365815c1fc61f926501
ms.sourcegitcommit: e5df3fd267352528eaab5546f817d64d648b297f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/18/2019
ms.locfileid: "74163103"
---
# <a name="configuring-certificate-enrollment-web-service-for-certificate-key-based-renewal-on-a-custom-port"></a>カスタムポートで証明書キーに基づく更新の証明書の登録 Web サービスを構成する

> 執筆者: Windows グループを使用した Jitesh Thakur、Meera Mohideen、Technical advisor。
Windows グループを使用した ankit Tyagi サポートエンジニア

## <a name="summary"></a>概要

この記事では、443以外のカスタムポートに証明書の登録ポリシー Web サービス (CEP) と証明書の登録 Web サービス (CES) を実装する手順について説明します。この方法では、証明書キーに基づく書き換えによって自動のCEP および CES の更新機能。

この記事では、CEP と CES の動作、およびセットアップガイドラインについても説明します。

> [!Note]
> この記事に含まれるワークフローは、特定のシナリオに適用されます。 同じワークフローが、状況によっては機能しない場合があります。 ただし、原則は変わりません。
>
> 免責事項: このセットアップは、CEP および CES サーバーの既定の HTTPS 通信にポート443を使用しない特定の要件に対して作成されます。 この設定は可能ですが、サポートが制限されています。 お客様のサービスとサポートは、提供されている web サーバー構成からの最小偏差を使用して、このガイドに従っている場合に最適です。

## <a name="scenario"></a>シナリオ

この例では、手順は次の構成を使用する環境に基づいています。

- Active Directory 証明書サービス (AD CS) 公開キー基盤 (PKI) を持つ Contoso.com フォレスト。

- サービスアカウントで実行されている1台のサーバー上に構成されている2つの CEP/CES インスタンス。 1つのインスタンスでは、最初の登録にユーザー名とパスワードを使用します。 もう1つは、書き換え専用モードでのキーベースの書き換えに証明書ベースの認証を使用する方法です。

- ユーザーは、ユーザー名とパスワードの資格情報を使用してコンピューターの証明書を登録するワークグループまたはドメインに参加していないコンピューターを持っています。

- HTTPS を介したユーザーから CEP および CES への接続は、49999などのカスタムポートで行われます。 (このポートは動的ポート範囲から選択され、他のサービスによって静的ポートとしては使用されません)。

- 証明書の有効期間が終了すると、コンピューターは証明書ベースの CES キーベースの書き換えを使用して、同じチャネルで証明書を更新します。

![展開](media/certificate-enrollment-certificate-key-based-renewal-1.png)

## <a name="configuration-instructions"></a>構成の手順

### <a name="overview"></a>概要 

1. キーベースの書き換え用にテンプレートを構成します。

2. 前提条件として、ユーザー名とパスワードの認証用に CEP および CES サーバーを構成します。   
   この環境では、インスタンスを "CEPCES01" と呼びます。

3.  同じサーバー上で証明書ベースの認証に PowerShell を使用して、別の CEP および CES インスタンスを構成します。 CES インスタンスは、サービスアカウントを使用します。

    この環境では、インスタンスを "CEPCES02" と呼びます。 使用されるサービスアカウントは "cep、" です。

4.  クライアント側の設定を構成します。

### <a name="configuration"></a>構成

このセクションでは、初期登録を構成する手順について説明します。

> [!Note]
> CES が機能するように、ユーザーサービスアカウント、MSA、または GMSA を構成することもできます。

前提条件として、ユーザー名とパスワードの認証を使用して、サーバーで CEP および CES を構成する必要があります。

#### <a name="configure-the-template-for-key-based-renewal"></a>キーベースの書き換え用にテンプレートを構成する

既存のコンピューターテンプレートを複製し、テンプレートの次の設定を構成することができます。

1. 証明書テンプレートの [サブジェクト名] タブで、[**自動登録更新要求に対して既存の証明書のサブジェクト情報**を**要求**して使用する] オプションが選択されていることを確認します。
   新しいテンプレートの ![](media/certificate-enrollment-certificate-key-based-renewal-2.png) 

2. 発行の **[要件]** タブに切り替えて、 **[CA 証明書マネージャーの承認]** チェックボックスをオンにします。
   ![発行の要件](media/certificate-enrollment-certificate-key-based-renewal-3.png) 

3. **読み取り**と**登録**のアクセス許可を、このテンプレートの**cepの vc**サービスアカウントに割り当てます。

4. CA で新しいテンプレートを発行します。

> [!Note]
> 互換性が Windows Server 2016 以降のバージョンに設定されている場合、テンプレートが表示されないという既知の問題があるため、テンプレートの互換性設定が**Windows server 2012 R2**に設定されていることを確認してください。 詳細については、「windows server [2016 またはそれ以降の ca または CEP サーバーから Windows server 2016 CA 互換証明書テンプレートを選択できません](https://support.microsoft.com/en-in/help/4508802/cannot-select-certificate-templates-in-windows-server-2016)詳細」を参照してください。


#### <a name="configure-the-cepces01-instance"></a>CEPCES01 インスタンスを構成する

##### <a name="step-1-install-the-instance"></a>手順 1: インスタンスをインストールする

CEPCES01 インスタンスをインストールするには、次のいずれかの方法を使用します。

**方法1**

ユーザー名とパスワードの認証に CEP と CES を有効にするための詳細な手順については、次の記事を参照してください。

[証明書の登録ポリシー Web サービスガイダンス](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831625(v=ws.11))

[証明書の登録 Web サービスガイダンス](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831822(v=ws.11)#configure-a-ca-for-the-certificate-enrollment-web-service)

> [!Note]
> CEP と CES の両方のインスタンスのユーザー名とパスワードの認証を構成する場合は、[キーベースの書き換えを有効にする] オプションを選択しないようにしてください。

**方法2**

次の PowerShell コマンドレットを使用して、CEP インスタンスと CES インスタンスをインストールできます。

```PowerShell
Import-Module ServerManager
Add-WindowsFeature Adcs-Enroll-Web-Pol
Add-WindowsFeature Adcs-Enroll-Web-Svc
```

```PowerShell
Install-AdcsEnrollmentPolicyWebService -AuthenticationType Username -SSLCertThumbprint "sslCertThumbPrint"
```

このコマンドは、ユーザー名とパスワードを認証に使用することを指定することによって、証明書の登録ポリシー Web サービス (CEP) をインストールします。 

> [!Note]
> このコマンドでは、\<**Sslcertthumbprint**\> は、IIS のバインドに使用される証明書の拇印です。

```PowerShell
Install-AdcsEnrollmentWebService -ApplicationPoolIdentity -CAConfig "CA1.contoso.com\contoso-CA1-CA" -SSLCertThumbprint "sslCertThumbPrint" -AuthenticationType Username
```

このコマンドは、証明書の登録 Web サービス (CES) をインストールして、 **CA1.contoso.com**のコンピューター名の証明機関と**CA1**の ca 共通名を使用します。 CES の id は、既定のアプリケーションプール id として指定されます。 認証の種類は**username**です。 SSLCertThumbPrint は、IIS のバインドに使用される証明書の拇印です。

##### <a name="step-2-check-the-internet-information-services-iis-manager-console"></a>手順2インターネットインフォメーションサービス (IIS) マネージャーコンソールを確認する

インストールが正常に完了すると、インターネットインフォメーションサービス (IIS) マネージャーコンソールに次の表示が表示されます。
![IIS マネージャー](media/certificate-enrollment-certificate-key-based-renewal-4.png) 

**[既定の Web サイト]** で、 **[ADPolicyProvider_CEP_UsernamePassword]** を選択し、 **[アプリケーションの設定]** を開きます。 **ID**と**URI**をメモしておきます。

管理用の**フレンドリ名**を追加できます。

#### <a name="configure-the-cepces02-instance"></a>CEPCES02 インスタンスを構成する

##### <a name="step-1-install-the-cep-and-ces-for-key-based-renewal-on-the-same-server"></a>手順 1: キーベースの更新のための CEP と CES を同じサーバーにインストールします。 

PowerShell で次のコマンドを実行します。

```PowerShell
Install-AdcsEnrollmentPolicyWebService -AuthenticationType Certificate -SSLCertThumbprint "sslCertThumbPrint" -KeyBasedRenewal
```

このコマンドは、証明書の登録ポリシー Web サービス (CEP) をインストールし、認証に証明書を使用することを指定します。 

> [!Note]
> このコマンドでは、\<SSLCertThumbPrint\> は、IIS のバインドに使用される証明書の拇印です。 

キーベースの更新により、証明書クライアントは既存の証明書のキーを使用して認証を行うことで、証明書を更新できます。 キーベースの書き換えモードでは、サービスはキーベースの更新に設定されている証明書テンプレートのみを返します。

```PowerShell
Install-AdcsEnrollmentWebService -CAConfig "CA1.contoso.com\contoso-CA1-CA" -SSLCertThumbprint "sslCertThumbPrint" -AuthenticationType Certificate -ServiceAccountName "Contoso\cepcessvc" -ServiceAccountPassword (read-host "Set user password" -assecurestring) -RenewalOnly -AllowKeyBasedRenewal
```

このコマンドは、証明書の登録 Web サービス (CES) をインストールして、 **CA1.contoso.com**のコンピューター名の証明機関と**CA1**の ca 共通名を使用します。 

このコマンドでは、証明書の登録 Web サービスの id が、 **cepの vc**サービスアカウントとして指定されています。 認証の種類は**certificate**です。 **Sslcertthumbprint**は、IIS のバインドに使用される証明書の拇印です。

**RenewalOnly**コマンドレットを使用すると、CES を更新専用モードで実行できます。 **Allowkeybased 書き換え**コマンドレットは、CES が登録サーバーに対するキーベースの更新要求を受け入れることも指定します。 これらは、セキュリティプリンシパルに直接マップされない認証用の有効なクライアント証明書です。

> [!Note]
> サービスアカウントは、サーバー上の**Iisusers**グループに属している必要があります。

##### <a name="step-2-check-the-iis-manager-console"></a>手順 2. IIS マネージャーコンソールを確認する

インストールが正常に完了すると、IIS マネージャーコンソールに次の表示が表示されます。
![IIS マネージャー](media/certificate-enrollment-certificate-key-based-renewal-5.png) 

既定の **[Web サイト]** の **[KeyBasedRenewal_ADPolicyProvider_CEP_Certificate]** を選択し、 **[アプリケーションの設定]** を開きます。 **ID**と**URI**をメモしておきます。 管理用の**フレンドリ名**を追加できます。

> [!Note]
> インスタンスが新しいサーバーにインストールされている場合は、id を確認して、CEPCES01 インスタンスで生成されたものと同じ ID であることを確認してください。 値が異なる場合は、値を直接コピーして貼り付けることができます。

#### <a name="complete-certificate-enrollment-web-services-configuration"></a>証明書の登録 Web サービスの構成の完了

CEP および CES の機能の代わりに証明書を登録できるようにするには、Active Directory でワークグループのコンピューターアカウントを構成してから、サービスアカウントで制約付き委任を構成する必要があります。

##### <a name="step-1-create-a-computer-account-of-the-workgroup-computer-in-active-directory"></a>手順 1: Active Directory でワークグループコンピューターのコンピューターアカウントを作成する

このアカウントは、キーベースの書き換えに対する認証と、証明書テンプレートの [Publish to Active Directory] オプションに使用されます。

> [!Note]
> クライアントコンピューターにドメインを参加させる必要はありません。 KBR for dsmapper サービスで証明書ベースの認証を行うときに、このアカウントは画像に含まれています。

![新しいオブジェクト](media/certificate-enrollment-certificate-key-based-renewal-6.png) 
 
##### <a name="step-2-configure-the-service-account-for-constrained-delegation-s4u2self"></a>手順 2: 制約付き委任用にサービスアカウントを構成する (S4U2Self)

次の PowerShell コマンドを実行して、制約付き委任 (S4U2Self または任意の認証プロトコル) を有効にします。

```PowerShell
Get-ADUser -Identity cepcessvc | Set-ADAccountControl -TrustedToAuthForDelegation $True
Set-ADUser -Identity cepcessvc -Add @{'msDS-AllowedToDelegateTo'=@('HOST/CA1.contoso.com','RPCSS/CA1.contoso.com')}
```

> [!Note]
> このコマンドでは、\<cepの vc\> がサービスアカウントであり、< CA1 > が証明機関です。

> [!Important]
> 同じジョブを実行するために制約付き委任を使用しているため、この構成では CA の RENEWALONBEHALOF フラグを有効にしません。 これにより、CA のセキュリティにサービスアカウントのアクセス許可が追加されないようにすることができます。

##### <a name="step-3-configure-a-custom-port-on-the-iis-web-server"></a>手順 3: IIS web サーバーでカスタムポートを構成する

1. IIS マネージャーコンソールで、[既定の Web サイト] を選択します。

2. [操作] ウィンドウで、[サイトバインドの編集] を選択します。 

3. 既定のポート設定を443からカスタムポートに変更します。 例のスクリーンショットは、ポートの設定が49999であることを示しています。
   ポートの変更 ![](media/certificate-enrollment-certificate-key-based-renewal-7.png) 

##### <a name="step-4-edit-the-ca-enrollment-services-object-on-active-directory"></a>手順 4: Active Directory で CA 登録サービスオブジェクトを編集する

1. ドメインコントローラーで、adsiedit を開きます。

2. [構成パーティションに接続](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/ff730188(v=ws.10))し、CA 登録サービスオブジェクトに移動します。
   
   CN = ENTCA、CN = Enrollment Services、CN = Public Key Services、CN = Services、CN = Configuration、DC = contoso、DC = com

3. CA オブジェクトを右クリックして編集します。 アプリケーション設定で見つかった CEP および CES サーバー Uri でカスタムポートを使用して、 **mspki-site-name**属性を変更します。 次に、例を示します。

   ```
   140https://cepces.contoso.com:49999/ENTCA_CES_UsernamePassword/service.svc/CES0   
   181https://cepces.contoso.com:49999/ENTCA_CES_Certificate/service.svc/CES1
   ```
   
   ![ADSI エディター](media/certificate-enrollment-certificate-key-based-renewal-8.png) 

#### <a name="configure-the-client-computer"></a>クライアントコンピューターを構成する

クライアントコンピューターで、登録ポリシーと自動登録ポリシーを設定します。 これを行うには、次の手順に従います。

1. [**開始** > **実行**] を選択し、「 **gpedit.msc**」と入力します。

2. **[コンピューターの構成]** の **[Windows の設定]**  > セキュリティの **[設定]** の順に選択し、 **[公開キーのポリシー]** をクリックし > ます。

3. 次のスクリーンショットの設定と一致するように、[**証明書サービスクライアント-自動登録] ポリシー**を有効にします。
   ![証明書グループポリシー](media/certificate-enrollment-certificate-key-based-renewal-9.png)
 
4. **証明書サービスクライアント証明書の登録ポリシー**を有効にします。

   」を参照します。 **[追加]** をクリックして登録ポリシーを追加し、ADSI で編集した**USERNAMEPASSWORD**で CEP URI を入力します。
   
   b. **[認証の種類]** で、 **[ユーザー名/パスワード]** を選択します。
   
   c. 優先順位を**10**に設定し、ポリシーサーバーを検証します。
      ![の登録ポリシー](media/certificate-enrollment-certificate-key-based-renewal-10.png)

   > [!Note]
   > ポート番号が URI に追加されていること、およびファイアウォールで許可されていることを確認してください。

5. コンピューターの最初の証明書を certlm .msc で登録します。
   ![の登録ポリシー](media/certificate-enrollment-certificate-key-based-renewal-11.png)

   KBR テンプレートを選択し、証明書を登録します。
   ![の登録ポリシー](media/certificate-enrollment-certificate-key-based-renewal-12.png)

6. **Gpedit.msc を**再度開きます。 **[証明書サービスクライアント-証明書の登録ポリシー]** を編集し、キーに基づく更新登録ポリシーを追加します。

   」を参照します。 **[追加]** をクリックし、ADSI で編集した**証明書**を含む CEP URI を入力します。 
   
   b. 優先度を**1**に設定し、ポリシーサーバーを検証します。 最初に登録した証明書を認証して選択するよう求められます。

   ![登録ポリシー](media/certificate-enrollment-certificate-key-based-renewal-13.png) 

> [!Note]
> キーベースの更新登録ポリシーの優先順位の値が、ユーザー名パスワード登録ポリシーの優先順位よりも低いことを確認してください。 最初の設定は、最も低い優先順位に与えられます。

## <a name="testing-the-setup"></a>セットアップのテスト

自動更新が機能していることを確認するには、mmc を使用して同じキーを使用して証明書を更新することで、手動更新が機能することを確認します。 また、更新中に証明書を選択するように求めるメッセージが表示されます。 先ほど登録した証明書を選択できます。 プロンプトが必要です。

コンピューターの個人証明書ストアを開き、[アーカイブ済み証明書] ビューを追加します。 これを行うには、ローカルコンピューターアカウントスナップインを mmc.exe に追加し、 **[証明書 (ローカルコンピューター)]** をクリックして強調表示します。 mmc の右側または上部にある [**操作] タブ**で **[表示]** をクリックし、 **[オプションの表示]** をクリックして、アーカイブされた **[証明書]** をクリックし、[ **OK]** を

### <a name="method-1"></a>方法1 

次のコマンドを実行します。

```PowerShell
certreq -machine -q -enroll -cert <thumbprint> renew
```

![コマンドを使用します](media/certificate-enrollment-certificate-key-based-renewal-14.png)

### <a name="method-2"></a>方法 2

クライアントコンピューターの日時を、証明書テンプレートの更新時間に進めます。

たとえば、証明書テンプレートの有効期間が2日間で、8時間の更新設定が構成されているとします。 この例の証明書は午前4:00 に発行されています。 月の18日に、は午前4:00 に有効期限が切れます。 20になります。 自動登録エンジンは、再起動時および8時間ごと (約) にトリガーされます。

したがって、時刻を午後8:10 時に進める場合は、 19日に、更新ウィンドウがテンプレートで8時間に設定されていたため、Certutil-pulse (AE エンジンをトリガーする) を実行すると、証明書が登録されます。

![コマンドを使用します](media/certificate-enrollment-certificate-key-based-renewal-15.png)
 
テストが完了したら、時刻の設定を元の値に戻してから、クライアントコンピューターを再起動します。

> [!Note]
> 前のスクリーンショットは、CA の日付が18に設定されているため、自動登録エンジンが想定どおりに動作することを示す例です。 そのため、証明書の発行は続行されます。 実際の状況では、この大量の更新は行われません。

## <a name="references"></a>参照先

[テストラボガイド: 証明書キーベースの書き換えのデモンストレーション](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj590165(v%3Dws.11))

[証明書の登録 Web サービス](https://techcommunity.microsoft.com/t5/Ask-the-Directory-Services-Team/Certificate-Enrollment-Web-Services/ba-p/397385)

[AdcsEnrollmentPolicyWebService](https://docs.microsoft.com/powershell/module/adcsdeployment/install-adcsenrollmentpolicywebservice?view=win10-ps)

[AdcsEnrollmentWebService](https://docs.microsoft.com/powershell/module/adcsdeployment/install-adcsenrollmentwebservice?view=win10-ps)

関連項目

[Windows Server セキュリティフォーラム](https://aka.ms/adcsforum)

[Active Directory 証明書サービス (AD CS) 公開キー基盤 (PKI) に関してよく寄せられる質問 (FAQ)](https://aka.ms/adcsfaq)

[Windows PKI ドキュメントリファレンスおよびライブラリ](https://social.technet.microsoft.com/wiki/contents/articles/987.windows-pki-documentation-reference-and-library.aspx)

[Windows PKI ブログ](https://blogs.technet.com/b/pki/)

[Web 登録プロキシページのカスタムサービスアカウントで Kerberos の制約付き委任 (S4U2Proxy または Kerberos のみ) を構成する方法](https://support.microsoft.com/help/4494313/configuring-web-enrollment-proxy-for-s4u2proxy-constrained-delegation)