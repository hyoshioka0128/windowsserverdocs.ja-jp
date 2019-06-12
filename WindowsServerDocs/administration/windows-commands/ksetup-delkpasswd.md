---
title: ksetup:delkpasswd
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: a1c701707f736fe51a1f4af70a2571e63025f281
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438040"
---
# <a name="ksetupdelkpasswd"></a>ksetup:delkpasswd

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

領域の Kerberos パスワード サーバー (Kpasswd) を削除します。 このコマンドの使用方法の例については、次を参照してください。 [例](#BKMK_Examples)します。
## <a name="syntax"></a>構文
```
ksetup /delkpasswd <RealmName> <KpasswdName>
```
### <a name="parameters"></a>パラメーター

|   パラメーター   |                                                                                                   説明                                                                                                   |
|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  <RealmName>  |                                CORP. などの大文字の DNS 名と領域名が指定されています。CONTOSO.COM では、既定値として表示領域または領域 = **ksetup**を実行します。                                |
| <KpasswdName> | Kerberos パスワード サーバーとして使用する KDC 名 mitkdc.contoso.com などの大文字、完全修飾ドメイン名で表されます。 KDC 名を省略した場合、DNS は Kdc を検索するために使用可能性があります。 |

## <a name="remarks"></a>注釈
コマンドを実行**ksetup** KDC 名を確認します。 場合**kpasswd =** マッピングが構成されていませんし、出力は表示されません。 場合、複数のマッピングを表示、設定します。
## <a name="BKMK_Examples"></a>例
CORP. の領域を確認します。CONTOSO.COM では、パスワード サーバーとして、Windows 以外の KDC サーバー mitkdc.contoso.com を使用します。
```
ksetup /delkpasswd CORP.CONTOSO.COM mitkdc.contoso.com
```
コマンドは、意図したとおりの動作を確認するには、実行**ksetup** CORP. の領域を確認するための Windows コンピューター上CONTOSO.COM は Kerberos パスワード サーバー (KDC 名) にマップされていません。
## <a name="additional-references"></a>その他の参照
-   [ksetup](ksetup.md)
-   [ksetup:delkpasswd](ksetup-delkpasswd.md)
-   [コマンド ライン構文の記号](command-line-syntax-key.md)
