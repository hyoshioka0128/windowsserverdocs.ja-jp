---
title: ホスト ガーディアン サービスのトラブルシューティング
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 80ea38f4-4de6-4f85-8188-33a63bb1cf81
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 7fe01039b47c36d940973fba97d25c401f5af8a7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59851373"
---
# <a name="troubleshooting-guarded-hosts"></a>保護されたホストのトラブルシューティング

> 適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016

このトピックを展開すると、保護されたファブリックで保護された HYPER-V ホストの動作に発生する一般的な問題の解決方法について説明します。
最初のコマンドを試してください、問題の性質の不明な場合、[保護され、fabric 診断](guarded-fabric-troubleshoot-diagnostics.md)可能性を絞り込むために、HYPER-V ホストで発生します。

## <a name="guarded-host-feature"></a>ホスト機能の保護

HYPER-V ホストに問題が発生する場合は、最初にいることを確認、 **Host Guardian HYPER-V サポート**機能がインストールされています。
この機能は、HYPER-V ホストに重要な構成設定の一部が不足しているとシールドされた Vm のプロビジョニングおよびプロビジョニングの構成証明に合格できるようにするソフトウェア。

機能がインストールされているかどうかを確認するには、サーバー マネージャーを使用して、または管理者特権の PowerShell ウィンドウで、次のコマンドを実行します。

```powershell
Get-WindowsFeature HostGuardian
```

機能がインストールされていない場合は、次の PowerShell コマンドを使用してインストールします。

```powershell
Install-WindowsFeature HostGuardian -Restart
```

## <a name="attestation-failures"></a>構成証明書エラー

