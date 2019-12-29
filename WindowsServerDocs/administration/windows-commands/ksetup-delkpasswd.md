---
title: 'ksetup: delkpasswd'
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2db0bfcd-bc08-48e3-9f30-65b6411839c6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dce7d9666040ff0c234139932ea60e3589dfecb2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375134"
---
# <a name="ksetupdelkpasswd"></a>ksetup: delkpasswd

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

領域の Kerberos パスワードサーバー (Kpasswd) を削除します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。
## <a name="syntax"></a>構文
```
ksetup /delkpasswd <RealmName> <KpasswdName>
```
### <a name="parameters"></a>パラメーター

|   パラメーター   |                                                                                                   説明                                                                                                   |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  <RealmName>  |                                領域名は、CORP などの大文字の DNS 名で表されます。CONTOSO.COM は、 **ksetup**の実行時に既定の領域または領域 = として表示されます。                                |
| <KpasswdName> | Kerberos パスワードサーバーとして使用される KDC 名は、大文字と小文字を区別しない完全修飾ドメイン名 (mitkdc.contoso.com など) として記述されます。 KDC 名を省略した場合、DNS を使用して Kdc を見つけることができます。 |

## <a name="remarks"></a>コメント
コマンド**ksetup**を実行して、KDC 名を確認します。 **Kpasswd =** が出力に表示されない場合、マッピングは構成されていません。 複数のマッピングが表示されます (設定されている場合)。
## <a name="BKMK_Examples"></a>例
領域 CORP を確認します。CONTOSO.COM は、Windows 以外の KDC サーバー mitkdc.contoso.com をパスワードサーバーとして使用します。
```
ksetup /delkpasswd CORP.CONTOSO.COM mitkdc.contoso.com
```
コマンドが意図したとおりに動作したことを確認するには、Windows コンピューターで**ksetup**を実行して、realm CORP を確認します。CONTOSO.COM が Kerberos パスワードサーバー (KDC 名) にマップされていません。
## <a name="additional-references"></a>その他の参照情報
-   [ksetup](ksetup.md)
-   [ksetup: delkpasswd](ksetup-delkpasswd.md)
-   [コマンド ライン構文の記号](command-line-syntax-key.md)
