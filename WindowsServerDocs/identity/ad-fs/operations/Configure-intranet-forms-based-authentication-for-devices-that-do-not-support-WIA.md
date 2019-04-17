---
ms.assetid: d562ef46-f240-48be-bbd4-fd88fc6bbbdc
title: "WIA をサポートしないデバイス用のイントラネット フォーム ベース認証を構成します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: c78dc702cbff8eab487c6c077dfe57b0f0663342
ms.sourcegitcommit: 5012c078b410f59261edf0cc917393467243a5c7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/23/2018
---
# <a name="configuring-intranet-forms-based-authentication-for-devices-that-do-not-support-wia"></a>WIA をサポートしないデバイス用のイントラネット フォーム ベース認証を構成します。

>適用対象: Windows Server 2016、Windows Server 2012 R2

既定では、Windows 統合認証 (WIA) が有効になっている Active Directory フェデレーション サービス (AD FS) で Windows Server 2012 R2 ですべてのアプリケーションの認証用のブラウザーを使用する組織の内部ネットワーク (イントラネット) 内に発生する認証要求にします。 たとえば、Ws-federation を使用するブラウザー ベースのアプリケーションまたは OAuth プロトコルを使用する SAML プロトコルおよび豊富なアプリケーションをこれらできます。 WIA では、資格情報を手動で入力することがなく、アプリケーションへのシームレスなログオンを持つエンドユーザーを提供します。 ただし、一部のデバイスやブラウザー WIA をサポートできる、できないため、これらのデバイスからの認証要求が失敗します。 また、NTLM をネゴシエートする特定のブラウザーでのエクスペリエンスは望ましくありません。 このようなデバイスやブラウザーのフォーム ベースの認証にフォールバックすることをお勧めします。

Windows Server 2016 および Windows Server 2012 R2 の AD FS では、フォーム ベース認証への切り替えをサポートするユーザー エージェントの一覧を構成すること、管理者を提供します。 フォールバックは 2 つの構成によって可能になります。


- **WIASupportedUserAgentStrings**のプロパティ、`Set-ADFSProperties`内線番号
- **WindowsIntegratedFallbackEnabled**のプロパティ、 `Set-AdfsGlobalAuthenticationPolicy` commmandlet

**WIASupportedUserAgentStrings** WIA をサポートするユーザー エージェントを定義します。 AD FS は、ブラウザーまたはブラウザー コントロールでログインを実行するときに、ユーザー エージェント文字列を分析します。 かどうか、ユーザー エージェント文字列のコンポーネントと一致しないで構成されているユーザー エージェント文字列のコンポーネントのいずれか**WIASupportedUserAgentStrings**プロパティ、AD FS がフォールバックして提供する、フォーム ベース認証を提供する、 **WindowsIntegratedFallbackEnabled**フラグが True に設定します。

新しい AD FS のインストールでは既定では、作成したユーザー エージェント文字列の一致のセットがあります。 ただし、これらがあります有効期限切れのブラウザーやデバイスへの変更に基づいています。 特に、Windows デバイスでは、トークンでのマイナー バリエーションと同様のユーザー エージェント文字列があります。 次の Windows PowerShell の例では、シームレスな WIA をサポートしている現在の市場ではデバイスの現在のセットの最適なガイダンスを提供します。

    Set-AdfsProperties -WIASupportedUserAgents @("MSIE 6.0", "MSIE 7.0; Windows NT", "MSIE 8.0", "MSIE 9.0", "MSIE 10.0; Windows NT 6", "Windows NT 6.3; Trident/7.0", "Windows NT 6.3; Win64; x64; Trident/7.0", "Windows NT 6.3; WOW64; Trident/7.0", "Windows NT 6.2; Trident/7.0", "Windows NT 6.2; Win64; x64; Trident/7.0", "Windows NT 6.2; WOW64; Trident/7.0", "Windows NT 6.1; Trident/7.0", "Windows NT 6.1; Win64; x64; Trident/7.0", "Windows NT 6.1; WOW64; Trident/7.0", "MSIPC", "Windows Rights Management Client")

