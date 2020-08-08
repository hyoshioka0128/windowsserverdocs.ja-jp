---
title: HGS で必要な TPM モード情報をキャプチャする
ms.topic: article
ms.assetid: 915b1338-5085-481b-8904-75d29e609e93
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 04/01/2019
ms.openlocfilehash: a0bc065f9654091ece18445488e4b46cfb197ad3
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87944152"
---
# <a name="authorize-guarded-hosts-using-tpm-based-attestation"></a>TPM ベースの構成証明を使用して保護されたホストを承認する

>適用対象: windows server 2019、Windows Server (半期チャネル)、Windows Server 2016

TPM モードでは、TPM 識別子 (プラットフォーム識別子または保証キー EKpub とも呼ばれます) を使用し \[ \] て、特定のホストが "保護された" として承認されているかどうかを判断します。 このモードの構成証明では、セキュアブートとコード整合性の測定を使用して、特定の Hyper-v ホストが正常な状態であり、信頼されたコードのみが実行されていることを確認します。 構成証明によってとが正常でないことを確認するには、次の成果物を取得する必要があります。

1.  TPM 識別子 (EKpub)

    -  この情報は、各 Hyper-v ホストに固有です。

2.  TPM ベースライン (ブート測定)

    -  これは、同じクラスのハードウェア上で実行されるすべての Hyper-v ホストに適用されます。

3.  コード整合性ポリシー (許可されているバイナリのホワイトリスト)

    -  これは、共通のハードウェアとソフトウェアを共有するすべての Hyper-v ホストに適用されます。

「参照ホスト」からベースラインポリシーと CI ポリシーをキャプチャすることをお勧めします。これは、データセンター内の Hyper-v ハードウェア構成の一意のクラスを表します。 Windows Server バージョン1709以降では、サンプル CI ポリシーは C:\Windows\schemas\CodeIntegrity\ExamplePolicies. に含まれています。

## <a name="versioned-attestation-policies"></a>バージョン管理された構成証明ポリシー

Windows Server 2019 では、 *v2 構成*証明と呼ばれる構成証明の新しい方法が導入されています。この方法では、EKPUB を HGS に追加するために TPM 証明書が存在している必要があります。 Windows Server 2016 で使用されている v1 構成証明方法では、HgsAttestationTpmHost または他の TPM 構成証明書のコマンドレットを実行してアーティファクトをキャプチャするときに-Force フラグを指定することで、この安全性チェックを無効にできました。 Windows Server 2019 以降では、v2 構成証明が既定で使用されるため、証明書なしで TPM を登録する必要がある場合は、HgsAttestationTpmHost を実行するときに-PolicyVersion v1 フラグを指定する必要があります。 -Force フラグは、v2 構成証明では機能しません。

ホストは、すべてのアーティファクト (EKPub + TPM ベースライン + CI ポリシー) が同じバージョンの構成証明を使用しているかどうかのみを証明できます。 V2 構成証明が最初に試行され、それが失敗した場合は v1 構成証明が使用されます。 つまり、v1 構成証明を使用して TPM 識別子を登録する必要がある場合は、-PolicyVersion v1 フラグを指定して、TPM ベースラインをキャプチャし、CI ポリシーを作成するときに v1 構成証明を使用する必要があります。 V2 構成証明を使用して TPM ベースラインと CI ポリシーを作成した後で、TPM 証明書を使用せずに保護されたホストを追加する必要がある場合は、-PolicyVersion v1 フラグを使用して各成果物を再作成する必要があります。

## <a name="capture-the-tpm-identifier-platform-identifier-or-ekpub-for-each-host"></a>各ホストの TPM 識別子 (プラットフォーム識別子または EKpub) をキャプチャする

