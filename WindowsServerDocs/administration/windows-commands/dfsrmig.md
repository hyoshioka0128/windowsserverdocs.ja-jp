---
title: dfsrmig
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e1b6a464-6a93-4e66-9969-04f175226d8d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: da05aec5ca5a5634585c5f5406181c5c90ee3a30
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856943"
---
# <a name="dfsrmig"></a>dfsrmig

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

`dfsrmig`コマンドの分散ファイル システム (DFS) レプリケーションは、SYSvol レプリケーション ファイル レプリケーション サービス (FRS) からに移行、移行の進行状況に関する情報を提供、および active directory Domain Services (AD DS) オブジェクトに変更されます移行をサポートします。
このコマンドを使用する方法の例については、次を参照してください。、[例](#BKMK_examples)このドキュメントで後述する「します。
## <a name="syntax"></a>構文
```
dfsrmig [/SetGlobalState <state> | /GetGlobalState | /GetMigrationState | /createGlobalObjects | 
/deleteRoNtfrsMember [<read_only_domain_controller_name>] | /deleteRoDfsrMember [<read_only_domain_controller_name>] | /?]
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/SetGlobalState <state>|によって指定された値に対応する状態をドメインに必要なグローバル移行状態を設定*状態*します。<br /><br />移行またはロールバック プロセスを進めてするには、有効な状態を順番にこのコマンドを使用します。 このオプションを使用すると、開始および AD DS で PDC エミュレーターのグローバルの移行の状態を設定して、移行プロセスを制御できます。 PDC エミュレーターが使用できない場合、このコマンドは失敗します。<br /><br /> グローバルの移行の状態は、安定した状態にのみ設定できます。 有効な値*状態*、したがって、 **0**開始状態の**1**の準備済みの状態を**2** 、リダイレクトされた状態のと**3**除去済み状態にします。<br /><br />値を使用して、そのため、削除状態への移行は元に戻すことは、その状態からロールバックはできません**3**の*状態*のみが完全に committd SYSvol の DFS レプリケーションを使用するにはレプリケーション。|
|/GetGlobalState|PDC エミュレーターで実行すると、AD DS データベースのローカル コピーから、ドメインの現在のグローバルの移行状態を取得します。<br /><br />このオプションを使用して、正しいグローバル移行の状態を設定することを確認します。 移行の安定した状態では、グローバル移行の状態のためにできるのみ、結果を**dfsrmig**コマンドを使用してレポートを **/GetGlobalState**オプションが、で設定できる状態に対応 **/SetGlobalState**オプション。<br /><br />実行する必要があります、 **dfsrmig**コマンドと、 **/GetGlobalState**オプションは、PDC エミュレーター。 active directory のレプリケーションは、ドメイン内の他のドメイン コント ローラーにグローバル状態をレプリケートしますが、実行する場合、レプリケーションの待機時間は損なわことができます、 **dfsrmig**コマンドと、 **/GetGlobalState** PDC エミュレーター以外のドメイン コント ローラー オプション。 PDC エミュレーター以外のドメイン コント ローラーのローカルの移行の状態を確認するには、使用、 **/GetMigrationState**オプションを使用します。|
|/GetMigrationState|ドメイン内のすべてのドメイン コント ローラーの現在のローカルの移行状態を取得し、ローカル状態が現在グローバル移行の状態と一致するかどうかを決定します。<br /><br />すべてのドメイン コント ローラーがグローバルの移行の状態に達したかどうかを判断するのにには、このオプションを使用します。 出力、 **dsfrmig**コマンドを使用すると、 **/GetMigrationState**オプションは、現在のグローバル状態への移行が完了し、いずれかのローカルの移行の状態が一覧表示されるかどうかを示します。現在のグローバルの移行の状態に達していないドメイン コント ローラー。 ドメイン コント ローラーのローカルの移行状態は、現在のグローバルの移行の状態に達していないドメイン コント ローラーの状態の遷移を含めることができます。|
|/createGlobalObjects|DFS レプリケーションを使用して AD DS では、グローバル オブジェクトと設定を作成します。<br /><br />DFS レプリケーション サービスはこれらの AD DS オブジェクトおよび設定を自動的に作成すると、start 状態から準備された状態への移行中のため、通常の移行プロセス中にこのオプションを使用する必要ありません必要があります。 次の状況で、これらのオブジェクトと設定を手動で作成するのにには、このオプションを使用します。<br /><br />-   **移行中に新しい読み取り専用ドメイン コント ローラーを昇格**します。 DFS レプリケーション サービスでは、start 状態から準備された状態への移行中に、AD DS オブジェクトおよび DFS レプリケーションの設定が自動的に作成されます。 新しい読み取り専用ドメイン コント ローラーは、移行後に、ドメインの昇格しますが、除去済みの状態に移行する前に、新しくアクティブ化された読み取り専用ドメイン コント ローラーに対応するオブジェクトは作成されません AD DS が原因でレプリケーションの場合、移行が失敗します。<br />-この場合は、実行することができます、 **dfsrmig**コマンドと、 **/createGlobalObjects**がまだないに読み取り専用ドメイン コント ローラーで、オブジェクトを手動で作成するにはオプションです。 このコマンドを実行しても、オブジェクトと DFS レプリケーション サービスの設定が既に存在するドメイン コント ローラーには影響しません。<br />-   **DFS レプリケーション サービスのグローバル設定が見つからないか、削除された**します。 これらの設定が特定のドメイン コント ローラーの不足している場合は、start 状態から準備された状態への移行がドメイン コント ローラーの準備の遷移の状態。 この場合、使用することができます、 **dfsrmig**コマンドと、 **/createGlobalObjects**オプションの設定を手動で作成します。 **注:** これらの設定で DFS レプリケーション サービスの前に、PDC エミュレーターからの読み取り専用ドメイン コント ローラーにレプリケートする必要があります、PDC エミュレーターでは、読み取り専用ドメイン コント ローラーの DFS レプリケーション サービスの AD DS のグローバル設定が作成される、ため、読み取り専用ドメイン コント ローラーには、これらの設定を使用できます。 このレプリケーションではアクティブなディレクトリ レプリケーション待機時間が、ため発生する時間がかかることができます。|
|/deleteRoNtfrsMember [<read_only_domain_controller_name>]|指定された読み取り専用ドメイン コント ローラーに対応する、FRS レプリケーション用の AD DS のグローバル設定を削除しますかの値が指定されていない場合は、FRS レプリケーションのすべての読み取り専用ドメイン コント ローラーを AD DS のグローバル設定を削除します*read_only_。domain_controller_name*します。<br /><br />DFS レプリケーション サービスは、自動的にリダイレクトされた状態から除去済み状態への移行中にこれらの AD DS 設定が削除されるため、通常の移行プロセス中にこのオプションを使用する必要ありません必要があります。 読み取り専用ドメイン コント ローラーは、AD DS からこれらの設定を削除することはできません、ため、PDC エミュレーターは、この操作を実行し、変更が最終的に active directory レプリケーションの該当する待機時間の後読み取り専用ドメイン コント ローラーにレプリケートします。<br /><br />自動削除が読み取り専用ドメイン コント ローラーに失敗し、リダイレクトされた状態から除去済み状態への移行中に長い ime に対して読み取り専用ドメイン コント ローラーを停止させる場合にのみ、AD DS の設定を手動で削除するのにには、このオプションを使用します。|
|/deleteRoDfsrMember [<read_only_domain_controller_name>]|指定された読み取り専用ドメイン コント ローラーに対応する、DFS レプリケーション用の AD DS のグローバル設定を削除しますかの値が指定されていない場合、すべての読み取り専用ドメイン コント ローラー、AD DS のグローバル設定 DFS レプリケーションを削除します*read_only_domain_controller_name*します。<br /><br />このオプションを使用して、自動削除が読み取り専用ドメイン コント ローラーに失敗し、読み取り専用ドメイン コント ローラーを長時間停止させる場合にのみ、AD DS の設定を手動で削除する時間の開始状態に、移行の準備ができた状態にロールバックするときにします。|
|/?|コマンド プロンプトにヘルプを表示します。 実行に相当**dfsrmig**オプションなし。|
## <a name="remarks"></a>注釈
-   dfsrmig.exe、DFS レプリケーション サービスの場合、移行ツールは、DFS レプリケーション サービスと共にインストールされます。
    新しい Windows Server 2008 サーバーの場合は、Dcpromo.exe は、インストールし、コンピューターのドメイン コント ローラーを昇格したときに、DFS レプリケーション サービスを開始します。 ときに、サーバーを Windows Server 2003 から Windows Server 2008、アップグレード プロセスのインストールをアップグレードし、DFS レプリケーション サービスを開始します。 DFS レプリケーション サービスをインストールして開始する、DFS レプリケーション役割サービスをインストールする必要はありません。
-   **Dfsrmig** FRS から DFS レプリケーションへの SYSvol の移行はで動作するドメイン コント ローラーに対して実行できる専用のために、ツールが Windows Server 2008 のドメイン機能レベルで実行するドメイン コント ローラーでのみサポートされて、 Windows Server 2008 ドメインの機能レベル。
-   実行することができます、 **dfsrmig**任意のドメイン コント ローラーが操作を作成または AD DS を操作するコマンド オブジェクトが (読み取り専用ドメイン コント ローラー) ではなく読み取り/書き込み可能ドメイン コント ローラーでのみ使用できます。
-   実行している**dfsrmig**オプションを指定せず、コマンド プロンプトでヘルプを表示します。
## <a name="BKMK_examples"></a>例
グローバルの移行の状態を準備済みに設定する (**1**) への移行または型の準備済みの状態からロールバックを開始します。
```
dfsrmig /SetGlobalState 1
```
開始するグローバルの移行状態を設定する (**0**) 型の開始状態にロールバックを開始します。
```
dfsrmig /SetGlobalState 0
```
グローバルの移行の状態を表示するには、次のように入力します。
```
dfsrmig /GetGlobalState
```
この例からの典型的な出力を示しています、 **dfsrmig/GetGlobalState**コマンド。
```
Current DFSR global state:  Prepared 
Succeeded.
```
すべてのドメイン コント ローラーでローカルのマイグレーションの状態がグローバルの移行の状態およびローカルの状態が、グローバル状態と一致しません、ドメイン コント ローラーのローカルの移行状態を一致するかどうかに関する情報を表示するには、次のように入力します。
```
dfsrmig /GetMigrationState
```
この例からの典型的な出力を示しています、 **dfsrmig/GetMigrationState**コマンドをすべてのドメイン コント ローラーでローカルのマイグレーションの状態がグローバルの移行の状態と一致します。
```
All Domain Controllers have migrated successfully to Global state ( Prepared ).
Migration has reached a consistent state on all Domain Controllers.
Succeeded.
```
この例からの典型的な出力を示しています、 **dfsrmig/GetMigrationState**コマンドをいくつかのドメイン コント ローラーのローカルな移行の状態ではグローバルの移行の状態が一致しません。
```
The following Domain Controllers are not in sync with Global state ( Prepared ):
Domain Controller (Local Migration State)   DC type
=========
CONTOSO-DC2 ( start )   ReadOnly DC
CONTOSO-DC3 ( Preparing )   Writable DC
Migration has not yet reached a consistent state on all domain controllers
State information might be stale due to AD latency.
```
これらの設定が自動的に作成されません移行中にドメイン コント ローラーに AD DS で DFS レプリケーションを使用して、グローバル オブジェクトと設定を作成または、これらの設定が存在しないか、入力します。
```
dfsrmig /createGlobalObjects
```
FRS レプリケーション読み取り専用ドメイン コント ローラーのこれらの設定が移行プロセスによって自動的に削除削除されなかった場合に contoso-dc2 をという名前の AD DS のグローバル設定を削除するには、次のように入力します。
```
dfsrmig /deleteRoNtfrsMember contoso-dc2
```
移行プロセスでこれらの設定が自動的に削除されない場合は、FRS レプリケーションのすべての読み取り専用ドメイン コント ローラーを AD DS のグローバル設定を削除するには、次のように入力します。
```
dfsrmig /deleteRoNtfrsMember
```
読み取り専用ドメイン コント ローラーが、移行プロセスでこれらの設定が自動的に削除されない場合に contoso-dc2 をという名前の AD DS のグローバル設定 DFS レプリケーションを削除するには、次のように入力します。
```
dfsrmig /deleteRoDfsrMember contoso-dc2
```
移行プロセスでこれらの設定が自動的に削除されない場合は、すべての読み取り専用ドメイン コント ローラー、AD DS のグローバル設定の DFS レプリケーションを削除するには、次のように入力します。
```
dfsrmig /deleteRoDfsrMember
```
## <a name="additional-references"></a>その他の参照
[コマンドライン構文キー](https://go.microsoft.com/fwlink/?LinkId=122056)

[SYSvol の移行シリーズ:第 2 部 dfsrmig.exe:SYSvol の移行ツール](https://go.microsoft.com/fwlink/?LinkID=121757)
