---
title: 'ksetup: addkpasswd'
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 72c27cb6b068dc46cd58e753b4b08d68b39bfb20
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375192"
---
# <a name="ksetupaddkpasswd"></a>ksetup: addkpasswd



領域の Kerberos パスワード (Kpasswd) サーバーアドレスを追加します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。

## <a name="syntax"></a>構文

```
ksetup /addkpasswd <RealmName> [<KpasswdName>]
```

### <a name="parameters"></a>パラメーター

ワークステーションで認証される kerberos 領域が Kerberos 変更パスワードプロトコルをサポートしている場合は、Windows オペレーティングシステムを実行しているクライアントコンピューターで Kerberos パスワードサーバーを使用するように構成できます。 この設定は、領域側で構成されます。

|パラメーター|説明|
|---------|-----------|
|\<RealmName >|領域名は、CORP などの大文字の DNS 名で表されます。CONTOSO.COM は、 **ksetup**の実行時に既定の領域または領域 = として表示されます。|
|\<KpasswdName >|Kerberos パスワードサーバーとして使用される KDC 名は、大文字と小文字を区別しない完全修飾ドメイン名 (mitkdc.microsoft.com など) として記述されます。 KDC 名を省略した場合、DNS を使用して Kdc を見つけることができます。|

## <a name="remarks"></a>コメント

ワークステーションで認証される kerberos 領域が Kerberos 変更パスワードプロトコルをサポートしている場合は、Windows オペレーティングシステムを実行しているクライアントコンピューターで Kerberos パスワードサーバーを使用するように構成できます。

コマンド**ksetup**を実行して、KDC 名を確認します。 **Kpasswd =** が出力に表示されない場合、マッピングは構成されていません。

KDC 名は、一度に1つずつ追加できます。

## <a name="BKMK_Examples"></a>例

「CORP」という領域を構成します。CONTOSO.COM は、Windows 以外の KDC サーバー mitkdc.contoso.com をパスワードサーバーとして使用するようにします。
```
ksetup /addkpasswd CORP.CONTOSO.COM mitkdc.contoso.com
```
これにより、Windows 以外の Kerberos パスワードサーバーは、このサーバーと領域の間の認証用のすべてのパスワードを制御します。

#### <a name="additional-references"></a>その他の参照情報

-   [Ksetup](ksetup.md)
-   [Ksetup:delkpasswd](ksetup-delkpasswd.md)
-   [コマンド ライン構文の記号](command-line-syntax-key.md)