---
title: AD FS のトークン署名証明書とトークン暗号化解除証明書を取得して構成する
description: このドキュメントでは、の TS および TD 証明書を取得して構成する方法について説明し AD FS
author: jenfieldmsft
ms.author: billmath
manager: samueld
ms.date: 10/23/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 608f78ed03bc102cbdffb8abcc52244450b97b3c
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70865626"
---
# <a name="obtain-and-configure-ts-and-td-certificates-for-ad-fs"></a>AD FS の TS および TD 証明書を取得して構成する

このトピックでは、AD FS トークン署名証明書とトークン暗号化解除証明書が最新であることを確認するために実行できるタスクと手順について説明します。

トークン署名証明書は標準の X509 証明書であり、フェデレーションサーバーが発行するすべてのトークンに安全に署名するために使用されます。 トークン暗号化解除証明書は、受信トークンの暗号化を解除するために使用される標準の X509 証明書です。 また、フェデレーションメタデータでも公開されます。

詳細については、[証明書の要件](../design/ad-fs-requirements.md#BKMK_1)を参照してください。

## <a name="determine-whether-ad-fs-renews-the-certificates-automatically"></a>AD FS によって証明書が自動的に更新されるかどうかを判断する
既定では、AD FS は、初期構成時と証明書の有効期限が近づいているときの両方で、トークン署名証明書とトークン暗号化解除証明書を自動的に生成するように構成されます。

次の Windows PowerShell コマンド`Get-AdfsProperties`を実行できます。
  
  ![Set-adfsproperties](media/configure-TS-TD-certs-ad-fs/ts1.png)
  
AutoCertificateRollover プロパティは、AD FS がトークン署名証明書とトークン暗号化解除証明書を自動的に更新するように構成されているかどうかを示します。

AutoCertificateRollover が TRUE に設定されている場合、AD FS 証明書は AD FS で自動的に更新および構成されます。 新しい証明書が構成されたら、障害を回避するために、(証明書利用者信頼または要求プロバイダー信頼によって AD FS ファームで表される) 各フェデレーションパートナーがこの新しい証明書で更新されていることを確認する必要があります。
    
AD FS がトークン署名証明書とトークン暗号化解除証明書を自動的に更新するように構成されていない場合 (AutoCertificateRollover が False に設定されている場合)、AD FS は新しいトークン署名証明書またはトークン暗号化解除証明書の使用を自動的に生成または開始しません。 これらのタスクは手動で実行する必要があります。
    
トークン署名証明書とトークン暗号化解除証明書を自動的に更新するように AD FS が構成されている場合 (AutoCertificateRollover が TRUE に設定されている場合)、いつ更新するかを決定できます。

CertificateGenerationThreshold では、新しい証明書が生成されるまでに証明書が何日前に作成されるかを示します。

CertificatePromotionThreshold は、新しい証明書が生成されてからプライマリ証明書に昇格されるまでの日数を決定します (つまり、AD FS は、それを使用して、id プロバイダーからのトークンに署名し、トークンを復号化します)。

![Set-adfsproperties](media/configure-TS-TD-certs-ad-fs/ts2.png)
  
トークン署名証明書とトークン暗号化解除証明書を自動的に更新するように AD FS が構成されている場合 (AutoCertificateRollover が TRUE に設定されている場合)、いつ更新するかを決定できます。

 - **CertificateGenerationThreshold**では、新しい証明書が生成されるまでに証明書が何日前に作成されるかを示します。
 - **CertificatePromotionThreshold**は、新しい証明書が生成されてからプライマリ証明書に昇格されるまでの日数を決定します (つまり、AD FS は、その証明書を使用して、問題のあるトークンに署名し、id からトークンを復号化します。プロバイダー)。

## <a name="determine-when-the-current-certificates-expire"></a>現在の証明書の有効期限を確認する
次の手順を使用して、プライマリトークン署名証明書とトークン暗号化解除証明書を識別し、現在の証明書の有効期限がいつ切れるかを判断できます。

次の Windows PowerShell コマンドを実行できます`Get-AdfsCertificate –CertificateType token-signing` : ( `Get-AdfsCertificate –CertificateType token-decrypting `または)。 または、MMC で現在の証明書を確認することもできます。サービス > 証明書。

![Get-adfscertificate](media/configure-TS-TD-certs-ad-fs/ts3.png)

**IsPrimary**値が**True**に設定されている証明書は、AD FS が現在使用している証明書です。

次の日付**は、新しい**プライマリトークンの署名または暗号化解除の証明書を構成する必要がある日付を示します。

サービスの継続性を確保するには、すべてのフェデレーションパートナー (証明書利用者信頼または要求プロバイダー信頼のいずれかによって AD FS ファームで表される) が、この有効期限の前に新しいトークン署名証明書とトークン暗号化解除証明書を使用する必要があります。 このプロセスの計画は、少なくとも60日前に開始することをお勧めします。

## <a name="generating-a-new-self-signed-certificate-manually-prior-to-the-end-of-the-grace-period"></a>猶予期間が終了する前に、手動で新しい自己署名証明書を生成する
猶予期間が終了する前に、新しい自己署名証明書を手動で生成するには、次の手順を使用します。

1. プライマリ AD FS サーバーにログオンしていることを確認します。
2. Windows PowerShell を開き、次のコマンドを実行します。`Add-PSSnapin "microsoft.adfs.powershell"`
3. 必要に応じて、AD FS で現在の署名証明書を確認できます。 これを行うには、コマンド`Get-ADFSCertificate –CertificateType token-signing`を実行します。 コマンドの出力を確認し、一覧にある証明書の後にない日付を確認します。
4. 新しい証明書を生成するには、次のコマンドを実行して、AD FS サーバー `Update-ADFSCertificate –CertificateType token-signing`上の証明書を更新して更新します。
5. 次のコマンドをもう一度実行して、更新を確認します。`Get-ADFSCertificate –CertificateType token-signing`
6. 2つの証明書が表示されます。そのうちの1つは、今後約1年の日付では**なく**、 **IsPrimary**の値が**False**になっています。

>[!IMPORTANT]
>サービスが停止しないようにするには、「How to update Azure AD を有効なトークン署名証明書と共に更新する方法」の手順を実行して Azure AD の証明書情報を更新します。

## <a name="if-youre-not-using-self-signed-certificates"></a>自己署名証明書を使用していない場合...
自動的に生成された既定の自己署名トークン署名証明書とトークン暗号化解除証明書を使用していない場合は、これらの証明書を手動で更新して構成する必要があります。

まず、証明機関から新しい証明書を取得し、各フェデレーションサーバーのローカルコンピューターの個人証明書ストアにインポートする必要があります。 手順については、[証明書のインポート](https://technet.microsoft.com/library/cc754489.aspx)に関する記事を参照してください。

次に、この証明書をセカンダリ AD FS トークンの署名または暗号化解除証明書として構成する必要があります。 (プライマリ証明書に昇格する前に、フェデレーションパートナーがこの新しい証明書を使用するのに十分な時間を確保するために、セカンダリ証明書として構成します)。

### <a name="to-configure-a-new-certificate-as-a-secondary-certificate"></a>新しい証明書をセカンダリ証明書として構成するには
1. PowerShell を開き、次のように実行します。`Set-ADFSProperties -AutoCertificateRollover $false`
2. 証明書をインポートしたら、 **AD FS 管理**コンソールを開きます。
3. **[サービス]** を展開し、 **[証明書]** を選択します。
4. 操作 ウィンドウで、**トークン署名証明書の追加** をクリックします。
![Get-adfscertificate](media/configure-TS-TD-certs-ad-fs/ts4.png)</br>
5. 表示されている証明書の一覧から新しい証明書を選択し、[OK] をクリックします。
6.  PowerShell を開き、次のように実行します。`Set-ADFSProperties -AutoCertificateRollover $true`

>[!WARNING]
>新しい証明書に秘密キーが関連付けられていること、および AD FS サービスアカウントに秘密キーへの読み取りアクセス許可が付与されていることを確認します。 各フェデレーションサーバーでこれを確認します。 これを行うには、[証明書] スナップインで新しい証明書を右クリックし、[すべてのタスク] をクリックして、[秘密キーの管理] をクリックします。

フェデレーションパートナーが新しい証明書を使用するのに十分な時間が与えられたら (フェデレーションメタデータをプルするか、新しい証明書の公開キーを送信するか)、セカンダリ証明書をプライマリ証明書に昇格させる必要があります。

### <a name="to-promote-the-new-certificate-from-secondary-to-primary"></a>新しい証明書をセカンダリからプライマリに昇格させるには

1. **AD FS 管理**コンソールを開きます。
2. **[サービス]** を展開し、 **[証明書]** を選択します。
3. セカンダリトークン署名証明書をクリックします。
4. **[操作]** ウィンドウで、 **[プライマリとして設定]** をクリックします。 確認プロンプトで [はい] をクリックします。
![Get-adfscertificate](media/configure-TS-TD-certs-ad-fs/ts5.png)</br>


## <a name="updating-federation-partners"></a>フェデレーションパートナーの更新

### <a name="partners-who-can-consume-federation-metadata"></a>フェデレーションメタデータを使用できるパートナー
新しいトークン署名証明書またはトークン暗号化解除証明書を更新して構成した場合は、証明書利用者信頼によって AD FS で表されるすべてのフェデレーションパートナー (リソース組織またはアカウント組織のパートナー) であることを確認する必要があります。要求プロバイダー信頼) が新しい証明書を取得しました。

### <a name="partners-who-can-not-consume-federation-metadata"></a>フェデレーションメタデータを使用できないパートナー
フェデレーションパートナーがフェデレーションメタデータを使用できない場合は、新しいトークン署名/トークン暗号化解除証明書の公開キーを手動で送信する必要があります。 新しい証明書公開キー (チェーン全体を含める場合は .cer ファイルまたは. p7b ファイル) を、すべてのリソース組織またはアカウント組織のパートナー (証明書利用者信頼と要求プロバイダー信頼によって AD FS で表されます) に送信します。 パートナーは、新しい証明書を信頼するために変更を実装する必要があります。

### <a name="promote-to-primary-if-autocertificaterollover-is-false"></a>プライマリに昇格する (AutoCertificateRollover が False の場合)
**AutoCertificateRollover**が**False**に設定されている場合、AD FS は新しいトークン署名証明書またはトークン暗号化解除証明書の使用を自動的に生成または開始しません。 これらのタスクは手動で実行する必要があります。
すべてのフェデレーションパートナーが新しいセカンダリ証明書を使用するのに十分な時間が経過したら、このセカンダリ証明書をプライマリに昇格させます (MMC スナップインで、セカンダリトークン署名証明書をクリックし、[操作] ウィンドウで [] をクリックします)。**プライマリとして設定**します。)

## <a name="updating-azure-ad"></a>Azure AD の更新
AD FS は、既存の AD DS 資格情報を使用してユーザーを認証することで、Office 365 などの Microsoft クラウドサービスへのシングルサインオンアクセスを提供します。  証明書の使用方法の詳細については[、「Office 365 用フェデレーション証明書の更新」および「Azure AD](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-o365-certs)」を参照してください。