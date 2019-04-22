---
title: repair-bde
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 534dca1a-05f7-4ea8-ac24-4fe5f14f988a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9e2bce0c0a0f12a3a171c161a669c903044e8b4b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813543"
---
# <a name="repair-bde"></a>repair-bde



アクセスでは、ドライブが BitLocker を使用して暗号化されている場合、深刻な破損しているハード_ディスク上のデータが暗号化されます。 有効な回復パスワードまたは回復キーを使用してデータの暗号化が解除されるなら、repair-bde はドライブの重要な部分を再構築して、回復可能なデータを修復できます。 ドライブの BitLocker メタデータ データが破損した場合は、回復パスワードまたは回復キーに加えて、バックアップ キー パッケージを提供できる必要があります。 Active Directory ドメイン サービス (AD DS) バックアップの既定の設定を使用した場合、このキー パッケージは AD DS にバックアップされます。 このキー パッケージと回復パスワードまたは回復キーを使用すると、ディスクが破損した場合でも、BitLocker で保護されたドライブの部分の暗号化を解除できます。 各キー パッケージは、対応するドライブ識別子があるドライブに対してのみ動作します。 使用することができます、 [Active Directory の BitLocker 回復パスワード ビューアー](https://technet.microsoft.com/library/dd875531(v=ws.10).aspx)を AD DS からこのキー パッケージを取得します。

> [!NOTE]
> BitLocker 回復パスワード ビューアーでは、サーバーの管理を使用して、Windows Server 2012 にインストール可能なオプションの管理機能の 1 つとして含まれます。

次の制限事項は、repair-bde コマンド ライン ツールが存在します。
-   修復 bde は、暗号化または復号化プロセス中に失敗したドライブを修復できません。
-   修復 bde は、ドライブの暗号化の場合、ドライブが暗号化されている完全前提としています。

このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
repair-bde <InputVolume> <OutputVolumeorImage> [-rk] [–rp] [-pw] [–kp] [–lf] [-f] [{-?|/?}]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<InputVolume>|修復する BitLocker の暗号化されたドライブのドライブ文字を識別します。 ドライブ文字は、コロンを含める必要があります。例えば：**C:** します。|
|\<OutputVolumeorImage>|修復されたドライブのコンテンツの格納先となるドライブを識別します。 出力ドライブ上のすべての情報は上書きされます。|
|rk|ボリュームのロックを解除するために使用する必要があります、回復キーの場所を示します。 このコマンドは、としても指定する **- recoverykey**します。|
|-rp|ボリュームのロックを解除するために使用する必要がありますの数字の回復パスワードを指定します。 このコマンドは、としても指定する **- recoverypassword**します。|
|-pw|ボリュームのロック解除に使用するパスワードを指定します。 このコマンドは、としても指定する **-パスワード**|
|-kp|ボリュームのロック解除に使用できる回復キー パッケージを識別します。 このコマンドは、としても指定する **- keypackage**します。|
|-lf|Repair-bde エラー、警告、および情報メッセージを格納するファイルへのパスを指定します。 このコマンドは、としても指定する **-logfile**します。|
|-f|これをロックできない場合でもマウントを解除するボリュームを強制します。 このコマンドは、としても指定する **-強制**します。|
|-? または /?|コマンド プロンプトでヘルプを表示します。|

## <a name="remarks"></a>注釈

キー パッケージへのパスが指定されていない場合**修復 bde**キー パッケージのドライブを検索します。 ただし、ハード ドライブが破損した場合、**修復 bde**できないパッケージを検索することがあり、パスを指定するように求められます。

## <a name="BKMK_Examples"></a>例

次の例では、ドライブ C を修復して、ドライブ F に保存されている回復キー ファイル (RecoveryKey.bek) を使用して、ドライブ D に C ドライブからコンテンツを記述しようとし、ドライブ Z にログ ファイル (log.txt) にこの試行の結果を書き込みます。
```
repair-bde C: D: -rk F:\RecoveryKey.bek –lf Z:\log.txt
```
次の例は、C ドライブの修復し、指定された 48 桁の回復パスワードを使用して、ドライブ D に C ドライブに、コンテンツを書き込むを試みます。 各ブロックを分離することをハイフンでは、6 桁の 8 つのブロックで、回復パスワードを入力する必要があります。
```
repair-bde C: D: -rp 111111-222222-333333-444444-555555-666666-777777-888888
```
次の例では、強制的にマウントを解除するドライブ C と C ドライブの修復し、回復キー ファイル (RecoveryKey.bek) ドライブ F に保存されている、回復キー パッケージを使用して、ドライブ D に C ドライブに、コンテンツを書き込むを試みます
```
repair-bde C: D: -kp F:\RecoveryKeyPackage -rk F:\RecoveryKey.bek -f
```
次の例では、ドライブ C を修復し、ドライブ D に C ドライブからコンテンツを記述しようとして入力を求められたら、c: ドライブのロックを解除するパスワードを入力する必要があります。
```
repair-bde C: D: -pw
```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンドライン構文キー](command-line-syntax-key.md)