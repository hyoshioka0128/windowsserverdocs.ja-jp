---
title: 'secedit: 検証'
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9fb06354-f55a-4ca4-9fbc-9a872eb9b9cf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cca64f6b2904ed11f6b45e316c8e4da0093c373e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877913"
---
# <a name="seceditvalidate"></a>secedit: 検証



セキュリティ テンプレート (.inf ファイル) に格納されているセキュリティ設定を検証します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
Secedit /validate <configuration file name>  

```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|構成ファイルの名前|必須。</br>検証で適用するセキュリティ テンプレートのパスとファイル名を指定します。|

## <a name="remarks"></a>注釈

セキュリティ テンプレートを検証する場合に役立ちますが破損しているまたは不適切に設定します。

無効なセキュリティ テンプレートは適用されません。

ログ ファイルは更新されません。

Windows Server 2008 で `Secedit /refreshpolicy` に置き換えられました `gpupdate`します。 セキュリティ設定を更新する方法については、次を参照してください。 [Gpupdate](gpupdate.md)します。

## <a name="BKMK_Examples"></a>例

いることを確認するセキュリティ テンプレートに、ロールバックが実行されると、ロールバック inf ファイル、secRBKcontoso.inf は無効です。
```
Secedit /validate secRBKcontoso.inf
```

#### <a name="additional-references"></a>その他の参照情報

-   [secedit:generaterollback](secedit-generaterollback.md)
-   [Secedit](secedit.md)
-   [コマンドライン構文キー](command-line-syntax-key.md)