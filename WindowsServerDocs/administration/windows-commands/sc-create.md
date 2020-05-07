---
title: Sc.exe 作成
description: Sc.exe ユーティリティを使用して Windows Service Manager に新しいサービスを登録する方法について説明します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 59416460-0661-4fef-85cc-73e9d8f4beb4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9e1a581273def291502bf01e3fc9acf0c296707b
ms.sourcegitcommit: 95b60384b0b070263465eaffb27b8e3bb052a4de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/06/2020
ms.locfileid: "82850103"
---
# <a name="scexe-create"></a>Sc.exe 作成

サブキーとサービスのエントリをレジストリおよびサービス コントロール マネージャー データベースを作成します。

## <a name="syntax"></a>構文

```
sc.exe [<ServerName>] create [<ServiceName>] [type= {own | share | kernel | filesys | rec | interact type= {own | share}}] [start= {boot | system | auto | demand | disabled | delayed-auto }] [error= {normal | severe | critical | ignore}] [binpath= <BinaryPathName>] [group= <LoadOrderGroup>] [tag= {yes | no}] [depend= <dependencies>] [obj= {<AccountName> | <ObjectName>}] [displayname= <DisplayName>] [password= <Password>]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<ServerName>|サービスが配置されているリモート サーバーの名前を指定します。 名前には、汎用名前付け規則 (UNC) 形式 (myserver など\\ \\) を使用する必要があります。 SC.exe をローカルで実行するには、このパラメーターを省略します。|
|\<ServiceName>|によって返されるサービスの名前を指定、 **られて** 操作します。|
|type = {独自\|の\|共有\|カーネル\| filesys \| rec の種類 = { \|独自の共有}}|サービスの種類を指定します。 既定の設定は **型 = 独自**します。</br>**独自** -サービスが、独自のプロセスで実行されるように指定します。 実行可能ファイルは他のサービスと共有されません。 これが既定の設定です。</br>**共有** -サービスが共有プロセスとして実行されるように指定します。 その他のサービス実行可能ファイルを共有します。</br>**カーネル** のドライバーを指定します。</br>**filesys** -ファイル システム ドライバーを指定します。</br>**推奨値** -(コンピューターで使用されるファイル システムを特定する) ファイルが認識システム ドライバーを指定します。</br>**対話** -サービスがユーザーからの入力を受け取って、デスクトップと対話できることを指定します。 対話型サービスは、LocalSystem アカウントで実行する必要があります。 この型と組み合わせて使用する必要があります **型 = 独自** または **型 = 共有**します。 **Type = 相互作用**によって、無効なパラメーターエラーが生成されます。|
|開始 = {ブート\|システム\|の\|自動\|要求\|が無効になりました遅延-自動}|サービスの開始の種類を指定します。 既定の設定は **開始要求を =** です。</br>**ブート** のブート ローダーによって読み込まれるデバイス ドライバーを指定します。</br>**システム** のカーネルの初期化中に開始されるデバイス ドライバーを指定します。</br>**自動** -コンピューターが再起動されるたびに自動的に開始するサービスを指定します。 コンピューターにログオンできない場合でも、サービスが実行されることに注意します。</br>**必要に応じて** -を手動で起動するサービスを指定します。 これは既定値の場合 **開始 =** が指定されていません。</br>**無効になっている** -サービスを起動できないように指定します。 無効なサービスを開始するには、他のいくつかの値に開始の種類を変更します。</br>**遅延自動** -サービスが自動的に開始短い形式の時刻が、その他の自動サービスの開始後を指定します。|
|エラー = {通常\|の\|重大\|クリティカルな無視}|コンピューターを起動すると、サービスが失敗した場合は、エラーの重大度を指定します。 既定の設定は **エラー = normal**します。</br>**通常** -エラーを記録するように指定します。 メッセージ ボックスが表示されたら、サービスの開始に失敗したユーザーに通知します。 起動が続行されます。 これが既定の設定です。</br>**重大な** -エラーが (可能な場合) に記録するように指定します。 コンピューターは、前回正常起動時の構成と再起動を試みます。 コンピューターを再起動することが発生する可能性がサービス可能性がありますもことはできませんを実行します。</br>**重要な** -エラーが (可能な場合) に記録するように指定します。 コンピューターは、前回正常起動時の構成と再起動を試みます。 前回正常起動時の構成が失敗した場合、スタートアップも失敗し、ブート プロセスが Stop エラーで停止します。</br>**無視** -エラーがログに記録し、起動処理は続行するように指定します。 イベントログにエラーを記録する以外に、ユーザーに通知は与えられません。|
|binpath = \<binaryp name>|サービスのバイナリ ファイルへのパスを指定します。 既定値はありません **binpath =**, 、この文字列を提供する必要があります。|
|グループ = \<loadordergroup>|このサービスがメンバーになっているグループの名前を指定します。 グループの一覧は、レジストリの**HKLM\System\CurrentControlSet\Control\ServiceGroupOrder**サブキーに格納されます。 既定値は、null です。|
|タグ = {はい\|いいえ}|TagID があるかどうかを示します CreateService 呼び出しから取得します。 タグは、ブート開始またはシステム開始ドライバーに対してだけ使用されます。|
|依存 = \<依存関係>|サービスまたはこのサービスが開始する前に、まずグループの名前を指定します。 名前は、スラッシュ (/) で区切られます。|
|obj = {\<AccountName> \| \<ObjectName>}|サービスが実行されますが、またはドライバーを実行する Windows ドライバー オブジェクトの名前を指定するアカウントの名前を指定します。|
|displayname = \<displayname>|ユーザー インターフェイスのプログラムでサービスを識別するために使用できるフレンドリ名を指定します。|
|パスワード = \<パスワード>|パスワードを指定します。 LocalSystem 以外のアカウントを使用する場合に必要です。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>解説

-   各コマンド ライン オプションは、等号 (=) は、オプション名の一部です。
-   スペースは、オプションとその値の間で必要な (たとえば、 **型 = 独自**します。 スペースを省略した場合、操作は失敗します。

## <a name="examples"></a>例

次の例は、 **sc.exe create**コマンドを使用する方法を示しています。
```
sc.exe \\myserver create NewService binpath= c:\windows\system32\NewServ.exe
sc.exe create NewService binpath= c:\windows\system32\NewServ.exe type= share start= auto depend= +TDI NetBIOS
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)