ホストがホスト ガーディアン サービスの構成証明を渡さない場合しなくなりますシールドされた Vm を実行できません。
出力[Get-hgsclientconfiguration](https://technet.microsoft.com/library/dn914500.aspx)をホストするがわかりますそのホストが構成証明が失敗した理由に関する情報。

次の表に表示される値の説明、 **AttestationStatus**フィールドと、該当する場合の潜在的な次の手順。

AttestationStatus         | 説明
--------------------------|------------
有効期限切れ                   | ホストの構成証明書は以前は、渡されたが、発行された正常性証明書の有効期限が切れた。 ホストと HGS 時刻が同期を確認します。
InsecureHostConfiguration | HGS で構成されている構成証明書ポリシーに準拠していなかったために、ホストは、構成証明を合格しませんでした。 詳細については、AttestationSubStatus テーブルを参照してください。
NotConfigured             | ホストは、HGS を使用して、構成証明とキーの保護用に構成されていません。 代わりにローカル モードで構成されます。 このホストが保護されたファブリック内にある場合を使用して、[セット HgsClientConfiguration](https://technet.microsoft.com/library/dn914494.aspx) HGS サーバーの Url を提供しています。
渡されました。                    | ホストには、構成証明が渡されます。
TransientError            | ネットワーク、サービス、またはその他の一時的なエラーのため、最後の構成証明試行が失敗しました。 最後の操作を再試行してください。
TpmError                  | ホストは、tpm を装備したエラーのため、前回の構成証明試行を完了できませんでした。 詳細については、TPM のログを参照してください。
UnauthorizedHost          | ホストは、シールドされた Vm を実行する、権限がないために、構成証明を合格しませんでした。 シールドされた Vm を実行するように HGS によって信頼されているセキュリティ グループに所属していることを確認します。
Unknown                   | ホストが HGS でまだ証明は試行されません。


ときに**AttestationStatus**として報告された**InsecureHostConfiguration**で 1 つまたは複数の理由が設定されて、 **AttestationSubStatus**フィールド。
次の表では、AttestationSubStatus と問題を解決する方法のヒントについては、使用可能な値について説明します。

AttestationSubStatus       | その意味と対処方法
---------------------------|-------------------------------
BitLocker                  | ホストの OS ボリュームが BitLocker で暗号化されません。 、これを解決する[BitLocker を有効にする](https://technet.microsoft.com/itpro/windows/keep-secure/bitlocker-basic-deployment)OS ボリュームまたは[HGS 上の BitLocker ポリシーを無効にする](guarded-fabric-manage-hgs.md#review-attestation-policies)します。
CodeIntegrityPolicy        | ホストは、コード整合性ポリシーを使用して構成されていないか、HGS サーバーによって信頼されているポリシーを使用していません。 コード整合性ポリシーが構成されて、ホストが再起動して、ポリシーが HGS サーバーに登録を確認してください。 詳細については、次を参照してください。[作成し、コード整合性ポリシーを適用](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md#create-and-apply-a-code-integrity-policy)します。
DumpsEnabled               | ホストを構成するクラッシュ ダンプを許可するか、メモリ ダンプを live は、HGS ポリシーによって許可されていません。 これを解決するには、ホストのダンプを無効にします。
DumpEncryption             | クラッシュ ダンプを許可するホストを構成または実行中のメモリ ダンプしますが、それらのダンプは暗号化されません。 ホストのダンプを無効にするか、または[ダンプ暗号化を構成する](https://technet.microsoft.com/windows-server-docs/virtualization/hyper-v/manage/about-dump-encryption)します。
DumpEncryptionKey          | ホストは、許可して、ダンプを暗号化するように構成が、暗号化することを HGS 既知の証明書を使用していません。 これを解決するのには[ダンプ暗号化キーを更新](https://technet.microsoft.com/windows-server-docs/virtualization/hyper-v/manage/about-dump-encryption)ホスト上または[キー HGS に登録](guarded-fabric-manage-hgs.md#authorizing-new-guarded-hosts)。
FullBoot                   | ホストは、スリープ状態または休止状態から再開します。 クリーンで完全なブートを許可するホストを再起動します。
HibernationEnabled         | ホストは、休止状態を許可するは、HGS ポリシーによって許可されていない休止状態ファイルを暗号化せずに構成されます。 休止状態を無効にし、ホストを再起動または[ダンプ暗号化を構成する](https://technet.microsoft.com/windows-server-docs/virtualization/hyper-v/manage/about-dump-encryption)します。
HypervisorEnforcedCodeIntegrityPolicy | ホストは、ハイパーバイザーによって適用されるコード整合性ポリシーを使用して構成されていません。 コードの整合性が有効になっているか、構成、および、ハイパーバイザーによって適用されることを確認します。 参照してください、 [Device Guard 展開ガイド](https://technet.microsoft.com/itpro/windows/keep-secure/deploy-device-guard-deploy-code-integrity-policies)詳細についてはします。
Iommu                      | ホストの仮想化ベースのセキュリティ機能は、HGS ポリシーで必要に応じて、ダイレクト メモリ アクセスの攻撃に対する保護のため、IOMMU デバイスを要求するように構成されていません。 ホストがほとんどサポートを有効にし、その Device Guard は確認[DMA 保護を必要とするように構成](https://technet.microsoft.com/itpro/windows/keep-secure/deploy-device-guard-enable-virtualization-based-security#enable-virtualization-based-security-vbs-and-device-guard)VBS を起動するときにします。
PagefileEncryption         | ページのファイルの暗号化には、ホストでは無効です。 これを解決するには、次のように実行します。`fsutil behavior set encryptpagingfile 1`ページ ファイルの暗号化を有効にします。 詳細については、次を参照してください。 [fsutil の動作](https://technet.microsoft.com/library/cc785435.aspx)します。
セキュア ブート                 | セキュア ブートがかどうか、このホストで有効にしないかを使用して Microsoft セキュア ブート テンプレート。 [セキュア ブートを有効にする](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/disabling-secure-boot#enable_secure_boot)この問題を解決するのには Microsoft セキュア ブート テンプレートを使用します。
SecureBootSettings         | このホスト上の TPM ベースラインには、HGS で信頼のいずれかと一致しません。 これは、新しいハードウェアまたはソフトウェアをインストールすることで、UEFI 起動機関、DBX 変数、debug フラグ、またはカスタムのセキュア ブートのポリシーが変更されたときに発生します。 現在のハードウェア、ファームウェア、およびソフトウェア構成のこのコンピューターを信頼する場合は、[新しい TPM ベースラインをキャプチャ](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md#capture-the-tpm-baseline-for-each-unique-class-of-hardware)と[HGS に登録](guarded-fabric-manage-hgs.md#authorizing-new-guarded-hosts)します。
TcgLogVerification         | TCG ログ (TPM ベースライン) を取得または検証できません。 これは、ホストのファームウェア、TPM、またはその他のハードウェア コンポーネントに問題を示していることができます。 場合は、ホストは、Windows を起動する前に PXE ブートを試行するように構成、古いネットワーク ブート プログラム (NBP) もこのエラーが発生します。 PXE ブートが有効にすると、すべての Nbp は最新の状態を確認します。
VirtualSecureMode          | 仮想化ベースのセキュリティ機能は、ホストで実行されていません。 VBS が有効になっており、システムが、構成を満たしていることを確認します。[プラットフォームのセキュリティ機能](https://technet.microsoft.com/itpro/windows/keep-secure/deploy-device-guard-enable-virtualization-based-security#validate-enabled-device-guard-hardware-based-security-features)します。 参照してください、 [Device Guard ドキュメント](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide)VBS 要件の詳細について。
