---
title: cmstp
description: 接続マネージャーサービスプロファイルをインストールまたは削除する cmstp.exe のリファレンス記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 34aad544-11c3-4e85-8bbf-5bc5a971da93
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8f7bc7bc4b90dced8074fa685ad79c65747e0ded
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85929810"
---
# <a name="cmstp"></a>cmstp

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

接続マネージャーサービスプロファイルをインストールまたは削除します。 オプションのパラメーターを指定せずに、 **cmstp.exe**では、オペレーティングシステムとユーザーのアクセス許可に適した既定の設定を使用してサービスプロファイルがインストールされます。

## <a name="syntax"></a>Syntax

構文 1-これは、カスタムインストールアプリケーションで使用される一般的な構文です。 この構文を使用するには、ファイルが格納されているディレクトリから**cmstp.exe**を実行する必要があり `<serviceprofilefilename>.exe` ます。

```
<serviceprofilefilename>.exe /q:a /c:cmstp.exe <serviceprofilefilename>.inf [/nf] [/s] [/u]
```

構文2
```
cmstp.exe [/nf] [/s] [/u] [drive:][path]serviceprofilefilename.inf
```

#### <a name="parameters"></a>パラメーター
| パラメーター | 説明 |
| --------- | ----------- |
| `<serviceprofilefilename>.exe` | インストールするプロファイルを含むインストールパッケージを名前で指定します。<p>構文1では必須ですが、構文2では無効です。 |
| /q:a | ユーザーにメッセージを表示せずにプロファイルをインストールするように指定します。 インストールが成功したことを示す確認メッセージが引き続き表示されます。<p>構文1では必須ですが、構文2では無効です。 |
| [ドライブ:]道`<serviceprofilefilename>.inf` | 必須です。 プロファイルのインストール方法を決定する構成ファイルを名前で指定します。<p>[Drive:] [path] パラメーターは、構文1では無効です。 |
| /nf | サポートファイルをインストールしないことを指定します。 |
| /s | サービスプロファイルをサイレントインストールまたはアンインストールすることを指定します (ユーザーの応答を求めたり、確認メッセージを表示したりする必要はありません)。 これは、 **/u**と組み合わせて使用できる唯一のパラメーターです。|
| /U | サービスプロファイルをアンインストールする必要があることを指定します。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

## <a name="examples"></a>例

サポートファイルを使用せずに、*架空*のサービスプロファイルをインストールするには、次のように入力します。

```
fiction.exe /c:cmstp.exe fiction.inf /nf
```

1人のユーザーの*架空*のサービスプロファイルをサイレントインストールするには、次のように入力します。

```
fiction.exe /c:cmstp.exe fiction.inf /s /su
```

*架空*のサービスプロファイルをサイレントモードでアンインストールするには、次のように入力します。

```
fiction.exe /c:cmstp.exe fiction.inf /s /u
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
