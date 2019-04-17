---
ms.assetid: 299e4fb9-8f1a-4275-ad7d-dad4f1594657
title: チュートリアルの iOS デバイスのワークプ レース ジョイン
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 0a8643bab913dfec07c6bbea0c068e1240f16c5b
ms.sourcegitcommit: a2260c96b0e49519d180c7382b921ce8ddb053fe
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/04/2018
---
# <a name="walkthrough-workplace-join-with-an-ios-device"></a>チュートリアル: iOS デバイスでワークプ レースに参加します。

>Windows Server 2012 R2 の適用対象:

このトピックでは、ワークプ レース ジョイン、iOS デバイスでします。 手順を完了する必要があります、 [Windows Server 2012 R2 の AD FS のラボ環境を設定](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)セクション前に、このチュートリアルを試すことができます。 アクセスしたのと同じ会社の web アプリケーションにアクセスするデバイスを使用できる[チュートリアル: Windows デバイスでの社内参加](Walkthrough--Workplace-Join-with-a-Windows-Device.md)します。

## <a name="join-an-ios-device-with-workplace-join"></a>ワークプ レース ジョインで iOS デバイスを参加させる

> [!IMPORTANT]
> IOS デバイスでの Active Directory フェデレーション サービス (AD FS) の構成に使用した、Secure Socket Layer (SSL) 証明書を信頼する必要があります、オンプレミスの DRS が構成されているときに[手順 2: デバイス登録サービスによるフェデレーション サーバー (ADFS1) を構成する](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md#BKMK_4)、ワークプ レース ジョインを正常にします。
> 
> -   場合は、AD FS の SSL 証明書は、テスト証明機関 (CA) から発行された、iOS デバイスに証明機関の証明書をインストールする必要があります。
> -   証明機関の証明書が、web サイトで公開されている場合、iOS デバイスから web サイトを参照して証明書をインストールします。

このデモでは、ワークプ レースをデバイスを参加させます。

#### <a name="to-join-an-ios-device-to-a-workplace"></a>IOS デバイスを職場に参加させる

1.  -   **ときに、Azure Active Directory Device Registration サービスは、構成済みの DRS:** Apple Safari を開いて、iOS デバイス用の Azure Active Directory Device Registration サービス Over-the-Air プロファイル エンドポイントに移動し、<`https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/<yourdomainname` > で <`yourdomainname`> は Azure Active Directory で構成したドメイン名です。 たとえば、ドメイン名が contoso.com の場合は、URL は次のようになります。 `https://enterpriseregistration.windows.net/enrollmentserver/otaprofile/contoso.com`

    -   **オンプレミスの DRS が構成済みの DRS がとき**: Apple Safari を開いて、iOS デバイス用のデバイス登録サービス (DRS) Over-the-Air プロファイル エンドポイントに移動`https://adf1s.contoso.com/enrollmentserver/otaprofile`

    この URL をユーザーに通信するためにさまざまな方法があります。 推奨される方法の 1 つは、カスタム アプリケーション アクセスでこの URL を発行する AD FS でのメッセージが拒否されました。 これについては、今後予定されているセクションで説明:[アプリケーション アクセス ポリシーとカスタム アクセス拒否メッセージを作成](https://docs.microsoft.com/azure/active-directory/active-directory-device-registration-on-premises-setup#create-an-application-access-policy-and-custom-access-denied-message)

2.  会社のドメイン アカウントを使用して web ページにログオンします。 ** roberth@contoso.com **とパスワード: ** P@ssword**します。

3.  プロファイルのインストールを求められます。 **プロファイルのインストール**画面で、[**インストール**します。

4.  プロファイルのインストールを確認するメッセージが表示されたら、] をクリックして**今すぐインストール**します。

5.  お客様のデバイスには、デバイスのロックを解除するのに PIN が必要とする場合、PIN の入力を求められます。

6.  表示された場合、プロファイルのインストールが完了したら、**プロファイルがインストールされている**画面です。 をクリックして**完了**します。

    Safari に戻ります。 閉じるか、safari を通知するメッセージが表示されます。

> [!TIP]
> 表示したり、ワークプ レース ジョイン プロファイルを削除するを参照して**設定**、] をクリックして**全般**、] をクリックし、**プロファイル**、iOS デバイスでします。

## <a name="see-also"></a>参照してください。


- [Join to Workplace from 任意のデバイス用の SSO とシームレスな 2 要素認証を企業アプリケーション間で](Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)
- [Windows Server 2012 R2 の AD FS のラボ環境を設定します。](../../ad-fs/deployment/Set-up-the-lab-environment-for-AD-FS-in-Windows-Server-2012-R2.md)
- [Windows デバイスのチュートリアル: 職場への参加](Walkthrough--Workplace-Join-with-a-Windows-Device.md)



