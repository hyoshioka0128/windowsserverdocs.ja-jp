---
title: manage-bde
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 276a7841-7289-48d4-a57d-bc7c300affbb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4f103a8277f84487e2434034a149e056a8deee57
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2020
ms.locfileid: "83820782"
---
# <a name="manage-bde"></a>manage-bde



使用を有効にするか、BitLocker をオフにすると、指定のメカニズムのロックを解除し、回復方法を更新し、BitLocker で保護されたデータ ドライブのロックを解除します。 このコマンド ライン ツールは、の代わりに使用できる、 **BitLocker ドライブ暗号化** コントロール パネルの項目。

## <a name="syntax"></a>構文

```
manage-bde [-status] [–on] [–off] [–pause] [–resume] [–lock] [–unlock] [–autounlock] [–protectors] [–tpm]
[–SetIdentifier] [-ForceRecovery] [–changepassword] [–changepin] [–changekey] [-KeyPackage] [–upgrade] [-WipeFreeSpace] [{-?|/?}] [{-help|-h}]
```

#### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|[Manage-bde: status](manage-bde-status.md)|BitLocker で保護されているかどうかは、コンピューターで、すべてのドライブについての情報を提供します。|
|[Manage-bde: on](manage-bde-on.md)|ドライブを暗号化し、BitLocker をオンにします。|
|[Manage-bde: off](manage-bde-off.md)|ドライブの暗号化を解除し、BitLocker をオフにします。 復号化が完了すると、すべてのキー プロテクターが削除されます。|
|[Manage-bde: pause](manage-bde-pause.md)|一時停止します。 暗号化または復号化します。|
|[Manage-bde: resume](manage-bde-resume.md)|暗号化または復号化を再開します。|
|[Manage-bde: lock](manage-bde-lock.md)|BitLocker で保護されたデータにアクセスできなくなります。|
|[Manage-bde: unlock](manage-bde-unlock.md)|回復パスワードまたは回復キーを BitLocker で保護されたデータにアクセスできます。|
|[Manage-bde: autounlock](manage-bde-autounlock.md)|データ ドライブの自動ロック解除を管理します。|
|[Manage-bde: protectors](manage-bde-protectors.md)|暗号化キーの保護方法を管理します。|
|[Manage-bde: tpm](manage-bde-tpm.md)|コンピューターのトラステッド プラットフォーム モジュール (TPM) を構成します。 このコマンドは Windows 8 を実行するコンピューターではサポートされていないか、 **win8_server_2**します。 これらのコンピューター上の TPM を管理するには、Windows PowerShell の TPM の管理] MMC スナップインまたは TPM 管理コマンドレットを使用します。|
|[Manage-bde: setidentifier](manage-bde-setidentifier.md)|指定された値にドライブのドライブ識別子のフィールドを設定、 **、組織の一意の識別子を提供する** グループ ポリシー設定です。|
|[Manage-bde:ForceRecovery](manage-bde-forcerecovery.md)|再起動時に復旧モードに BitLocker で保護されたドライブを強制します。 このコマンドは、TPM に関連するすべてのキー プロテクターをドライブから削除します。 コンピューターが再起動したら、回復パスワードまたは回復キーは、ドライブのロック解除に使用できます。|
|[Manage-bde: changepassword](manage-bde-changepassword.md)|データ ドライブでパスワードを変更します。|
|[Manage-bde: changepin](manage-bde-changepin.md)|オペレーティング システム ドライブの暗証番号 (pin) を変更します。|
|[Manage-bde: changekey](manage-bde-changekey.md)|オペレーティング システム ドライブのスタートアップ キーを変更します。|
|[Manage-bde:KeyPackage](manage-bde-keypackage.md)|ドライブのキー パッケージを生成します。|
|[Manage-bde: upgrade](manage-bde-upgrade.md)|BitLocker のバージョンにアップグレードします。|
|[Manage-bde:WipeFreeSpace](manage-bde-wipefreespace.md)|ドライブの空き領域を消去します。|
|-? または /?|コマンドプロンプトで簡単なヘルプを表示します。|
|-help または-h|表示は、コマンド プロンプトでヘルプを完了します。|

## <a name="examples"></a>例

は、コンピューター上のドライブを表示し、BitLocker で保護されているかどうか、および現在の暗号化の状態であるかどうかを識別します。
```
manage-bde -status
```
回復パスワードのオプションを使用してドライブ C で BitLocker を有効にする方法を説明します。 回復パスワードは BitLocker によって生成され、画面に表示することを記録できるようにします。
```
manage-bde –on C: -recoverypassword
```
回復パスワードを使用して BitLocker で保護されたドライブのロックを解除する方法を示します。
```
manage-bde –unlock E: -recoverypassword 111111-222222-333333-444444-555555-666666-777777-888888
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [コマンドラインを使用して BitLocker を有効にします。](https://technet.microsoft.com/library/dd894351(v=ws.10).aspx)
