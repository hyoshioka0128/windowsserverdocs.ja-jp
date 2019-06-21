---
title: HGS で必要な TPM モード情報をキャプチャします。
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 915b1338-5085-481b-8904-75d29e609e93
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 04/01/2019
ms.openlocfilehash: 24d81e3d2c31b3493563f3f3e2ab3f92afff2c06
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67284137"
---
# <a name="authorize-guarded-hosts-using-tpm-based-attestation"></a>TPM ベースの構成証明を使用して保護されたホストを承認します。

>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016

TPM のモードには、TPM の識別子が使用されます (プラットフォームの識別子または保証キーとも呼ばれます\[EKpub\])"で保護されます。"として、特定のホストが承認されたかどうかを決定するを開始するには。 構成証明書のこのモードでは、セキュア ブートとコードの整合性の測定値を使用して、特定の HYPER-V ホストが正常な状態があり、信頼されたコードだけが実行されていることを確認します。 構成証明書が正常でないと何を理解するためには、次の成果物をキャプチャする必要があります。

1.  TPM の識別子 (EKpub)

    -  この情報は各 HYPER-V ホストに一意です。

2.  TPM ベースライン (ブート測定値)

    -  これは、同じクラスのハードウェア上で実行されるすべての HYPER-V ホストに適用されます。

3.  コード整合性ポリシー (許可されているバイナリのホワイト リスト)

    -  これは一般的なハードウェアおよびソフトウェアを共有するすべての HYPER-V ホストに適用されます。

ベースラインおよび CI ポリシーから「参照ホスト」を把握することをお勧めします。 各データ センター内の Hyper-v ハードウェアの構成の一意のクラスの担当者は。 Windows Server バージョン 1709 以降では、CI ポリシーのサンプルが C:\Windows\schemas\CodeIntegrity\ExamplePolicies に含まれています。 

## <a name="versioned-attestation-policies"></a>バージョン管理された構成証明書ポリシー

Windows Server 2019 構成証明書と呼ばれる新しいメソッドが導入されています*v2 構成証明*を TPM の証明書が、EKPub を HGS に追加するために存在する必要があります。 Windows Server 2016 で使用される v1 の構成証明方法を指定することで、この安全性チェックをオーバーライドできますを許可されている Force フラグは、成果物をキャプチャするには、追加 HgsAttestationTpmHost またはその他の TPM 構成証明のコマンドレットを実行するとします。 以降では、Windows Server 2019 は、v2 の構成証明書が既定で使用し、証明書なしの TPM を登録する必要がある場合、追加 HgsAttestationTpmHost を実行するときに、PolicyVersion - v1 のフラグを指定する必要があります。 -Force フラグは、v2 の構成証明書では機能しません。 

ホストすべてに証明できるだけの成果物 (EKPub + TPM ベースライン + CI ポリシー) 構成証明書の同じバージョンを使用します。 V2 の構成証明は最初に試行し、失敗した場合、v1 の構成証明書が使用されます。 つまり、v1 の構成証明を使用して TPM id を登録する必要がある場合も、TPM ベースラインをキャプチャして CI ポリシーを作成するときに、v1 の構成証明を使用する - PolicyVersion v1 フラグを指定する必要があります。 TPM の証明書がない保護されたホストを追加する必要がある後でし、TPM ベースラインおよび CI ポリシーは、v2 の構成証明を使用して作成された場合、PolicyVersion - v1 のフラグを使用して各成果物を再作成する必要があります。 

## <a name="capture-the-tpm-identifier-platform-identifier-or-ekpub-for-each-host"></a>各ホストの TPM id (プラットフォームの識別子または EKpub) をキャプチャします。

