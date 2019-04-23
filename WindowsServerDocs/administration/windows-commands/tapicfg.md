---
title: tapicfg
description: TAPI アプリケーション ディレクトリ パーティションを管理する方法について説明します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c0e642ce-5d98-4edb-9a65-1dff09aef4e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 6e89b1e3d7638fbcbe0140658d2d2a9af1ccd852
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886513"
---
# <a name="tapicfg"></a>tapicfg

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

作成、削除、または TAPI アプリケーション ディレクトリ パーティションを表示または既定の TAPI アプリケーション ディレクトリ パーティションを設定します。 TAPI 3.1 クライアントは、TAPI ディレクトリとの通信を検索して、ディレクトリ サービス ロケーター サービスでこのアプリケーション ディレクトリ パーティションに情報を使用できます。使用することも**tapicfg**を作成または TAPI クライアントをドメインに TAPI アプリケーション ディレクトリ パーティションを効率的に見つけるサービス接続ポイントを削除します。 詳細については、「解説」を参照してください。 コマンドの構文を表示するには、コマンドをクリックします。 
-   [tapicfg インストール](#BKMK_install)
-   [tapicfg の削除](#BKMK_remove)
-   [tapicfg publishscp 思い出して](#BKMK_publishscp)
-   [tapicfg removescp 思い出して](#BKMK_removescp)
-   [tapicfg ショー](#BKMK_show)
-   [tapicfg makedefault 思い出して](#BKMK_makedefault)

## <a name="BKMK_install"></a>tapicfg インストール
TAPI アプリケーション ディレクトリ パーティションを作成します。

### <a name="syntax"></a>構文
```
tapicfg install /directory:<PartitionName> [/server:<DCName>] [/forcedefault]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|install /directory:\<PartitionName>|必須。 作成するには、TAPI アプリケーション ディレクトリ パーティションの DNS 名を指定します。 この名前は、完全修飾ドメイン名である必要があります。|
|/server:\<DCName>|TAPI アプリケーション ディレクトリ パーティションを作成するドメイン コント ローラーの DNS 名を指定します。 ドメイン コント ローラー名が指定されていないローカル コンピューターの名前が使用されます。|
|/forcedefault|このディレクトリが既定の TAPI アプリケーション ディレクトリ パーティションがドメインであることを指定します。 ドメインに複数の TAPI アプリケーション ディレクトリ パーティションがあります。<br /><br />使用するかどうかにかかわらず、既定値として設定されて自動的にこのディレクトリが、ドメインに作成された最初の TAPI アプリケーション ディレクトリ パーティションの場合、 **/forcedefault**オプション。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="BKMK_remove"></a>tapicfg の削除
TAPI アプリケーション ディレクトリ パーティションを削除します。

### <a name="syntax"></a>構文
```
tapicfg remove /directory:<PartitionName>
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|remove /directory:\<PartitionName>|必須。 削除するには、TAPI アプリケーション ディレクトリ パーティションの DNS 名を指定します。 この名前は完全修飾ドメイン名である必要がありますに注意してください。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="BKMK_publishscp"></a>tapicfg publishscp 思い出して
TAPI アプリケーション ディレクトリ パーティションを公開するサービス接続ポイントを作成します。

### <a name="syntax"></a>構文
```
tapicfg publishscp /directory:<PartitionName> [/domain:<DomainName>] [/forcedefault]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|publishscp /directory:\<PartitionName>|必須。 サービス接続ポイントの TAPI アプリケーション ディレクトリ パーティションの DNS 名が発行を指定します。|
|/domain:\<DomainName >|サービスの接続がポイントするドメインの DNS 名の作成を指定します。 ドメイン名が指定されていない場合は、ローカル ドメイン名が使用されます。|
|/forcedefault|このディレクトリが既定の TAPI アプリケーション ディレクトリ パーティションがドメインであることを指定します。 ドメインに複数の TAPI アプリケーション ディレクトリ パーティションがあります。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="BKMK_removescp"></a>tapicfg removescp 思い出して
TAPI アプリケーション ディレクトリ パーティション用のサービス接続ポイントを削除します。

### <a name="syntax"></a>構文
```
tapicfg removescp /directory:<PartitionName> [/domain:<DomainName>]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|removescp /directory:\<PartitionName>|必須。 サービス接続ポイントを削除する TAPI アプリケーション ディレクトリ パーティションの DNS 名を指定します。|
|/domain:\<ドメイン名 >|サービス接続ポイントを削除するドメインの DNS 名を指定します。 ドメイン名が指定されていない場合は、ローカル ドメイン名が使用されます。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="BKMK_show"></a>tapicfg ショー
ドメインの名前と TAPI アプリケーション ディレクトリ パーティションの場所が表示されます。

### <a name="syntax"></a>構文
```
tapicfg show [/defaultonly][ /domain:<DomainName>]
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/defaultonly|ドメインの名前と場所の既定 TAPI アプリケーション ディレクトリ パーティションのみが表示されます。|
|/domain:\<ドメイン名 >|TAPI アプリケーション ディレクトリ パーティションが表示されているドメインの DNS 名を指定します。 ドメイン名が指定されていない場合は、ローカル ドメイン名が使用されます。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="BKMK_makedefault"></a>tapicfg makedefault 思い出して
ドメインの既定の TAPI アプリケーション ディレクトリ パーティションを設定します。

### <a name="syntax"></a>構文
```
tapicfg makedefault /directory:<PartitionName> [/domain:<DomainName>]  
```
### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|makedefault /directory:\<PartitionName>|必須。 ドメインの既定のパーティションとして設定 TAPI アプリケーション ディレクトリ パーティションの DNS 名を指定します。 この名前は完全修飾ドメイン名である必要がありますに注意してください。 TAPI アプリケーション ディレクトリ パーティションが既定値として設定されているドメインの DNS 名を指定します。 ドメイン名が指定されていない場合は、ローカル ドメイン名が使用されます。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈
Enterprise Admins グループのメンバーをいずれかを実行する active directory である必要があります**tapicfg インストール**(TAPI アプリケーション ディレクトリ パーティションを作成) するまたは**tapicfg 削除**(TAPI アプリケーションを削除するにはディレクトリ パーティションの場合)。

このコマンド ライン ツールは、ドメインのメンバーである任意のコンピューターで実行できます。

適切なフォントおよび言語のサポートがインストールされている場合、国際または Unicode 文字を含む (TAPI アプリケーション ディレクトリ パーティション、サーバー、およびドメインの名前) などのユーザー指定のテキストが正しく表示のみ。

Windows XP または Windows Server 2003 オペレーティング システムを実行している TAPI クライアントは、ILS サーバーまたは TAPI アプリケーション ディレクトリ パーティションのいずれかを照会できますので、ILS が、特定のアプリケーションをサポートするために必要な場合は、組織でインターネット ロケーター サービス (ILS) サーバーを使用することもできます。

使用することができます**tapicfg**を作成またはサービス接続ポイントを削除します。 何らかの理由 (たとえば、格納されているドメインの名前を変更する場合)、TAPI アプリケーション ディレクトリ パーティションの名前を変更する場合は、既存のサービス接続ポイントを削除し、発行される TAPI アプリケーション ディレクトリ パーティションの新しい DNS 名を含む新しいものを作成する必要があります。 それ以外の場合、TAPI クライアントを見つけて、TAPI アプリケーション ディレクトリ パーティションにアクセスできません。 (たとえば、特定の TAPI アプリケーション ディレクトリ パーティションに TAPI データを公開するたくはない) 場合は、メンテナンスやセキュリティのためのサービス接続ポイントを削除することもできます。

## <a name="examples"></a>例
サーバー上の名前付きの tapifiction.testdom.microsoft.com testdc.testdom.microsoft.com という名前で新しいドメインの既定の TAPI アプリケーション ディレクトリ パーティションとして設定し、TAPI アプリケーション ディレクトリ パーティションを作成するには、次のように入力します。
```
tapicfg install /directory:tapifiction.testdom.microsoft.com /server:testdc.testdom.microsoft.com /forcedefault
```
新しいドメインの既定の TAPI アプリケーション ディレクトリ パーティションの名前を表示するには、次のように入力します。
```
tapicfg show /defaultonly
```
## <a name="additional-references"></a>その他の参照情報
-   [コマンドライン構文キー](command-line-syntax-key.md)
