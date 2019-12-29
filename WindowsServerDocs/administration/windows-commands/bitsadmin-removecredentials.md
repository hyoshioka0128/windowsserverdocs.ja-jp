---
title: bitsadmin removecredentials
description: '**Bitsadmin removecredentials**の Windows コマンドに関するトピックでは、ジョブから資格情報を削除します。'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 34a5bae9304a9db9f47f437276270ca06b1ebeee
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380817"
---
# <a name="bitsadmin-removecredentials"></a>bitsadmin removecredentials

ジョブから資格情報を削除します。

**BITS 1.2 以前**: サポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /RemoveCredentials <Job> <Target> <Scheme>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|移行先|サーバーまたはプロキシ|
|体系|次のいずれかです。</br>-BASIC: ユーザー名とパスワードがクリアテキストでサーバーまたはプロキシに送信される認証方式。</br>-DIGEST —チャレンジ応答認証方式。サーバーが指定したデータ文字列をチャレンジに使用します。</br>-NTLM-Windows ネットワーク環境での認証にユーザーの資格情報を使用するチャレンジ応答認証方式。</br>-NEGOTIATE — Simple and Protected negotiate protocol (Snego) は、認証に使用するスキームを決定するために、サーバーまたはプロキシとネゴシエートするチャレンジ/レスポンス認証方式です。 たとえば、Kerberos プロトコルや NTLM です。</br>-PASSPORT-Microsoft が提供する一元化された認証サービスで、メンバーサイトにシングルログオンを提供します。|

## <a name="BKMK_examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブから資格情報を削除します。
```
C:\>bitsadmin /RemoveCredentials myDownloadJob SERVER BASIC
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)