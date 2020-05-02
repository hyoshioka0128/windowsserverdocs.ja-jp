---
title: 'ksetup: addkpasswd'
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d3196995-1b38-48ff-ba08-911cfab77317
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c260c711ae87f88be8b9466e73afaf3fe1c83a1e
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724735"
---
# <a name="ksetupaddkpasswd"></a>ksetup: addkpasswd



領域の Kerberos パスワード (Kpasswd) サーバーアドレスを追加します。

## <a name="syntax"></a>構文

```
ksetup /addkpasswd <RealmName> [<KpasswdName>]
```

#### <a name="parameters"></a>パラメーター

ワークステーションで認証される kerberos 領域が Kerberos 変更パスワードプロトコルをサポートしている場合は、Windows オペレーティングシステムを実行しているクライアントコンピューターで Kerberos パスワードサーバーを使用するように構成できます。 この設定は、領域側で構成されます。

|パラメーター|[説明]|
|---------|-----------|
|\<RealmName>|領域名は、CORP などの大文字の DNS 名で表されます。CONTOSO.COM は、 **ksetup**の実行時に既定の領域または領域 = として表示されます。|
|\<KpasswdName>|Kerberos パスワードサーバーとして使用される KDC 名は、大文字と小文字を区別しない完全修飾ドメイン名 (mitkdc.microsoft.com など) として記述されます。 KDC 名を省略した場合、DNS を使用して Kdc を見つけることができます。|

## <a name="remarks"></a>Remarks

ワークステーションで認証される kerberos 領域が Kerberos 変更パスワードプロトコルをサポートしている場合は、Windows オペレーティングシステムを実行しているクライアントコンピューターで Kerberos パスワードサーバーを使用するように構成できます。

コマンド**ksetup**を実行して、KDC 名を確認します。 **Kpasswd =** が出力に表示されない場合、マッピングは構成されていません。

KDC 名は、一度に1つずつ追加できます。

## <a name="examples"></a>例

「CORP」という領域を構成します。CONTOSO.COM は、Windows 以外の KDC サーバー mitkdc.contoso.com をパスワードサーバーとして使用するようにします。
```
ksetup /addkpasswd CORP.CONTOSO.COM mitkdc.contoso.com
```
これにより、Windows 以外の Kerberos パスワードサーバーは、このサーバーと領域の間の認証用のすべてのパスワードを制御します。

## <a name="additional-references"></a>その他のリファレンス

-   [Ksetup](ksetup.md)
-   [Ksetup:delkpasswd](ksetup-delkpasswd.md)
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)