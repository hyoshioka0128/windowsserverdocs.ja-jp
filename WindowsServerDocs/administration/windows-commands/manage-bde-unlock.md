---
title: manage-bde のロック解除
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7852bf7d-9102-40be-adcb-71e8f4dfde72
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3fd303116e101c8c8503d220ba382d6cdd994ad3
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724067"
---
# <a name="manage-bde-unlock"></a>manage-bde: unlock



回復パスワードまたは回復キーを使用して BitLocker で保護されたドライブのロックを解除します。

## <a name="syntax"></a>構文

```
manage-bde -unlock {-recoverypassword <Password>|-recoverykey <PathToExternalKeyFile>} <Drive> [-certificate {-cf PathToCertificateFile | -ct CertificateThumbprint} {-pin}] [-password] [-computername <Name>] [{-?|/?}] [{-help|-h}]
```

#### <a name="parameters"></a>パラメーター

|パラメーター|値|説明|
|---------|-----|-----------|
|-recoverypassword||ドライブのロックを解除する回復パスワードが使用されることを指定します。Rp の短縮形:|
||\<パスワード>|ドライブのロックを解除するために使用する回復パスワードを表します。|
|-recoverykey||外部の回復キー ファイルがドライブのロック解除に使用されることを指定します。 短縮形: rk|
||\<PathToExternalKeyFile>|ドライブのロックを解除するために使用される、外部の回復キー ファイルを表します。|
||\<ドライブ>|コロンの後にドライブ文字を表します。|
|-証明書||ボリュームを unclock BitLocker 証明書のローカル ユーザーの証明書については、ローカル ユーザーの証明書ストアにあります。 短縮形:-cert|
||<-cf PathToCertificateFile >|証明書ファイルへのパス|
||<-ct CertificateThumbprint >|必要に応じて、暗証番号 (pin) を含む証明書の拇印 (の暗証番号 (pin))。|
|-パスワード||ボリュームのロックを解除するパスワードを入力するプロンプトが表示されます。 短縮形: pw|
|-computername||別のコンピューターに BitLocker による保護を変更する、bde.exe を使用することを指定します。 短縮形: cn|
||\<Name>|BitLocker による保護を変更するコンピューターの名前を表します。 指定できる値には、コンピューターの NetBIOS 名とコンピューターの IP アドレスが含まれます。|
|-? または /?||コマンドプロンプトで簡単なヘルプを表示します。|
|-help または-h||表示は、コマンド プロンプトでヘルプを完了します。|

## <a name="examples"></a>例

**-Unlock**コマンドを使用して、別のドライブのバックアップフォルダーに保存されている回復キーファイルでドライブ E のロックを解除する方法を示します。
```
manage-bde –unlock E: -recoverykey F:\Backupkeys\recoverykey.bek
```

## <a name="additional-references"></a>その他のリファレンス

-   - [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [Manage-bde](manage-bde.md)