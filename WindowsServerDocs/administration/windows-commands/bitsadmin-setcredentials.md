---
title: bitsadmin setcredentials
description: '**Bitsadmin setcredentials**に関する Windows コマンドのトピック。資格情報をジョブに追加します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3cd099a4-9e85-46d8-8527-edb6dfab7f97
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 96b3973e9b5c01e2577873fa292e4c0725498f91
ms.sourcegitcommit: 141f2d83f70cb467eee59191197cdb9446d8ef31
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/11/2020
ms.locfileid: "81123032"
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

| パラメーター | 説明 |
| -------------- | -------------- |
| 送信 | ジョブの表示名または GUID。 |
| target | **サーバー**または**プロキシ**のいずれかを使用します。 |
| スキーム | 次のいずれかを使用します。<ul><li>**BASIC.。** ユーザー名とパスワードがクリアテキストでサーバーまたはプロキシに送信される認証方式。</li><li>**ダイジェスト.** チャレンジ応答認証方式。サーバーが指定したデータ文字列をチャレンジに使用します。</li><li>**Ml.** Windows ネットワーク環境での認証にユーザーの資格情報を使用するチャレンジ応答認証スキーム。</li><li>**NEGOTIATE (Simple および Protected ネゴシエーションプロトコルとも呼ばれます)。** 認証に使用するスキームを決定するために、サーバーまたはプロキシとネゴシエートするチャレンジ/レスポンス認証スキーム。 たとえば、Kerberos プロトコルや NTLM です。</li><li>**Network.** Microsoft が提供する一元化された認証サービスで、メンバーサイトにシングルログオンを提供します。</li></ul> |
| &lt;ユーザー名&gt; | ユーザーの名前。 |
| password | 指定した*ユーザー名*に関連付けられているパスワード。 |

## <a name="examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブに資格情報を追加します。

```
C:\>bitsadmin /setcredentials myDownloadJob SERVER BASIC Edward password20
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)