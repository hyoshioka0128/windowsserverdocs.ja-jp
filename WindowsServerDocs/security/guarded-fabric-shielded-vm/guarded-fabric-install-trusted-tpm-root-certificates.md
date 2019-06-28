---
title: 信頼済み TPM ルート証明書をインストールします。
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 06/27/2019
ms.openlocfilehash: 0d42befcfacfffd302cfcb27f9f3c2c973534398
ms.sourcegitcommit: 2c2c37170c65434179bcf2989d557f97dcbe1b9f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2019
ms.locfileid: "67419230"
---
# <a name="install-trusted-tpm-root-certificates"></a>信頼済み TPM ルート証明書をインストールします。

>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016

TPM 構成証明を使用するように HGS を構成するときに、サーバーで Tpm のベンダーを信頼するように HGS を構成する必要があります。
この余分な検証プロセスでは、のみ、信頼できる Tpm は、HGS を証明することにより、します。
信頼されていない TPM の登録を試みる場合`Add-HgsAttestationTpmHost`、TPM ベンダーが信頼されていないことを示すエラーが表示されます。

を、Tpm を信頼するには、ルートとでは、サーバーの Tpm 保証キーの署名に使用される中間の署名証明書は、HGS にインストールする必要があります。
データ センターでは、複数の TPM モデルを使用する場合は、モデルごとに異なる証明書をインストールする必要があります。
HGS は"TrustedTPM_RootCA"になり、仕入先の証明書の"TrustedTPM_IntermediateCA"証明書を格納します。

> [!NOTE]
> TPM ベンダーの証明書は、既定では Windows にインストールされているものとは異なる特定のルートと TPM ベンダーで使用される中間証明書を表します。

信頼済み TPM ルートおよび中間証明書のコレクションは便宜を図るマイクロソフトによって発行されました。
次の手順を使用して、これらの証明書をインストールすることができます。
TPM 証明書は、以下のパッケージには含まれません、ルートと、特定の TPM モデルの中間証明書を取得するには、TPM ベンダーやサーバー OEM にお問い合わせください。

次の手順を繰り返します**HGS サーバーがすべて**:

1.  最新パッケージをダウンロード[ https://go.microsoft.com/fwlink/?linkid=2097925](https://go.microsoft.com/fwlink/?linkid=2097925)します。

2.  信頼性を保証する cab ファイルの署名を確認します。 署名が有効でない場合は、続行しないでください。

    ```powershell
    Get-AuthenticodeSignature .\TrustedTpm.cab
    ```
    
    次に出力の例を示します。
    
    ```
    Directory: C:\Users\Administrator\Downloads
        
    SignerCertificate                         Status                                 Path
    -----------------                         ------                                 ----
    0DD6D4D4F46C0C7C2671962C4D361D607E370940  Valid                                  TrustedTpm.cab
    ```

2.  Cab ファイルを展開します。

    ```
    mkdir .\TrustedTPM
    expand.exe -F:* <Path-To-TrustedTpm.cab> .\TrustedTPM
    ```

3.  既定では、構成スクリプトはすべて TPM ベンダーの証明書をインストールします。 特定の TPM ベンダーの証明書をインポートする場合は、組織によって信頼されていない TPM ベンダーのフォルダーを削除します。

4.  信頼された証明書パッケージをインストールするには、展開したフォルダーで、セットアップ スクリプトを実行します。

    ```
    cd .\TrustedTPM
    .\setup.cmd
    ```

新しい証明書またはそれ以前のインストール中にスキップ意図的に追加するを HGS クラスター内のすべてのノードで上記の手順を繰り返します。
既存の証明書信頼されたままになりますが、展開された cab ファイルを新しい証明書を信頼済み TPM に追加されますを格納します。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [ファブリック DNS の構成](guarded-fabric-configuring-fabric-dns-tpm.md)



