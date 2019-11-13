---
ms.assetid: 299e4fb9-8f1a-4275-ad7d-dad4f1594657
title: チュートリアル-iOS デバイスでの Workplace Join
description: ''
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 10/18/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 5214165c2843461a2da8b574ad28f92b0e0bc64d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407496"
---
# <a name="walkthrough-workplace-join-with-an-ios-device"></a>チュートリアル: iOS デバイスの Workplace Join


> [!IMPORTANT] 
> この方法は、完全なオンプレミスの顧客のみに関連しています。 ハイブリッドまたはクラウド専用のお客様は、この方法を使用して iOS デバイスを登録することはできません。 また、オンプレミスの顧客がクラウドに移行する場合、この方法は互換性がありません。 デバイスを登録解除し、クラウドに登録する必要があります。 

このトピックでは、iOS デバイスでのワークプレース ジョインについて説明します。 このチュートリアルを実行する前に、「 [Windows Server 2012 R2 で AD FS 用のラボ環境](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)をセットアップする」セクションの手順を完了する必要があります。 デバイスを使用すると、 [「チュートリアル: Windows デバイスでの Workplace Join](Walkthrough--Workplace-Join-with-a-Windows-Device.md)」でアクセスしたのと同じ会社の web アプリケーションにアクセスできます。


## <a name="join-an-ios-device-with-workplace-join"></a>ワークプレース ジョインによる iOS デバイスの参加

> [!IMPORTANT]
> オンプレミスの DRS を構成するとき、ワークプレース ジョインを正常に完了するには、「 [Step 2: Configure the federation server (ADFS1) with Device Registration Service](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_4)」で Active Directory フェデレーション サービス (AD FS) の構成に使用した SSL (Secure Socket Layer) 証明書を iOS デバイスで信頼する必要があります。
> 
> -   AD FS の SSL 証明書がテスト用の証明機関 (CA) から発行されたものである場合、その証明機関の証明書を iOS デバイスにインストールする必要があります。
> -   証明機関の証明書が Web サイトに公開されている場合、iOS デバイスから Web サイトを参照して証明書をインストールできます。

ここでは、デバイスを職場に参加させます。

#### <a name="to-join-an-ios-device-to-a-workplace"></a>iOS デバイスを職場に参加させるには

1. -   **Azure Active Directory Device Registration サービスが構成済みの DRS である場合:** Apple Safari を開き、iOS デバイスの Azure Active Directory Device Registration service Over Air Profile エンドポイントに移動します。 <`https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/<yourdomainname` > <`yourdomainname`> で構成したドメイン名です。 たとえば、ドメイン名が contoso.com の場合、URL は次のようになります。`https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/contoso.com`

   -   **オンプレミスの drs が構成済みの drs**である場合: Apple Safari を開いて、iOS デバイスのデバイス登録サービス (DRS) を介して無線プロファイルのエンドポイントに移動し `https://adf1s.contoso.com/enrollmentserver/otaprofile`

   ユーザーにこの URL を伝えるには多くの方法があります。 推奨される方法の 1 つは、AD FS のカスタム アプリケーション アクセス拒否メッセージでこの URL を発行するというものです。 これについては、「 [アプリケーション アクセス ポリシーと、カスタム アクセス拒否メッセージを作成します](https://docs.microsoft.com/azure/active-directory/active-directory-device-registration-on-premises-setup#create-an-application-access-policy-and-custom-access-denied-message)」セクションを参照してください。

2. 会社のドメインアカウント ( <strong>roberth@contoso.com</strong>とパスワード: <strong>P@ssword</strong>) を使用して、web ページにログオンします。

3. プロファイルのインストールを求められます。 **[プロファイルのインストール]** 画面で、 **[インストール]** をクリックします。

4. プロファイルのインストール確認メッセージが表示されたら、 **[今すぐインストール]** をクリックします。

5. デバイスのロック解除にパスコードが必要な場合は、パスコードの入力を求められます。

6. プロファイルのインストールが完了すると、 **[インストール完了]** 画面が表示されます。 **[完了]** をクリックします。

   Safari に戻ります。 Safari を閉じることができる旨のメッセージが表示されます。

> [!TIP]
> ワークプレース ジョイン プロファイルを表示または削除するには、iOS デバイスで **[設定]** アイコンをクリックし、 **[一般]** 、 **[プロファイル]** の順にクリックします。

## <a name="see-also"></a>参照


- [任意のデバイスからの職場への参加による業務用アプリケーション間の SSO とシームレスな 2 要素認証](Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)
- [Windows Server 2012 R2 で AD FS 用のラボ環境をセットアップする](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)
- [チュートリアル: Windows デバイスでの Workplace Join](Walkthrough--Workplace-Join-with-a-Windows-Device.md)



