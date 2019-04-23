---
title: manage-bde
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f6a12814-df74-416c-a04a-62ea8512263e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b50cad64025e85824a8f0a27d773ffb614491fe5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841183"
---
# <a name="manage-bde-on"></a>manage-bde: 上



ドライブを暗号化し、BitLocker をオンにします。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
manage-bde –on <Drive> {[-recoveryPassword <NumericalPassword>]|[-recoverykey <PathToExternalDirectory>]|[-startupkey <PathToExternalKeyDirectory>]|[-certificate]|
[-tpmandpin]|[-tpmandpinandstartupkey <PathToExternalKeyDirectory>]|[-tpmandstartupkey <PathToExternalKeyDirectory>]|[-password]|[-ADAccountOrGroup <Domain\Account>]}
[-UsedSpaceOnly][-encryptionmethod {aes128_diffuser|aes256_diffuser|aes128|aes256}] [-skiphardwaretest] [-discoveryvolumetype <FileSystemType>] [-ForceEncryptionType <type>] [-RemoveVolumeShadowCopies][-computername <Name>] 
[{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<ドライブ >|コロンの後にドライブ文字を表します。|
|-recoverypassword|数字のパスワード保護機能を追加します。 使用することも **- rp**としてこのコマンドの簡易版です。|
|\<NumericalPassword>|回復パスワードを表します。|
|-recoverykey|回復用の外部キー プロテクターを追加します。 使用することも**rk**としてこのコマンドの簡易版です。|
|\<PathToExternalDirectory >|回復キーをディレクトリのパスを表します。|
|-startupkey|スタートアップの外部キー保護機能を追加します。 使用することも **-sk**としてこのコマンドの簡易版です。|
|\<PathToExternalKeyDirectory >|スタートアップ キーには、ディレクトリ パスを表します。|
|-証明書|データ ドライブのパブリック キー保護機能を追加します。 使用することも **-cert** としてこのコマンドの簡易版です。|
|-tpmandpin|トラステッド プラットフォーム モジュール (TPM) と、オペレーティング システム ドライブの個人識別番号 (PIN) 保護が機能を追加します。 使用することも **-tp**としてこのコマンドの簡易版です。|
|-tpmandstartupkey|オペレーティング システム ドライブの TPM とスタートアップ キー プロテクターを追加します。 使用することも **-やれ**としてこのコマンドの簡易版です。|
|-tpmandpinandstartupkey|TPM、PIN、およびオペレーティング システム ドライブのスタートアップ キーの保護機能を追加します。 使用することも **- tpsk**としてこのコマンドの簡易版です。|
|-パスワード|データ ドライブのパスワードのキー保護機能を追加します。 使用することも **- pw** としてこのコマンドの簡易版です。|
|-ADAccountOrGroup|ボリュームの SID に基づく id 保護機能を追加します。 ボリュームは、ユーザーまたはコンピューターに適切な資格情報がある場合に自動的に解除されます。 コンピューター アカウントを指定する場合は、追加、 **$** コンピューターに名前を指定し、指定 **– サービス**の代わりに、BitLocker のサーバーのコンテンツで、ロックの解除が発生することを示すために、ユーザー。 使用することも **-sid** としてこのコマンドの簡易版です。|
|-UsedSpaceOnly|使用済み領域のみ暗号化するには、暗号化モードを設定します。 使用済み領域を含むボリュームのセクションでは暗号化されますが、空き領域は表示されません。 このオプションが指定されていない場合は、すべての使用領域と、ボリューム上の空き領域が暗号化されます. 使用することも **-使用**としてこのコマンドの簡易版です。|
|-encryptionMethod|暗号化アルゴリズムとキーのサイズを構成します。 使用することも **-em**としてこのコマンドの簡易版です。|
|-skiphardwaretest|ハードウェア テストをせずに暗号化を開始します。 使用することも **-s**としてこのコマンドの簡易版です。|
|-discoveryvolumetype|検出データ ドライブを使用するファイル システムを指定します。 検出データ ドライブが FAT 形式、BitLocker で保護されたリムーバブル データ ドライブを BitLocker で保護されたドライブを表示する Windows Vista または Windows XP オペレーティング システムを使用できるように、BitLocker To Go リーダーが含まれていますに追加された非表示ドライブ。|
|-ForceEncryptionType|ソフトウェアまたはハードウェアの暗号化を使用する BitLocker を強制します。 どちらかを指定することができます**ハードウェア**または**ソフトウェア**暗号化の種類として。 場合、**ハードウェア**パラメーターを選択すると、ドライブがハードウェアの暗号化をサポートしていませんが、manage-bde でエラーが返されます。 グループ ポリシー設定では、指定した暗号化の種類で禁止、manage-bde ではエラーが返されます。 使用することも **-fet**としてこのコマンドの簡易版です。|
|-RemoveVolumeShadowCopies|ボリュームのボリューム シャドウ コピーの deletikon を強制します。 このコマンドを実行した後、以前のシステム復元ポイントを使用してこのボリュームを復元することはできません。 使用することも **- rvsc**としてこのコマンドの簡易版です。|
|\<FileSystemType>|検出データ ドライブで使用できるファイル システムを指定します。FAT32、既定では、または none。|
|-computername|別のコンピューターで BitLocker 保護を変更する、manage-bde が使用されていることを指定します。 使用することも **- cn**としてこのコマンドの簡易版です。|
|\<名 >|BitLocker による保護を変更するコンピューターの名前を表します。 指定できる値には、コンピューターの NetBIOS 名とコンピューターの IP アドレスが含まれます。|
|-? または /?|ヘルプの簡単なコマンド プロンプトが表示されます。|
|--help または-h|表示は、コマンド プロンプトでヘルプを完了します。|

## <a name="BKMK_Examples"></a>例

次の例を使用して、 **-で**コマンドを C ドライブの BitLocker を有効にし、ドライブを回復パスワードを追加します。
```
manage-bde –on C: -recoverypassword
```
次の例を使用して、 **-で**C ドライブの BitLocker を有効にし、ドライブに回復パスワードを追加し、ドライブ E に回復キーを保存するコマンド
```
manage-bde –on C: -recoverykey E:\ -recoverypassword
```
次の例を使用して、 **-で**オペレーティング システム ドライブのロックを解除する (USB キー) などの外部キー プロテクターを使用して、C ドライブの BitLocker を有効にするコマンド。 このメソッドは、TPM がないコンピューターで BitLocker を使用している場合に必要です。
```
manage-bde -on C: -startupkey E:\
```
次の例を使用して、 **-で**コマンド データ ドライブ E の BitLocker をオンにし、パスワード、キー保護機能を追加します。 Manage-bde は、このコマンドを入力した後、パスワードの入力を求められます。
```
manage-bde –on E: -pw
```
次の例を使用して、 **-で**オペレーティング システムのドライブ C の BitLocker を有効にして、ハードウェア ベースの暗号化を使用するコマンド。
```
manage-bde –on C: -fet Hardware
```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンドライン構文キー](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)