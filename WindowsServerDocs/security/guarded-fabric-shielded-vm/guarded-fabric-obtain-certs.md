---
title: HGS の証明書を取得する
ms.topic: article
ms.assetid: f4b4d1a8-bf6d-4881-9150-ddeca8b48038
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 09/25/2019
ms.openlocfilehash: 995a115b9e611500732e4674880ee4ca4b204e14
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87989115"
---
# <a name="obtain-certificates-for-hgs"></a>HGS の証明書を取得する

>適用対象: windows server 2019、Windows Server (半期チャネル)、Windows Server 2016

HGS を展開するときに、シールドされた VM を起動するために必要な機密情報を保護するために使用される署名証明書と暗号化証明書を入力するよう求められます。
これらの証明書は HGS から離脱されることはなく、実行しているホストが正常であることがわかっている場合にのみ、シールドされた VM キーの暗号化解除に使用されます。
テナント (VM 所有者) は、証明書の公開半分を使用して、シールドされた Vm を実行するデータセンターを承認します。
このセクションでは、HGS で互換性のある署名証明書と暗号化証明書を取得するために必要な手順について説明します。

## <a name="request-certificates-from-your-certificate-authority"></a>証明機関から証明書を要求する

必須ではありませんが、信頼された証明機関から証明書を取得することを強くお勧めします。
これにより、VM の所有者は、シールドされた Vm を実行するために、正しい HGS サーバー (つまり、サービスプロバイダーまたはデータセンター) を承認しているかどうかを確認できます。
エンタープライズシナリオでは、独自のエンタープライズ CA を使用してこれらの証明書を発行することもできます。
ホストとサービスプロバイダーでは、よく知られているパブリック CA の使用を検討する必要があります。

署名証明書と暗号化証明書は、どちらも次の certificiate プロパティを使用して発行する必要があります ("推奨" とマークされていない場合)。

証明書テンプレートのプロパティ | 必須値
------------------------------|----------------
暗号化プロバイダー               | 任意のキー格納プロバイダー (KSP)。 従来の暗号化サービスプロバイダー (Csp) はサポートされて**いません**。
キーアルゴリズム                 | RSA
最小キー サイズ              | 2048 ビット
署名アルゴリズム           | 推奨: SHA256
キー使用法                     | デジタル署名*とデータの*暗号化
拡張キー使用法            | サーバー認証
キー更新ポリシー            | 同じキーで更新します。 異なるキーを使用して HGS 証明書を更新すると、シールドされた Vm を起動できなくなります。
サブジェクト名                  | 推奨: 会社の名前または web アドレス。 この情報は、シールドデータファイルウィザードで VM の所有者に表示されます。

これらの要件は、ハードウェアまたはソフトウェアによってサポートされる証明書を使用するかどうかによって適用されます
セキュリティ上の理由から、秘密キーがシステムからコピーされないようにするには、ハードウェアセキュリティモジュール (HSM) で HGS キーを作成することをお勧めします。
HSM ベンダーからのガイダンスに従って、上記の属性で証明書を要求し、すべての HGS ノードに HSM KSP をインストールして承認します。

すべての HGS ノードは、同じ署名証明書と暗号化証明書にアクセスする必要があります。
ソフトウェアベースの証明書を使用している場合は、パスワードを使用して証明書を PFX ファイルにエクスポートし、HGS で証明書を管理できるようにすることができます。
また、各 HGS ノードのローカルコンピューターの証明書ストアに証明書をインストールし、HGS に拇印を指定することもできます。
両方のオプションについては、「 [HGS クラスターの初期化](guarded-fabric-initialize-hgs.md)」を参照してください。

## <a name="create-self-signed-certificates-for-test-scenarios"></a>テストシナリオ用に自己署名証明書を作成する

HGS ラボ環境を作成していて、または証明機関を使用する必要がない場合は、自己署名証明書を作成できます。
シールドデータファイルウィザードで証明書情報をインポートするときに警告が表示されますが、すべての機能は同じままです。

自己署名証明書を作成して PFX ファイルにエクスポートするには、PowerShell で次のコマンドを実行します。

```powershell
$certificatePassword = Read-Host -AsSecureString -Prompt "Enter a password for the PFX file"

$signCert = New-SelfSignedCertificate -Subject "CN=HGS Signing Certificate"
Export-PfxCertificate -FilePath .\signCert.pfx -Password $certificatePassword -Cert $signCert
Remove-Item $signCert.PSPath

$encCert = New-SelfSignedCertificate -Subject "CN=HGS Encryption Certificate"
Export-PfxCertificate -FilePath .\encCert.pfx -Password $certificatePassword -Cert $encCert
Remove-Item $encCert.PSPath
```

## <a name="request-an-ssl-certificate"></a>SSL 証明書を要求する

Hyper-v ホストと HGS の間で送信されるすべてのキーと機密情報はメッセージレベルで暗号化されます。つまり、この情報は、HGS または Hyper-v に知られているキーを使用して暗号化されるので、だれかがネットワークトラフィックをスニッフィングして Vm にキーを盗むことを防ぐことができます。
ただし、コンプライアンス reqiurements がある場合、または Hyper-v と HGS 間のすべての通信を暗号化する場合は、トランスポートレベルですべてのデータを暗号化する SSL 証明書を使用して HGS を構成することができます。

Hyper-v ホストと HGS ノードはどちらも、指定した SSL 証明書を信頼する必要があるため、エンタープライズ証明機関から SSL 証明書を要求することをお勧めします。 証明書を要求するときは、次のものを指定してください。

SSL 証明書のプロパティ | 必須値
-------------------------|---------------
サブジェクト名             | HGS クラスターの名前 (分散ネットワーク名または仮想コンピューターオブジェクトの FQDN と呼ばれます)。 これは、に指定された HGS サービス名と HGS ドメイン名を連結したものになり `Initialize-HgsServer` ます。
サブジェクト代替名 | 別の DNS 名を使用して HGS クラスターに接続する場合は (たとえば、ロードバランサーの背後にある場合)、証明書要求の SAN フィールドにこれらの DNS 名を含めてください。

HGS サーバーを初期化するときにこの証明書を指定するためのオプションについては、「[最初の hgs ノードの構成](guarded-fabric-initialize-hgs.md)」を対象としています。
また、 [HgsServer](/powershell/module/hgsserver/set-hgsserver?view=win10-ps)コマンドレットを使用して、後で SSL 証明書を追加または変更することもできます。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [HGS のインストール](guarded-fabric-choose-where-to-install-hgs.md)