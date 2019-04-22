---
title: manage-bde のロックを解除します。
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7852bf7d-9102-40be-adcb-71e8f4dfde72
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a86267890449be2048221940e5955e49f30f99f3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814603"
---
# <a name="manage-bde-unlock"></a>manage-bde: ロックを解除



回復パスワードまたは回復キーを使用して BitLocker で保護されたドライブのロックを解除します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
manage-bde -unlock {-recoverypassword <Password>|-recoverykey <PathToExternalKeyFile>} <Drive> [-certificate {-cf PathToCertificateFile | -ct CertificateThumbprint} {-pin}] [-password] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

### <a name="parameters"></a>パラメーター

|パラメーター|Value|説明|
|---------|-----|-----------|
|-recoverypassword||ドライブのロックを解除する回復パスワードが使用されることを指定します。Rp の短縮形:|
||\<パスワード >|ドライブのロックを解除するために使用する回復パスワードを表します。|
|-recoverykey||外部の回復キー ファイルがドライブのロック解除に使用されることを指定します。 短縮形: rk|
||\<PathToExternalKeyFile >|ドライブのロックを解除するために使用される、外部の回復キー ファイルを表します。|
||\<ドライブ >|コロンの後にドライブ文字を表します。|
|-証明書||ボリュームを unclock BitLocker 証明書のローカル ユーザーの証明書については、ローカル ユーザーの証明書ストアにあります。 短縮形:-cert|
||<-cf PathToCertificateFile >|証明書ファイルへのパス|
||<-ct CertificateThumbprint >|必要に応じて、暗証番号 (pin) を含む証明書の拇印 (の暗証番号 (pin))。|
|-パスワード||ボリュームのロックを解除するパスワードを入力するプロンプトが表示されます。 短縮形: pw|
|-computername||別のコンピューターに BitLocker による保護を変更する、bde.exe を使用することを指定します。 短縮形: cn|
||\<名 >|BitLocker による保護を変更するコンピューターの名前を表します。 指定できる値には、コンピューターの NetBIOS 名とコンピューターの IP アドレスが含まれます。|
|-? または /?||ヘルプの簡単なコマンド プロンプトが表示されます。|
|--help または-h||表示は、コマンド プロンプトでヘルプを完了します。|

## <a name="BKMK_Examples"></a>例

次の例を使用して、 **-ロックを解除** 別のドライブにバックアップ フォルダーに保存されている回復キー ファイルを持つドライブ E のロックを解除するコマンドです。
```
manage-bde –unlock E: -recoverykey "F:\Backupkeys\recoverykey.bek"
```

#### <a name="additional-references"></a>その他の参照情報

-   [コマンドライン構文キー](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)