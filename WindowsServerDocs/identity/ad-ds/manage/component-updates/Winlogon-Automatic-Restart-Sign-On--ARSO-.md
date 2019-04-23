---
ms.assetid: cb834273-828a-4141-9387-37dd8270e932
title: Winlogon 自動再起動サインオン (ARSO)
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 4024a00c6c186aa929e88cb2aa86b0ec04a731b3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59883623"
---
# <a name="winlogon-automatic-restart-sign-on-arso"></a>Winlogon 自動再起動サインオン (ARSO)

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

**作成者**:Justin Turner、シニア サポート エスカレーション エンジニア、Windows グループ

> [!NOTE]
> この内容は Microsoft カスタマー サポート エンジニアによって作成され、TechNet が通常提供しているトピックよりも詳細な Windows Server 2012 R2 の機能やソリューションの技術的説明を求めている、経験豊かな管理者とシステム設計者を対象としています。 ただし、TechNet と同様の編集過程は実施されていないため、言語によっては通常より洗練されていない文章が見られる場合があります。

## <a name="overview"></a>概要
Windows 8 では、ロック画面アプリが導入されました。  これらはアプリケーションを実行し、ユーザーのセッションのロック中に、通知を表示する (カレンダーの予定、電子メールやメッセージなどです。)。  再起動時にこれらのロック画面通知を表示するデバイスの Windows Update プロセスによって再起動が失敗します。  一部のユーザーは、これらのロック画面アプリケーションに依存します。

## <a name="whats-changed"></a>変更点は?
ユーザーが Windows 8.1 デバイスにサインインするときに LSA はユーザーの資格情報を lsass.exe によってのみアクセス可能な暗号化されたメモリに保存します。 Windows Update では、ユーザーが存在せず、自動的に再起動を開始したときはこれらの資格情報を使用して、ユーザーの自動ログオンを構成します。 TCB 特権を持つシステムとして実行されている Windows Update でこれを行う RPC 呼び出しを開始します。

ユーザーを自動的には、再起動に Autologon メカニズムを使用してサインインし、さらに、ユーザーのセッションを保護するロックされます。 資格情報の管理は LSA によって行われますが、winlogon プロセスを使用してをロックすることを行われます。  自動的に署名して、コンソールで、ユーザーのロックでは、ユーザーのロック画面アプリケーションは再起動して利用できるになります。

> [!NOTE]
> Windows Update には、再起動が強制実行され、前回の対話ユーザーが自動的にサインオンしている、セッションがロックされているそのユーザーのロック画面アプリを実行できます。

![winlogon](media/Winlogon-Automatic-Restart-Sign-On--ARSO-/GTR_ADDS_LockScreenApp.gif)

![winlogon](media/Winlogon-Automatic-Restart-Sign-On--ARSO-/GTR_ADDS_LockScreen.gif)

**簡単な概要**

-   Windows Update の再起動が必要

-   コンピューターを再起動することは、(*を実行中のアプリはデータは失われません*) ですか?。

    -   再起動をします。

    -   再びログインします。

    -   コンピューターのロック

-   有効になっているか、グループ ポリシーによって無効になっています

    -   Server Sku で既定で無効になっています。

-   なぜでしょうか。

    -   戻り、ユーザーがログオンするまで、一部の更新プログラムを終了できません。

    -   良いユーザー エクスペリエンス: 15 分の更新のインストールを完了するを待機する必要はありません

-   その方法は? 自動ログオン

    -   パスワードが格納されて、その資格情報では、ログインを使用

    -   ページングされたメモリに LSA シークレットとして資格情報の保存

    -   BitLocker が有効になっている場合にのみ有効にできます。

## <a name="group-policy-sign-in-last-interactive-user-automatically-after-a-system-initiated-restart"></a>グループ ポリシー:システムによる再起動後に自動的に前回の対話ユーザーでサインインする
Windows 8.1/Windows Server 2012 R2、Windows Update 再起動した後に、ロック画面のユーザーの自動ログオンは Server Sku をオプトインされ、クライアントの sku の登録を取り消します。

**ポリシーの場所:** コンピューターの構成 > ポリシー > 管理用テンプレート > Windows コンポーネント > Windows のログオン オプション

**ポリシー名:** システムによる再起動後に自動的に前回の対話ユーザーでサインインする

