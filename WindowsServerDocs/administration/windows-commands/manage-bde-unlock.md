---
title: manage-bde のロック解除
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7852bf7d-9102-40be-adcb-71e8f4dfde72
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e26952ca8c2b20cb0cb8efa167fca81e27b692a0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80839739"
---
# <a name="manage-bde-unlock"></a>manage-bde: unlock



回復パスワードまたは回復キーを使用して BitLocker で保護されたドライブのロックを解除します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
manage-bde -unlock {-recoverypassword <Password>|-recoverykey <PathToExternalKeyFile>} <Drive> [-certificate {-cf PathToCertificateFile | -ct CertificateThumbprint} {-pin}] [-password] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

#### <a name="parameters"></a>パラメーター

|パラメーター|値|説明|
|---------|-----|-----------|
|-recoverypassword||ドライブのロックを解除する回復パスワードが使用されることを指定します。Rp の短縮形:|
||\<パスワード >|ドライブのロックを解除するために使用する回復パスワードを表します。|
|-recoverykey||外部の回復キー ファイルがドライブのロック解除に使用されることを指定します。 短縮形: rk|
||\<PathToExternalKeyFile >|ドライブのロックを解除するために使用される、外部の回復キー ファイルを表します。|
||\<ドライブ >|コロンの後にドライブ文字を表します。|
|-証明書||ボリュームを unclock BitLocker 証明書のローカル ユーザーの証明書については、ローカル ユーザーの証明書ストアにあります。 短縮形:-cert|
||<-cf PathToCertificateFile >|証明書ファイルへのパス|
||<-ct CertificateThumbprint >|必要に応じて、暗証番号 (pin) を含む証明書の拇印 (の暗証番号 (pin))。|
|-password||ボリュームのロックを解除するパスワードを入力するプロンプトが表示されます。 短縮形: pw|
|-computername||別のコンピューターに BitLocker による保護を変更する、bde.exe を使用することを指定します。 短縮形: cn|
||\<名 >|BitLocker による保護を変更するコンピューターの名前を表します。 指定できる値には、コンピューターの NetBIOS 名とコンピューターの IP アドレスが含まれます。|
|-? または /?||コマンドプロンプトで簡単なヘルプを表示します。|
|-help または-h||表示は、コマンド プロンプトでヘルプを完了します。|

## <a name="examples"></a><a name=BKMK_Examples></a>例

次の例を使用して、 **-ロックを解除** 別のドライブにバックアップ フォルダーに保存されている回復キー ファイルを持つドライブ E のロックを解除するコマンドです。
```
manage-bde –unlock E: -recoverykey F:\Backupkeys\recoverykey.bek
```

## <a name="additional-references"></a>その他の参照情報

-   - [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)