1.  ファブリックのドメインに各ホスト上の TPM が使用できる状態 - は、TPM が初期化され、所有権の取得を確認します。 TPM の状態を確認するを TPM 管理コンソール (tpm.msc) を開くかを実行して**Get Tpm**管理者特権の Windows PowerShell ウィンドウでします。 TPM がない場合、**準備**状態では、それを初期化し、その所有権を設定する必要があります。 これ行う TPM 管理コンソールで、またはを実行して**Initialize Tpm**します。

2.  保護された各ホストでは、その EKpub を取得する管理者特権での Windows PowerShell コンソールで、次のコマンドを実行します。 `<HostName>`でこのホストを識別するために適切な一意のホスト名に置き換えて、- のホスト名または名前 (該当する場合)、fabric インベントリ サービスで使用できます。 便宜上、ホストの名前を使用して出力ファイルを名前します。

    ```powershell
    (Get-PlatformIdentifier -Name '<HostName>').InnerXml | Out-file <Path><HostName>.xml -Encoding UTF8
    ```
3.  各 XML ファイルに一意の名前を保護されたホストとなる各ホストには、上記の手順を繰り返します。

4.  結果の XML ファイルを HGS 管理者に提供します。

5.  HGS のドメインに、HGS サーバーで管理者特権の Windows PowerShell コンソールを開き、次のコマンドを実行します。 XML ファイルの各コマンドを繰り返します。

    ```powershell
    Add-HgsAttestationTpmHost -Path <Path><Filename>.xml -Name <HostName>
    ```

    > [!NOTE]
    > 場合は、信頼されていない保証キー証明書 (EKCert) に関する TPM id を追加するときにエラーが発生したことを確認します。、 [TPM ルート証明書が追加されている信頼された](guarded-fabric-install-trusted-tpm-root-certificates.md)HGS ノードにします。
    > さらに、一部の TPM ベンダーでは、EKCerts は使用しないでください。
    > メモ帳などのエディターで XML ファイルを開いて、EKCert が不足していると、EKCert がないことを示すエラー メッセージの確認が見つかったかどうかを確認できます。
    > これは、ケース、および信頼すること、コンピューターで TPM が認証済みで、使用することができる場合、 `-Force` HGS にホストの識別子を追加するパラメーター。 Windows Server の 2019 でも使用する必要があります、`-PolicyVersion v1`パラメーターを使用する場合`-Force`します。 これには、Windows Server 2016 の動作に一貫性のあるポリシーが作成されを使用する必要があります`-PolicyVersion v1`CI ポリシーとも TPM ベースラインを登録するときにします。

## <a name="create-and-apply-a-code-integrity-policy"></a>作成し、コード整合性ポリシーを適用

コード整合性ポリシーにより、ホスト上で実行する信頼できる実行ファイルのみの実行が許可されていることを確認します。 マルウェアおよびその他の実行可能ファイルの外部の信頼できる実行可能ファイルは実行をされません。

保護されたホストごとには、TPM のモードでシールドされた Vm を実行するために適用されるコード整合性ポリシーが必要です。 HGS に追加することで信頼できる正確なコード整合性ポリシーを指定します。 ポリシーを適用する、ブロック、ポリシーに準拠してまたは単に監査していないソフトウェア (ポリシーで定義されていないソフトウェアが実行されるときに、イベント ログ) は、コード整合性ポリシーを構成できます。 

Windows Server バージョン 1709 以降では、コード整合性ポリシーのサンプルは、C:\Windows\schemas\CodeIntegrity\ExamplePolicies での Windows に含まれています。 Windows Server の 2 つのポリシーが推奨されます。

- **AllowMicrosoft**:Microsoft によって署名されたすべてのファイルを許可します。 SQL や、Exchange などのサーバー アプリケーションでこのポリシーをお勧めマイクロソフトによって発行されたエージェントによって、サーバーを監視する場合またはします。
- **DefaultWindows_Enforced**:Windows に同梱されており、Office などの Microsoft によってリリースされたその他のアプリケーションが認められないファイルにのみ許可します。 組み込みのサーバーの役割と、HYPER-V などの機能のみを実行しているサーバーには、このポリシーを使用することをお勧めします。 

