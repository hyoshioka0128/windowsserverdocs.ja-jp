---
ms.assetid: c17d143b-86b4-47c0-b76e-1862dda8f0bd
title: チュートリアル - Windows デバイスのワークプ レース ジョイン
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 8b3b2934e7aa177e873e19d77530b2d796ccd521
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66188897"
---
# <a name="walkthrough-workplace-join-with-a-windows-device"></a>チュートリアル: 職場への Windows デバイスの参加

このトピックでは、ワークプレース ジョインを使用して Windows デバイスを職場に接続する方法と、シングル サインオンを使用して Web アプリケーションにアクセスする方法を説明します。 手順を完了する必要があります、 [Windows Server 2012 R2 で AD FS のラボ環境をセットアップ](../deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)セクションの前に、このチュートリアルを試すことができます。

## <a name="access-the-web-application-before-device-registration"></a>デバイス登録前の Web アプリケーションへのアクセス
このチュートリアルでは、デバイスを職場に参加させる前に、会社の Web アプリケーションにアクセスします。 Web ページには、セキュリティ トークンに含まれていた信頼性情報が表示されます。 信頼性情報の一覧に、使用するデバイスについての情報が含まれていないことがわかります。 また、シングル サインオンを使用できないこともわかります。

#### <a name="to-access-the-web-application-before-you-use-workplace-join-on-your-device"></a>デバイスでワークプレース ジョインを使用する前に Web アプリケーションにアクセスするには

1.  Microsoft アカウントを使用して Client1 にログオンします。

2.  Internet Explorer を汎用の要求アプリへの参照を開いて **https://webserv1.contoso.com/claimapp** します。

3.  会社のドメイン アカウントを使用して web ページにログオン: **roberth@contoso.com**、パスワード:  **P@ssword** します。

4.  Web ページに、セキュリティ トークンに含まれるすべての信頼性情報が一覧表示されます。 セキュリティ トークンにはユーザーの信頼性情報のみが存在します。

5.  Internet Explorer を閉じます。

6.  Internet Explorer を開き、同じ要求ベースのアプリケーションに移動します **https://webserv1.contoso.com/claimapp** します。

7.  資格情報の入力を再度、求められます。 ワークプレース ジョインを使用してデバイスから職場に接続していないため、シングル サインオンは機能していません。

## <a name="join-your-device-with-workplace-join"></a>ワークプレース ジョインによるデバイスの参加

> [!IMPORTANT]
> ワークプ レース ジョインを成功させるのには、クライアント コンピューター (Client1) は、Active Directory フェデレーション サービス (AD FS) を構成するために使用された SSL 証明書を信頼する必要があります[手順 2。With Device Registration Service (ADFS1) フェデレーション サーバーを構成する](../deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_4)します。 また、証明書の失効情報の検証が可能になっている必要もあります。 ワークプレース ジョインで問題が発生した場合は、Client1 のイベント ログを確認できます。
> 
> イベント ログを表示するには、イベント ビューアーを開き、 **[アプリケーションとサービス ログ]** 、 **[Microsoft]** 、 **[Windows]** の順に展開し、 **[ワークプレース ジョイン]** をクリックします。

#### <a name="to-join-your-device-with-workplace-join"></a>ワークプレース ジョインを使用してデバイスを参加させるには

1.  Microsoft アカウントを使用して Client1 にログオンします。

2.  **スタート**画面で、**チャーム** バーを開き、 **[設定]** チャームをクリックします。 **[PC 設定の変更]** を選択します。

3.  **[PC 設定]** ページで **[ネットワーク]** を選択し、 **[社内]** をクリックします。

4.  **職場へのアクセスを取得またはデバイスの管理を有効にする、UserID を入力**ボックスに「 **roberth@contoso.com**、順にクリックします**参加**します。

5.  資格情報を求められたら、入力 **roberth@contoso.com** とパスワード:  **P@ssword** します。 **[OK]** をクリックします。

6.  次のメッセージが表示されます:"このデバイスは社内のネットワークに参加しています"

### <a name="access-the-web-application-after-joining-the-workplace"></a>職場への参加後の Web アプリケーションへのアクセス
ここでは、ワークプレース ジョインを使用して接続されたデバイスから会社の Web アプリケーションにアクセスします。 Web ページには、セキュリティ トークンに含まれていた信頼性情報が表示されます。 信頼性情報の一覧に、デバイスとユーザーの両方の情報が含まれていることがわかります。 また、シングル サインオンを使用できることもわかります。

##### <a name="to-access-the-web-application-after-joining-the-workplace"></a>職場への参加後に Web アプリケーションにアクセスするには

1.  Microsoft アカウントを使用して **Client1** にログオンします。

2.  Internet Explorer を汎用の要求アプリへの参照を開いて **https://webserv1.contoso.com/claimapp** します。

3.  会社のドメイン アカウントを使用して web ページにログオン: **roberth@contoso.com**、パスワード:  **P@ssword** します。

4.  Web ページに、セキュリティ トークンに含まれる信頼性情報が一覧表示されます。 トークンにはユーザーとデバイスの両方の信頼性情報が含まれています。

5.  Internet Explorer を閉じます。

6.  Internet Explorer を開き、同じ要求ベースのアプリケーションに移動します **https://webserv1.contoso.com/claimapp** します。

7.  今回は資格情報の入力を **求められません** 。 ワークプレース ジョインを使用したデバイスから接続しているため、シングル サインオンが機能しています。

## <a name="see-also"></a>関連項目
[任意のデバイスからの SSO とシームレスな 2 つ目 Factor Authentication Across Company Applications ワークプ レースへの参加](Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)
[Windows Server 2012 R2 で AD FS のラボ環境をセットアップ](../deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)
 [チュートリアル:Workplace Join で iOS デバイスをワークプレースに参加させる](Walkthrough--Workplace-Join-with-an-iOS-Device.md)