上記のコマンドは、AD FS は、WIA の次のユース ケースをのみカバーことを確認します。

ユーザー エージェント|使用例|
-----|-----|
MSIE 6.0|IE 6.0|
MSIE 7.0。Windows NT|IE 7、イントラネット ゾーンで IE します。 "Windows NT"フラグメントは、デスクトップ オペレーティング システムによって送信されます。|
MSIE 8.0|IE 8.0 (デバイスがない送信、ためより具体的にする必要があります)|
MSIE 9.0|IE 9.0 (デバイスがない送信より具体的ために必要ないいえ)|
MSIE 10.0 です。Windows NT 6|Windows XP およびデスクトップ オペレーティング システムの新しいバージョンの IE 10.0</br></br>送信するため、Windows Phone 8.0 デバイス] (優先順位の設定をモバイル) は除外されます。</br></br>ユーザー エージェント: mozilla/5.0 (互換性のあります。MSIE 10.0 です。Windows Phone 8.0 です。Trident/6.0 です。IEMobile/10.0 です。ARM です。タッチ操作です。NOKIA です。Lumia 920)|
Windows NT; 6.3Trident/7.0</br></br>Windows NT; 6.3Win64 です。x64 です。Trident/7.0</br></br>Windows NT; 6.3WOW64 です。Trident/7.0| Windows 8.1 デスクトップ オペレーティング システム、さまざまなプラットフォーム|
Windows NT 6.2 です。Trident/7.0</br></br>Windows NT 6.2 です。Win64 です。x64 です。Trident/7.0</br></br>Windows NT 6.2 です。WOW64 です。Trident/7.0|Windows 8 のデスクトップ オペレーティング システム、さまざまなプラットフォーム|
Windows NT 6.1;Trident/7.0</br></br>Windows NT 6.1;Win64 です。x64 です。Trident/7.0</br></br>Windows NT 6.1;WOW64 です。Trident/7.0|Windows 7 のデスクトップ オペレーティング システム プラットフォーム|
MSIPC| Microsoft Information Protection とクライアントの制御|
Windows Rights Management クライアント|Windows Rights Management クライアント|

WIASupportedUserAgents 文字列に記載されているもの以外のユーザー エージェントのフォーム ベース認証への切り替えを有効にするために、WindowsIntegratedFallbackEnabled フラグを true に設定します。

    Set-AdfsGlobalAuthenticationPolicy -WindowsIntegratedFallbackEnabled $true

また、イントラネットのフォーム ベースの認証が有効になっていることを確認します。

## <a name="configuring-wia-for-chrome"></a>Chrome の WIA を構成します。
WIA をサポートしている AD FS の構成には、Chrome、またはその他のユーザー エージェントを追加できます。 これにより、AD FS によって保護されたリソースにアクセスするときに、資格情報を手動で入力することがなくアプリケーションをシームレスにログオンします。 Chrome で WIA を有効にするのには、次の手順に従います。

Chrome の AD FS の構成のユーザー エージェント文字列を追加します。

    Set-AdfsProperties -WIASupportedUserAgents ((Get-ADFSProperties | Select -ExpandProperty WIASupportedUserAgents) + “Chrome”)
    
Chrome のユーザー エージェント文字列が、AD FS のプロパティで設定できるようになりましたことの確認します。

    Get-AdfsProperties | Select -ExpandProperty WIASupportedUserAgents

![認証を構成します。](media/Configure-intranet-forms-based-authentication-for-devices-that-do-not-support-WIA/chrome1.png) 

>[!NOTE]   
> 新しいブラウザーとデバイスがリリースされるは、それらのユーザー エージェントの機能を調整して、ブラウザーとデバイスを使用すると言わときに、ユーザーの認証のエクスペリエンスを最適化するために、それに応じて、AD FS 構成を更新することをお勧めします。 具体的にはお勧め再評価すること、 **WIASupportedUserAgents** WIA をサポート マトリックスを新しいデバイスまたはブラウザーの種類を追加するときに、AD FS で設定します。


