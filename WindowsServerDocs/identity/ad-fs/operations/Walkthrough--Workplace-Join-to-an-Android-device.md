---
ms.assetid: a33bd54c-e6db-4b58-8264-c0f34bd8ba39
title: チュートリアル - Android デバイスをワークプ レース ジョイン
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 73dbe4d62d460f9487467c7d4198d62b3b6af539
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66188931"
---
# <a name="walkthrough-workplace-join-to-an-android-device"></a>チュートリアル: Android デバイスをワークプ レース ジョイン



## <a name="join-your-device-with-workplace-join"></a>ワークプレース ジョインによるデバイスの参加

> [!NOTE]
> Android のワークプ レース ジョインでは、Azure Active Directory Device Registration Service が必要です。 条件付きのデバイス ポリシーはオンプレミスでを適用するためにデバイス オブジェクトの書き戻しオプションを有効にディレクトリ同期ツール (DirSync) をデプロイする必要があります。 現時点では、デバイスの書き戻しを Active Directory に Azure Active Directory から最新の状態に 3 時間かかります。 そのため、ユーザーは、職場アカウントを作成した後、オンプレミスの web アプリケーションへのアクセスに 3 時間まで待機する必要があります。 Azure Active Directory Device Registration の展開の詳細については、サービスを参照してください、 [Azure Active Directory Device Registration サービスの概要](https://msdn.microsoft.com/library/azure/dn788908.aspx)

#### <a name="create-a-work-account-that-joins-your-device-with-workplace-join"></a>ワークプ レース ジョインを使用してデバイスを参加させる作業アカウントを作成します。

1.  デバイスをワークプ レース ジョインで連結された職場アカウントを作成するため、デバイスに Azure Authenticator アプリケーションをインストールする必要があります。 次の URL は、Android デバイスでの Azure authenticator アプリをインストールし、職場アカウントを追加する方法手順が記載されています。 職場アカウントでは、Android デバイスを信頼済みデバイスにし、デバイス上のアプリケーションにシングル サインオン (SSO) を提供します。 推奨に従って、IT 管理者は、web アプリケーションにアクセスし、最新の基幹業務アプリケーションを信頼済みデバイスを使用できます。 詳細については、次を参照してください。 [Android 用の Azure Authenticator](https://docs.microsoft.com/azure/multi-factor-authentication/end-user/microsoft-authenticator-app-how-to)します。

## <a name="see-also"></a>関連項目
[任意のデバイスからの SSO とシームレスな 2 つ目 Factor Authentication Across Company Applications ワークプ レースへの参加](Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)
[Azure Active Directory Device Registration Service を使用して、オンプレミス条件付きアクセスの設定](https://docs.microsoft.com/azure/active-directory/active-directory-device-registration-on-premises-setup)


