---
title: ksetup delkpasswd
description: Ksetup delkpasswd コマンドの参照記事。これにより、領域の Kerberos パスワードサーバー (kpasswd) が削除されます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2db0bfcd-bc08-48e3-9f30-65b6411839c6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 05002c860575bce84748adc2fc353f0994d559ab
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926138"
---
# <a name="ksetup-delkpasswd"></a>ksetup delkpasswd

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

領域の Kerberos パスワードサーバー (kpasswd) を削除します。

## <a name="syntax"></a>構文

```
ksetup /delkpasswd <realmname> <kpasswdname>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<realmname>` |  CORP など、大文字の DNS 名を指定します。CONTOSO.COM は、 **ksetup**の実行時に既定の領域または**領域 =** として表示されます。 |
| `<kpasswdname>` | Kerberos パスワードサーバーを指定します。 大文字と小文字を区別しない、完全修飾ドメイン名 (mitkdc.contoso.com など) として記述されています。 KDC 名を省略した場合、DNS を使用して Kdc を見つけることができます。 |

### <a name="examples"></a>例

領域 CORP を確保します。CONTOSO.COM は、Windows 以外の KDC サーバー mitkdc.contoso.com をパスワードサーバーとして使用し、次のように入力します。

```
ksetup /delkpasswd CORP.CONTOSO.COM mitkdc.contoso.com
```

領域 CORP を確保します。CONTOSO.COM が Kerberos パスワードサーバー (KDC 名) にマップされていない場合は、 `ksetup` Windows コンピューターにと入力し、出力を表示します。

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [ksetup コマンド](ksetup.md)

- [ksetup delkpasswd コマンド](ksetup-delkpasswd.md)
