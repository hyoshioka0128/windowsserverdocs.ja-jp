---
title: nslookup
description: Nslookup コマンドの参照記事。ドメインネームシステム (DNS) インフラストラクチャの診断に使用できる情報が表示されます。
ms.topic: article
ms.assetid: 41516932-7833-434a-aa92-b4cf0f9a7ef7
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7d01f167a198803db269e97e806a6d2867074d60
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87885321"
---
# <a name="nslookup"></a>nslookup

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ドメインネームシステム (DNS) インフラストラクチャの診断に使用できる情報を表示します。 このツールを使用する前に、DNS のしくみについて理解しておく必要があります。 Nslookup コマンドラインツールは、TCP/IP プロトコルがインストールされている場合にのみ使用できます。

Nslookup コマンドラインツールには、対話型と非対話の2つのモードがあります。

データを1つだけ検索する必要がある場合は、非対話モードを使用することをお勧めします。 最初のパラメーターとして、検索するコンピューターの名前または IP アドレスを入力します。 2番目のパラメーターには、DNS ネームサーバーの名前または IP アドレスを入力します。 2番目の引数を省略した場合、 **nslookup**では既定の DNS ネームサーバーが使用されます。

複数のデータを検索する必要がある場合は、対話モードを使用できます。 最初のパラメーターとしてハイフン (-) を入力し、2番目のパラメーターに DNS ネームサーバーの名前または IP アドレスを入力します。 両方のパラメーターを省略した場合、このツールは既定の DNS ネームサーバーを使用します。 対話モードの使用時には、次の操作を実行できます。

- CTRL キーを押しながら B キーを押すと、対話型のコマンドをいつでも中断できます。

- **Exit を入力し**て終了します。

- 組み込みコマンドをコンピューター名として扱います。その際、その前にエスケープ文字 ( \) . 認識されないコマンドは、コンピューター名として解釈されます。

## <a name="syntax"></a>構文

```
nslookup [exit | finger | help | ls | lserver | root | server | set | view] [options]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| [nslookup 終了](nslookup-exit-command.md) | Nslookup コマンドラインツールを終了します。 |
| [nslookup 指](nslookup-finger-command.md) | 現在のコンピューター上の finger サーバーに接続します。 |
| [nslookup help](nslookup-help.md) | サブコマンドの簡単な概要を表示します。 |
| [nslookup ls](nslookup-ls.md) | DNS ドメインの情報を一覧表示します。 |
| [nslookup lserver](nslookup-lserver.md) | 指定された DNS ドメインに既定のサーバーを変更します。 |
| [nslookup root](nslookup-root.md) | DNS ドメイン名空間のルートに対して、既定のサーバーをサーバーに変更します。 |
| [nslookup server](nslookup-server.md) | 指定された DNS ドメインに既定のサーバーを変更します。 |
| [nslookup set](nslookup-set.md) | 参照の機能に影響する構成設定を変更します。 |
| [nslookup set all](nslookup-set-all.md) | 構成設定の現在の値を出力します。 |
| [nslookup set class](nslookup-set-class.md) | クエリクラスを変更します。 クラスは、情報のプロトコルグループを指定します。 |
| [nslookup set d2](nslookup-set-d2.md) | 完全デバッグモードをオンまたはオフにします。 すべてのパケットのすべてのフィールドが出力されます。 |
| [nslookup set debug](nslookup-set-debug.md) | デバッグモードをオンまたはオフにします。 |
| [nslookup set domain](nslookup-set-domain.md) | 既定の DNS ドメイン名を、指定された名前に変更します。 |
| [nslookup set port](nslookup-set-port.md) | 既定の TCP/UDP DNS ネームサーバーポートを、指定された値に変更します。 |
| [nslookup set querytype](nslookup-set-querytype.md) | クエリのリソースレコードの種類を変更します。 |
| [nslookup set recurse](nslookup-set-recurse.md) | DNS ネームサーバーに情報がない場合に他のサーバーを照会するように指示します。 |
| [nslookup set retry](nslookup-set-retry.md) | 再試行回数を設定します。 |
| [nslookup set root](nslookup-set-root.md) | クエリに使用するルートサーバーの名前を変更します。 |
| [nslookup set search](nslookup-set-search.md) | 応答が受信されるまで、DNS ドメインの検索リスト内の DNS ドメイン名を要求に追加します。 これは、セットと参照要求に少なくとも1つのピリオドが含まれている場合に適用されますが、末尾にピリオドは付きません。 |
| [nslookup set srchlist](nslookup-set-srchlist.md) | 既定の DNS ドメイン名と検索一覧を変更します。 |
| [nslookup set timeout](nslookup-set-timeout.md) | 要求への応答を待機する秒数の初期値を変更します。 |
| [nslookup set type](nslookup-set-type.md) | クエリのリソースレコードの種類を変更します。 |
| [nslookup set vc](nslookup-set-vc.md) | サーバーに要求を送信するときに、仮想回線を使用するかどうかを指定します。 |
| [nslookup view](nslookup-view.md) | 前の**ls**サブコマンドの出力を並べ替えて一覧表示します。 |

### <a name="remarks"></a>Remarks

- *ComputerTofind*が IP アドレスであり、クエリが**A**または**PTR**リソースレコードの種類の場合は、コンピューターの名前が返されます。

- *ComputerTofind*が名前で、末尾のピリオドがない場合は、既定の DNS ドメイン名が名前に追加されます。 この動作は、 **set**サブコマンド ( **domain**、 **srchlist**、 **defname**、および**search**) の状態によって異なります。

- *ComputerTofind*の代わりにハイフン (-) を入力すると、コマンドプロンプトが**nslookup**対話モードに変更されます。

- 参照要求が失敗した場合、コマンドラインツールには次のようなエラーメッセージが表示されます。

  | エラー メッセージ | 説明 |
  | ------------- | ----------- |
  | タイムアウトしました |サーバーは、一定の時間が経過してから特定の回数の再試行を行った後に、要求に応答しませんでした。 [Nslookup set timeout](nslookup-set-timeout.md)コマンドを使用して、タイムアウト期間を設定できます。 [Nslookup set retry](nslookup-set-retry.md)コマンドを使用して、再試行回数を設定できます。 |
  | サーバーからの応答がありません | サーバーコンピューターで DNS ネームサーバーが実行されていません。 |
  | レコードがありません | DNS ネームサーバーは、コンピューター名が有効であっても、現在のクエリの種類のリソースレコードを持っていません。 クエリの種類は、 [nslookup set querytype](nslookup-set-querytype.md)コマンドを使用して指定します。 |
  | 存在しないドメイン | コンピューター名または DNS ドメイン名が存在しません。 |
  | 接続が拒否されたか、ネットワークに到達できません | DNS ネームサーバーまたはフィンガーサーバーへの接続を確立できませんでした。 このエラーは、通常、 **ls**および**finger**要求で発生します。 |
  | サーバーエラー | DNS ネームサーバーがデータベース内で内部の不整合を検出したため、有効な回答を返すことができませんでした。 |
  | 拒絶 | DNS ネームサーバーが要求の処理を拒否しました。 |
  | 形式エラー | DNS ネームサーバーで、要求パケットの形式が正しくないことが検出されました。 **Nslookup**でエラーが発生している可能性があります。 |

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
