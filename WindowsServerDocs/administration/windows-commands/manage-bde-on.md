---
title: 管理-bde オン
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f6a12814-df74-416c-a04a-62ea8512263e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1785c10ade5f7aace8595d8d0972fb1fa315232b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80840015"
---
# <a name="manage-bde-on"></a>manage-bde: on



ドライブを暗号化し、BitLocker をオンにします。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
manage-bde –on <Drive> {[-recoveryPassword <NumericalPassword>]|[-recoverykey <PathToExternalDirectory>]|[-startupkey <PathToExternalKeyDirectory>]|[-certificate]|
[-tpmandpin]|[-tpmandpinandstartupkey <PathToExternalKeyDirectory>]|[-tpmandstartupkey <PathToExternalKeyDirectory>]|[-password]|[-ADAccountOrGroup <Domain\Account>]}
[-UsedSpaceOnly][-encryptionmethod {aes128_diffuser|aes256_diffuser|aes128|aes256}] [-skiphardwaretest] [-discoveryvolumetype <FileSystemType>] [-ForceEncryptionType <type>] [-RemoveVolumeShadowCopies][-computername <Name>] 
[{-?|/?}] [{-help|-h}]
```

#### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<ドライブ >|コロンの後にドライブ文字を表します。|
|-recoverypassword|数字のパスワード保護機能を追加します。 また、 **-rp**をこのコマンドの省略版として使用することもできます。|
|\<NumericalPassword >|回復パスワードを表します。|
|-recoverykey|回復用の外部キー保護機能を追加します。 このコマンドの省略版として **-rk**を使用することもできます。|
|\<PathToExternalDirectory >|回復キーへのディレクトリパスを表します。|
|-startupkey|スタートアップ用の外部キー保護機能を追加します。 また、このコマンドの省略版として **-sk**を使用することもできます。|
|\<PathToExternalKeyDirectory >|スタートアップキーへのディレクトリパスを表します。|
|-証明書|データドライブの公開キープロテクターを追加します。 使用することも **-cert** としてこのコマンドの簡易版です。|
|-tpmandpin|オペレーティングシステムドライブのトラステッドプラットフォームモジュール (TPM) と暗証番号 (PIN) の保護機能を追加します。 また、このコマンドの省略版として **-tp**を使用することもできます。|
|-tpmandstartupkey|オペレーティングシステムドライブの TPM とスタートアップキーの保護機能を追加します。 このコマンドの省略版として **-やれやれ**を使用することもできます。|
|-tpmandpinandstartupkey|オペレーティングシステムドライブの TPM、PIN、スタートアップキーの保護機能を追加します。 また、このコマンドの省略版として **-tpsk**を使用することもできます。|
|-password|データドライブのパスワードキー保護機能を追加します。 使用することも **- pw** としてこのコマンドの簡易版です。|
|-ADAccountOrGroup|ボリュームの SID ベースの id プロテクターを追加します。 ユーザーまたはコンピューターが適切な資格情報を持っている場合、ボリュームは自動的にロック解除されます。 コンピューターアカウントを指定する場合は、コンピューター名に **$** を追加し、 **-service**を指定して、ユーザーではなく BitLocker サーバーのコンテンツでロック解除が行われることを示します。 使用することも **-sid** としてこのコマンドの簡易版です。|
|-UsedSpaceOnly|暗号化モードを、使用領域のみの暗号化に設定します。 使用済み領域を含むボリュームのセクションは暗号化されますが、空き領域は暗号化されません。 このオプションが指定されていない場合、ボリュームの使用済み領域と空き領域がすべて暗号化されます。 このコマンドの簡略版と**して使用すること**もできます。|
|-encryptionMethod|暗号化アルゴリズムとキーサイズを構成します。 また、このコマンドの省略版として **-em**を使用することもできます。|
|-skiphardwaretest|ハードウェアテストなしで暗号化を開始します。 また、このコマンドの省略版として **-s**を使用することもできます。|
|-discoveryvolumetype|探索データドライブに使用するファイルシステムを指定します。 検出データドライブは、FAT 形式の BitLocker で保護されたリムーバブルデータドライブに追加された隠しドライブで、Windows Vista または Windows XP オペレーティングシステムを使用して BitLocker で保護されたドライブを表示できるように、BitLocker To Go リーダーが含まれています。|
|-ForceEncryptionType|BitLocker でソフトウェアまたはハードウェアの暗号化を強制的に使用します。 暗号化の種類として、**ハードウェア**または**ソフトウェア**を指定できます。 **ハードウェア**パラメーターが選択されていても、ドライブがハードウェアの暗号化をサポートしていない場合、manage-bde はエラーを返します。 指定した暗号化の種類がグループポリシー設定で禁止されている場合、manage-bde はエラーを返します。 このコマンドの省略版として **-fet**を使用することもできます。|
|-RemoveVolumeShadowCopies|ボリュームのボリュームシャドウコピーを強制的に deletikon します。 このコマンドを実行した後、以前のシステム復元ポイントを使用してこのボリュームを復元することはできません。 このコマンドの簡略版として **-rvsc**を使用することもできます。|
|\<FileSystemType >|検出データドライブと共に使用できるファイルシステム (FAT32、既定、またはなし) を指定します。|
|-computername|別のコンピューター上の BitLocker 保護を変更するために管理-bde を使用することを指定します。 また、このコマンドの省略版として **-cn**を使用することもできます。|
|\<名 >|BitLocker による保護を変更するコンピューターの名前を表します。 指定できる値には、コンピューターの NetBIOS 名とコンピューターの IP アドレスが含まれます。|
|-? または /?|コマンドプロンプトで簡単なヘルプを表示します。|
|-help または-h|表示は、コマンド プロンプトでヘルプを完了します。|

## <a name="examples"></a><a name=BKMK_Examples></a>例

次の例では、 **-on**コマンドを使用してドライブ C の BitLocker をオンにし、回復パスワードをドライブに追加する方法を示します。
```
manage-bde –on C: -recoverypassword
```
次の例では、 **-on**コマンドを使用して、ドライブ C に対して BitLocker を有効にし、回復パスワードをドライブに追加し、回復キーをドライブ E に保存する方法を示します。
```
manage-bde –on C: -recoverykey E:\ -recoverypassword
```
次の例では、 **-on**コマンドを使用して、オペレーティングシステムドライブのロックを解除する外部キープロテクター (USB キーなど) を使用してドライブ C の BitLocker を有効にする方法を示します。 TPM が搭載されていないコンピューターで BitLocker を使用する場合は、この方法が必要です。
```
manage-bde -on C: -startupkey E:\
```
次の例では、 **-on**コマンドを使用して、データドライブ E に対して BitLocker を有効にし、パスワードキー保護機能を追加する方法を示します。 このコマンドを入力すると、manage-bde によってパスワードの入力が求められます。
```
manage-bde –on E: -pw
```
次の例では、 **-on**コマンドを使用して、オペレーティングシステムドライブ C の BitLocker をオンにし、ハードウェアベースの暗号化を使用する方法を示します。
```
manage-bde –on C: -fet Hardware
```

## <a name="additional-references"></a>その他の参照情報

-   - [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)