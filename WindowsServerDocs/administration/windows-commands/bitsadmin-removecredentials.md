---
title: bitsadmin removecredentials
description: Bitsadmin **removecredentials**の Windows コマンドに関するトピックでは、ジョブから資格情報が削除されます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4a78ce9a-1feb-4811-a000-cce81287b22b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 55ff7e2a813c7cc6b60e04d55ef63804a2aed796
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849845"
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
| 送信 | ジョブの表示名または GUID。 |
| target | **サーバー**または**プロキシ**のいずれかを使用します。 |
| スキーム | 次のいずれかを使用します。<ul><li>**基本的な。** ユーザー名とパスワードがクリアテキストでサーバーまたはプロキシに送信される認証方式。</li><li>**ダイジェスト.** チャレンジ応答認証方式。サーバーが指定したデータ文字列をチャレンジに使用します。</li><li>**Ml.** Windows ネットワーク環境での認証にユーザーの資格情報を使用するチャレンジ応答認証スキーム。</li><li>**negotiate (Simple および Protected ネゴシエーションプロトコルとも呼ばれます)。** 認証に使用するスキームを決定するために、サーバーまたはプロキシとネゴシエートするチャレンジ/レスポンス認証スキーム。 たとえば、Kerberos プロトコルや NTLM です。</li><li>**network.** Microsoft が提供する一元化された認証サービスで、メンバーサイトにシングルログオンを提供します。</li></ul> |

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、 *Mydownloadjob*という名前のジョブから資格情報を削除します。

```
C:\>bitsadmin /removecredentials myDownloadJob server basic
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)