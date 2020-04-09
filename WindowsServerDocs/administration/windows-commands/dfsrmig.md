---
title: dfsrmig
description: Dfsrmig の Windows コマンドに関するトピックでは、ファイルレプリケーションサービス (FRS) から分散ファイルシステム (DFS) レプリケーションに SYSvol レプリケーションを移行し、移行の進行状況に関する情報を提供して、移行をサポートするために active directory ドメインサービス (AD DS) オブジェクトを変更します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e1b6a464-6a93-4e66-9969-04f175226d8d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d688832169cf216e628fe761f85d708a78103d89
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80846165"
---
# <a name="dfsrmig"></a>dfsrmig

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

SYSvol レプリケーションをファイルレプリケーションサービス (FRS) から分散ファイルシステム (DFS) レプリケーションに移行し、移行の進行状況に関する情報を提供して、移行をサポートするように active directory ドメインサービス (AD DS) オブジェクトを変更します。

このコマンドの使用方法の例については、このドキュメントで後述する「[例](#BKMK_examples)」を参照してください。

## <a name="syntax"></a>構文

```
dfsrmig [/SetGlobalState <state> | /GetGlobalState | /GetMigrationState | /createGlobalObjects | 
/deleteRoNtfrsMember [<read_only_domain_controller_name>] | /deleteRoDfsrMember [<read_only_domain_controller_name>] | /?]
```

### <a name="parameters"></a>パラメーター

|Parameter |説明 | |-----_ |------ | |/SetGlobalState <state> |ドメインの必要なグローバル移行状態を、 *state*によって指定された値に対応する状態に設定します。<p>移行またはロールバックプロセスを続行するには、このコマンドを使用して、有効な状態を順番に切り替えます。 このオプションを使用すると、PDC エミュレーターの AD DS でグローバル移行状態を設定することによって、移行プロセスを開始および制御できます。 PDC エミュレーターが使用できない場合、このコマンドは失敗します。<p>グローバル移行状態は、安定した状態にのみ設定できます。 このため、 *state*の有効な値は start 状態の場合は**0** 、準備済み状態の場合は**1** 、リダイレクトされた状態の場合は**2** 、削除された状態の場合は**3**になります。<p>削除された状態への移行は元に戻すことができず、その状態からロールバックすることはできません。そのため、SYSvol レプリケーションに DFS レプリケーションを使用するように完全にコミットする場合にのみ、*状態*に値**3**を使用してください |。|/GetGlobalState |PDC エミュレーターで実行されるときに、AD DS データベースのローカルコピーからドメインの現在のグローバル移行状態を取得します。<p>このオプションを使用して、正しいグローバル移行状態が設定されていることを確認します。 **Dfsrmig**コマンドが **/GetGlobalState**オプションを使用して報告する結果は、グローバルな移行状態に限定されます。そのため、 **/SetGlobalState**オプションを使用して設定できる状態に対応しています。<p>PDC エミュレーターでのみ、 **/GetGlobalState**オプションを使用して**dfsrmig**コマンドを実行する必要があります。 active directory レプリケーションは、グローバル状態をドメイン内の他のドメインコントローラーにレプリケートしますが、PDC エミュレーター以外のドメインコントローラーで **/GetGlobalState**オプションを指定して**dfsrmig**コマンドを実行すると、レプリケーションの遅延によって不整合が発生する可能性があります。 PDC エミュレーター以外のドメインコントローラーのローカル移行の状態を確認するには、代わりに **/GetMigrationState**オプションを使用します。 | |/GetMigrationState |ドメイン内のすべてのドメインコントローラーについて、現在のローカルの移行状態を取得し、それらのローカルの状態が現在のグローバル移行状態と一致するかどうかを判断します。<p>このオプションを使用して、すべてのドメインコントローラがグローバル移行状態に達したかどうかを確認します。 **/GetMigrationState**オプションを使用する場合の**dsfrmig**コマンドの出力では、現在のグローバル状態への移行が完了したかどうかが示され、現在のグローバル移行状態に達していないドメインコントローラーのローカル移行状態が一覧表示されます。 ドメインコントローラーのローカル移行の状態には、現在のグローバル移行状態に達していないドメインコントローラーの移行状態を含めることができます。 | |/createGlobalObjects |DFS レプリケーションが使用する AD DS のグローバルオブジェクトと設定を作成します。<p>DFS レプリケーションサービスは、開始状態から準備済み状態への移行中にこれらの AD DS オブジェクトと設定を自動的に作成するため、通常の移行プロセスではこのオプションを使用する必要はありません。 このオプションを使用すると、次の状況でこれらのオブジェクトと設定を手動で作成できます。<p>**移行中に新しい読み取り専用ドメインコントローラーが昇格さ**-  ます。 DFS レプリケーションサービスは、開始状態から準備済み状態への移行中に DFS レプリケーションの AD DS オブジェクトと設定を自動的に作成します。 この移行の後、新しい読み取り専用ドメインコントローラーがドメイン内で昇格された場合でも、削除された状態に移行する前に、新しくアクティブ化された読み取り専用ドメインコントローラーに対応するオブジェクトが AD DS に作成されず、レプリケーションと移行が失敗します。<br />-この場合は、 **/createGlobalObjects**オプションを使用して**dfsrmig**コマンドを実行して、まだ存在しない読み取り専用ドメインコントローラー上にオブジェクトを手動で作成することができます。 このコマンドを実行しても、DFS レプリケーションサービスのオブジェクトと設定が既に存在するドメインコントローラーには影響しません。<p>**DFS レプリケーションサービスのグローバル設定がないか、削除された**- 。 特定のドメインコントローラーに対してこれらの設定がない場合、開始状態から準備済み状態への移行は、ドメインコントローラーの [移行の準備中] 状態で停止します。 この場合は、 **dfsrmig**コマンドと **/createGlobalObjects**オプションを使用して、手動で設定を作成できます。 **注:** 読み取り専用ドメインコントローラーの DFS レプリケーションサービスのグローバル AD DS 設定は PDC エミュレーター上で作成されるため、読み取り専用ドメインコントローラーの DFS レプリケーションサービスがこれらの設定を使用できるようにするには、これらの設定を PDC エミュレーターから読み取り専用ドメインコントローラーにレプリケートする必要があります。 Active ディレクトリレプリケーションの待機時間が原因で、このレプリケーションが発生するまでに時間がかかることがあります。 | |/deleteRoNtfrsMember [< read_only_domain_controller_name >] |指定した読み取り専用ドメインコントローラーに対応する FRS レプリケーションのグローバル AD DS 設定を削除するか、 *read_only_domain_controller_name*に値が指定されていない場合は、すべての読み取り専用ドメインコントローラーの frs レプリケーションのグローバル AD DS 設定を削除します。<p>通常の移行プロセスでは、このオプションを使用する必要はありません。これは、リダイレクトされた状態から削除された状態への移行中に、DFS レプリケーションサービスによってこれらの AD DS 設定が自動的に削除されるためです。 読み取り専用ドメインコントローラーは、これらの設定を AD DS から削除することはできないため、PDC エミュレーターはこの操作を実行します。この変更は、active directory レプリケーションで適用可能な待機時間が経過すると、最終的に読み取り専用ドメインコントローラーにレプリケートされます。<p>このオプションを使用して、読み取り専用ドメインコントローラーで自動削除が失敗した場合にのみ AD DS 設定を手動で削除し、リダイレクトされた状態から削除された状態への移行中に長い ime の読み取り専用ドメインコントローラーを停止する場合にのみ、このオプションを使用します。 | |/deleteRoDfsrMember [< read_only_domain_controller_name >] |指定した読み取り専用ドメインコントローラーに対応する DFS レプリケーションのグローバル AD DS 設定を削除するか、 *read_only_domain_controller_name*に値が指定されていない場合は、すべての読み取り専用ドメインコントローラーに対して DFS レプリケーションのグローバル AD DS 設定を削除します。<p>このオプションを使用すると、読み取り専用ドメインコントローラーで自動削除が失敗し、準備状態から開始状態に移行をロールバックするときに、読み取り専用ドメインコントローラーが長時間停止した場合にのみ、手動で AD DS 設定を削除できます。 | |/? |コマンドプロンプトでヘルプを表示します。 オプションを指定せずに**dfsrmig**を実行することと同じです。 |

## <a name="remarks"></a>コメント
- DFS レプリケーションサービス用の移行ツールである dfsrmig は、DFS レプリケーションサービスと共にインストールされます。
 新しい Windows Server 2008 サーバーの場合、Dcpromo.exe は、コンピューターをドメインコントローラーに昇格させるときに、DFS レプリケーションサービスをインストールして起動します。 サーバーを Windows Server 2003 から Windows Server 2008 にアップグレードすると、アップグレードプロセスによって DFS レプリケーションサービスがインストールされ、開始されます。 DFS レプリケーションサービスをインストールして開始するために、DFS レプリケーションの役割サービスをインストールする必要はありません。
- **Dfsrmig**ツールは、windows server 2008 ドメインの機能レベルで実行されているドメインコントローラーでのみサポートされています。これは、FRS から DFS レプリケーションへの SYSvol 移行は、windows server 2008 ドメインの機能レベルで動作するドメインコントローラーでのみ可能であるためです。
- **Dfsrmig**コマンドは任意のドメインコントローラーで実行できますが、AD DS オブジェクトを作成または操作する操作は、読み取り/書き込み可能なドメインコントローラー (読み取り専用ドメインコントローラーではない) でのみ許可されます。
- オプションを指定せずに**dfsrmig**を実行すると、コマンドプロンプトでヘルプが表示されます。

## <a name="examples"></a><a name=BKMK_examples></a>例
グローバル移行状態を準備済み (**1**) に設定し、準備済み状態からの移行またはロールバックを開始するには、次のように入力します。
 ```
 dfsrmig /SetGlobalState 1
 ```
 グローバル移行状態を開始 (**0**) に設定し、開始状態へのロールバックを開始するには、次のように入力します。
 ```
 dfsrmig /SetGlobalState 0
 ```
 グローバル移行の状態を表示するには、次のように入力します。
 ```
 dfsrmig /GetGlobalState
 ```
 この例は、 **dfsrmig/GetGlobalState**コマンドからの一般的な出力を示しています。
 ```
 Current DFSR global state: Prepared 
 Succeeded.
 ```
 すべてのドメインコントローラー上のローカル移行状態がグローバルの移行状態と、ローカルの状態がグローバル状態と一致しないドメインコントローラーのローカル移行状態と一致するかどうかに関する情報を表示するには、次のように入力します。
 ```
 dfsrmig /GetMigrationState
 ```
 この例では、すべてのドメインコントローラー上のローカル移行状態がグローバル移行状態と一致した場合の、 **dfsrmig/GetMigrationState**コマンドからの一般的な出力を示します。
 ```
 All Domain Controllers have migrated successfully to Global state ( Prepared ).
 Migration has reached a consistent state on all Domain Controllers.
 Succeeded.
 ```
 この例では、一部のドメインコントローラー上のローカル移行状態がグローバル移行状態と一致しない場合の、 **dfsrmig/GetMigrationState**コマンドからの一般的な出力を示します。
 ```
  The following Domain Controllers are not in sync with Global state ( Prepared ):
  Domain Controller (Local Migration State)  DC type
  =========
  CONTOSO-DC2 ( start )  ReadOnly DC
  CONTOSO-DC3 ( Preparing )  Writable DC
  Migration has not yet reached a consistent state on all domain controllers
  State information might be stale due to AD latency.
 ```
移行中に自動的に作成されなかった、または設定がないドメインコントローラーで、AD DS で DFS レプリケーション使用するグローバルオブジェクトと設定を作成するには、次のように入力します。
```
dfsrmig /createGlobalObjects
```
Contoso-dc2 という名前の読み取り専用ドメインコントローラーの FRS レプリケーションのグローバル AD DS 設定を削除するには、移行プロセスによってこれらの設定が自動的に削除されなかった場合は、次のように入力します。
```
dfsrmig /deleteRoNtfrsMember contoso-dc2
```
すべての読み取り専用ドメインコントローラーの FRS レプリケーションのグローバル AD DS 設定を削除するには、次のように入力します。
```
dfsrmig /deleteRoNtfrsMember
```
Contoso-dc2 という名前の読み取り専用ドメインコントローラーのグローバル AD DS DFS レプリケーション設定を削除するには、移行プロセスによってこれらの設定が自動的に削除されていない場合は、次のように入力します。
```
dfsrmig /deleteRoDfsrMember contoso-dc2
```
すべての読み取り専用ドメインコントローラーのグローバル AD DS DFS レプリケーション設定を削除するには、それらの設定が移行プロセスによって自動的に削除されなかった場合は、次のように入力します。
```
dfsrmig /deleteRoDfsrMember
```
## <a name="additional-references"></a>その他の参照情報
- [コマンド ライン構文の記号](https://go.microsoft.com/fwlink/?LinkId=122056)

- [SYSvol 移行シリーズ: パート 2 dfsrmig: SYSvol 移行ツール](https://go.microsoft.com/fwlink/?LinkID=121757)
