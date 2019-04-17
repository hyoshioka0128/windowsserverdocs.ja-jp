---
ms.assetid: cb834273-828a-4141-9387-37dd8270e932
title: "Winlogon 自動再起動サインオン (ARSO)"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 27d4285d34105908555458a95bd70fc04fd2901a
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="winlogon-automatic-restart-sign-on-arso"></a>Winlogon 自動再起動サインオン (ARSO)

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

**作成者**: Windows グループに Justin チューナー シニア サポート エスカレーション エンジニア

> [!NOTE]
> このコンテンツが、Microsoft カスタマー サポート エンジニアによって書き込まれるあり、経験豊富な管理者と TechNet の通常のトピックよりも機能と Windows Server 2012 R2 で解決策の詳細な技術的説明を求めているシステム アーキテクトです。 ただし、実施されていません、同様の編集過程のため、TechNet の「新機能が見つかった通常より洗練されて、言語によってように見える場合があります。

## <a name="overview"></a>概要
Windows 8 では、ロック画面のアプリが導入されました。  これらは、アプリケーションを実行し、ユーザーのセッションのロック中に通知を表示 (カレンダーの予定、電子メールとメッセージなど。)。  再起動時にこれらのロック画面通知を表示する、Windows Update プロセスによって再起動がデバイスが失敗します。  一部のユーザーは、これらのロック画面アプリケーションに依存します。

## <a name="whats-changed"></a>新機能が変更されたか。
ユーザーが Windows 8.1 デバイスにサインインするときに LSA はユーザーの資格情報を lsass.exe によってのみアクセス可能な暗号化されたメモリに保存します。 Windows Update では、ユーザーが存在せず、自動的に再起動を開始する場合はこれらの資格情報を使用して、ユーザーの自動ログオンを構成します。 TCB 特権を持つシステムとして実行されている Windows Update では、これを行う RPC 呼び出しを開始します。

での再起動をユーザーが自動的に自動ログオンのメカニズムを使用してログインし、さらに、ユーザーのセッションを保護するロックされます。 ロックが開始されますを介して Winlogon 一方、資格情報の管理は LSA によって行われます。  自動的に署名し、本体上のユーザーのロックをユーザーのロック画面アプリケーションは再起動して利用します。

> [!NOTE]
> Windows Update 再起動の強制、前回の対話ユーザーが自動的にサインオンして、セッションがロックされているため、ユーザーのロック画面のアプリを実行できます。

![winlogon](media/Winlogon-Automatic-Restart-Sign-On--ARSO-/GTR_ADDS_LockScreenApp.gif)

![winlogon](media/Winlogon-Automatic-Restart-Sign-On--ARSO-/GTR_ADDS_LockScreen.gif)

**簡単な概要**

-   Windows Update の再起動が必要

-   コンピューターを再起動することは、(*実行中のアプリにデータは失われません*) ですか?

    -   再起動をします。

    -   再びログインします。

    -   コンピューターのロック

-   有効になっているか、グループ ポリシーによって無効になっています

    -   Server Sku で既定で無効になっています。

-   なぜでしょうか。

    -   ユーザーがログオンに戻るまで、一部の更新プログラムを終了できません。

    -   良いユーザー エクスペリエンス: 15 分の更新のインストールを完了するまで待機する必要はありません

-   どう。 自動ログオン

    -   パスワードが格納されて、その資格情報を使用してログインします。

    -   ページングされたメモリに LSA シークレットとして資格情報の保存

    -   BitLocker が有効にした場合にのみ有効にできます。

## <a name="group-policy-sign-in-last-interactive-user-automatically-after-a-system-initiated-restart"></a>グループ ポリシー: サインインが前回の対話ユーザー システムによる再起動後に自動的に
Windows 8.1 で Windows Server 2012 R2、Windows Update 再起動した後にロック画面のユーザーの自動ログオンは Server Sku をオプトインおよびクライアント Sku の参加を中止します。

**ポリシーの場所:**コンピューターの構成 > ポリシー > 管理用テンプレート > Windows コンポーネント > Windows のログオン オプション

**ポリシー名:**サインインが前回の対話ユーザー システムによる再起動後に自動的に

**サポートされている:**には、少なくとも Windows Server 2012 R2、Windows 8.1 または Windows RT 8.1

