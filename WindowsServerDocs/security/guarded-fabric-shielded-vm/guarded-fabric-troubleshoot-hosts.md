---
title: ホストガーディアンサービスのトラブルシューティング
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: 80ea38f4-4de6-4f85-8188-33a63bb1cf81
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 09/25/2019
ms.openlocfilehash: ec885670ca6808e89c63848781c4ff3dc27799b8
ms.sourcegitcommit: 2a15de216edde8b8e240a4aa679dc6d470e4159e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77465606"
---
# <a name="troubleshooting-guarded-hosts"></a>保護されたホストのトラブルシューティング

> 適用対象: windows server 2019、Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、保護されたファブリックで保護された Hyper-v ホストを展開または運用するときに発生する一般的な問題の解決策について説明します。
問題の性質がわからない場合は、まず Hyper-v ホストで保護された[ファブリックの診断](guarded-fabric-troubleshoot-diagnostics.md)を実行して、考えられる原因を絞り込みます。

## <a name="guarded-host-feature"></a>保護されたホスト機能

Hyper-v ホストで問題が発生している場合は、まず**Host Guardian Hyper-v サポート**機能がインストールされていることを確認してください。
この機能がないと、Hyper-v ホストには、構成証明を渡したり、シールドされた Vm をプロビジョニングしたりするための重要な構成設定とソフトウェアが不足します。

機能がインストールされているかどうかを確認するには、サーバーマネージャーを使用するか、管理者特権の PowerShell ウィンドウで次のコマンドを実行します。

```powershell
Get-WindowsFeature HostGuardian
```

機能がインストールされていない場合は、次の PowerShell コマンドを使用してインストールします。

```powershell
Install-WindowsFeature HostGuardian -Restart
```

## <a name="attestation-failures"></a>構成証明のエラー

