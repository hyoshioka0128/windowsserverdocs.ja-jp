---
title: 'ksetup: delkpasswd'
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2db0bfcd-bc08-48e3-9f30-65b6411839c6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2de1546b112041f7035a711852140e9bb34babe3
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724678"
---
# <a name="ksetupdelkpasswd"></a>ksetup: delkpasswd

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

領域の Kerberos パスワードサーバー (Kpasswd) を削除します。
## <a name="syntax"></a>構文
```
ksetup /delkpasswd <RealmName> <KpasswdName>
```
#### <a name="parameters"></a>パラメーター

|   パラメーター   |                                                                                                   [説明]                                                                                                   |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  <RealmName>  |                                領域名は、CORP などの大文字の DNS 名で表されます。CONTOSO.COM は、 **ksetup**の実行時に既定の領域または領域 = として表示されます。                                |
| <KpasswdName> | Kerberos パスワードサーバーとして使用される KDC 名は、大文字と小文字を区別しない完全修飾ドメイン名 (mitkdc.contoso.com など) として記述されます。 KDC 名を省略した場合、DNS を使用して Kdc を見つけることができます。 |

## <a name="remarks"></a>Remarks
コマンド**ksetup**を実行して、KDC 名を確認します。 **Kpasswd =** が出力に表示されない場合、マッピングは構成されていません。 複数のマッピングが表示されます (設定されている場合)。
## <a name="examples"></a>例
領域 CORP を確認します。CONTOSO.COM は、Windows 以外の KDC サーバー mitkdc.contoso.com をパスワードサーバーとして使用します。
```
ksetup /delkpasswd CORP.CONTOSO.COM mitkdc.contoso.com
```
コマンドが意図したとおりに動作したことを確認するには、Windows コンピューターで**ksetup**を実行して、realm CORP を確認します。CONTOSO.COM が Kerberos パスワードサーバー (KDC 名) にマップされていません。
## <a name="additional-references"></a>その他のリファレンス
-   [ksetup](ksetup.md)
-   [ksetup: delkpasswd](ksetup-delkpasswd.md)
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)
