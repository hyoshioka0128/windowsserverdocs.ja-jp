---
ms.assetid: c17d143b-86b4-47c0-b76e-1862dda8f0bd
title: "チュートリアル - Windows デバイスでワークプ レース ジョイン"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: fd222eb47982591e051594e8a572443b65c0357f
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="walkthrough-workplace-join-with-a-windows-device"></a>Windows デバイスのチュートリアル: 職場への参加

>適用対象: Windows Server 2016、Windows Server 2012 R2

このトピックでは、ワークプ レース ジョインを使用して、Windows デバイスを職場に接続する方法とシングル サインオンを使用して web アプリケーションにアクセスする方法について説明します。 手順を完了する必要があります、 [Windows Server 2012 R2 の AD FS のラボ環境を設定](../deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)セクション前に、このチュートリアルを試すことができます。

## <a name="access-the-web-application-before-device-registration"></a>デバイスの登録する前に web アプリケーションにアクセスします。
このチュートリアルでは、お客様のデバイスを職場に参加する前に、会社の web アプリケーションにアクセスします。 Web ページには、セキュリティ トークンに含まれていた信頼性情報が表示されます。 信頼性情報の一覧に、デバイスに関する情報が含まれていないことに注意してください。 シングル サインオンがないこともわかります。

#### <a name="to-access-the-web-application-before-you-use-workplace-join-on-your-device"></a>デバイスでワークプ レース ジョインを使用する前に、web アプリケーションにアクセスするには

1.  Microsoft アカウントで Client1 にログオンします。

2.  Internet Explorer を汎用的なクレーム アプリへの参照を開いて**https://webserv1.contoso.com/claimapp**します。

3.  会社のドメイン アカウントを使用して web ページにログオンします。 ** roberth@contoso.com **、パスワード: ** P@ssword**します。

4.  Web ページには、セキュリティ トークン内のすべての信頼性情報が一覧表示します。 ユーザーの信頼性情報のみが、セキュリティ トークン内に存在します。

5.  Internet Explorer を閉じます。

6.  Internet Explorer を開き、同じ要求ベースのアプリケーションに移動**https://webserv1.contoso.com/claimapp**します。

7.  もう一度資格情報の入力を求められますことに注意してください。 ワークプ レース ジョインを使用してデバイスを職場に接続されていないと、したがって、シングル サインオン必要はありません。

## <a name="join-your-device-with-workplace-join"></a>ワークプ レース ジョインでデバイスを参加させる

> [!IMPORTANT]
> ワークプ レース ジョインを成功させるのには、クライアント コンピューター (Client1) は、Active Directory フェデレーション サービス (AD FS) の構成に使用された SSL 証明書を信頼する必要があります[手順 2: Configure the Federation Server を with Device Registration Service (ADFS1)](../deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_4)します。 また、証明書の失効情報を検証できる必要があります。 ワークプ レース ジョインで問題が発生した場合は、Client1 で、イベント ログを表示できます。
> 
> イベント ログを表示するには、イベント ビューアーを開き、展開**アプリケーションとサービス ログ**、展開**Microsoft**、展開**Windows**、] をクリックし、**ワークプ レース ジョイン**します。

#### <a name="to-join-your-device-with-workplace-join"></a>ワークプ レース ジョインでデバイスを参加させる

1.  Microsoft アカウントで Client1 にログオンします。

2.  **開始**] 画面で、オープン、**チャーム**バーし、を選択、**設定**チャームします。 選択**PC 設定の変更**します。

3.  **PC 設定の**] ページで、[**ネットワーク**、] をクリックし、**ワークプ レース**します。

4.  **職場へのアクセスを取得またはデバイスの管理を有効にするユーザー Id を入力**ボックスに、入力** roberth@contoso.com **、] をクリックし、**参加**します。

5.  資格情報を求められたら、入力** roberth@contoso.com **、およびパスワード: ** P@ssword**します。 をクリックして**OK**します。

6.  メッセージが表示されるはず:「このデバイスが参加している、職場のネットワーク」。

### <a name="access-the-web-application-after-joining-the-workplace"></a>職場への参加後に web アプリケーションにアクセスします。
デモのこの部分では、ワークプ レース ジョインで接続されているデバイスから会社の web アプリケーションにアクセスします。 Web ページには、セキュリティ トークンに含まれていた信頼性情報が表示されます。 信頼性情報の一覧が、デバイスとユーザーの両方の情報が含まれていることを確認します。 シングル サインオンできるようになりましたがあることを確認することも可能性があります。

##### <a name="to-access-the-web-application-after-joining-the-workplace"></a>職場への参加後に web アプリケーションにアクセスするには

1.  ログオン**Client1** 、Microsoft アカウントにします。

2.  Internet Explorer を汎用的なクレーム アプリへの参照を開いて**https://webserv1.contoso.com/claimapp**します。

3.  会社のドメイン アカウントを使用して web ページにログオンします。 ** roberth@contoso.com **、パスワード: ** P@ssword**します。

4.  Web ページには、セキュリティ トークンの信頼性情報が一覧表示します。 ユーザーのトークンには、ユーザーとデバイスの両方の信頼性情報が含まれています。

5.  Internet Explorer を閉じます。

6.  Internet Explorer を開き、同じ要求ベースのアプリケーションに移動**https://webserv1.contoso.com/claimapp**します。

7.  **しない**、資格情報をもう一度入力を求めるメッセージが表示されます。 ワークプ レース ジョインを使用してデバイスから接続しているし、シングル サインオンがあるためです。

## <a name="see-also"></a>参照してください。
[任意のデバイスからの SSO とシームレスな 2 つ目 Factor Authentication Across Company Applications 職場への参加](Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)
[Windows Server 2012 R2 の AD FS のラボ環境を設定](../deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)
[チュートリアル: iOS デバイスでの社内参加](Walkthrough--Workplace-Join-with-an-iOS-Device.md)



