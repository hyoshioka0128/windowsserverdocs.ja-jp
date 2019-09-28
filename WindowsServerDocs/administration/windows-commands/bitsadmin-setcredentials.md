---
title: bitsadmin setcredentials
description: '**Bitsadmin setcredentials**の Windows コマンドに関するトピック-資格情報をジョブに追加します。'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 70ac9a01a2e713b5a2fb881f327a52552a6bbec6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380721"
---
# <a name="bitsadmin-setcredentials"></a>bitsadmin setcredentials

ジョブに資格情報を追加します。

**BITS 1.2 以前**: サポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /SetCredentials <Job> <Target> <Scheme> <Username> <Password>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|移行先|サーバーまたはプロキシ|
|体系|次のいずれかです。</br>-BASIC: ユーザー名とパスワードがクリアテキストでサーバーまたはプロキシに送信される認証方式。</br>-DIGEST —チャレンジ応答認証方式。サーバーが指定したデータ文字列をチャレンジに使用します。</br>-NTLM-Windows ネットワーク環境での認証にユーザーの資格情報を使用するチャレンジ応答認証方式。</br>-NEGOTIATE — Simple and Protected negotiate protocol (Snego) は、認証に使用するスキームを決定するために、サーバーまたはプロキシとネゴシエートするチャレンジ/レスポンス認証方式です。 たとえば、Kerberos プロトコルや NTLM です。</br>-PASSPORT-Microsoft が提供する一元化された認証サービスで、メンバーサイトにシングルログオンを提供します。|
|Username|指定された資格情報の名前|
|Password|指定された*ユーザー名*に関連付けられているパスワード|

## <a name="BKMK_examples"></a>例

次の例では、 *Mydownloadjob*という名前のジョブに資格情報を追加します。
```
C:\>bitsadmin /RemoveCredentials myDownloadJob SERVER BASIC Edward Password20
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)