---
title: TPM で信頼された構成証明のホスト情報を追加する
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: f0aa575b-b34e-4f6c-8416-ed3e398e0ad2
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 06/21/2019
ms.openlocfilehash: 35efca71278c288189819d6c9fc49ba8195d18a1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386820"
---
>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016

### <a name="add-host-information-for-tpm-trusted-attestation"></a>TPM で信頼された構成証明のホスト情報を追加する

TPM モードでは、ファブリック管理者は3種類のホスト情報をキャプチャし、それぞれを HGS 構成に追加する必要があります。

- 各 Hyper-v ホストの TPM 識別子 (EKpub)
- コード整合性ポリシー、Hyper-v ホストで許可されているバイナリのホワイトリスト
- 同じクラスのハードウェア上で実行される一連の Hyper-v ホストを表す TPM ベースライン (ブート測定)

ファブリック管理者が情報をキャプチャしたら、次の手順に従って、その情報を HGS 構成に追加します。

1. EKpub 情報を含む XML ファイルを取得し、それらを HGS サーバーにコピーします。 ホストごとに1つの XML ファイルがあります。 次に、HGS サーバーの管理者特権の Windows PowerShell コンソールで、次のコマンドを実行します。 各 XML ファイルに対してコマンドを繰り返します。

    ```powershell
    Add-HgsAttestationTpmHost -Path <Path><Filename>.xml -Name <HostName>
    ```

    > [!NOTE]
    > 信頼されていない保証キー証明書 (EKCert) に関する TPM 識別子を追加するときにエラーが発生した場合は、[信頼された tpm ルート証明書が HGS ノードに追加され](guarded-fabric-install-trusted-tpm-root-certificates.md)ていることを確認します。
    > また、一部の TPM ベンダーは EKCerts を使用しません。
    > EKCert がないかどうかを確認するには、メモ帳などのエディターで XML ファイルを開き、EKCert が見つからなかったことを示すエラーメッセージがないかどうかを確認します。
    > この場合、コンピューターの TPM が本物であることを信頼している場合は、`-Force` フラグを使用してこの安全性チェックを無効にし、ホスト id を HGS に追加することができます。

2. ホスト用にファブリック管理者が作成したコード整合性ポリシーをバイナリ形式 (@no__t 横-0. p7b) で取得します。 それを HGS サーバーにコピーします。 その後、次のコマンドを実行します。

    @No__t-0 の場合は、適用先のホストの種類を示す CI ポリシーの名前を指定します。 ベストプラクティスとしては、コンピューターのメーカー/モデルの後に名前を指定し、それを実行する特別なソフトウェア構成を指定することをお勧めします。<br>@No__t-0 の場合は、コード整合性ポリシーのパスとファイル名を指定します。

    ```powershell
    Add-HgsAttestationCIPolicy -Path <Path> -Name '<PolicyName>'
    ```
    
    > [!NOTE]
    > 署名済みのコード整合性ポリシーを使用している場合は、HGS と同じポリシーの署名されていないコピーを登録します。
    > コード整合性ポリシーの署名は、ポリシーの更新を制御するために使用されますが、ホスト TPM には測定されないため、HGS で証明することはできません。

3. ファブリック管理者が参照ホストからキャプチャした TCGlog ファイルを取得します。 ファイルを HGS サーバーにコピーします。 その後、次のコマンドを実行します。 通常、ポリシーには、それが表すハードウェアのクラス (たとえば、"製造元のモデルのリビジョン") の後に名前を指定します。

    ```powershell
    Add-HgsAttestationTpmPolicy -Path <Filename>.tcglog -Name '<PolicyName>'
    ```

これで、TPM モード用に HGS クラスターを構成するプロセスが完了します。 ファブリック管理者は、ホストの構成を完了する前に、HGS から2つの Url を指定する必要がある場合があります。 これらの Url を取得するには、HGS サーバーで[HgsServer](https://docs.microsoft.com/powershell/module/hgsserver/get-hgsserver?view=win10-ps)を実行します。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [構成証明を確認する](guarded-fabric-confirm-hosts-can-attest-successfully.md)
