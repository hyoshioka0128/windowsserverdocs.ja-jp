---
title: bitsadmin sea pertokenflags
description: '**Bitsadmin se pertokenflags**の Windows コマンドに関するトピックでは、BITS 転送ジョブに関連付けられているヘルパートークンの使用フラグを設定しています。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 77fac03dba2bb0686a98206405622e2eb398953e
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/11/2020
ms.locfileid: "81122975"
---
# <a name="bitsadmin-sethelpertokenflags"></a>bitsadmin sea pertokenflags

BITS 転送ジョブに関連付けられている  [ヘルパートークン](https://docs.microsoft.com/windows/win32/bits/helper-tokens-for-bits-transfer-jobs)の使用フラグを設定します。

> [!NOTE]
> このコマンドは、BITS 3.0 以前ではサポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /sethelpertokenflags <job> <flags>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| 送信 | ジョブの表示名または GUID。 |
| flags | 次のようなヘルパートークン値を使用できます。<ul><li>**0x0001.** アップロードジョブのローカルファイルを開き、ダウンロードジョブの一時ファイルを作成または名前変更するため、またはアップロード/応答ジョブの応答ファイルを作成または名前を変更するために使用します。</li><li>**0x0002.** サーバーメッセージブロック (SMB) のアップロードジョブまたはダウンロードジョブのリモートファイルを開くため、または暗黙の NTLM または Kerberos 資格情報に対する HTTP サーバーまたはプロキシチャレンジに対する応答として使用されます。</li></ul>HTTP 経由で資格情報を送信するには、 `/setcredentialsjob targetscheme null null` を呼び出す必要があります。 |

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
