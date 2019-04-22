---
title: 取得し、AD FS のトークンの署名とトークン暗号化解除証明書を構成します。
description: このドキュメントを取得して、TS と TD を構成する方法を説明します AD FS 用の証明書。
author: jenfieldmsft
ms.author: billmath
manager: samueld
ms.date: 10/23/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: d16a886c9fb8f88748ffe732a75f0fd6a32c3702
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820213"
---
# <a name="obtain-and-configure-ts-and-td-certificates-for-ad-fs"></a>取得し、TS と TD 証明書を AD FS の構成

このトピックでは、タスクと、AD FS トークン署名とトークン暗号化解除証明書が最新であることを確認するときに実行する手順について説明します。

トークン署名証明書が標準の X509 証明書を安全にフェデレーション サーバーが発行するすべてのトークンの署名に使用します。 トークン暗号化解除証明書は、標準の X509 証明書、受信トークンを復号化するために使用します。 フェデレーション メタデータにも発行されます。

追加情報を参照してください[証明書の要件。](../design/ad-fs-requirements.md#BKMK_1)

## <a name="determine-whether-ad-fs-renews-the-certificates-automatically"></a>AD FS が自動的に証明書を更新するかどうかを判断します。
既定では、AD FS は、初期構成時と、証明書は、有効期限の日付に近づいているときにトークンの署名とトークン暗号化解除証明書を自動的に生成するように構成します。

次の Windows PowerShell コマンドを実行することができます:`Get-AdfsProperties`します。
  
  ![Get-adfsproperties](media/configure-TS-TD-certs-ad-fs/ts1.png)
  
AutoCertificateRollover プロパティは、トークンの署名と暗号化解除証明書を自動的にトークンを更新する AD FS が構成されているかどうかについて説明します。

AutoCertificateRollover が TRUE に設定されている場合、AD FS 証明書を更新して、AD FS で自動的に構成できます。 新しい証明書の構成が済んだら、障害発生を回避するためにする必要があります (証明書利用者信頼または要求プロバイダー信頼のいずれかによって、AD FS ファームで表される) 各フェデレーション パートナーが更新されるようにこの新しい証明書を使用します。
    
AD FS がトークンの署名を更新するように構成し、トークンがない場合は、復号化する場合に自動的に (AutoCertificateRollover が False に設定) に証明書、AD FS が生成は自動的に、または新しいトークン署名やトークン暗号化解除証明書の使用を開始します。 これらのタスクを手動で実行する必要があります。
    
トークンの署名と暗号化解除証明書を自動的にトークンを更新する AD FS が構成されている場合 (AutoCertificateRollover が TRUE に設定) 更新と判断できます。

CertificateGenerationThreshold では、何日前の日付の後、証明書の新しい証明書は生成されたについて説明します。

CertificatePromotionThreshold が何日後に、新しい証明書が生成プライマリ証明書に昇格することを決定します (つまり、AD FS は開始を発行するトークンの署名し、id プロバイダーからトークンを復号化するために使用)。

![Get-adfsproperties](media/configure-TS-TD-certs-ad-fs/ts2.png)
  
トークンの署名と暗号化解除証明書を自動的にトークンを更新する AD FS が構成されている場合 (AutoCertificateRollover が TRUE に設定) 更新と判断できます。

 - **CertificateGenerationThreshold**何日前の日付の後、証明書の新しい証明書が生成するについて説明します。
 - **CertificatePromotionThreshold**何日後に、新しい証明書が生成プライマリ証明書に昇格することを決定します (つまり、AD FS は使用を開始を発行するトークンに署名し、id からのトークン暗号化解除プロバイダーの場合)。

## <a name="determine-when-the-current-certificates-expire"></a>現在の証明書が有効期限が決まります
現在の証明書の有効期限が切れるかを判断して、プライマリ トークン署名とトークン暗号化解除証明書を識別するためには、次の手順を使用できます。

次の Windows PowerShell コマンドを実行することができます: `Get-AdfsCertificate –CertificateType token-signing` (または`Get-AdfsCertificate –CertificateType token-decrypting `)。 または、MMC の現在の証明書を調べることができます。サービスには、証明書]-> [です。

![Get-adfscertificate](media/configure-TS-TD-certs-ad-fs/ts3.png)

対象の証明書、 **IsPrimary**値に設定されて**True**は AD FS を使用している証明書です。

日付、**後**日付を新しいプライマリ トークン署名、または証明書を復号化を構成する必要があります。

サービスの継続性を確保するには、(証明書利用者信頼または要求プロバイダー信頼のいずれかによって、AD FS ファームで表される) のすべてのフェデレーション パートナーは、新しいトークン署名とこの有効期限の前に、トークン暗号化解除証明書を使用する必要があります。 このプロセスには少なくとも 60 日間で事前の計画を開始することをお勧めします。

## <a name="generating-a-new-self-signed-certificate-manually-prior-to-the-end-of-the-grace-period"></a>猶予期間の終了前に手動で新しい自己署名証明書を生成します。
猶予期間の終了前に手動で新しい自己署名証明書を生成するのに、次の手順を使用することができます。

1. プライマリ AD FS サーバーにログオンしていることを確認します。
2. Windows PowerShell を開き、次のコマンドを実行します。 `Add-PSSnapin "microsoft.adfs.powershell"`
3. 必要に応じて、AD FS で現在の署名証明書を確認することができます。 これを行うには、次のコマンドを実行します:`Get-ADFSCertificate –CertificateType token-signing`します。 表示されているすべての証明書の後ではなく日付を表示するコマンドの出力を確認します。
4. 新しい証明書を生成するには、更新し、AD FS サーバーの証明書を更新するには、次のコマンドを実行します:`Update-ADFSCertificate –CertificateType token-signing`します。
5. 次のコマンドを再度実行して、更新プログラムを確認します。 `Get-ADFSCertificate –CertificateType token-signing`
6. 2 つの証明書が表示されるはず、うちの 1 つが、**後**を約 1 年間、将来の日付、 **IsPrimary**値は**False**します。

>[!IMPORTANT]
>サービスの停止を回避するには、有効なトークン署名証明書を Azure AD を更新する方法の手順を実行して Azure AD の証明書情報を更新します。

## <a name="if-youre-not-using-self-signed-certificates"></a>自己署名証明書を使用していない場合.
自動的に生成される既定値を使用していない、自己署名トークンの署名およびトークン暗号化解除証明書の場合は、更新して、これらの証明書を手動で構成する必要があります。

まず、証明機関から新しい証明書を取得し、各フェデレーション サーバーでローカル コンピューター個人証明書ストアにインポートする必要があります。 手順については、次を参照してください。、[証明書をインポート](https://technet.microsoft.com/library/cc754489.aspx)記事。

このとして、セカンダリ AD FS トークン署名証明書または暗号化解除証明書を構成する必要があります。 (構成するプライマリ証明書に昇格する前に、この新しい証明書を使用するには、十分な時間に、フェデレーション パートナーを許可する証明書をセカンダリとして)。

### <a name="to-configure-a-new-certificate-as-a-secondary-certificate"></a>セカンダリ証明書として、新しい証明書を構成するには
1. PowerShell を開き、次を実行します。 `Set-ADFSProperties -AutoCertificateRollover $false`
2. 1 回、証明書をインポートしました。 開く、 **AD FS 管理**コンソール。
3. 展開**サービス**選び**証明書**します。
4. 操作 ウィンドウで、次のようにクリックします。 **トークン署名証明書**します。
![Get-adfscertificate](media/configure-TS-TD-certs-ad-fs/ts4.png)</br>
5. 表示されている証明書の一覧から、新しい証明書を選択し、[ok] をクリックします。
6.  PowerShell を開き、次を実行します。 `Set-ADFSProperties -AutoCertificateRollover $true`

>[!WARNING]
>新しい証明書が関連付けられている秘密キーを持つことを確認し、秘密キーへのアクセス許可を読み取り、AD FS サービス アカウントが許可されていること。 各フェデレーション サーバーでは、これを確認します。 証明書スナップインで、これには、新しい証明書を右クリックし、すべてのタスク をクリックしますおよび秘密キーの管理を順にクリックします。

フェデレーション パートナー (フェデレーション メタデータをプル、または新しい証明書の公開キーを送信する) 新しい証明書を使用するための十分な時間を許可した後は、プライマリ証明書をセカンダリ証明書を昇格する必要があります。

### <a name="to-promote-the-new-certificate-from-secondary-to-primary"></a>新しい証明書をセカンダリからプライマリへ昇格するには

1. 開く、 **AD FS 管理**コンソール。
2. 展開**サービス**選び**証明書**します。
3. セカンダリ トークン署名証明書をクリックします。
4. **アクション**ウィンドウで、をクリックして**プライマリとして設定**します。 確認プロンプトで、[はい] をクリックします。
![Get-adfscertificate](media/configure-TS-TD-certs-ad-fs/ts5.png)</br>


## <a name="updating-federation-partners"></a>フェデレーション パートナーを更新しています

### <a name="partners-who-can-consume-federation-metadata"></a>パートナーのフェデレーション メタデータを使用することができます。
更新が新しいトークン署名やトークン暗号化解除証明書を構成していて必要があること確認する、すべてのフェデレーション パートナー (パーティの信頼をリソース組織またはアカウント組織のパートナーの AD fs 証明書利用者によって表されると要求プロバイダー信頼の場合) が新しい証明書を選択します。

### <a name="partners-who-can-not-consume-federation-metadata"></a>パートナーのフェデレーション メタデータを使用しないことができます。
場合は、フェデレーション パートナーは、フェデレーション メタデータを消費することはできません、する必要があります手動で送信する、新しいトークン署名]、[トークン暗号化解除証明書の公開キー。 アカウント (証明書利用者信頼と要求プロバイダー信頼での AD FS で表されます) 組織のパートナーまたはリソース組織のすべてを新しい証明書公開キー (.cer ファイルまたは .p7b をチェーン全体を含めたい場合) を送信します。 新しい証明書を信頼する側の変更を実装パートナーが存在します。

### <a name="promote-to-primary-if-autocertificaterollover-is-false"></a>(AutoCertificateRollover が False の場合)、プライマリに昇格します。
場合**AutoCertificateRollover**に設定されている**False**AD FS が自動的に生成されていない、またはトークンの署名またはトークン復号化証明書の新規の使用を開始します。 これらのタスクを手動で実行する必要があります。
新しいセカンダリ証明書を使用するフェデレーション パートナーのすべてのための十分な期間があるので、プライマリ (、MMC スナップインで、セカンダリ トークン署名証明書をクリックし、操作 ウィンドウで次のようにクリックします。 このセカンダリ証明書を昇格させます。**プライマリとして設定**)。

## <a name="updating-azure-ad"></a>Azure AD を更新しています
AD FS は、既存の AD DS 資格情報を使用してユーザーを認証することによって、Office 365 などの Microsoft クラウド サービスへのシングル サインオン アクセスを提供します。  証明書の使用の詳細については、次を参照してください。 [Office 365 と Azure AD のフェデレーション証明書を書き換える](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-o365-certs)します。