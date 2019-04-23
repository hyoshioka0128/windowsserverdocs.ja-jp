---
ms.assetid: 299e4fb9-8f1a-4275-ad7d-dad4f1594657
title: チュートリアル - iOS デバイスのワークプ レース ジョイン
description: ''
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 10/18/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: c9c66b5bbe5fff83010859abe6ea4759d5bc4be0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59853633"
---
# <a name="walkthrough-workplace-join-with-an-ios-device"></a>チュートリアル: IOS デバイスのワークプ レース ジョイン

>適用先:Windows Server 2012 R2

> [!IMPORTANT] 
> このメソッドは、オンプレミスの顧客のみ完全に関連します。 ハイブリッドまたはクラウドのみのお客様は、自分の iOS デバイスを登録するのにこのメソッドを使用する必要があります。 オンプレミスの顧客がクラウドに移行することと、このメソッドに互換性がありません。 デバイスの登録を解除し、クラウドに登録されている必要があります。 

このトピックでは、iOS デバイスでのワークプレース ジョインについて説明します。 手順を完了する必要があります、 [Windows Server 2012 R2 で AD FS のラボ環境をセットアップ](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)セクションの前に、このチュートリアルを試すことができます。 デバイスを使用するには、同じ会社の web アプリケーションにアクセスする[チュートリアル。Windows デバイスのワークプ レース ジョイン](Walkthrough--Workplace-Join-with-a-Windows-Device.md)します。


## <a name="join-an-ios-device-with-workplace-join"></a>ワークプレース ジョインによる iOS デバイスの参加

> [!IMPORTANT]
> IOS デバイスがで Active Directory フェデレーション サービス (AD FS) を構成するために使用した Secure Socket Layer (SSL) 証明書を信頼する必要があります、オンプレミスの DRS が構成されている[手順 2。フェデレーション サーバー (ADFS1) with Device Registration Service に構成する](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_4)、ワークプ レース ジョインが成功します。
> 
> -   AD FS の SSL 証明書がテスト用の証明機関 (CA) から発行されたものである場合、その証明機関の証明書を iOS デバイスにインストールする必要があります。
> -   証明機関の証明書が Web サイトに公開されている場合、iOS デバイスから Web サイトを参照して証明書をインストールできます。

ここでは、デバイスを職場に参加させます。

#### <a name="to-join-an-ios-device-to-a-workplace"></a>iOS デバイスを職場に参加させるには

1.  -   **Azure Active Directory Device Registration サービスが構成済みの DRS である場合:** Apple Safari を開いて、iOS デバイス用の Azure Active Directory Device Registration サービス Over-the-Air プロファイル エンドポイントに移動します <`https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/<yourdomainname` > ここ <`yourdomainname`> Azure Active Directory で構成したドメイン名です。 たとえば、ドメイン名が contoso.com の場合、URL は次のようになります。`https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/contoso.com`

    -   **オンプレミスの DRS が構成済みの DRS である場合**:Apple Safari を開いて、iOS デバイス用のデバイス登録サービス (DRS) Over-the-Air プロファイル エンドポイントに移動します `https://adf1s.contoso.com/enrollmentserver/otaprofile`

    ユーザーにこの URL を伝えるには多くの方法があります。 推奨される方法の 1 つは、AD FS のカスタム アプリケーション アクセス拒否メッセージでこの URL を発行するというものです。 これについては、次のセクションで説明します。[アプリケーションのアクセス ポリシーとカスタム アクセス拒否メッセージを作成します。](https://docs.microsoft.com/azure/active-directory/active-directory-device-registration-on-premises-setup#create-an-application-access-policy-and-custom-access-denied-message)

2.  会社のドメイン アカウントを使用して web ページにログオン: **roberth@contoso.com**とパスワード:  **P@ssword**します。

3.  プロファイルのインストールを求められます。 **[プロファイルのインストール]** 画面で、 **[インストール]** をクリックします。

4.  プロファイルのインストール確認メッセージが表示されたら、 **[今すぐインストール]** をクリックします。

5.  デバイスのロック解除にパスコードが必要な場合は、パスコードの入力を求められます。

6.  プロファイルのインストールが完了すると、 **[インストール完了]** 画面が表示されます。 **[完了]** をクリックします。

    Safari に戻ります。 Safari を閉じることができる旨のメッセージが表示されます。

> [!TIP]
> ワークプレース ジョイン プロファイルを表示または削除するには、iOS デバイスで **[設定]** アイコンをクリックし、 **[一般]**、 **[プロファイル]** の順にクリックします。

## <a name="see-also"></a>関連項目


- [SSO およびシームレスな第 2 の任意のデバイスから社内への参加要素用アプリケーション間での認証](Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)
- [Windows Server 2012 R2 で AD FS のラボ環境のセットアップします。](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)
- [チュートリアル: Windows デバイスのワークプ レース ジョイン](Walkthrough--Workplace-Join-with-a-Windows-Device.md)



