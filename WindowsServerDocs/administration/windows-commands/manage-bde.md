---
title: manage-bde
description: BitLocker をオンまたはオフにしたり、ロックを解除したり、回復方法を更新したり、BitLocker で保護されているデータドライブのロックを解除したりする、manage-bde コマンドの参照記事。
ms.topic: article
ms.assetid: 276a7841-7289-48d4-a57d-bc7c300affbb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d1d910f9787d2a952a5e844c4aedb3d4c5ca53fa
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87886560"
---
# <a name="manage-bde"></a>manage-bde

BitLocker をオンまたはオフにし、ロック解除メカニズムを指定し、回復方法を更新して、BitLocker で保護されているデータドライブのロックを解除します。

> [!NOTE]
> このコマンド ライン ツールは、の代わりに使用できる、 **BitLocker ドライブ暗号化** コントロール パネルの項目。

## <a name="syntax"></a>構文

```
manage-bde [-status] [–on] [–off] [–pause] [–resume] [–lock] [–unlock] [–autounlock] [–protectors] [–tpm]
[–setidentifier] [-forcerecovery] [–changepassword] [–changepin] [–changekey] [-keypackage] [–upgrade] [-wipefreespace] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- |------------ |
| [manage-bde ステータス](manage-bde-status.md) | BitLocker で保護されているかどうかは、コンピューターで、すべてのドライブについての情報を提供します。 |
| [管理-bde オン](manage-bde-on.md) | ドライブを暗号化し、BitLocker をオンにします。 |
| [manage-bde をオフにします](manage-bde-off.md) | ドライブの暗号化を解除し、BitLocker をオフにします。 復号化が完了すると、すべてのキー プロテクターが削除されます。 |
| [manage-bde pause](manage-bde-pause.md) | 一時停止します。 暗号化または復号化します。 |
| [manage-bde resume](manage-bde-resume.md) | 暗号化または復号化を再開します。 |
| [manage-bde ロック](manage-bde-lock.md) | BitLocker で保護されたデータにアクセスできなくなります。 |
| [manage-bde のロック解除](manage-bde-unlock.md) | 回復パスワードまたは回復キーを BitLocker で保護されたデータにアクセスできます。 |
| [manage-bde 自動ロック解除](manage-bde-autounlock.md) | データ ドライブの自動ロック解除を管理します。 |
| [manage-bde プロテクターの管理](manage-bde-protectors.md) | 暗号化キーの保護方法を管理します。 |
| [manage-bde tpm](manage-bde-tpm.md) | コンピューターのトラステッド プラットフォーム モジュール (TPM) を構成します。 このコマンドは、Windows 8 または**win8_server_2**を実行しているコンピューターではサポートされていません。 これらのコンピューター上の TPM を管理するには、Windows PowerShell の TPM の管理] MMC スナップインまたは TPM 管理コマンドレットを使用します。 |
| [manage-bde setidentifier](manage-bde-setidentifier.md)   | 指定された値にドライブのドライブ識別子のフィールドを設定、 **、組織の一意の識別子を提供する** グループ ポリシー設定です。 |
| [manage-bde ForceRecovery](manage-bde-forcerecovery.md) | 再起動時に復旧モードに BitLocker で保護されたドライブを強制します。 このコマンドは、TPM に関連するすべてのキー プロテクターをドライブから削除します。 コンピューターが再起動したら、回復パスワードまたは回復キーは、ドライブのロック解除に使用できます。 |
| [manage-bde changepassword](manage-bde-changepassword.md) | データ ドライブでパスワードを変更します。 |
| [manage-bde changepin を管理する](manage-bde-changepin.md) | オペレーティング システム ドライブの暗証番号 (pin) を変更します。 |
| [manage-bde 変更キーを管理します。](manage-bde-changekey.md) | オペレーティング システム ドライブのスタートアップ キーを変更します。 |
| [manage-bde KeyPackage](manage-bde-keypackage.md) | ドライブのキー パッケージを生成します。 |
| [manage-bde のアップグレード](manage-bde-upgrade.md) | BitLocker のバージョンにアップグレードします。 |
| [manage-bde WipeFreeSpace 領域](manage-bde-wipefreespace.md) | ドライブの空き領域を消去します。 |
| -? または /? | コマンドプロンプトで簡単なヘルプを表示します。 |
| -help または-h | 表示は、コマンド プロンプトでヘルプを完了します。 |

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [コマンドラインを使用して BitLocker を有効にします。](/previous-versions/windows/it-pro/windows-7/dd894351(v=ws.10))
