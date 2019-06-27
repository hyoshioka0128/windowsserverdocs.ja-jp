---
title: TPM によって信頼された構成証明書のホスト情報を追加します。
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: f0aa575b-b34e-4f6c-8416-ed3e398e0ad2
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 06/21/2019
ms.openlocfilehash: 99be11bfec02924f93d9f759676e1eea364daa18
ms.sourcegitcommit: 545dcfc23a81943e129565d0ad188263092d85f6
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2019
ms.locfileid: "67407638"
---
>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016

### <a name="add-host-information-for-tpm-trusted-attestation"></a>TPM によって信頼された構成証明書のホスト情報を追加します。

TPM モードでは、ファブリック管理者は、キャプチャの 3 種類のホストについては、それぞれの HGS の構成に追加する必要があります。

- 各 HYPER-V ホストの TPM id (EKpub)
- コード整合性ポリシーでは、HYPER-V ホスト用に許可されているバイナリのホワイト リスト
- HYPER-V のセットを表す TPM ベースライン (ブート測定値) をホスト ハードウェアと同じクラス上で実行されます。

次の手順に従って HGS の構成に追加後、ファブリック管理者は、情報をキャプチャしてください。

1. EKpub 情報が含まれてし、HGS サーバーにコピーする XML ファイルを取得します。 ホストごとに 1 つの XML ファイルがあります。 次に、HGS サーバーで管理者特権で Windows PowerShell コンソールでは、次のコマンドを実行します。 XML ファイルの各コマンドを繰り返します。

    ```powershell
    Add-HgsAttestationTpmHost -Path <Path><Filename>.xml -Name <HostName>
    ```

    > [!NOTE]
    > 場合は、信頼されていない保証キー証明書 (EKCert) に関する TPM id を追加するときにエラーが発生したことを確認します。、 [TPM ルート証明書が追加されている信頼された](guarded-fabric-install-trusted-tpm-root-certificates.md)HGS ノードにします。
    > さらに、一部の TPM ベンダーでは、EKCerts は使用しないでください。
    > メモ帳などのエディターで XML ファイルを開いて、EKCert が不足していると、EKCert がないことを示すエラー メッセージの確認が見つかったかどうかを確認できます。
    > これは、ケース、および信頼すること、コンピューターで TPM が認証済みで、使用することができる場合、`-Force`この安全性チェックをオーバーライドし、HGS をホストの識別子を追加するフラグ。

2. バイナリ形式で、ホストのファブリック管理者が作成したコード整合性ポリシーの取得 (\*.p7b)。 HGS サーバーにコピーします。 次のコマンドを実行します。

    `<PolicyName>`に適用されるホストの種類を記述する CI ポリシーの名前を指定します。 しているコンピューターで実行される特別なソフトウェア構成の型/モデルの後に名前を付けることをお勧めします。<br>`<Path>`、コード整合性ポリシーのファイル名とパスを指定します。

    ```powershell
    Add-HgsAttestationCIPolicy -Path <Path> -Name '<PolicyName>'
    ```
    
    > [!NOTE]
    > 符号付きのコード整合性ポリシーを使用している場合、同じポリシーの符号なしのコピーを HGS に登録します。
    > コード整合性ポリシーの署名は、ポリシーの更新プログラムの制御に使用されるホストの TPM には測定されませんいて、したがって HGS によってを証明することはできません。

3. 参照をホストから、ファブリック管理者がキャプチャされる TCGlog ファイルを取得します。 HGS サーバーにファイルをコピーします。 次のコマンドを実行します。 通常、(たとえば、「製造元のモデルのバージョン」) のハードウェアを表すクラスの後に、ポリシーに名前をされます。

    ```powershell
    Add-HgsAttestationTpmPolicy -Path <Filename>.tcglog -Name '<PolicyName>'
    ```

これは、TPM モード、HGS クラスターを構成するプロセスを完了します。 ファブリック管理者は、ホストの構成を完了する前に、HGS から 2 つの Url を指定する必要があります。 これらを取得する Url、HGS サーバーで、次のように実行します。 [Get HgsServer](https://docs.microsoft.com/powershell/module/hgsserver/get-hgsserver?view=win10-ps)します。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [構成証明を確認する](guarded-fabric-confirm-hosts-can-attest-successfully.md)
