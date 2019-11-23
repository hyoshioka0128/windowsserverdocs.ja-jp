---
ms.assetid: a33bd54c-e6db-4b58-8264-c0f34bd8ba39
title: チュートリアル-Android デバイスへの Workplace Join
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: c021e8b67963df4f885059c75eff5e94d6dcdafb
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407470"
---
# <a name="walkthrough-workplace-join-to-an-android-device"></a>チュートリアル: Android デバイスへの Workplace Join



## <a name="join-your-device-with-workplace-join"></a>ワークプレース ジョインによるデバイスの参加

> [!NOTE]
> Android workplace join には Azure Active Directory Device Registration サービスが必要です。 条件付きデバイスポリシーをオンプレミスで適用するには、ディレクトリ同期ツール (DirSync) をデバイスオブジェクトの書き戻しオプションが有効になっている状態で展開する必要があります。 現時点では、Azure Active Directory から Active Directory へのデバイスの書き戻しには最大3時間かかることがあります。 そのため、ユーザーは職場アカウントを作成した後、オンプレミスの web アプリケーションにアクセスするまで3時間待つ必要があります。 Azure Active Directory Device Registration サービスの展開の詳細については、「」、「 [Azure Active Directory Device Registration サービスの概要](https://msdn.microsoft.com/library/azure/dn788908.aspx)」を参照してください。

#### <a name="create-a-work-account-that-joins-your-device-with-workplace-join"></a>ワークプレースジョインを使用してデバイスに参加する職場アカウントを作成する

1.  デバイスにワークプレースジョインを参加させる職場アカウントを作成するには、デバイスに Azure Authenticator アプリケーションをインストールする必要があります。 次の URL では、Android デバイスに Azure authenticator アプリをインストールし、仕事用アカウントを追加する方法について説明しています。 職場アカウントによって、Android デバイスが信頼されたデバイスになり、デバイス上のアプリケーションにシングルサインオン (SSO) が提供されます。 IT 管理者が推奨するように、信頼されたデバイスを使用して、web アプリケーションや最新の基幹業務アプリケーションにアクセスできます。 詳細については、「 [Android 用の Azure Authenticator](https://docs.microsoft.com/azure/multi-factor-authentication/end-user/microsoft-authenticator-app-how-to)」を参照してください。

## <a name="see-also"></a>参照
[任意のデバイスからの職場への参加による企業アプリケーション間の SSO とシームレスな2要素認証](Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)
[Azure Active Directory Device Registration サービスを使用したオンプレミスの条件付きアクセスの設定](https://docs.microsoft.com/azure/active-directory/active-directory-device-registration-on-premises-setup)