**サポートされています。** Windows Server 2012 R2、Windows 8.1、Windows RT 8.1 またはそれ以降

**説明/ヘルプ:**

このポリシー設定では、Windows Update によるシステムの再起動後にデバイスが前回の対話ユーザーで自動的にサインインするかどうかを制御します。

有効にするか、このポリシー設定を構成していない場合、デバイスは Windows Update による再起動後に自動サインインを構成するユーザーの資格情報 (ユーザー名、ドメイン、および暗号化されたパスワードを含む) を安全に保存します。 Windows Update による再起動後、ユーザーは自動的にサインインし、そのユーザー用に構成されたすべてのロック画面アプリでセッションは自動的にロックされます。

このポリシー設定を無効にした場合、デバイスでは、Windows Update による再起動後の自動サインインのためにユーザーの資格情報が保存されることはありません。 システムの再起動後、ユーザーのロック画面アプリは再起動されません。

**レジストリ エディター**

|［値の名前］|種類|データ|
|--------------|--------|--------|
|DisableAutomaticRestartSignOn|DWORD|0<br /><br />**例:**<br /><br />0 (有効)。<br /><br />1 (無効)|

**ポリシーのレジストリの場所:** HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System

**種類:** DWORD

**レジストリ名:** DisableAutomaticRestartSignOn

値:0 または 1

0 = 有効

1 = 無効

![winlogon](media/Winlogon-Automatic-Restart-Sign-On--ARSO-/GTR_ADDS_SignInPolicy.gif)

## <a name="troubleshooting"></a>トラブルシューティング
WinLogon が自動的にロックしたときに WinLogon の状態のトレースは WinLogon イベント ログに格納されます。

自動ログオンの構成処理のステータスが記録されます。

-   成功した場合

    -   そのために記録します。

-   障害の場合。

    -   失敗の原因を記録します。

-   BitLocker の状態が変更されたとき。

    -   資格情報の削除がログに記録します。

        -   これらは、LSA 操作のログに保存されます。

### <a name="reasons-why-autologon-might-fail"></a>自動ログオンが失敗する理由
ユーザーの自動ログインを実現できないいくつかのケースもあります。  このセクションでは、既知のシナリオが発生する可能性がこれをキャプチャします。

### <a name="user-must-change-password-at-next-login"></a>ユーザーは次回ログイン時にパスワードを変更する必要があります。
ユーザーのログインは、次回のログイン時のパスワードの変更が必要な場合、ブロックされた状態を入力できます。  ほとんどの場合、再起動の前に検出されたすべてではなく使用できます (パスワードの有効期限の到達、シャット ダウンし、次回のログインの間です。

### <a name="user-account-disabled"></a>ユーザー アカウントを無効に
無効になっている場合でも、既存のユーザー セッションを管理できます。  再起動を無効になっているアカウントが検出されてローカルでほとんどの場合、事前にドメイン アカウントを (いくつかのドメインは、DC 上でアカウントが無効になっている場合でもにログイン シナリオの作業をキャッシュ) に、必ずしも gp に応じて。

### <a name="logon-hours-and-parental-controls"></a>ログオン時間、保護者による制限
保護者による制限とログオン時間は、作成すると、新しいユーザー セッションを禁止できます。  再起動がこの期間中に発生した場合、ユーザーはログインを許可されません。  ロックするか、対応するアクションとしてログアウトを原因となるその他のポリシーがあります。  特に、メンテナンス期間がこの期間中に一般がある場合はベッドの時間とウェイク アップのアカウントのロックダウンが発生する、多くの子の例では問題にできます。

## <a name="additional-resources"></a>その他のリソース
**SEQ テーブル\\\*アラビア語 3。ARSO 用語集**

|用語|定義|
|--------|--------------|
|Autologon|自動ログオンは、いくつかのリリースの Windows に存在した機能です。  これは Windows の自動ログオン v3.01 などのツールがある Windows のドキュメント化された機能 *[http:/technet.microsoft.com/sysinternals/bb963905.aspx](https://technet.microsoft.com/sysinternals/bb963905.aspx)*<br /><br />デバイスの 1 人のユーザーの資格情報を入力しなくても自動的にサインインできます。 資格情報が構成され、暗号化された LSA シークレットとしてレジストリに格納します。|


