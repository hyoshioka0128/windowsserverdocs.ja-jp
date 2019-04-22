---
title: bitsadmin removecredentials
description: Windows コマンド」のトピック**bitsadmin removecredentials** -ジョブからの資格情報を削除します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4a78ce9a-1feb-4811-a000-cce81287b22b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cbd65442ff0d74ec1179a49df5d4a94785f3dd25
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59822293"
---
# <a name="bitsadmin-removecredentials"></a>bitsadmin removecredentials

ジョブからの資格情報を削除します。

**1.2 およびそれ以前の BITS**: サポートされません。

## <a name="syntax"></a>構文

```
bitsadmin /RemoveCredentials <Job> <Target> <Scheme>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|対象|サーバーまたはプロキシ|
|スキーム|次のいずれかです。</br>-基本的な — これには、サーバーまたはプロキシにクリア テキストでユーザー名とパスワードを送信します。 認証スキームです。</br>-ダイジェスト: チャレンジのデータのサーバーで指定された文字列を使用するチャレンジ/レスポンス認証スキームです。</br>-NTLM: Windows のネットワーク環境での認証、ユーザーの資格情報を使用するチャレンジ/レスポンス認証スキームです。</br>-NEGOTIATE、Simple and Protected ネゴシエーション プロトコル (%tsnego) は、サーバーまたは認証に使用するスキームを決定するプロキシとネゴシエートするチャレンジ/レスポンス認証スキームとも呼ばれます。 たとえば、Kerberos プロトコルや NTLM です。</br>-PASSPORT: メンバー サイトにシングル ログオンを提供する、Microsoft によって提供される認証の集中管理サービス。|

## <a name="BKMK_examples"></a>例

次の例では、資格情報を削除という名前のジョブから*myDownloadJob*します。
```
C:\>bitsadmin /RemoveCredentials myDownloadJob SERVER BASIC
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)