1.  ファブリックドメインで、各ホストの TPM が使用できる状態であることを確認します。つまり、TPM が初期化され、所有権が取得されます。 Tpm の状態を確認するには、tpm 管理コンソール (tpm .msc) を開くか、管理者特権の Windows PowerShell ウィンドウで**Get tpm**を実行します。 TPM が**準備完了**状態でない場合は、初期化し、その所有権を設定する必要があります。 これを行うには、TPM 管理コンソールを使用するか、または**初期化-tpm**を実行します。

2.  保護された各ホストで、管理者特権の Windows PowerShell コンソールで次のコマンドを実行して、EKpub を取得します。 では `<HostName>` 、一意のホスト名を、このホストを識別するのに適した名前に置き換えます。これは、ホスト名またはファブリックインベントリサービスによって使用される名前 (使用可能な場合) になります。 便宜上、ホストの名前を使用して出力ファイルに名前を指定します。

    ```powershell
    (Get-PlatformIdentifier -Name '<HostName>').InnerXml | Out-file <Path><HostName>.xml -Encoding UTF8
    ```
3.  保護されたホストになる各ホストに対して上記の手順を繰り返します。各 XML ファイルに一意の名前を付けます。

4.  結果の XML ファイルを HGS 管理者に提供します。

5.  HGS ドメインで、HGS サーバー上の管理者特権の Windows PowerShell コンソールを開き、次のコマンドを実行します。 各 XML ファイルに対してコマンドを繰り返します。

    ```powershell
    Add-HgsAttestationTpmHost -Path <Path><Filename>.xml -Name <HostName>
    ```

    > [!NOTE]
    > 信頼されていない保証キー証明書 (EKCert) に関する TPM 識別子を追加するときにエラーが発生した場合は、[信頼された tpm ルート証明書が HGS ノードに追加され](guarded-fabric-install-trusted-tpm-root-certificates.md)ていることを確認します。
    > また、一部の TPM ベンダーは EKCerts を使用しません。
    > EKCert がないかどうかを確認するには、メモ帳などのエディターで XML ファイルを開き、EKCert が見つからなかったことを示すエラーメッセージがないかどうかを確認します。
    > この場合、コンピューターの TPM が本物であることを信頼している場合は、パラメーターを使用して、 `-Force` ホスト id を HGS に追加できます。 Windows Server 2019 では、を使用するときにもパラメーターを使用する必要があり `-PolicyVersion v1` `-Force` ます。 これにより、Windows Server 2016 の動作と一貫性のあるポリシーが作成され、 `-PolicyVersion v1` CI ポリシーと TPM のベースラインも登録するときにを使用する必要があります。

## <a name="create-and-apply-a-code-integrity-policy"></a>コード整合性ポリシーを作成して適用する

コード整合性ポリシーを使用すると、ホスト上で実行する信頼できる実行可能ファイルのみを実行できるようになります。
信頼できる実行可能ファイルの外部にあるマルウェアおよびその他の実行可能ファイルは実行できません。

保護された各ホストには、シールドされた Vm を TPM モードで実行するために、コード整合性ポリシーが適用されている必要があります。
信頼する正確なコード整合性ポリシーを指定するには、それらを HGS に追加します。
コードの整合性ポリシーは、ポリシーを適用したり、ポリシーに準拠していないソフトウェアをブロックしたり、単に監査 (ポリシーに定義されていないソフトウェアが実行されたときにイベントをログに記録) するように構成できます。

Windows Server バージョン1709以降では、サンプルコードの整合性ポリシーは C:\Windows\schemas\CodeIntegrity\ExamplePolicies. の Windows に含まれています。 Windows Server には、次の2つのポリシーをお勧めします。

- **Allowmicrosoft**: microsoft によって署名されたすべてのファイルを許可します。 このポリシーは、SQL や Exchange などのサーバーアプリケーションや、Microsoft によって発行されたエージェントによってサーバーが監視されている場合に推奨されます。
- **DefaultWindows_Enforced**: Windows に付属しているファイルのみを許可し、Office など、Microsoft がリリースした他のアプリケーションを許可しません。 このポリシーは、組み込みのサーバーの役割と、Hyper-v などの機能のみを実行するサーバーに推奨されます。

