---
title: bitsadmin setsecurityflags
description: Bitsadmin setsecurityflags の Windows コマンドに関するトピックでは、BITS で証明書失効リストをチェックするかどうかを決定し、特定の証明書エラーを無視し、サーバーが HTTP 要求をリダイレクトするときに使用するポリシーを定義する、HTTP のフラグを設定します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 0da5cbf5-5f7f-4833-bbbe-c4e8379a78ab
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8a7b857bb398e3061a3435a730bf9a751ee2c5e3
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80849145"
---
# <a name="bitsadmin-setsecurityflags"></a>bitsadmin setsecurityflags

BITS が証明書失効リストを確認し、特定の証明書エラーを無視して、サーバーが HTTP 要求をリダイレクトするときに使用するポリシーを定義するかどうかを決定する HTTP のフラグを設定します。 値は符号なし整数です。

## <a name="syntax"></a>構文

```
bitsadmin /SetSecurityFlags <Job> <Value>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|Job|ジョブの表示名または GUID|
|値|「解説」を参照|

## <a name="remarks"></a>コメント

**Value**パラメーターには、次の通知フラグを1つ以上含めることができます。

|操作|バイナリ表現|
|------|---------------------|
|CRL チェックを有効にする|最下位ビットを設定する|
|サーバー証明書の無効な共通名を無視する|右側から2番目のビットを設定します。|
|サーバー証明書の無効な日付を無視する|右から3番目のビットを設定します。|
|サーバー証明書の無効な証明機関を無視する|右側の4番目のビットを設定します。|
|証明書の無効な使用を無視する|右から5番目のビットを設定します。|
|リダイレクトポリシー|右側から11番目から11番目のビットによって制御されます。</br>0、0、0のリダイレクトは、自動的に許可されます。</br>0、0、1-リダイレクトが発生した場合、IBackgroundCopyFile インターフェイスのリモート名が更新されます。</br>0, 1, 0 ビットは、リダイレクトが発生した場合にジョブを失敗させます。|
|HTTPS から HTTP へのリダイレクトを許可する|右から12番目のビットを設定します。|

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例では、セキュリティフラグを設定して、 *myjob*という名前のジョブの CRL チェックを有効にします。
```
C:\>bitsadmin /SetSecurityFlags myJob 0x0001
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)