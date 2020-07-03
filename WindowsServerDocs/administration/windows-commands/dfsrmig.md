---
title: dfsrmig
description: Dfsrmig コマンドの参照記事。 FRS から DFS レプリケーションに SYSvol レプリケーションを移行し、移行の進行状況に関する情報を提供し、移行をサポートする AD DS オブジェクトを変更します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e1b6a464-6a93-4e66-9969-04f175226d8d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 87882ebe0beb687f704c5573091f56c067c278ee
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85928642"
---
# <a name="dfsrmig"></a>dfsrmig

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

DFS レプリケーションサービスの移行ツールである dfsrmig.exe は、DFS レプリケーションサービスと共にインストールされます。 このツールでは、ファイルレプリケーションサービス (FRS) から分散ファイルシステム (DFS) レプリケーションに SYSvol レプリケーションを移行します。 また、移行の進行状況に関する情報を提供し、移行をサポートするために Active Directory Domain Services (AD DS) オブジェクトを変更します。

## <a name="syntax"></a>構文

```
dfsrmig [/setglobalstate <state> | /getglobalstate | /getmigrationstate | /createglobalobjects |
/deleterontfrsmember [<read_only_domain_controller_name>] | /deleterodfsrmember [<read_only_domain_controller_name>] | /?]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `/setglobalstate <state>` | ドメインのグローバル移行状態を、 *state*によって指定された値に対応する1つに設定します。 グローバル移行状態は、安定した状態にのみ設定できます。 *状態*の値は次のとおりです。<ul><li>**0** -開始状態</li><li>**1** -準備された状態</li><li>**2** -リダイレクトされた状態</li><li>**3** -状態を消去しました</li></ul> |
| /getglobalstate | PDC エミュレーターで実行されるときに、AD DS データベースのローカルコピーからドメインの現在のグローバル移行状態を取得します。 このオプションを使用して、正しいグローバル移行状態が設定されていることを確認します。<p>**重要:** PDC エミュレーターでのみ、このコマンドを実行する必要があります。 |
| /getmigrationstate | ドメイン内のすべてのドメインコントローラーの現在のローカル移行状態を取得し、それらのローカルの状態が現在のグローバル移行状態と一致するかどうかを判断します。 このオプションを使用して、すべてのドメインコントローラがグローバル移行状態に達したかどうかを確認します。 |
| /createglobalobjects | DFS レプリケーションが使用する AD DS のグローバルオブジェクトと設定を作成します。 このオプションを使用してオブジェクトと設定を手動で作成する必要があるのは、次の場合だけです。<ul><li>**移行中に、新しい読み取り専用ドメインコントローラーが昇格され**ます。 **準備**され**た状態に**移行した後、新しい読み取り専用ドメインコントローラーがドメイン内で昇格された場合は、新しいドメインコントローラーに対応するオブジェクトが作成されず、レプリケーションが失敗し、移行が失敗します。</li><li>**DFS レプリケーションサービスのグローバル設定がないか、削除されました**。 これらの設定がドメインコントローラーにない場合、**開始**状態から**準備**済み状態への移行は、移行の**準備中**の状態で停止します。 **注:** 読み取り専用ドメインコントローラーの DFS レプリケーションサービスのグローバル AD DS 設定は PDC エミュレーター上で作成されるため、読み取り専用ドメインコントローラーの DFS レプリケーションサービスがこれらの設定を使用できるようにするには、これらの設定を PDC エミュレーターから読み取り専用ドメインコントローラーにレプリケートする必要があります。 レプリケーションの待ち時間が Active Directory ため、このレプリケーションの実行には時間がかかることがあります。 |
| `/deleterontfrsmember [<read_only_domain_controller_name>]` | 指定した読み取り専用ドメインコントローラーに対応する FRS レプリケーションのグローバル AD DS 設定を削除するか、に値が指定されていない場合は、すべての読み取り専用ドメインコントローラーの FRS レプリケーションのグローバル AD DS 設定を削除し `<read_only_domain_controller_name>` ます。<p>通常の移行プロセスでは、このオプションを使用する必要はありません。これは、**リダイレクト**された状態から**削除**された状態への移行中に、DFS レプリケーションサービスによってこれらの AD DS 設定が自動的に削除されるためです。 読み取り専用ドメインコントローラーで自動削除が失敗した場合にのみ、このオプションを使用して AD DS 設定を手動で削除します。また、**リダイレクト**された状態から**削除**済み状態への移行中に長い ime の読み取り専用ドメインコントローラーを停止します。 |
| `/deleterodfsrmember [<read_only_domain_controller_name>]` | 指定した読み取り専用ドメインコントローラーに対応する DFS レプリケーションのグローバル AD DS 設定を削除するか、に値が指定されていない場合は、すべての読み取り専用ドメインコントローラーのグローバル AD DS DFS レプリケーション設定を削除し `<read_only_domain_controller_name>` ます。<p>このオプションを使用すると、読み取り専用ドメインコントローラーで自動削除が失敗し、準備状態から開始状態に移行をロールバックするときに、読み取り専用ドメインコントローラーが長時間停止した場合にのみ、手動で AD DS 設定を削除できます。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

#### <a name="remarks"></a>注釈

- コマンドを使用して、 `/setglobalstate <state>` PDC エミュレーター上の AD DS のグローバル移行状態を設定し、移行プロセスを開始および制御します。 PDC エミュレーターが使用できない場合、このコマンドは失敗します。

- **削除**された状態への移行は元に戻すことができないため、ロールバックは不可能です。そのため、SYSvol レプリケーションに DFS レプリケーションを使用するために完全にコミットされている場合にのみ、*状態*に**3**を使用します。

- グローバル移行の状態は、安定した移行状態である必要があります。

- レプリケーションでは、グローバル状態がドメイン内の他のドメインコントローラーにレプリケートされますが、レプリケーションの待機時間が原因で、 `dfsrmig /getglobalstate` PDC エミュレーター以外のドメインコントローラーでを実行すると、不整合が発生する可能性があります。 Active Directory

- の出力は、 `dsfrmig /getmigrationstate` 現在のグローバル状態への移行が完了しているかどうかを示し、現在のグローバル移行状態にまだ到達していないドメインコントローラーのローカル移行状態を一覧表示します。 ドメインコントローラーのローカル移行の状態には、現在のグローバル移行状態に達していないドメインコントローラーの移行状態を含めることもできます。

- 読み取り専用ドメインコントローラーは、AD DS から設定を削除することはできません。 PDC エミュレーターはこの操作を実行します。変更は、active directory レプリケーションで適用される待機時間の後に、最終的に読み取り専用ドメインコントローラーにレプリケートされます。

- **Dfsrmig**コマンドは、Windows Server ドメインの機能レベルで実行されているドメインコントローラーでのみサポートされています。これは、FRS から DFS レプリケーションへの SYSvol 移行は、そのレベルで動作するドメインコントローラーでのみ可能であるためです。

- **Dfsrmig**コマンドは任意のドメインコントローラーで実行できますが、AD DS オブジェクトを作成または操作する操作は、読み取り/書き込み可能なドメインコントローラー (読み取り専用ドメインコントローラーではない) でのみ許可されます。

## <a name="examples"></a>例

グローバル移行状態を準備済み (**1**) に設定し、移行を開始したり、準備された状態からロールバックしたりするには、次のように入力します。

```
dfsrmig /setglobalstate 1
```

グローバル移行状態を開始 (**0**) に設定し、開始状態へのロールバックを開始するには、次のように入力します。

```
dfsrmig /setglobalstate 0
```

グローバル移行の状態を表示するには、次のように入力します。

```
dfsrmig /getglobalstate
```

コマンドからの出力 `dfsrmig /getglobalstate` :

```
Current DFSR global state: Prepared
Succeeded.
```

すべてのドメインコントローラー上のローカルの移行状態がグローバル移行状態と一致するかどうか、およびローカルの状態がグローバル状態と一致しないローカルの移行状態があるかどうかに関する情報を表示するには、次のように入力します。

```
dfsrmig /GetMigrationState
```

`dfsrmig /getmigrationstate`すべてのドメインコントローラー上のローカル移行状態がグローバル移行状態と一致したときのコマンドからの出力:

```
All Domain Controllers have migrated successfully to Global state (Prepared).
Migration has reached a consistent state on all Domain Controllers.
Succeeded.
```

`dfsrmig /getmigrationstate`一部のドメインコントローラーでローカルの移行状態がグローバル移行状態と一致しない場合のコマンドからの出力。

```
The following Domain Controllers are not in sync with Global state (Prepared):
Domain Controller (Local Migration State) DC type
=========
CONTOSO-DC2 (start) ReadOnly DC
CONTOSO-DC3 (Preparing) Writable DC
Migration has not yet reached a consistent state on all domain controllers
State information might be stale due to AD latency.
```

移行中に自動的に作成されなかった、または設定がないドメインコントローラーで、AD DS で DFS レプリケーション使用するグローバルオブジェクトと設定を作成するには、次のように入力します。

```
dfsrmig /createglobalobjects
```

Contoso-dc2 という名前の読み取り専用ドメインコントローラーの FRS レプリケーションのグローバル AD DS 設定を削除するには、移行プロセスによってこれらの設定が自動的に削除されなかった場合は、次のように入力します。

```
dfsrmig /deleterontfrsmember contoso-dc2
```

すべての読み取り専用ドメインコントローラーの FRS レプリケーションのグローバル AD DS 設定を削除するには、次のように入力します。

```
dfsrmig /deleterontfrsmember
```

Contoso-dc2 という名前の読み取り専用ドメインコントローラーのグローバル AD DS DFS レプリケーション設定を削除するには、移行プロセスによってこれらの設定が自動的に削除されていない場合は、次のように入力します。

```
dfsrmig /deleterodfsrmember contoso-dc2
```

すべての読み取り専用ドメインコントローラーのグローバル AD DS DFS レプリケーション設定を削除するには、それらの設定が移行プロセスによって自動的に削除されなかった場合は、次のように入力します。

```
dfsrmig /deleterodfsrmember
```

ヘルプを表示するには、コマンドプロンプトで次のように入力します。

```
dfsrmig
```

```
dfsrmig /?
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](https://go.microsoft.com/fwlink/?LinkId=122056)

- [SYSvol 移行シリーズ: パート 2 dfsrmig.exe: SYSvol 移行ツール](https://techcommunity.microsoft.com/t5/storage-at-microsoft/sysvol-migration-series-part-2-8211-dfsrmig-exe-the-sysvol/ba-p/423470)

- [Active Directory Domain Services](../../identity/ad-ds/get-started/virtual-dc/active-directory-domain-services-overview.md)
