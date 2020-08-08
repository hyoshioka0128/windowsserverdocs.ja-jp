---
title: 手順 7. インターネットからの DirectAccess 接続をテストする
description: このトピックは、「テストラボガイド-OTP 認証を使用した DirectAccess のデモンストレーション」と「RSA SecurID for Windows Server 2016」に含まれています。
manager: brianlic
ms.topic: article
ms.assetid: ed2a1616-30c6-482a-9a02-4a5023621f58
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 18cf11af84ab43e7fe0fd4ea93f10e61159048a8
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87963968"
---
# <a name="step-7-test-directaccess-connectivity-from-the-internet"></a>手順 7. インターネットからの DirectAccess 接続をテストする

>適用先:Windows Server (半期チャネル)、Windows Server 2016

DirectAccess のワンタイムパスワード (OTP) の展開は、Homenet サブネットからテストされ、インターネットからテストできるようになりました。

### <a name="to-test-otp-functionality-from-the-internet-on-client1"></a>CLIENT1 でインターネットから OTP 機能をテストするには

1. CLIENT1 で、 **User1**としてログオンしていることを確認します。 CLIENT1 を企業ネットワークサブネットに接続します。

2. **スタート**画面で、「**powershell.exe**」と入力し、[ **powershell**] を右クリックします。次に、[**詳細設定**] をクリックし、[**管理者として実行**] をクリックします。 [**ユーザー アカウント制御**] ダイアログ ボックスが表示されたら、表示された操作が正しいことを確認し、[**はい**] をクリックします。

3. Windows PowerShell ウィンドウで、「 **gpupdate/force** 」と入力し、enter キーを押します。

4. CLIENT1 のサブネットから CLIENT1 を取り外し、インターネットに接続して、コンピューターを再起動します。

5. CLIENT1 で Internet Explorer を開き、アドレスバーに「」と入力して、 **https://app1.corp.contoso.com/** enter キーを押します。 F5 キーを押します。

   サイトを開けません。

6. **スタート**画面で「**rsa**」と入力し、[ **rsa SecurID トークン**] をクリックします。

7. RSA SecurID トークンによってワンタイムパスワードが変更されるまで待ってから、[**コピー**] をクリックします。

8. 通知領域の **[ネットワーク接続]** アイコンをクリックして、DA メディア マネージャーにアクセスします。

9. [**職場の接続**] をクリックし、[**続行**] をクリックします。

10. Ctrl + Alt + Del キーを押し、[**ワンタイムパスワード (OTP)** ] タイルをクリックします。

11. 以前にコピーした8桁のトークンコードを貼り付けて、[ **OK]** をクリックします。 認証が完了するまで待ちます。 DirectAccess Workplace の接続状態が [**接続**中 "になります。

12. Internet Explorer のアドレスバーに「」と入力し、enter **https://app1.corp.contoso.com/** キーを押します。 F5 キーを押します。 APP1 の既定の IIS Web サイトが表示されます。

13. Internet Explorer のアドレスバーに「」と入力し、enter **https://app2.corp.contoso.com/** キーを押します。 F5 キーを押します。 APP2 に既定の IIS web サイトが表示されます。

14. **スタート**画面で「<strong> \\ \app1\files</strong>」と入力し、enter キーを押します。

15. [**ファイル**] [共有フォルダー] ウィンドウで、 **Example.txt**ファイルをダブルクリックします。 Example.txt ファイルの内容が表示されます。

16. **スタート**画面で「<strong> \\ \app2\files</strong>」と入力し、enter キーを押します。

17. [**ファイル**] [共有フォルダー] ウィンドウで、**新しいテキスト Document.txt**ファイルをダブルクリックします。 新しいテキスト Document.txt ファイルの内容が表示されます。