最初かどうかがない、何かを確認する監査 (ログ) モードでの CI ポリシーを作成して実稼働ワークロードをホストのポリシーを適用することをお勧めします。 

使用する場合、[新規 CIPolicy](https://docs.microsoft.com/powershell/module/configci/new-cipolicy?view=win10-ps)独自に生成するコマンドレットのコード整合性ポリシーは、次のように使用する規則レベルを決定する必要があります。 プライマリ レベルをお勧め**パブリッシャー**にフォールバックして**ハッシュ**、署名された CI ポリシーを変更することがなく更新するソフトウェアを最もデジタルことができます。
CI ポリシーを変更することがなくサーバーで、同じ公開元によって作成された新しいソフトウェアをインストールこともできます。
デジタル署名されていない実行可能ファイルがハッシュされる--これらのファイルへの更新プログラムで、新しい CI ポリシーを作成する必要があります。
使用可能な CI ポリシー ルール レベルの詳細については、次を参照してください。[コード整合性ポリシーの展開: ポリシー ルールとファイルの規則](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/select-types-of-rules-to-create#windows-defender-application-control-policy-rules)とコマンドレットのヘルプ。

1.  参照ホストで、新しいコード整合性ポリシーを生成します。 次のコマンドでポリシーの作成、**パブリッシャー**レベルへのフォールバックとともに**ハッシュ**します。 XML ファイルを Windows と HGS を適用し、それぞれ、CI ポリシーを測定する必要があります。 バイナリ ファイル形式に変換します。

    ```powershell
    New-CIPolicy -Level Publisher -Fallback Hash -FilePath 'C:\temp\HW1CodeIntegrity.xml' -UserPEs

    ConvertFrom-CIPolicy -XmlFilePath 'C:\temp\HW1CodeIntegrity.xml' -BinaryFilePath 'C:\temp\HW1CodeIntegrity.p7b'
    ```

    >[!NOTE]
    >上記のコマンドは、監査モードでのみ、CI ポリシーを作成します。 ホストで実行されている権限のないバイナリはブロックされません。 適用されているポリシーは、運用環境でのみ使用する必要があります。

2.  簡単に見つけることはできる場所コード整合性ポリシー ファイル (XML ファイル) を保持します。 CI ポリシーまたはマージの今後の更新プログラムがシステムからの変更を適用するには、後でこのファイルを編集する必要があります。

3.  参照をホストする CI ポリシーが適用されます。

    1.  CI ポリシーを使用するマシンを構成するには、次のコマンドを実行します。 CI ポリシーを展開することもできます。[グループ ポリシー](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/deploy-windows-defender-application-control-policies-using-group-policy)または[System Center Virtual Machine Manager](https://docs.microsoft.com/system-center/vmm/guarded-deploy-host?view=sc-vmm-2019#manage-and-deploy-code-integrity-policies-with-vmm)します。

        ```powershell
        Invoke-CimMethod -Namespace root/Microsoft/Windows/CI -ClassName PS_UpdateAndCompareCIPolicy -MethodName Update -Arguments @{ FilePath = "C:\temp\HW1CodeIntegrity.p7b" }
        ```

    2.  ポリシーを適用するホストを再起動します。

3.  コード整合性ポリシーをテストするには、一般的なワークロードを実行します。 これには、実行されている Vm をファブリック管理エージェント、バックアップ エージェント、またはコンピューターのツールのトラブルシューティングを含めることができます。 コード整合性違反がない場合を確認し、必要に応じて、CI ポリシーを更新します。

4.  強制モードに CI ポリシーを変更するには、更新された CI ポリシー XML ファイルに対して、次のコマンドを実行しています。

    ```powershell
    Set-RuleOption -FilePath 'C:\temp\HW1CodeIntegrity.xml' -Option 3 -Delete

    ConvertFrom-CIPolicy -XmlFilePath 'C:\temp\HW1CodeIntegrity.xml' -BinaryFilePath 'C:\temp\HW1CodeIntegrity_enforced.p7b'
    ```

5.  次のコマンドを使用してすべての (同じハードウェアとソフトウェアの構成) をホストする CI ポリシーが適用されます。

    ```powershell
    Invoke-CimMethod -Namespace root/Microsoft/Windows/CI -ClassName PS_UpdateAndCompareCIPolicy -MethodName Update -Arguments @{ FilePath = "C:\temp\HW1CodeIntegrity.p7b" }
    
    Restart-Computer
    ```

    >[!NOTE]
    >ホストに CI ポリシーを適用するときに、これらのマシン上のソフトウェアの更新時に注意します。 最初、CI ポリシーに準拠している任意のカーネル モード ドライバーすると、コンピューターが起動を妨げる可能性があります。 

6.  バイナリ ファイルを提供する (この例では、HW1CodeIntegrity で\_enforced.p7b) HGS 管理者に。

7.  HGS のドメインでは、HGS サーバーに、コード整合性ポリシーをコピーし、次のコマンドを実行します。

    `<PolicyName>`に適用されるホストの種類を記述する CI ポリシーの名前を指定します。 しているコンピューターで実行される特別なソフトウェア構成の型/モデルの後に名前を付けることをお勧めします。<br>`<Path>`、コード整合性ポリシーのファイル名とパスを指定します。

    ```powershell
    Add-HgsAttestationCIPolicy -Path <Path> -Name '<PolicyName>'
    ```

## <a name="capture-the-tpm-baseline-for-each-unique-class-of-hardware"></a>各一意のクラスのハードウェアの TPM ベースラインをキャプチャします。

TPM ベースラインは、ハードウェア、データ センター ファブリック内の各一意のクラスに必要です。 「参照ホスト」をもう一度使用します。 

1. 参照ホストでは、HYPER-V の役割と Host Guardian HYPER-V サポート機能がインストールされていることを確認します。

    >[!WARNING]
    >Host Guardian HYPER-V サポート機能は、一部のデバイスと互換性がない可能性があります、コードの整合性の仮想化ベースの保護を使用できます。 この機能を有効にする前に、ラボでこの構成のテストを強くお勧めします。 そうしないと、データ損失やブルー スクリーン エラー (Stop エラーとも呼ばれます) などを含む予期しないエラーが発生することがあります。

    ```powershell
    Install-WindowsFeature Hyper-V, HostGuardian -IncludeManagementTools -Restart
    ```
        
2. ベースライン ポリシーをキャプチャするには、管理者特権での Windows PowerShell コンソールで、次のコマンドを実行します。
        
    ```powershell
    Get-HgsAttestationBaselinePolicy -Path 'HWConfig1.tcglog'
    ```

    >[!NOTE]
    >使用する必要があります、 **- SkipValidation** IOMMU が存在する、仮想化ベースのセキュリティを有効にし、実行、またはコード整合性ポリシーを適用、参照をホストにセキュア ブートがない場合にフラグを有効にします。 これらの検証は、ホストでシールドされた VM の実行の最小要件を認識して設計されています。 -SkipValidation フラグを使用しても、コマンドレットの出力は変わりませんエラーだけで最適化します。

3.  HGS 管理者に TPM ベースライン (TCGlog ファイル) を提供します。

4.  HGS のドメインには、HGS サーバーに TCGlog ファイルをコピーし、次のコマンドを実行します。 通常、(たとえば、「製造元のモデルのバージョン」) のハードウェアを表すクラスの後に、ポリシーに名前をされます。

    ```powershell
    Add-HgsAttestationTpmPolicy -Path <Filename>.tcglog -Name '<PolicyName>'
    ```

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [構成証明を確認する](guarded-fabric-confirm-hosts-can-attest-successfully.md)
