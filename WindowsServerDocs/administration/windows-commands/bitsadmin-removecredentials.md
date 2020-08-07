---
title: bitsadmin removecredentials
description: Bitsadmin removecredentials コマンドの参照記事。ジョブから資格情報が削除されます。
ms.topic: article
ms.assetid: 4a78ce9a-1feb-4811-a000-cce81287b22b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2e2d9d045af51b273f7b64a8513daf3f8adb3895
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87893356"
---
# <a name="bitsadmin-removecredentials"></a>bitsadmin removecredentials

ジョブから資格情報を削除します。

> [!NOTE]
> このコマンドは、BITS 1.2 以前ではサポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /removecredentials <job> <target> <scheme>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |
| ターゲット (target) | **サーバー**または**プロキシ**のいずれかを使用します。 |
| scheme | 次のいずれかを使用します:<ul><li>**BASIC.。** ユーザー名とパスワードがクリアテキストでサーバーまたはプロキシに送信される認証方式。</li><li>**ダイジェスト.** チャレンジ応答認証方式。サーバーが指定したデータ文字列をチャレンジに使用します。</li><li>**Ml.** Windows ネットワーク環境での認証にユーザーの資格情報を使用するチャレンジ応答認証スキーム。</li><li>**NEGOTIATE (Simple および Protected ネゴシエーションプロトコルとも呼ばれます)。** 認証に使用するスキームを決定するために、サーバーまたはプロキシとネゴシエートするチャレンジ/レスポンス認証スキーム。 たとえば、Kerberos プロトコルや NTLM です。</li><li>**Network.** Microsoft が提供する一元化された認証サービスで、メンバーサイトにシングルログオンを提供します。</li></ul> |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブから資格情報を削除するには、次のようにします。

```
bitsadmin /removecredentials myDownloadJob SERVER BASIC
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
