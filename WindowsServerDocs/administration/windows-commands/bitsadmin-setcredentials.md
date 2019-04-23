---
title: bitsadmin setcredentials
description: Windows コマンド」のトピック**bitsadmin setcredentials** -ジョブに資格情報を追加します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3cd099a4-9e85-46d8-8527-edb6dfab7f97
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 923dcff7d268d40b72db3254e2a97c808c7c7253
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877393"
---
# <a name="bitsadmin-setcredentials"></a>bitsadmin setcredentials

ジョブには、資格情報を追加します。

**1.2 およびそれ以前の BITS**: サポートされません。

## <a name="syntax"></a>構文

```
bitsadmin /SetCredentials <Job> <Target> <Scheme> <Username> <Password>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|対象|サーバーまたはプロキシ|
|スキーム|次のいずれかです。</br>-基本的な — これには、サーバーまたはプロキシにクリア テキストでユーザー名とパスワードを送信します。 認証スキームです。</br>-ダイジェスト: チャレンジのデータのサーバーで指定された文字列を使用するチャレンジ/レスポンス認証スキームです。</br>-NTLM: Windows のネットワーク環境での認証、ユーザーの資格情報を使用するチャレンジ/レスポンス認証スキームです。</br>-NEGOTIATE、Simple and Protected ネゴシエーション プロトコル (%tsnego) は、サーバーまたは認証に使用するスキームを決定するプロキシとネゴシエートするチャレンジ/レスポンス認証スキームとも呼ばれます。 たとえば、Kerberos プロトコルや NTLM です。</br>-PASSPORT: メンバー サイトにシングル ログオンを提供する、Microsoft によって提供される認証の集中管理サービス。|
|Username|指定された資格情報の名前|
|パスワード|関連付けられた、指定されたパスワード*ユーザー名*|

## <a name="BKMK_examples"></a>例

という名前のジョブを次の例 Adds 資格情報*myDownloadJob*します。
```
C:\>bitsadmin /RemoveCredentials myDownloadJob SERVER BASIC Edward Password20
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)