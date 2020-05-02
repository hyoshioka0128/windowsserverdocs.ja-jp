---
title: bitsadmin sethelpertokenflags
description: Bitsadmin se pertokenflags コマンドのリファレンストピック。 BITS 転送ジョブに関連付けられているヘルパートークンの使用フラグを設定します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 03/01/2019
ms.openlocfilehash: 2bb93664d88c0f346e2926102f97287ac8fc35de
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719369"
---
# <a name="bitsadmin-sethelpertokenflags"></a>bitsadmin sethelpertokenflags

BITS 転送ジョブに関連付けられている [ヘルパートークン](https://docs.microsoft.com/windows/win32/bits/helper-tokens-for-bits-transfer-jobs) の使用フラグを設定します。

> [!NOTE]
> このコマンドは、BITS 3.0 以前ではサポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /sethelpertokenflags <job> <flags>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| --------- | ----------- |
| ジョブ (job) | ジョブの表示名または GUID。 |
| flags | 次のようなヘルパートークン値を使用できます。<ul><li>**0x0001.** アップロードジョブのローカルファイルを開き、ダウンロードジョブの一時ファイルを作成または名前変更するため、またはアップロード/応答ジョブの応答ファイルを作成または名前を変更するために使用します。</li><li>**0x0002.** サーバーメッセージブロック (SMB) のアップロードジョブまたはダウンロードジョブのリモートファイルを開くため、または暗黙の NTLM または Kerberos 資格情報に対する HTTP サーバーまたはプロキシチャレンジに対する応答として使用されます。</li></ul>HTTP 経由で `/setcredentialsjob targetscheme null null` 資格情報を送信するには、を呼び出す必要があります。 |

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