まず、監査 (ログ) モードで CI ポリシーを作成して、何かが欠落していないかどうかを確認してから、ホストの運用ワークロードにポリシーを適用することをお勧めします。

[新しい-cipolicy](https://docs.microsoft.com/powershell/module/configci/new-cipolicy?view=win10-ps)コマンドレットを使用して独自のコード整合性ポリシーを生成する場合は、使用するルールレベルを決定する必要があります。
プライマリレベルの**パブリッシャー**では、**ハッシュ**にフォールバックすることをお勧めします。これにより、CI ポリシーを変更することなく、ほとんどのデジタル署名されたソフトウェアを更新できます。
同じ発行元によって作成された新しいソフトウェアは、CI ポリシーを変更せずにサーバーにインストールすることもできます。
デジタル署名されていない実行可能ファイルはハッシュされます。これらのファイルを更新するには、新しい CI ポリシーを作成する必要があります。
使用可能な CI ポリシーの規則レベルの詳細については、「[コードの整合性ポリシーの展開: ポリシー規則とファイル規則](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/select-types-of-rules-to-create#windows-defender-application-control-policy-rules)」および「コマンドレットのヘルプ」を参照してください。

1.  参照ホストで、新しいコード整合性ポリシーを生成します。 次のコマンドは、フォールバックにフォールバックして、**パブリッシャー**レベルでポリシーを**作成します。** 次に、XML ファイルをバイナリファイル形式に変換し、HGS は CI ポリシーを適用して測定する必要があります。

    ```powershell
    New-CIPolicy -Level Publisher -Fallback Hash -FilePath 'C:\temp\HW1CodeIntegrity.xml' -UserPEs

    ConvertFrom-CIPolicy -XmlFilePath 'C:\temp\HW1CodeIntegrity.xml' -BinaryFilePath 'C:\temp\HW1CodeIntegrity.p7b'
    ```

    >[!NOTE]
    >上記のコマンドは、監査モードでのみ CI ポリシーを作成します。 承認されていないバイナリがホストで実行されるのをブロックすることはありません。 運用環境では、強制されたポリシーのみを使用する必要があります。

2.  コード整合性ポリシーファイル (XML ファイル) は、簡単に見つけられるように保存しておいてください。 このファイルを後で編集して、CI ポリシーを適用するか、システムに加えられた今後の更新からの変更をマージする必要があります。

3.  参照ホストに CI ポリシーを適用します。

    1.  次のコマンドを実行して、CI ポリシーを使用するようにコンピューターを構成します。 また、[グループポリシー](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-control/deploy-windows-defender-application-control-policies-using-group-policy)または[System Center Virtual Machine Manager](https://docs.microsoft.com/system-center/vmm/guarded-deploy-host?view=sc-vmm-2019#manage-and-deploy-code-integrity-policies-with-vmm)を使用して CI ポリシーを展開することもできます。

        ```powershell
        Invoke-CimMethod -Namespace root/Microsoft/Windows/CI -ClassName PS_UpdateAndCompareCIPolicy -MethodName Update -Arguments @{ FilePath = "C:\temp\HW1CodeIntegrity.p7b" }
        ```

    2.  ポリシーを適用するには、ホストを再起動してください。

3.  一般的なワークロードを実行して、コード整合性ポリシーをテストします。 これには、実行中の Vm、ファブリック管理エージェント、バックアップエージェント、またはコンピューター上のトラブルシューティングツールが含まれる場合があります。 コード整合性違反があるかどうかを確認し、必要に応じて CI ポリシーを更新します。

4.  更新された CI ポリシー XML ファイルに対して次のコマンドを実行して、CI ポリシーを強制モードに変更します。

    ```powershell
    Set-RuleOption -FilePath 'C:\temp\HW1CodeIntegrity.xml' -Option 3 -Delete

    ConvertFrom-CIPolicy -XmlFilePath 'C:\temp\HW1CodeIntegrity.xml' -BinaryFilePath 'C:\temp\HW1CodeIntegrity_enforced.p7b'
    ```

5.  次のコマンドを使用して、CI ポリシーをすべてのホスト (同一のハードウェアとソフトウェアの構成) に適用します。

    ```powershell
    Invoke-CimMethod -Namespace root/Microsoft/Windows/CI -ClassName PS_UpdateAndCompareCIPolicy -MethodName Update -Arguments @{ FilePath = "C:\temp\HW1CodeIntegrity.p7b" }

    Restart-Computer
    ```

    >[!NOTE]
    >ホストに CI ポリシーを適用する場合や、これらのコンピューター上のソフトウェアを更新する場合は注意してください。 CI ポリシーに準拠していないカーネルモードドライバーは、コンピューターの起動を妨げている可能性があります。

6.  HGS 管理者にバイナリファイル (この例では HW1CodeIntegrity \_ . p7b) を指定します。

7.  HGS ドメインで、コード整合性ポリシーを HGS サーバーにコピーし、次のコマンドを実行します。

    `<PolicyName>`では、適用するホストの種類を示す CI ポリシーの名前を指定します。 ベストプラクティスとしては、コンピューターのメーカー/モデルの後に名前を指定し、それを実行する特別なソフトウェア構成を指定することをお勧めします。<br>`<Path>`では、コード整合性ポリシーのパスとファイル名を指定します。

    ```powershell
    Add-HgsAttestationCIPolicy -Path <Path> -Name '<PolicyName>'
    ```

## <a name="capture-the-tpm-baseline-for-each-unique-class-of-hardware"></a>ハードウェアの一意のクラスごとに TPM ベースラインをキャプチャする

データセンターファブリック内のハードウェアの一意のクラスごとに TPM ベースラインが必要です。 もう一度 "参照ホスト" を使用します。

1. 参照ホストで、Hyper-v の役割と Host Guardian Hyper-v のサポート機能がインストールされていることを確認します。

    >[!WARNING]
    >Host Guardian Hyper-v サポート機能を使用すると、一部のデバイスと互換性のない、コードの整合性を仮想化ベースで保護できます。 この機能を有効にする前に、ラボでこの構成をテストすることを強くお勧めします。 そうしないと、データ損失やブルー スクリーン エラー (Stop エラーとも呼ばれます) などを含む予期しないエラーが発生することがあります。

    ```powershell
    Install-WindowsFeature Hyper-V, HostGuardian -IncludeManagementTools -Restart
    ```

2. ベースラインポリシーをキャプチャするには、管理者特権の Windows PowerShell コンソールで次のコマンドを実行します。

    ```powershell
    Get-HgsAttestationBaselinePolicy -Path 'HWConfig1.tcglog'
    ```

    >[!NOTE]
    >参照ホストでセキュアブートが有効になっていない場合、IOMMU が有効になっている場合、仮想化ベースのセキュリティが有効で実行中の場合、またはコード整合性ポリシーが適用されている場合は、 **-skipvalidation**フラグを使用する必要があります。 これらの検証は、ホストでシールドされた VM を実行するための最小要件を認識するように設計されています。 -SkipValidation フラグを使用しても、コマンドレットの出力は変わりません。エラーをないだけです。

3.  TPM ベースライン (TCGlog ファイル) を HGS 管理者に提供します。

4.  HGS ドメインで、TCGlog ファイルを HGS サーバーにコピーし、次のコマンドを実行します。 通常、ポリシーには、それが表すハードウェアのクラス (たとえば、"製造元のモデルのリビジョン") の後に名前を指定します。

    ```powershell
    Add-HgsAttestationTpmPolicy -Path <Filename>.tcglog -Name '<PolicyName>'
    ```

## <a name="next-step"></a>次のステップ

> [!div class="nextstepaction"]
> [構成証明を確認する](guarded-fabric-confirm-hosts-can-attest-successfully.md)
