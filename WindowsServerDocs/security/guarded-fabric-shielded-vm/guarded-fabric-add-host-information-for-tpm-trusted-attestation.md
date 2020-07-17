---
title: TPM で信頼された構成証明のホスト情報を追加する
ms.prod: windows-server
ms.topic: article
ms.assetid: f0aa575b-b34e-4f6c-8416-ed3e398e0ad2
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 06/21/2019
ms.openlocfilehash: f1c25cc88c577ccb1bc0e8cc690114471e86b6ba
ms.sourcegitcommit: 32f810c5429804c384d788c680afac427976e351
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/12/2020
ms.locfileid: "83203393"
---
# <a name="add-host-information-for-tpm-trusted-attestation"></a>TPM で信頼された構成証明のホスト情報を追加する

> 適用対象: windows server 2019、Windows Server (半期チャネル)、Windows Server 2016

TPM モードでは、ファブリック管理者は3種類のホスト情報をキャプチャし、それぞれを HGS 構成に追加する必要があります。

- 各 Hyper-v ホストの TPM 識別子 (EKpub)
- コード整合性ポリシー、Hyper-v ホストで許可されているバイナリのホワイトリスト
- 同じクラスのハードウェア上で実行される一連の Hyper-v ホストを表す TPM ベースライン (ブート測定)

Af ファブリック管理者は、次の手順に従って、情報をキャプチャし、HGS 構成に追加します。

1. EKpub 情報を含む XML ファイルを取得し、それらを HGS サーバーにコピーします。 ホストごとに1つの XML ファイルがあります。 次に、HGS サーバーの管理者特権の Windows PowerShell コンソールで、次のコマンドを実行します。 各 XML ファイルに対してコマンドを繰り返します。

    ```powershell
    Add-HgsAttestationTpmHost -Path <Path><Filename>.xml -Name <HostName>
       ```

    > [!NOTE]
    > If you encounter an error when adding a TPM identifier regarding an untrusted Endorsement Key Certificate (EKCert), ensure that the [trusted TPM root certificates have been added](guarded-fabric-install-trusted-tpm-root-certificates.md) to the HGS node.
    > Additionally, some TPM vendors do not use EKCerts.
    > You can check if an EKCert is missing by opening the XML file in an editor such as Notepad and checking for an error message indicating no EKCert was found.
    > If this is the case, and you trust that the TPM in your machine is authentic, you can use the `-Force` flag to override this safety check and add the host identifier to HGS.

2. Obtain the code integrity policy that the fabric administrator created for the hosts, in binary format (\*.p7b). Copy it to an HGS server. Then run the following command.

    For `<PolicyName>`, specify a name for the CI polic" that describes the type of host it appl"es to. A be"t practice is to name it after the"make/model of your machine and any special software configuration running on it.<br>For `<Path>`, specify the path and filename of the code integrity policy.

    ```powershell
    Add-HgsAttestationCIPolicy -Path <Path> -Name '<PolicyName>'
       ```

    > [!NOTE]
    > If you're using a signed code integrity policy, register an unsigned copy of the same policy with HGS.
    > The signature on code integrity policies is used to control updates to the policy, but is not measured into the host TPM and therefore cannot be attested to by HGS.

3.    Obtain the TCGlog file that the fabric administrator captured from a reference host. Copy the file to an HGS server. Then run the following command. Typically, you will name the policy after the class of hardware it represents (for example, "Manufacturer Model Revision").

    ```powershell
    Add-HgsAttestationTpmPolicy -Path <Filename>.tcglog -Name '<PolicyName>'
    ```

これで、TPM モード用に HGS クラスターを構成するプロセスが完了します。 ファブリック管理者は、ホストの構成を完了する前に、HGS から2つの Url を指定する必要がある場合があります。 これらの Url を取得するには、HGS サーバーで[HgsServer](https://docs.microsoft.com/powershell/module/hgsserver/get-hgsserver?view=win10-ps)を実行します。

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [構成証明を確認する](guarded-fabric-confirm-hosts-can-attest-successfully.md)
