---
title: bitsadmin setcredentials
description: Bitsadmin setcredentials コマンドのリファレンストピックでは、資格情報をジョブに追加します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3cd099a4-9e85-46d8-8527-edb6dfab7f97
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4fbedcc65931e7d3cfb1719786f423b0d071b411
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719316"
---
# <a name="bitsadmin-setcredentials"></a>bitsadmin setcredentials

ジョブに資格情報を追加します。

> [!NOTE]
> このコマンドは、BITS 1.2 以前ではサポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /setcredentials <job> <target> <scheme> <username> <password>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| -------------- | -------------- |
| ジョブ (job) | ジョブの表示名または GUID。 |
| ターゲット (target) | **サーバー**または**プロキシ**のいずれかを使用します。 |
| scheme | 次のいずれかを使用します:<ul><li>**BASIC.。** ユーザー名とパスワードがクリアテキストでサーバーまたはプロキシに送信される認証方式。</li><li>**ダイジェスト.** チャレンジ応答認証方式。サーバーが指定したデータ文字列をチャレンジに使用します。</li><li>**Ml.** Windows ネットワーク環境での認証にユーザーの資格情報を使用するチャレンジ応答認証スキーム。</li><li>**NEGOTIATE (Simple および Protected ネゴシエーションプロトコルとも呼ばれます)。** 認証に使用するスキームを決定するために、サーバーまたはプロキシとネゴシエートするチャレンジ/レスポンス認証スキーム。 たとえば、Kerberos プロトコルや NTLM です。</li><li>**Network.** Microsoft が提供する一元化された認証サービスで、メンバーサイトにシングルログオンを提供します。</li></ul> |
| &lt;ユーザー名&gt; | ユーザーの名前です。 |
| password | 指定した*ユーザー名*に関連付けられているパスワード。 |

## <a name="examples"></a>例

*Mydownloadjob*という名前のジョブに資格情報を追加するには、次のようにします。

```
bitsadmin /setcredentials myDownloadJob SERVER BASIC Edward password20
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bitsadmin コマンド](bitsadmin.md)
