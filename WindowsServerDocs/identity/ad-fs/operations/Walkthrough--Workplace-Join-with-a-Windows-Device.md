---
ms.assetid: c17d143b-86b4-47c0-b76e-1862dda8f0bd
title: チュートリアル-Windows デバイスでの Workplace Join
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 4f2e3dbf5754b4b33aec972e40a91cbe67c82220
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87966979"
---
# <a name="walkthrough-workplace-join-with-a-windows-device"></a>チュートリアル:職場への Windows デバイスの参加

このトピックでは、ワークプレース ジョインを使用して Windows デバイスを職場に接続する方法と、シングル サインオンを使用して Web アプリケーションにアクセスする方法を説明します。 このチュートリアルを実行する前に、「 [Windows Server 2012 R2 で AD FS 用のラボ環境](../deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)をセットアップする」セクションの手順を完了する必要があります。

## <a name="access-the-web-application-before-device-registration"></a>デバイス登録前の Web アプリケーションへのアクセス
このチュートリアルでは、デバイスを職場に参加させる前に、会社の Web アプリケーションにアクセスします。 Web ページには、セキュリティ トークンに含まれていた信頼性情報が表示されます。 信頼性情報の一覧に、使用するデバイスについての情報が含まれていないことがわかります。 また、シングル サインオンを使用できないこともわかります。

#### <a name="to-access-the-web-application-before-you-use-workplace-join-on-your-device"></a>デバイスでワークプレース ジョインを使用する前に Web アプリケーションにアクセスするには

1. Microsoft アカウントを使用して Client1 にログオンします。

2. Internet Explorer を開き、汎用要求アプリを参照し **https://webserv1.contoso.com/claimapp** ます。

3. 会社のドメインアカウント <strong>roberth@contoso.com</strong> (パスワード:) を使用して、web ページにログオンし <strong>P@ssword</strong> ます。

4. Web ページに、セキュリティ トークンに含まれるすべての信頼性情報が一覧表示されます。 セキュリティ トークンにはユーザーの信頼性情報のみが存在します。

5. Internet Explorer を閉じます。

6. Internet Explorer を開き、同じ要求アプリ () に移動し **https://webserv1.contoso.com/claimapp** ます。

7. 資格情報の入力を再度、求められます。 ワークプレース ジョインを使用してデバイスから職場に接続していないため、シングル サインオンは機能していません。

## <a name="join-your-device-with-workplace-join"></a>ワークプレース ジョインによるデバイスの参加

> [!IMPORTANT]
> ワークプレース ジョインが正しく動作するには、クライアント コンピューター (Client1) で SSL 証明書を信頼する必要があります。この証明書は、「 [Step 2: Configure the Federation Server with Device Registration Service (ADFS1)](../deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_4)」で Active Directory フェデレーション サービス (AD FS) を構成する際に使用されたものです。 また、証明書の失効情報の検証が可能になっている必要もあります。 ワークプレース ジョインで問題が発生した場合は、Client1 のイベント ログを確認できます。
>
> イベント ログを表示するには、イベント ビューアーを開き、**[アプリケーションとサービス ログ]**、**[Microsoft]**、**[Windows]** の順に展開し、**[ワークプレース ジョイン]** をクリックします。

#### <a name="to-join-your-device-with-workplace-join"></a>ワークプレース ジョインを使用してデバイスを参加させるには

1. Microsoft アカウントを使用して Client1 にログオンします。

2. **スタート**画面で、**チャーム** バーを開き、**[設定]** チャームをクリックします。 **[PC 設定の変更]** を選択します。

3. **[PC 設定]** ページで **[ネットワーク]** を選択し、**[社内]** をクリックします。

4. [**ユーザー名を入力して職場へのアクセスを取得するか、デバイス管理を有効にする**] ボックスに「」と入力し、 <strong>roberth@contoso.com</strong> [**参加**] をクリックします。

5. 資格情報の入力を求められたら、「」と入力し、パスワードを入力し <strong>roberth@contoso.com</strong> <strong>P@ssword</strong> ます。 **[OK]** をクリックします。

6. 次のメッセージが表示されます:"このデバイスは社内のネットワークに参加しています"

### <a name="access-the-web-application-after-joining-the-workplace"></a>職場への参加後の Web アプリケーションへのアクセス
ここでは、ワークプレース ジョインを使用して接続されたデバイスから会社の Web アプリケーションにアクセスします。 Web ページには、セキュリティ トークンに含まれていた信頼性情報が表示されます。 信頼性情報の一覧に、デバイスとユーザーの両方の情報が含まれていることがわかります。 また、シングル サインオンを使用できることもわかります。

##### <a name="to-access-the-web-application-after-joining-the-workplace"></a>職場への参加後に Web アプリケーションにアクセスするには

1. Microsoft アカウントを使用して **Client1** にログオンします。

2. Internet Explorer を開き、汎用要求アプリを参照し **https://webserv1.contoso.com/claimapp** ます。

3. 会社のドメインアカウント <strong>roberth@contoso.com</strong> (パスワード:) を使用して、web ページにログオンし <strong>P@ssword</strong> ます。

4. Web ページに、セキュリティ トークンに含まれる信頼性情報が一覧表示されます。 トークンにはユーザーとデバイスの両方の信頼性情報が含まれています。

5. Internet Explorer を閉じます。

6. Internet Explorer を開き、同じ要求アプリ () に移動し **https://webserv1.contoso.com/claimapp** ます。

7. 今回は資格情報の入力を**求められません**。 ワークプレース ジョインを使用したデバイスから接続しているため、シングル サインオンが機能しています。

## <a name="see-also"></a>参照
[任意のデバイスからの職場への参加による企業アプリケーション間の SSO とシームレスな2要素認証](Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md) 
[Windows Server 2012 R2 で AD FS 用のラボ環境をセットアップする](../deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md) 
[チュートリアル: IOS デバイスでの Workplace Join](Walkthrough--Workplace-Join-with-an-iOS-Device.md)



