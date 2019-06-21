---
title: 手順 6 テスト DirectAccess ホームネット サブネットからの接続
description: このトピックでは、OTP 認証と Windows Server 2016 で RSA SecurID を使用した DirectAccess のデモンストレーションのテスト ラボ ガイドの一部
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b9b77cfd-8dd4-476b-a118-f3d6bf59e7b1
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c19376b7301068639ba1315af5e9f5a9a4514b3b
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67283055"
---
# <a name="step-6-test-directaccess-connectivity-from-the-homenet-subnet"></a>手順 6 テスト DirectAccess ホームネット サブネットからの接続

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

DirectAccess のワンタイム パスワード (OTP) の展開が完了し、ホームネット サブネットからの接続をテストすることができます。  
  
### <a name="to-test-otp-functionality-from-the-homenet-subnet-on-client1"></a>CLIENT1 でホームネット サブネットからの OTP の機能をテストするには  
  
1. CLIENT1 でとしてログオンしていることを確認します**User1**します。  
  
2. **開始**画面で「**powershell.exe**、を右クリックして**powershell** をクリック**詳細**、順にクリックします**実行管理者として**します。 **[ユーザー アカウント制御]** ダイアログ ボックスが表示されたら、表示された操作が正しいことを確認し、 **[はい]** をクリックします。  
  
3. Windows PowerShell ウィンドウで、入力**gpupdate/force**、ENTER キーを押します。  
  
4. CLIENT1 を Corpnet サブネットから外し、ホームネット サブネットに接続します。  
  
5. Client1 で、Internet Explorer を開き、アドレス バーに「 **https://app1.corp.contoso.com/** ENTER キーを押します。 F5 キーを押す。  
  
   サイトを開かないでください。  
  
6. **開始**画面で「**RSA**、 をクリック**RSA SecurID トークン**します。  
  
7. RSA SecurID トークンが 1 回限りのパスワードを変更するまで待機し、をクリックし、**コピー**します。  
  
8. 通知領域の **[ネットワーク接続]** アイコンをクリックして、DA メディア マネージャーにアクセスします。  
  
9. クリックして**Contoso の DirectAccess 接続**、 をクリック**続行**します。  
  
10. コントロール + Alt + Del キーを押すし、をクリックして、**ワンタイム パスワード (OTP)** を並べて表示します。  
  
11. コピー先の 8 桁のトークン コードを貼り付けて、をクリックして**OK**します。 認証が完了するまで待ちます。 DirectAccess の職場の接続状態になります**接続**します。  
  
12. Internet Explorer で、アドレス バーに「 **https://app1.corp.contoso.com/** ENTER キーを押します。 F5 キーを押す。 APP1 の既定の IIS Web サイトが表示されます。  
  
13. Internet Explorer アドレス バーに「 **https://app2.corp.contoso.com/** ENTER キーを押します。 F5 キーを押す。 APP2 の既定の IIS web サイトが表示されます。  
  
14. **開始**画面で「<strong>\\\app1\files</strong>、ENTER キーを押します。  
  
15. **ファイル**共有フォルダー ウィンドウで、ダブルクリックして、 **Example.txt**ファイル。 Example.txt ファイルの内容が表示されます。  
  
16. **開始**画面で「<strong>\\\app2\files</strong>、ENTER キーを押します。  
  
17. **ファイル**共有フォルダー ウィンドウで、ダブルクリックして、**新しい Text Document.txt**ファイル。 新しいテキスト ドキュメントの.txt ファイルの内容が表示されます。  
  


