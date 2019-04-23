---
title: ksetup:addkpasswd
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d3196995-1b38-48ff-ba08-911cfab77317
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2a85eb6dfe30c33126504744a7659fe2cc573087
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856823"
---
# <a name="ksetupaddkpasswd"></a>ksetup:addkpasswd



領域の Kerberos パスワード (Kpasswd) サーバーのアドレスを追加します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /addkpasswd <RealmName> [<KpasswdName>]
```

### <a name="parameters"></a>パラメーター

Kerberos 領域をワークステーション個別に認証するサポート、Kerberos では、パスワード プロトコルを変更する場合は、Kerberos パスワード サーバーを使用する Windows オペレーティング システムを実行しているクライアント コンピューターを構成できます。 この設定は、領域の側で構成されます。

|パラメーター|説明|
|---------|-----------|
|\<RealmName>|CORP. などの大文字の DNS 名と領域名が指定されています。CONTOSO.COM では、既定値として表示領域または領域 = **ksetup**を実行します。|
|\<KpasswdName>|Kerberos パスワード サーバーとして使用するのには、KDC 名 mitkdc.microsoft.com などの大文字と小文字の完全修飾ドメイン名で表されます。 KDC 名を省略した場合、DNS は Kdc を検索するために使用可能性があります。|

## <a name="remarks"></a>注釈

Kerberos 領域をワークステーション個別に認証するサポート、Kerberos では、パスワード プロトコルを変更する場合は、Kerberos パスワード サーバーを使用する Windows オペレーティング システムを実行しているクライアント コンピューターを構成できます。

コマンドを実行**ksetup** KDC 名を確認します。 場合**kpasswd =** が表示されない出力では、マッピングが構成されていません。

一度に 1 つの他の KDC 名を追加できます。

## <a name="BKMK_Examples"></a>例

Corp.、領域を構成します。CONTOSO.COM を使用するように、Windows 以外の KDC サーバー mitkdc.contoso.com、パスワード サーバーとして:
```
ksetup /addkpasswd CORP.CONTOSO.COM mitkdc.contoso.com
```
これは、結果、非 Windows Kerberos パスワード サーバー認証領域との間のすべてのパスワードを制御します。

#### <a name="additional-references"></a>その他の参照情報

-   [Ksetup](ksetup.md)
-   [ksetup:delkpasswd](ksetup-delkpasswd.md)
-   [コマンドライン構文キー](command-line-syntax-key.md)