**説明/ヘルプ:**

このポリシー設定では、デバイスは自動的にサインインが前回の対話ユーザー Windows 更新プログラムがシステムを再起動した後かどうかを制御します。

有効にするか、またはこのポリシー設定を構成しなかった場合、デバイスは、ユーザーの資格情報 (ユーザー名、ドメイン、および暗号化されたパスワードを含む) を安全に Windows Update による再起動後に自動サインインを構成を保存します。 Windows Update 再起動後に、ユーザーが自動的にサインインし、セッションがそのユーザー用に構成されたすべてのロック画面アプリで自動的にロックされています。

このポリシー設定を無効にした場合、デバイスが Windows Update による再起動後の自動サインイン ユーザーの資格情報を保存してされません。 システムの再起動後、ユーザーのロック画面アプリは再起動されません。

**レジストリ エディター**

|値の名前|種類|データ|
|--------------|--------|--------|
|DisableAutomaticRestartSignOn|DWORD|0<br /><br />**例:**<br /><br />0 (有効)。<br /><br />1 (無効)|

**ポリシーのレジストリの場所:** hklm \software\microsoft\windows\currentversion\policies\system

**型:** DWORD

**レジストリの名前:** DisableAutomaticRestartSignOn

値: 0 または 1

0 = 有効

1 = 無効になっています。

![winlogon](media/Winlogon-Automatic-Restart-Sign-On--ARSO-/GTR_ADDS_SignInPolicy.gif)

## <a name="troubleshooting"></a>トラブルシューティング
WinLogon が自動的にロック、ときに WinLogon の状態のトレースは WinLogon イベント ログに保存されます。

自動ログオンの構成の試行の状態がログに記録します。

-   成功した場合

    -   そのために記録します。

-   エラーの場合。

    -   失敗の原因を記録します。

-   BitLocker の状態が変更されたとき。

    -   資格情報の削除がログに記録します。

        -   これらは、LSA 操作のログに保存されます。

### <a name="reasons-why-autologon-might-fail"></a>自動ログオンが機能しない理由
ユーザーの自動ログインを実現できないいくつかのような場合があります。  このセクションでは、既知のシナリオが発生する可能性がこれをキャプチャする対象としています。

### <a name="user-must-change-password-at-next-login"></a>ユーザーは次回のログイン時にパスワードを変更する必要があります。
ユーザーのログインは、次回のログイン時にパスワードの変更が必要な場合、ブロックされた状態を入力できます。  ほとんどの場合、再起動の前に検出されたすべてではなくを指定できます (たとえば、パスワードの有効期限に到達できるシャット ダウンと次回のログインの間でします。

### <a name="user-account-disabled"></a>ユーザー アカウントを無効に
無効になっている場合でも、既存のユーザー セッションを維持することができます。  無効になっているアカウントの再起動が検出されてローカルほとんどの場合、事前にドメイン アカウントの (いくつかのドメインは、DC でアカウントが無効になっている場合でもにログイン シナリオの作業をキャッシュ) できない可能性があります gp に応じて。

### <a name="logon-hours-and-parental-controls"></a>ログオン時間、保護者による制限
ログオン時間、保護者は、新しいユーザー セッションを禁止が作成されないされます。  再起動がこの期間中に発生した場合、ユーザーがログインする許可されません。  ロックするか、対応アクションとしてログアウトを原因となるその他のポリシーがあります。  これは、特に、メンテナンス ウィンドウは、この時間中に一般場合、アカウントのロックダウンが発生するベッドの時間とウェイク アップ、多くの子場合の問題があります。

## <a name="additional-resources"></a>その他のリソース
**SEQ テーブル \\\ * ARABIC 3: ARSO 用語集**

|用語|定義|
|--------|--------------|
|自動ログオン|自動ログオンは、いくつかのリリースの Windows に存在した機能です。  これは Windows の自動ログオン v3.01 などのツールがある Windows の文書化された機能*[http:/technet.microsoft.com/sysinternals/bb963905.aspx](https://technet.microsoft.com/sysinternals/bb963905.aspx)*<br /><br />デバイスの 1 人のユーザーの資格情報を入力しなくても自動的にログインできます。 資格情報が構成され、暗号化された LSA シークレットとしてレジストリに格納されています。|


