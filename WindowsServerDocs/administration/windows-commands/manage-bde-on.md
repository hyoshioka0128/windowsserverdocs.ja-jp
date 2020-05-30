---
title: 管理-bde オン
description: ドライブを暗号化し、BitLocker を有効にする manage-bde on コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f6a12814-df74-416c-a04a-62ea8512263e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bad56c9ade19d94fc5acc9b34a8cc42fe43b7c0d
ms.sourcegitcommit: 29bc8740e5a8b1ba8f73b10ba4d08afdf07438b0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/30/2020
ms.locfileid: "84222855"
---
# <a name="manage-bde-on"></a>管理-bde オン

ドライブを暗号化し、BitLocker をオンにします。

## <a name="syntax"></a>構文

```
manage-bde –on <drive> {[-recoverypassword <numericalpassword>]|[-recoverykey <pathtoexternaldirectory>]|[-startupkey <pathtoexternalkeydirectory>]|[-certificate]|
[-tpmandpin]|[-tpmandpinandstartupkey <pathtoexternalkeydirectory>]|[-tpmandstartupkey <pathtoexternalkeydirectory>]|[-password]|[-ADaccountorgroup <domain\account>]}
[-usedspaceonly][-encryptionmethod {aes128_diffuser|aes256_diffuser|aes128|aes256}] [-skiphardwaretest] [-discoveryvolumetype <filesystemtype>] [-forceencryptiontype <type>] [-removevolumeshadowcopies][-computername <name>]
[{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<drive>` | コロンの後にドライブ文字を表します。 |
| -recoverypassword | 数字のパスワード保護機能を追加します。 また、 **-rp**をこのコマンドの省略版として使用することもできます。 |
| `<numericalpassword>` | 回復パスワードを表します。 |
| -recoverykey | 回復用の外部キー保護機能を追加します。 このコマンドの省略版として **-rk**を使用することもできます。 |
| `<pathtoexternaldirectory>` | 回復キーへのディレクトリパスを表します。 |
| -startupkey | スタートアップ用の外部キー保護機能を追加します。 また、このコマンドの省略版として **-sk**を使用することもできます。 |
| `<pathtoexternalkeydirectory>` | スタートアップキーへのディレクトリパスを表します。 |
| -証明書 | データドライブの公開キープロテクターを追加します。 使用することも **-cert** としてこのコマンドの簡易版です。 |
| -tpmandpin | オペレーティングシステムドライブのトラステッドプラットフォームモジュール (TPM) と暗証番号 (PIN) の保護機能を追加します。 また、このコマンドの省略版として **-tp**を使用することもできます。 |
| -tpmandstartupkey | オペレーティングシステムドライブの TPM とスタートアップキーの保護機能を追加します。 このコマンドの省略版として **-やれやれ**を使用することもできます。 |
| -tpmandpinandstartupkey | オペレーティングシステムドライブの TPM、PIN、スタートアップキーの保護機能を追加します。 また、このコマンドの省略版として **-tpsk**を使用することもできます。 |
| -パスワード | データドライブのパスワードキー保護機能を追加します。 使用することも **- pw** としてこのコマンドの簡易版です。 |
| -ADaccountorgroup | ボリュームの SID ベースの id プロテクターを追加します。 ユーザーまたはコンピューターが適切な資格情報を持っている場合、ボリュームは自動的にロック解除されます。 コンピューターアカウントを指定する場合は、 **$** コンピューター名にを追加し、 **-service**を指定して、ユーザーではなく BitLocker サーバーのコンテンツでロック解除が行われることを示します。 使用することも **-sid** としてこのコマンドの簡易版です。 |
| -used space のみ | 暗号化モードを、使用領域のみの暗号化に設定します。 使用済み領域を含むボリュームのセクションは暗号化されますが、空き領域は暗号化されません。 このオプションが指定されていない場合、ボリュームの使用済み領域と空き領域がすべて暗号化されます。 このコマンドの簡略版と**して使用すること**もできます。 |
| -encryptionMethod | 暗号化アルゴリズムとキーサイズを構成します。 また、このコマンドの省略版として **-em**を使用することもできます。 |
| -skiphardwaretest | ハードウェアテストなしで暗号化を開始します。 また、このコマンドの省略版として **-s**を使用することもできます。 |
| -discoveryvolumetype | 探索データドライブに使用するファイルシステムを指定します。 探索データドライブは、FAT 形式の BitLocker で保護されたリムーバブルデータドライブに追加された、BitLocker To Go リーダーを含む隠しドライブです。 |
| -forceencryptiontype | BitLocker でソフトウェアまたはハードウェアの暗号化を強制的に使用します。 暗号化の種類として、**ハードウェア**または**ソフトウェア**を指定できます。 **ハードウェア**パラメーターが選択されていても、ドライブがハードウェアの暗号化をサポートしていない場合、manage-bde はエラーを返します。 指定した暗号化の種類がグループポリシー設定で禁止されている場合、manage-bde はエラーを返します。 このコマンドの省略版として **-fet**を使用することもできます。 |
| -removevolumeshadowcopies | ボリュームのボリュームシャドウコピーを強制的に削除します。 このコマンドを実行した後、以前のシステム復元ポイントを使用してこのボリュームを復元することはできません。 このコマンドの簡略版として **-rvsc**を使用することもできます。 |
| `<filesystemtype>` | 検出データドライブと共に使用できるファイルシステム (FAT32、既定、またはなし) を指定します。 |
| -computername | 別のコンピューター上の BitLocker 保護を変更するために管理-bde を使用することを指定します。 また、このコマンドの省略版として **-cn**を使用することもできます。 |
| `<name>` | BitLocker による保護を変更するコンピューターの名前を表します。 指定できる値には、コンピューターの NetBIOS 名とコンピューターの IP アドレスが含まれます。 |
| -? または /? | コマンドプロンプトで簡単なヘルプを表示します。 |
| -help または-h | 表示は、コマンド プロンプトでヘルプを完了します。 |

### <a name="examples"></a>例

ドライブ C に対して BitLocker を有効にし、回復パスワードをドライブに追加するには、次のように入力します。

```
manage-bde –on C: -recoverypassword
```

ドライブ C に対して BitLocker を有効にするには、回復パスワードをドライブに追加し、回復キーをドライブ E に保存するには、次のように入力します。

```
manage-bde –on C: -recoverykey E:\ -recoverypassword
```

ドライブ C に対して BitLocker を有効にするには、外部キープロテクター (USB キーなど) を使用してオペレーティングシステムドライブのロックを解除するには、次のように入力します。

```
manage-bde -on C: -startupkey E:\
```

> [!IMPORTANT]
> TPM が搭載されていないコンピューターで BitLocker を使用する場合は、この方法が必要です。

データドライブ E に対して BitLocker を有効にし、パスワードキー保護機能を追加するには、次のように入力します。

```
manage-bde –on E: -pw
```

オペレーティングシステムドライブ C に対して BitLocker を有効にし、ハードウェアベースの暗号化を使用するには、次のように入力します。

```
manage-bde –on C: -fet hardware
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [manage-bde コマンドの管理](manage-bde-off.md)

- [manage-bde pause コマンド](manage-bde-pause.md)

- [manage-bde resume コマンド](manage-bde-resume.md)

- [manage-bde コマンド](manage-bde.md)
