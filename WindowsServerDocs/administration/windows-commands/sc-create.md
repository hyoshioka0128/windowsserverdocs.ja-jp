---
title: Sc を作成します。
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 59416460-0661-4fef-85cc-73e9d8f4beb4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c1596d3f58fd235039585283a7a6360d85201d7a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80835395"
---
# <a name="sc-create"></a>Sc を作成します。



サブキーとサービスのエントリをレジストリおよびサービス コントロール マネージャー データベースを作成します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
sc [<ServerName>] create [<ServiceName>] [type= {own | share | kernel | filesys | rec | interact type= {own | share}}] [start= {boot | system | auto | demand | disabled | delayed-auto }] [error= {normal | severe | critical | ignore}] [binpath= <BinaryPathName>] [group= <LoadOrderGroup>] [tag= {yes | no}] [depend= <dependencies>] [obj= {<AccountName> | <ObjectName>}] [displayname= <DisplayName>] [password= <Password>]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<ServerName >|サービスが配置されているリモート サーバーの名前を指定します。 名前には UNC (汎用名前付け規則) 形式 (たとえば、\\\\myserver) を使用する必要があります。 SC.exe をローカルで実行するには、このパラメーターを省略します。|
|\<ServiceName >|によって返されるサービスの名前を指定、 **られて** 操作します。|
|type = {独自 \| 共有 \| カーネル \| filesys \| rec \| 対話の種類 = {独自の \| 共有}}|サービスの種類を指定します。 既定の設定は **型 = 独自**します。</br>**独自** -サービスが、独自のプロセスで実行されるように指定します。 実行可能ファイルは他のサービスと共有されません。 これは、既定の設定です。</br>**共有** -サービスが共有プロセスとして実行されるように指定します。 その他のサービス実行可能ファイルを共有します。</br>**カーネル** のドライバーを指定します。</br>**filesys** -ファイル システム ドライバーを指定します。</br>**推奨値** -(コンピューターで使用されるファイル システムを特定する) ファイルが認識システム ドライバーを指定します。</br>**対話** -サービスがユーザーからの入力を受け取って、デスクトップと対話できることを指定します。 対話型サービスは、LocalSystem アカウントで実行する必要があります。 この型と組み合わせて使用する必要があります **型 = 独自** または **型 = 共有**します。 **Type = 相互作用**によって、無効なパラメーターエラーが生成されます。|
|開始 = {ブート \| システム \| 自動 \| 要求 \| 無効 \| 遅延-自動}|サービスの開始の種類を指定します。 既定の設定は **開始要求を =** です。</br>**ブート** のブート ローダーによって読み込まれるデバイス ドライバーを指定します。</br>**システム** のカーネルの初期化中に開始されるデバイス ドライバーを指定します。</br>**自動** -コンピューターが再起動されるたびに自動的に開始するサービスを指定します。 コンピューターにログオンできない場合でも、サービスが実行されることに注意します。</br>**必要に応じて** -を手動で起動するサービスを指定します。 これは既定値の場合 **開始 =** が指定されていません。</br>**無効になっている** -サービスを起動できないように指定します。 無効なサービスを開始するには、他のいくつかの値に開始の種類を変更します。</br>**遅延自動** -サービスが自動的に開始短い形式の時刻が、その他の自動サービスの開始後を指定します。|
|error = {normal \| 重大 \| 重大 \| 無視}|コンピューターを起動すると、サービスが失敗した場合は、エラーの重大度を指定します。 既定の設定は **エラー = normal**します。</br>**通常** -エラーを記録するように指定します。 メッセージ ボックスが表示されたら、サービスの開始に失敗したユーザーに通知します。 起動が続行されます。 これは、既定の設定です。</br>**重大な** -エラーが (可能な場合) に記録するように指定します。 コンピューターは、前回正常起動時の構成と再起動を試みます。 コンピューターを再起動することが発生する可能性がサービス可能性がありますもことはできませんを実行します。</br>**重要な** -エラーが (可能な場合) に記録するように指定します。 コンピューターは、前回正常起動時の構成と再起動を試みます。 前回正常起動時の構成が失敗した場合、スタートアップも失敗し、ブート プロセスが Stop エラーで停止します。</br>**無視** -エラーがログに記録し、起動処理は続行するように指定します。 イベントログにエラーを記録する以外に、ユーザーに通知は与えられません。|
|binpath = \<Binaryp/Name >|サービスのバイナリ ファイルへのパスを指定します。 既定値はありません **binpath =** , 、この文字列を提供する必要があります。|
|group = \<LoadOrderGroup >|このサービスがメンバーになっているグループの名前を指定します。 グループの一覧がレジストリに格納されている、 **HKLM\System\CurrentControlSet\Control\ServiceGroupOrder** サブキー。 既定値は null です。|
|tag = {yes \| no}|TagID があるかどうかを示します CreateService 呼び出しから取得します。 タグは、ブート開始またはシステム開始ドライバーに対してだけ使用されます。|
|依存関係 = \<依存関係 >|サービスまたはこのサービスが開始する前に、まずグループの名前を指定します。 名前は、スラッシュ (/) で区切られます。|
|obj = {\<AccountName > \| \<ObjectName >}|サービスが実行されますが、またはドライバーを実行する Windows ドライバー オブジェクトの名前を指定するアカウントの名前を指定します。|
|displayname = \<DisplayName >|ユーザー インターフェイスのプログラムでサービスを識別するために使用できるフレンドリ名を指定します。|
|パスワード = \<パスワード >|パスワードを指定します。 LocalSystem 以外のアカウントを使用する場合に必要です。|
|/?|コマンド プロンプトでヘルプを表示します。|

## <a name="remarks"></a>コメント

-   各コマンド ライン オプションは、等号 (=) は、オプション名の一部です。
-   スペースは、オプションとその値の間で必要な (たとえば、 **型 = 独自**します。 スペースを省略した場合、操作は失敗します。

## <a name="examples"></a><a name=BKMK_examples></a>例

次の例は、使用する方法を示して、 **sc 作成** コマンド。
```
sc \\myserver create NewService binpath= c:\windows\system32\NewServ.exe
sc create NewService binpath= c:\windows\system32\NewServ.exe type= share start= auto depend= +TDI NetBIOS
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
