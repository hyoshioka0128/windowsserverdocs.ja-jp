---
title: bitsadmin setcredentials
description: Bitsadmin setcredentials に関する Windows コマンドのトピック。資格情報をジョブに追加します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3cd099a4-9e85-46d8-8527-edb6dfab7f97
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 918bda93407e029cedaaf5eab937d1bb23dc3c4c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849645"
---
# <a name="bitsadmin-setcredentials"></a>bitsadmin setcredentials

ジョブに資格情報を追加します。

**BITS 1.2 以前**: サポートされていません。

## <a name="syntax"></a>構文

```
bitsadmin /SetCredentials <Job> <Target> <Scheme> <Username> <Password>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|Target|サーバーまたはプロキシ|
|体系|次のいずれかです。</br>-BASIC: ユーザー名とパスワードがクリアテキストでサーバーまたはプロキシに送信される認証方式。</br>-DIGEST —チャレンジ応答認証方式。サーバーが指定したデータ文字列をチャレンジに使用します。</br>-NTLM-Windows ネットワーク環境での認証にユーザーの資格情報を使用するチャレンジ応答認証方式。</br>-NEGOTIATE — Simple and Protected negotiate protocol (Snego) は、認証に使用するスキームを決定するために、サーバーまたはプロキシとネゴシエートするチャレンジ/レスポンス認証方式です。 たとえば、Kerberos プロトコルや NTLM です。</br>-PASSPORT-Microsoft が提供する一元化された認証サービスで、メンバーサイトにシングルログオンを提供します。|
|Username|指定された資格情報の名前|
|Password|指定された*ユーザー名*に関連付けられているパスワード|

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、 *Mydownloadjob*という名前のジョブに資格情報を追加します。
```
C:\>bitsadmin /RemoveCredentials myDownloadJob SERVER BASIC Edward Password20
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)