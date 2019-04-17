---
ms.assetid: a33bd54c-e6db-4b58-8264-c0f34bd8ba39
title: "チュートリアルの Android デバイスをワークプ レース ジョイン"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: cfe26947b6b0de28ea50367f82d52815fff8f323
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="walkthrough-workplace-join-to-an-android-device"></a>Android デバイスをワークプ レース ジョインのチュートリアル:

>適用対象: Windows Server 2016、Windows Server 2012 R2


## <a name="join-your-device-with-workplace-join"></a>ワークプ レース ジョインでデバイスを参加させる

> [!NOTE]
> Android のワークプ レース ジョインでは、Azure Active Directory Device Registration Service が必要です。 、条件付きのデバイス ポリシー内部設置型を強制するためには、デバイス オブジェクトの書き戻しオプションが有効でディレクトリ同期ツール (DirSync) を展開する必要があります。 現時点では、デバイス ライトバック Active Directory に Azure Active Directory からは、3 時間アップにかかることをがします。 そのため、ユーザーは、職場アカウントを作成した後、内部設置型の web アプリケーションにアクセスする 3 時間まで待機する必要があります。 サービスの Azure Active Directory Device Registration の展開の詳細についてを参照してください、 [Azure Active Directory デバイス登録サービスの概要](https://msdn.microsoft.com/library/azure/dn788908.aspx)

#### <a name="create-a-work-account-that-joins-your-device-with-workplace-join"></a>ワークプ レース ジョインを使用してデバイスを参加させる職場アカウントを作成します。

1.  デバイスをワークプ レース ジョインで結合する、職場アカウントを作成するのには、デバイス上の Azure Authenticator アプリケーションをインストールする必要があります。 次の URL は、Android デバイスを Azure authenticator アプリをインストールし、職場アカウントを追加する方法手順が記載されています。 職場アカウントは、Android デバイスを信頼されたデバイスにし、デバイス上のアプリケーションへのシングル サインオン (SSO) を提供します。 IT 管理者が推奨されている web アプリケーションにアクセスし、最新の基幹業務アプリケーションを信頼できるデバイスを使用できます。 詳細については、次を参照してください。 [Android 用の Azure Authenticator](https://docs.microsoft.com/azure/multi-factor-authentication/end-user/microsoft-authenticator-app-how-to)します。

## <a name="see-also"></a>参照してください。
[任意のデバイスからの SSO とシームレスな 2 つ目 Factor Authentication Across Company Applications 職場への参加](Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)
[Azure Active Directory Device Registration Service を使用して内部設置型条件付きアクセスのセットアップ](https://docs.microsoft.com/azure/active-directory/active-directory-device-registration-on-premises-setup)