ホストが構成証明をホストガーディアンサービスに渡していない場合は、シールドされた Vm を実行できません。
そのホストの[get-hgsclientconfiguration](https://technet.microsoft.com/library/dn914500.aspx)の出力には、そのホストが構成証明に失敗した理由に関する情報が表示されます。

次の表では、 **AttestationStatus**フィールドに表示される可能性がある値と、必要に応じて次の手順について説明します。

AttestationStatus         | 説明
--------------------------|------------
Expired                   | ホストは以前に構成証明を通過しましたが、発行された正常性証明書の有効期限が切れています。 ホストと HGS の時刻が同期されていることを確認してください。
InsecureHostConfiguration | ホストは、HGS に構成されている構成証明ポリシーに準拠していなかったため、構成証明に合格しませんでした。 詳細については、AttestationSubStatus テーブルを参照してください。
NotConfigured             | ホストは、構成証明およびキーの保護に HGS を使用するように構成されていません。 代わりに、ローカルモード用に構成されています。 このホストが保護されたファブリックにある場合は、 [get-hgsclientconfiguration](https://technet.microsoft.com/library/dn914494.aspx)を使用して HGS サーバーの url を指定します。
成功                    | ホストが構成証明に合格しました。
TransientError            | ネットワーク、サービス、またはその他の一時的なエラーが原因で、最後の構成証明の試行が失敗しました。 最後の操作を再試行してください。
TpmError                  | TPM でエラーが発生したため、ホストは最後の構成証明を完了できませんでした。 詳細については、TPM ログを参照してください。
UnauthorizedHost          | シールドされた Vm の実行が承認されていないため、ホストは構成証明を通過しませんでした。 シールドされた Vm を実行するために、ホストが HGS によって信頼されたセキュリティグループに属していることを確認します。
不明                   | ホストは、まだ HGS で証明を試行していません。

**AttestationStatus**が**Insecurehostconfiguration**として報告されると、1つまたは複数の理由が**AttestationSubStatus**フィールドに入力されます。
次の表では、AttestationSubStatus で使用できる値と、問題の解決方法に関するヒントについて説明します。

AttestationSubStatus       | 意味と対処方法
---------------------------|-------------------------------
BitLocker                  | ホストの OS ボリュームは、BitLocker によって暗号化されていません。 これを解決するには、OS ボリュームで[bitlocker を有効](https://technet.microsoft.com/itpro/windows/keep-secure/bitlocker-basic-deployment)にするか、 [HGS で bitlocker ポリシーを無効](guarded-fabric-manage-hgs.md#review-attestation-policies)にします。
CodeIntegrityPolicy        | ホストがコード整合性ポリシーを使用するように構成されていないか、または HGS サーバーによって信頼されているポリシーを使用していません。 コード整合性ポリシーが構成されていること、ホストが再起動されたこと、およびポリシーが HGS サーバーに登録されていることを確認してください。 詳細については、「[コード整合性ポリシーの作成と適用](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md#create-and-apply-a-code-integrity-policy)」を参照してください。
DumpsEnabled               | ホストは、HGS ポリシーで許可されていないクラッシュダンプまたはライブメモリダンプを許可するように構成されています。 これを解決するには、ホストのダンプを無効にします。
DumpEncryption             | ホストは、クラッシュダンプまたはライブメモリダンプを許可するように構成されていますが、これらのダンプは暗号化されていません。 ホストのダンプを無効にするか、[ダンプの暗号化を構成](https://technet.microsoft.com/windows-server-docs/virtualization/hyper-v/manage/about-dump-encryption)してください。
DumpEncryptionKey          | このホストはダンプを許可および暗号化するように構成されていますが、HGS に知られている証明書を使用して暗号化されていません。 これを解決するには、ホストの[暗号化キーのダンプを更新](https://technet.microsoft.com/windows-server-docs/virtualization/hyper-v/manage/about-dump-encryption)するか、または[HGS にキーを登録](guarded-fabric-manage-hgs.md#authorizing-new-guarded-hosts)します。
FullBoot                   | ホストがスリープ状態または休止状態から再開されました。 クリーンな完全ブートを許可するために、ホストを再起動してください。
HibernationEnabled         | このホストは、HGS ポリシーで許可されていない休止状態ファイルを暗号化せずに休止状態にするように構成されています。 休止状態を無効にし、ホストを再起動するか、 [dump encryption を構成](https://technet.microsoft.com/windows-server-docs/virtualization/hyper-v/manage/about-dump-encryption)します。
HypervisorEnforcedCodeIntegrityPolicy | ホストは、ハイパーバイザーによって適用されるコード整合性ポリシーを使用するように構成されていません。 ハイパーバイザーによってコードの整合性が有効、構成、および適用されていることを確認します。 詳細については、「 [Device Guard 展開ガイド](https://technet.microsoft.com/itpro/windows/keep-secure/deploy-device-guard-deploy-code-integrity-policies)」を参照してください。
Iommu                      | ホストの仮想化ベースのセキュリティ機能は、HGS ポリシーで必要とされる直接メモリアクセス攻撃からの保護のために、IOMMU デバイスを必要とするように構成されていません。 ホストに IOMMU があること、有効になっていること、および VBS を起動するときに、Device Guard が[DMA による保護を要求するように構成](https://technet.microsoft.com/itpro/windows/keep-secure/deploy-device-guard-enable-virtualization-based-security#enable-virtualization-based-security-vbs-and-device-guard)されていることを確認します。
PagefileEncryption         | ページファイルの暗号化がホストで有効になっていません。 これを解決するには `fsutil behavior set encryptpagingfile 1` を実行して、ページファイルの暗号化を有効にします。 詳細については、「 [fsutil behavior](https://technet.microsoft.com/library/cc785435.aspx)」を参照してください。
ブート                 | セキュアブートは、このホストで有効になっていないか、Microsoft セキュアブートテンプレートを使用していません。 この問題を解決するには、Microsoft セキュアブートテンプレートを使用して[セキュアブートを有効](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/disabling-secure-boot#enable_secure_boot)にします。
SecureBootSettings         | このホストの TPM ベースラインが、HGS によって信頼されているものと一致しません。 これは、UEFI 起動機関、DBX 変数、デバッグフラグ、またはカスタムセキュアブートポリシーが新しいハードウェアまたはソフトウェアのインストールによって変更された場合に発生する可能性があります。 このコンピューターの現在のハードウェア、ファームウェア、およびソフトウェアの構成を信頼する場合は、[新しい TPM ベースラインをキャプチャ](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md#capture-the-tpm-baseline-for-each-unique-class-of-hardware)して[HGS に登録](guarded-fabric-manage-hgs.md#authorizing-new-guarded-hosts)できます。
TcgLogVerification         | TCG ログ (TPM ベースライン) を取得または検証できません。 これは、ホストのファームウェア、TPM、またはその他のハードウェアコンポーネントに問題があることを示している可能性があります。 Windows を起動する前に、ホストが PXE ブートを試行するように構成されている場合は、古い Net Boot Program (NBP) でもこのエラーが発生することがあります。 PXE ブートが有効になっている場合は、すべての NBPs が最新の状態であることを確認します。
VirtualSecureMode          | 仮想化ベースのセキュリティ機能がホストで実行されていません。 VBS が有効になっていること、およびシステムが構成された[プラットフォームのセキュリティ機能](https://technet.microsoft.com/itpro/windows/keep-secure/deploy-device-guard-enable-virtualization-based-security#validate-enabled-device-guard-hardware-based-security-features)を満たしていることを確認してください。 VBS の要件の詳細については、 [Device Guard のドキュメント](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide)を参照してください。

## <a name="modern-tls"></a>最新の TLS

グループポリシーを展開した場合、または TLS 1.0 を使用しないように Hyper-v ホストを構成した場合は、シールドされた VM を起動しようとすると、"ホストガーディアンサービスクライアントが、呼び出し元のプロセスに代わってキープロテクターのラップを解除できませんでした" というエラーが発生することがあります。
これは、サポートされている TLS のバージョンを HGS サーバーとネゴシエートするときにシステムの既定の TLS バージョンが考慮されない、.NET 4.6 の既定の動作によるものです。

この動作を回避するには、次の2つのコマンドを実行して、すべての .NET アプリにシステムの既定の TLS バージョンを使用するように .NET を構成します。

```cmd
reg add HKLM\SOFTWARE\Microsoft\.NETFramework\v4.0.30319 /v SystemDefaultTlsVersions /t REG_DWORD /d 1 /f /reg:64
reg add HKLM\SOFTWARE\Microsoft\.NETFramework\v4.0.30319 /v SystemDefaultTlsVersions /t REG_DWORD /d 1 /f /reg:32
```

> [!WARNING]
> [システムの既定の TLS バージョン] 設定は、コンピューター上のすべての .NET アプリに影響します。 実稼働コンピューターに展開する前に、分離された環境でレジストリキーをテストしてください。

.NET 4.6 と TLS 1.0 の詳細については、「 [tls 1.0 の問題、第2版の解決](https://docs.microsoft.com/security/solving-tls1-problem)」を参照してください。
