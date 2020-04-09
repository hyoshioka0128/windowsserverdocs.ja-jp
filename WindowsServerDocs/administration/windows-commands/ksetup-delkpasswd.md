---
title: 'ksetup: delkpasswd'
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2db0bfcd-bc08-48e3-9f30-65b6411839c6
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b849265e6036f338413b75fe1da2067e4cdb4cd8
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841655"
---
# <a name="ksetupdelkpasswd"></a>ksetup: delkpasswd

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

領域の Kerberos パスワードサーバー (Kpasswd) を削除します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。
## <a name="syntax"></a>構文
```
ksetup /delkpasswd <RealmName> <KpasswdName>
```
#### <a name="parameters"></a>パラメーター

|   パラメーター   |                                                                                                   説明                                                                                                   |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  <RealmName>  |                                領域名は、CORP などの大文字の DNS 名で表されます。CONTOSO.COM は、 **ksetup**の実行時に既定の領域または領域 = として表示されます。                                |
| <KpasswdName> | Kerberos パスワードサーバーとして使用される KDC 名は、大文字と小文字を区別しない完全修飾ドメイン名 (mitkdc.contoso.com など) として記述されます。 KDC 名を省略した場合、DNS を使用して Kdc を見つけることができます。 |

## <a name="remarks"></a>コメント
コマンド**ksetup**を実行して、KDC 名を確認します。 **Kpasswd =** が出力に表示されない場合、マッピングは構成されていません。 複数のマッピングが表示されます (設定されている場合)。
## <a name="examples"></a><a name=BKMK_Examples></a>例
領域 CORP を確認します。CONTOSO.COM は、Windows 以外の KDC サーバー mitkdc.contoso.com をパスワードサーバーとして使用します。
```
ksetup /delkpasswd CORP.CONTOSO.COM mitkdc.contoso.com
```
コマンドが意図したとおりに動作したことを確認するには、Windows コンピューターで**ksetup**を実行して、realm CORP を確認します。CONTOSO.COM が Kerberos パスワードサーバー (KDC 名) にマップされていません。
## <a name="additional-references"></a>その他の参照情報
-   [ksetup](ksetup.md)
-   [ksetup: delkpasswd](ksetup-delkpasswd.md)
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)
