---
title: 手順は、インターネットから DirectAccess 接続を 7 のテスト
description: このトピックでは、OTP 認証と Windows Server 2016 で RSA SecurID を使用した DirectAccess のデモンストレーションのテスト ラボ ガイドの一部
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ed2a1616-30c6-482a-9a02-4a5023621f58
ms.author: pashort
author: shortpatti
ms.openlocfilehash: a7f67cfc33c2511bf4edbc5030235c97ceb9acf6
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67281277"
---
# <a name="step-7-test-directaccess-connectivity-from-the-internet"></a>手順は、インターネットから DirectAccess 接続を 7 のテスト

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

DirectAccess のワンタイム パスワード (OTP) 展開では、ホームネット サブネットからテストが完了し、インターネットからテストできます。  
  
### <a name="to-test-otp-functionality-from-the-internet-on-client1"></a>CLIENT1 で、インターネットからの OTP の機能をテストするには  
  
1. CLIENT1 でとしてログオンしていることを確認します**User1**します。 CLIENT1 を Corpnet サブネットに接続します。  
  
2. **開始**画面で「**powershell.exe**、を右クリックして**powershell** をクリック**詳細**、順にクリックします**実行管理者として**します。 **[ユーザー アカウント制御]** ダイアログ ボックスが表示されたら、表示された操作が正しいことを確認し、 **[はい]** をクリックします。  
  
3. Windows PowerShell ウィンドウで、入力**gpupdate/force** ENTER キーを押します。  
  
4. ホームネット サブネットから CLIENT1 を取り外し、インターネットに接続し、コンピューターを再起動します。  
  
5. Client1 で、Internet Explorer を開き、アドレス バーに「 **https://app1.corp.contoso.com/** ENTER キーを押します。 F5 キーを押す。  
  
   サイトを開かないでください。  
  
6. **開始**画面で「**RSA**、 をクリック**RSA SecurID トークン**します。  
  
7. RSA SecurID トークンが 1 回限りのパスワードを変更するまで待機し、をクリックし、**コピー**します。  
  
8. 通知領域の **[ネットワーク接続]** アイコンをクリックして、DA メディア マネージャーにアクセスします。  
  
9. クリックして**職場の接続**、 をクリック**続行**します。  
  
10. コントロール + Alt + Del キーを押すし、をクリックして、**ワンタイム パスワード (OTP)** を並べて表示します。  
  
11. コピー先の 8 桁のトークン コードを貼り付けて、をクリックして**OK**します。 認証が完了するまで待ちます。 DirectAccess の職場の接続状態になります**接続**します。  
  
12. Internet Explorer で、アドレス バーに「 **https://app1.corp.contoso.com/** ENTER キーを押します。 F5 キーを押す。 APP1 の既定の IIS Web サイトが表示されます。  
  
13. Internet Explorer アドレス バーに「 **https://app2.corp.contoso.com/** ENTER キーを押します。 F5 キーを押す。 APP2 の既定の IIS web サイトが表示されます。  
  
14. **開始**画面で「<strong>\\\app1\files</strong>、ENTER キーを押します。  
  
15. **ファイル**共有フォルダー ウィンドウで、ダブルクリックして、 **Example.txt**ファイル。 Example.txt ファイルの内容が表示されます。  
  
16. **開始**画面で「<strong>\\\app2\files</strong>、ENTER キーを押します。  
  
17. **ファイル**共有フォルダー ウィンドウで、ダブルクリックして、**新しい Text Document.txt**ファイル。 新しいテキスト ドキュメントの.txt ファイルの内容が表示されます。  
  


