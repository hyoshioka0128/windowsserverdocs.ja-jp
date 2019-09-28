---
title: 手順 6. Homenet サブネットからの DirectAccess 接続のテスト
description: このトピックは、「テストラボガイド-OTP 認証を使用した DirectAccess のデモンストレーション」と「RSA SecurID for Windows Server 2016」に含まれています。
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b9b77cfd-8dd4-476b-a118-f3d6bf59e7b1
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 9cce81998c6041aea223da29979a53d6069f599c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404746"
---
# <a name="step-6-test-directaccess-connectivity-from-the-homenet-subnet"></a>手順 6. Homenet サブネットからの DirectAccess 接続のテスト

>適用先:Windows Server (半期チャネル)、Windows Server 2016

DirectAccess のワンタイムパスワード (OTP) の展開が完了し、Homenet サブネットからの接続のテストを開始できるようになりました。  
  
### <a name="to-test-otp-functionality-from-the-homenet-subnet-on-client1"></a>CLIENT1 の Homenet サブネットから OTP 機能をテストするには  
  
1. CLIENT1 で、 **User1**としてログオンしていることを確認します。  
  
2. **スタート**画面で、「**powershell**」と入力し、 **[powershell]** を右クリックします。次に、 **[詳細設定]** をクリックし、 **[管理者として実行]** をクリックします。 **[ユーザー アカウント制御]** ダイアログ ボックスが表示されたら、表示された操作が正しいことを確認し、 **[はい]** をクリックします。  
  
3. Windows PowerShell ウィンドウで、「 **gpupdate/force**」と入力し、enter キーを押します。  
  
4. ネットワーク上のサブネットから CLIENT1 を取り外し、Homenet サブネットに接続します。  
  
5. CLIENT1 で Internet Explorer を開き、アドレスバーに「 **https://app1.corp.contoso.com/** 」と入力して、enter キーを押します。 F5 キーを押す。  
  
   サイトを開けません。  
  
6. **スタート**画面で「**rsa**」と入力し、 **[rsa SecurID トークン]** をクリックします。  
  
7. RSA SecurID トークンによってワンタイムパスワードが変更されるまで待ってから、 **[コピー]** をクリックします。  
  
8. 通知領域の **[ネットワーク接続]** アイコンをクリックして、DA メディア マネージャーにアクセスします。  
  
9. **[Contoso DirectAccess 接続]** をクリックし、 **[続行]** をクリックします。  
  
10. Ctrl + Alt + Del キーを押し、 **[ワンタイムパスワード (OTP)]** タイルをクリックします。  
  
11. 以前にコピーした8桁のトークンコードを貼り付けて、[ **OK]** をクリックします。 認証が完了するまで待ちます。 DirectAccess Workplace の接続状態が **接続**中 "になります。  
  
12. Internet Explorer で、アドレスバーに「 **https://app1.corp.contoso.com/** 」と入力し、enter キーを押します。 F5 キーを押す。 APP1 の既定の IIS Web サイトが表示されます。  
  
13. Internet Explorer のアドレスバーに「 **https://app2.corp.contoso.com/** 」と入力し、enter キーを押します。 F5 キーを押す。 APP2 に既定の IIS web サイトが表示されます。  
  
14. **スタート**画面で、「<strong>\\ \ app1\files</strong>」と入力し、enter キーを押します。  
  
15. **ファイル** 共有フォルダー ウィンドウで、**例の .txt**ファイルをダブルクリックします。 例の .txt ファイルの内容が表示されます。  
  
16. **スタート**画面で、「<strong>\\ \ app2\files</strong>」と入力し、enter キーを押します。  
  
17. **ファイル** 共有フォルダー ウィンドウで、**新しいテキストドキュメント .txt**ファイルをダブルクリックします。 新しいテキストドキュメント .txt ファイルの内容が表示されます。  
  


