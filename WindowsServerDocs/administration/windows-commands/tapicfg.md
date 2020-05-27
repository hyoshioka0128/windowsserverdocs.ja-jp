---
title: tapicfg
description: TAPI アプリケーションディレクトリパーティションを管理する方法について説明します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c0e642ce-5d98-4edb-9a65-1dff09aef4e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: c9b73a7b5d3a24e4fda34b772239fb987b671d06
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2020
ms.locfileid: "83821312"
---
# <a name="tapicfg"></a>tapicfg

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

作成、削除、または TAPI アプリケーション ディレクトリ パーティションを表示または既定の TAPI アプリケーション ディレクトリ パーティションを設定します。 TAPI 3.1 クライアントは、このアプリケーションディレクトリパーティションの情報をディレクトリサービスロケーターサービスと共に使用して、TAPI ディレクトリを検索し、通信することができます。また、 **tapicfg**を使用してサービス接続ポイントを作成または削除することもできます。これにより、tapi クライアントがドメイン内の tapi アプリケーションディレクトリパーティションを効率的に検索できるようになります。 詳細については、「解説」を参照してください。 コマンドの構文を表示するには、コマンドをクリックします。
-   [tapicfg インストール](#BKMK_install)
-   [tapicfg の削除](#BKMK_remove)
-   [tapicfg publishscp](#BKMK_publishscp)
-   [tapicfg removescp](#BKMK_removescp)
-   [tapicfg ショー](#BKMK_show)
-   [tapicfg makedefault](#BKMK_makedefault)

## <a name="tapicfg-install"></a><a name="BKMK_install"></a>tapicfg インストール
TAPI アプリケーション ディレクトリ パーティションを作成します。

### <a name="syntax"></a>構文
```
tapicfg install /directory:<PartitionName> [/server:<DCName>] [/forcedefault]
```
#### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|install/directory: \< PartitionName>|必須。 作成するには、TAPI アプリケーション ディレクトリ パーティションの DNS 名を指定します。 この名前は、完全修飾ドメイン名である必要があります。|
|/server: \< DCName>|TAPI アプリケーション ディレクトリ パーティションを作成するドメイン コント ローラーの DNS 名を指定します。 ドメイン コント ローラー名が指定されていないローカル コンピューターの名前が使用されます。|
|/forcedefault|このディレクトリが既定の TAPI アプリケーション ディレクトリ パーティションがドメインであることを指定します。 ドメインに複数の TAPI アプリケーション ディレクトリ パーティションがあります。<p>このディレクトリがドメインで作成された最初の TAPI アプリケーションディレクトリパーティションの場合は、 **/forcedefault**オプションを使用するかどうかに関係なく、既定値として自動的に設定されます。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="tapicfg-remove"></a><a name="BKMK_remove"></a>tapicfg の削除
TAPI アプリケーション ディレクトリ パーティションを削除します。

### <a name="syntax"></a>構文
```
tapicfg remove /directory:<PartitionName>
```
#### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|ディレクトリの削除: \< PartitionName>|必須。 削除するには、TAPI アプリケーション ディレクトリ パーティションの DNS 名を指定します。 この名前は完全修飾ドメイン名である必要がありますに注意してください。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="tapicfg-publishscp"></a><a name="BKMK_publishscp"></a>tapicfg publishscp
TAPI アプリケーション ディレクトリ パーティションを公開するサービス接続ポイントを作成します。

### <a name="syntax"></a>構文
```
tapicfg publishscp /directory:<PartitionName> [/domain:<DomainName>] [/forcedefault]
```
#### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|publishscp/directory: \< PartitionName>|必須。 サービス接続ポイントの TAPI アプリケーション ディレクトリ パーティションの DNS 名が発行を指定します。|
|/domain: \< DomainName>|サービスの接続がポイントするドメインの DNS 名の作成を指定します。 ドメイン名が指定されていない場合は、ローカル ドメイン名が使用されます。|
|/forcedefault|このディレクトリが既定の TAPI アプリケーション ディレクトリ パーティションがドメインであることを指定します。 ドメインに複数の TAPI アプリケーション ディレクトリ パーティションがあります。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="tapicfg-removescp"></a><a name="BKMK_removescp"></a>tapicfg removescp
TAPI アプリケーション ディレクトリ パーティション用のサービス接続ポイントを削除します。

### <a name="syntax"></a>構文
```
tapicfg removescp /directory:<PartitionName> [/domain:<DomainName>]
```
#### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|removescp/ディレクトリ: \< PartitionName>|必須。 サービス接続ポイントを削除する TAPI アプリケーション ディレクトリ パーティションの DNS 名を指定します。|
|/domain: \< DomainName>|サービス接続ポイントを削除するドメインの DNS 名を指定します。 ドメイン名が指定されていない場合は、ローカル ドメイン名が使用されます。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="tapicfg-show"></a><a name="BKMK_show"></a>tapicfg ショー
ドメインの名前と TAPI アプリケーション ディレクトリ パーティションの場所が表示されます。

### <a name="syntax"></a>構文
```
tapicfg show [/defaultonly][ /domain:<DomainName>]
```
#### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/defaultonly|ドメインの名前と場所の既定 TAPI アプリケーション ディレクトリ パーティションのみが表示されます。|
|/domain: \< DomainName>|TAPI アプリケーション ディレクトリ パーティションが表示されているドメインの DNS 名を指定します。 ドメイン名が指定されていない場合は、ローカル ドメイン名が使用されます。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="tapicfg-makedefault"></a><a name="BKMK_makedefault"></a>tapicfg makedefault
ドメインの既定の TAPI アプリケーション ディレクトリ パーティションを設定します。

### <a name="syntax"></a>構文
```
tapicfg makedefault /directory:<PartitionName> [/domain:<DomainName>]
```
#### <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|makedefault/directory: \< PartitionName>|必須。 ドメインの既定のパーティションとして設定 TAPI アプリケーション ディレクトリ パーティションの DNS 名を指定します。 この名前は完全修飾ドメイン名である必要がありますに注意してください。 TAPI アプリケーション ディレクトリ パーティションが既定値として設定されているドメインの DNS 名を指定します。 ドメイン名が指定されていない場合は、ローカル ドメイン名が使用されます。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈
**Tapicfg インストール**(tapi アプリケーションディレクトリパーティションを作成) または**TAPICFG remove** (tapi アプリケーションディレクトリパーティションを削除するため) のいずれかを実行するには、Active directory の Enterprise Admins グループのメンバーである必要があります。

このコマンド ライン ツールは、ドメインのメンバーである任意のコンピューターで実行できます。

適切なフォントおよび言語のサポートがインストールされている場合、国際または Unicode 文字を含む (TAPI アプリケーション ディレクトリ パーティション、サーバー、およびドメインの名前) などのユーザー指定のテキストが正しく表示のみ。

Windows XP または Windows Server 2003 オペレーティング システムを実行している TAPI クライアントは、ILS サーバーまたは TAPI アプリケーション ディレクトリ パーティションのいずれかを照会できますので、ILS が、特定のアプリケーションをサポートするために必要な場合は、組織でインターネット ロケーター サービス (ILS) サーバーを使用することもできます。

**Tapicfg**を使用して、サービス接続ポイントを作成または削除することができます。 何らかの理由 (たとえば、格納されているドメインの名前を変更する場合)、TAPI アプリケーション ディレクトリ パーティションの名前を変更する場合は、既存のサービス接続ポイントを削除し、発行される TAPI アプリケーション ディレクトリ パーティションの新しい DNS 名を含む新しいものを作成する必要があります。 それ以外の場合、TAPI クライアントを見つけて、TAPI アプリケーション ディレクトリ パーティションにアクセスできません。 (たとえば、特定の TAPI アプリケーション ディレクトリ パーティションに TAPI データを公開するたくはない) 場合は、メンテナンスやセキュリティのためのサービス接続ポイントを削除することもできます。

## <a name="examples"></a>例
サーバー上の名前付きの tapifiction.testdom.microsoft.com testdc.testdom.microsoft.com という名前で新しいドメインの既定の TAPI アプリケーション ディレクトリ パーティションとして設定し、TAPI アプリケーション ディレクトリ パーティションを作成するには、次のように入力します。
```
tapicfg install /directory:tapifiction.testdom.microsoft.com /server:testdc.testdom.microsoft.com /forcedefault
```
新しいドメインの既定の TAPI アプリケーション ディレクトリ パーティションの名前を表示するには、次のように入力します。
```
tapicfg show /defaultonly
```
## <a name="additional-references"></a>その他のリファレンス
- [コマンド ライン構文の記号](command-line-syntax-key.md)
