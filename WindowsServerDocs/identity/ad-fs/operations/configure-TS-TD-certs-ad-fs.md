---
title: "取得し、AD FS のトークン署名やトークン暗号化解除証明書を構成します。"
description: "このドキュメントを取得し、TS と TD を構成する方法について説明の AD FS の証明書"
author: jenfieldmsft
ms.author: billmath
manager: samueld
ms.date: 10/23/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 0d7f8ba4efb74a377f9f9d748949a934398ebefc
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="obtain-and-configure-ts-and-td-certificates-for-ad-fs"></a>取得し、TS と TD 証明書を AD FS の構成

このトピックでは、タスクと、AD FS トークン署名やトークン暗号化解除証明書が最新の状態であることを確認するときに実行する手順について説明します。

トークン署名証明書は標準の X509 証明書を安全にフェデレーション サーバーが発行するすべてのトークンの署名に使用します。 トークン暗号化解除証明書は、標準の X509 証明書されたトークンの暗号化を解除するために使用されます。 フェデレーション メタデータにも公開します。

詳細についてを参照してください[証明書の要件。](../design/ad-fs-requirements.md#BKMK_1)

## <a name="determine-whether-ad-fs-renews-the-certificates-automatically"></a>AD FS が自動的に証明書を更新するかどうかを判断します。
既定では、AD FS は、初期構成時と証明書は、有効期限に近づいているときにトークン署名やトークン暗号化解除証明書を自動的に生成するように構成します。

次の Windows PowerShell コマンドを実行することができます:`Get-AdfsProperties`します。
  
  ![Get-ADFSProperties](media/configure-TS-TD-certs-ad-fs/ts1.png)
  
AutoCertificateRollover プロパティは、更新トークン署名証明書とトークン暗号化証明書を自動的に解除する AD FS が構成されているかどうかについて説明します。

AutoCertificateRollover が TRUE に設定されている場合、AD FS 証明書を更新して、AD FS で自動的に構成できます。 新しい証明書を構成した後、システム停止を回避するために必要がありますを確認する各フェデレーション パートナー (要求プロバイダー信頼または証明書利用者信頼のいずれかによって、AD FS ファームで表される) は、この新しい証明書で更新します。
    
AD FS のトークン署名の更新に構成され、トークンがない場合は、証明書の暗号化を解除を自動的に (場合 AutoCertificateRollover を False に設定)、AD FS を自動的に生成または新しいトークン署名や証明書の暗号化を解除トークンの使用を開始します。 これらのタスクを手動で実行する必要があります。
    
更新トークン署名証明書とトークン暗号化証明書を自動的に解除する AD FS が構成されている場合 (AutoCertificateRollover を TRUE に設定) 更新ときを決定することができます。

CertificateGenerationThreshold では、証明書の後ではなく日付を前もってお客様に何日間、新しい証明書は生成されたについて説明します。

CertificatePromotionThreshold 何日後に、新しい証明書が生成されたプライマリ証明書に昇格することを決定する (つまり、AD FS は使い始めることを発行するトークンに署名し、id プロバイダーからトークン暗号化解除) します。

![Get-ADFSProperties](media/configure-TS-TD-certs-ad-fs/ts2.png)
  
更新トークン署名証明書とトークン暗号化証明書を自動的に解除する AD FS が構成されている場合 (AutoCertificateRollover を TRUE に設定) 更新ときを決定することができます。

 - **CertificateGenerationThreshold**証明書の後ではなく日付を前もってお客様に何日間、新しい証明書は生成されたについて説明します。
 - **CertificatePromotionThreshold**何日後に、新しい証明書が生成されたプライマリ証明書に昇格することを決定する (つまり、AD FS は開始発行トークンに署名し、ユーザーからのトークン暗号化解除に使用します。プロバイダー)。

## <a name="determine-when-the-current-certificates-expire"></a>現在の証明書の有効期限が切れる決定します。
プライマリのトークン署名と証明書の暗号化を解除トークンを識別し、現在の証明書の有効期限が切れるを決定する、次の手順を使用することができます。

次の Windows PowerShell コマンドを実行することができます: `Get-AdfsCertificate –CertificateType token-signing` (または`Get-AdfsCertificate –CertificateType token-decrypting `)。 または、MMC の現在の証明書を確認することができます。サービスに証明書]-> [します。

![Get-ADFSCertificate](media/configure-TS-TD-certs-ad-fs/ts3.png)

証明書を**IsPrimary**値に設定されて**True**は AD FS が現在使用している証明書。

に対して表示される日、**後ではなく**日付を新しいプライマリ トークン署名や証明書を復号化を構成する必要があります。

サービスの継続性を確保するには、新しいトークン署名し、この有効期限の前に、トークン暗号化解除証明書を (証明書利用者信頼または要求プロバイダー信頼のいずれかによって、AD FS ファームで表される) のすべてのフェデレーション パートナーが消費する必要があります。 60 日間以上を事前にこのプロセスの計画を開始することをお勧めします。

## <a name="generating-a-new-self-signed-certificate-manually-prior-to-the-end-of-the-grace-period"></a>猶予期間の終了前に手動で新しい自己署名証明書を生成します。
次の手順を使用するには、猶予期間の終了前に手動で新しい自己署名証明書を生成します。

1. プライマリの AD FS サーバーにログオンしていることを確認します。
2. Windows PowerShell を開き、次のコマンドを実行します。 `Add-PSSnapin "microsoft.adfs.powershell"`
3. 必要に応じて、AD FS で現在の署名証明書を確認することができます。 これを行うには、次のコマンドを実行します:`Get-ADFSCertificate –CertificateType token-signing`します。 表示されているすべての証明書の後ではなく日付を表示するコマンドの出力を確認します。
4. 新しい証明書を生成するには、更新し、AD FS サーバーの証明書を更新するには、次のコマンドを実行します:`Update-ADFSCertificate –CertificateType token-signing`します。
5. 次のコマンドをもう一度実行して、更新プログラムを確認します。 `Get-ADFSCertificate –CertificateType token-signing`
6. 次の 2 つの証明書を今すぐに表示されるはず、その 1 つが、**後ではなく**を約 1 年、将来の日付、**IsPrimary**値は**False**します。

>[!IMPORTANT]
>サービスの停止を回避するには、有効なトークン署名証明書で Azure AD を更新する方法で手順を実行して Azure AD の証明書情報を更新します。

## <a name="if-youre-not-using-self-signed-certificates"></a>自己署名証明書を使用していない場合.
使用していない、既定で自動的に生成される、自己署名トークン署名およびトークン暗号化解除証明書の場合は、更新およびこれらの証明書を手動で構成する必要があります。

まず、証明機関から新しい証明書を取得し、各フェデレーション サーバーでローカル コンピューターの個人用証明書ストアにインポートする必要があります。 手順については、次を参照してください。、[証明書をインポート](https://technet.microsoft.com/library/cc754489.aspx)記事です。

[このとしてセカンダリ AD FS トークン署名証明書または暗号化解除証明書を構成する必要があります。 (として構成すること、フェデレーション パートナーをプライマリ証明書に昇格する前に、この新しい証明書を利用するための十分な時間を許可するように、セカンダリ証明書)。

### <a name="to-configure-a-new-certificate-as-a-secondary-certificate"></a>セカンダリ証明書と新しい証明書を構成するには
1. PowerShell を開き、次を実行します。 `Set-ADFSProperties -AutoCertificateRollover $false`
2. 1 回、証明書をインポートしました。 開いている、**AD FS 管理**コンソール。
3. 展開**サービス**し、[**証明書**します。
4. [操作] ウィンドウで、をクリックして**追加トークン署名証明書**します。
![Get-ADFSCertificate](media/configure-TS-TD-certs-ad-fs/ts4.png)</br>
5. 表示されている証明書の一覧から、新しい証明書を選択し、[OK] をクリックします。
6.  PowerShell を開き、次を実行します。 `Set-ADFSProperties -AutoCertificateRollover $true`

>[!WARNING]
>新しい証明書に関連付けられている秘密キーを確認し、秘密キーにアクセス許可を読み取り、AD FS サービス アカウントが付与されています。 各フェデレーション サーバーでこれを確認します。 ためには、証明書スナップインで、新しい証明書を右クリックしてすべてのタスク]、[秘密キーの管理] をクリックします。

フェデレーション パートナー (フェデレーション メタデータを取得、または新しい証明書の公開キーを送信する) 新しい証明書を使用するための十分な時間のことを許可した後プライマリ証明書をセカンダリ証明書を昇格する必要があります。

### <a name="to-promote-the-new-certificate-from-secondary-to-primary"></a>プライマリ セカンダリから、新しい証明書に昇格するには

1. 開いている、**AD FS 管理**コンソール。
2. 展開**サービス**し、[**証明書**します。
3. セカンダリのトークン署名証明書をクリックします。
4. **アクション**] ウィンドウで、をクリックして**プライマリとして設定**します。 確認プロンプトで、[はい] をクリックします。
![Get-ADFSCertificate](media/configure-TS-TD-certs-ad-fs/ts5.png)</br>


## <a name="updating-federation-partners"></a>フェデレーション パートナーの更新

### <a name="partners-who-can-consume-federation-metadata"></a>パートナー フェデレーション メタデータを使用することができます。
場合がある更新して、新しいトークン署名やトークン暗号化解除証明書を構成する必要があること確認する、すべてのフェデレーション パートナー (リソース組織またはアカウント組織パートナーの AD fs 証明書利用者によって表されているパーティーの信頼と要求プロバイダー信頼) は、新しい証明書をくっついていません。

### <a name="partners-who-can-not-consume-federation-metadata"></a>パートナー フェデレーション メタデータを使用することはできません。
場合は、フェデレーション パートナーは、フェデレーション メタデータを消費することはできません、する必要があります手動で送信する、新しいトークン署名/トークン暗号化解除証明書の公開キー。 新しいの証明書の公開キーの送信 (.cer ファイルまたは .p7b チェーン全体を含めるにする場合) をリソース組織またはアカウント組織のパートナーのすべて (の AD fs 証明書利用者によって表されるパーティー信頼し、要求プロバイダー信頼関係)。 新しい証明書を信頼する側の変更を実装するパートナーが存在します。

### <a name="promote-to-primary-if-autocertificaterollover-is-false"></a>(AutoCertificateRollover が False の場合)、プライマリに昇格させる
場合**AutoCertificateRollover**に設定されている**False**AD FS が自動的に生成されていない、または新しいスタート画面を使用してトークンの署名または暗号化の解除証明書をトークンします。 これらのタスクを手動で実行する必要があります。
すべてのフェデレーション パートナーを新しいセカンダリ証明書を利用するための十分な期間を許可した後で、MMC スナップインで、[セカンダリのトークン署名証明書をクリックし、操作ウィンドウで、[プライマリ セカンダリこの証明書の販売促進します。**プライマリとして設定**.)

## <a name="updating-azure-ad"></a>Azure AD の更新
AD FS は、経由、既存の AD DS 資格情報でユーザーを認証することによって、Office 365 などの Microsoft クラウド サービスへのシングル サインオン アクセスを提供します。  証明書の使用の詳細については、次を参照してください。[Office 365 と Azure AD のフェデレーションの証明書を書き換える](https://docs.microsoft.com/en-us/azure/active-directory/connect/active-directory-aadconnect-o365-certs)します。