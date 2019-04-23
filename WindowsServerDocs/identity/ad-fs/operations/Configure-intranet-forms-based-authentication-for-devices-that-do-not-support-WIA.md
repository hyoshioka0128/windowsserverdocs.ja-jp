---
ms.assetid: d562ef46-f240-48be-bbd4-fd88fc6bbbdc
title: WIA をサポートしないデバイス用のイントラネット フォーム ベース認証を構成します。
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: cddc5d890114dec7e0053b16701db6f03c3cbbdf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889853"
---
# <a name="configuring-intranet-forms-based-authentication-for-devices-that-do-not-support-wia"></a>WIA をサポートしないデバイス用のイントラネット フォーム ベース認証を構成します。

>適用先:Windows Server 2016、Windows Server 2012 R2

既定では、Windows 統合認証 (WIA) が Active Directory フェデレーション サービス (AD FS) で Windows Server 2012 R2 を使用するアプリケーションに組織の内部ネットワーク (イントラネット) 内で発生する認証要求で有効にします。その認証のためのブラウザーです。 たとえば、Ws-federation を使用するブラウザー ベースのアプリケーションまたは OAuth プロトコルを使用する SAML のプロトコルとリッチ アプリケーションがあるこれらができます。 WIA では、自分の資格情報を手動で入力しなくても、アプリケーションへのシームレスなログオンを持つエンドユーザーを提供します。 ただし、一部のデバイスとブラウザーに WIA をサポートしていることはできませんし、その結果、これらのデバイスからの認証要求が失敗します。 また、NTLM をネゴシエートする特定のブラウザーでのエクスペリエンスは望ましくありません。 このようなデバイスおよびブラウザーのフォーム ベースの認証にフォールバックすることをお勧めします。

Windows Server 2016 および Windows Server 2012 R2 で AD FS では、フォーム ベースの認証にフォールバックをサポートするユーザー エージェントの一覧を構成することができます、管理者が提供します。 フォールバックは 2 つの構成によって実現されます。


- **WIASupportedUserAgentStrings**のプロパティ、`Set-ADFSProperties`コマンドレット
- **WindowsIntegratedFallbackEnabled**のプロパティ、`Set-AdfsGlobalAuthenticationPolicy`コマンドレット

**WIASupportedUserAgentStrings** WIA をサポートするユーザー エージェントを定義します。 AD FS は、ブラウザーまたはブラウザー コントロールでのログインを実行するときに、ユーザー エージェント文字列を分析します。 ユーザー エージェント文字列の要素に一致しないかどうかのコンポーネントで構成されているユーザー エージェント文字列の**WIASupportedUserAgentStrings**プロパティ、AD FS がフォールバックしてフォーム ベースの認証を提供します。されるとき、 **WindowsIntegratedFallbackEnabled**フラグが True に設定します。

新しい AD FS のインストールでは既定では、作成されたユーザー エージェント文字列の一致のセットがあります。 ただし、これらがあります期限切れのブラウザーおよびデバイスへの変更に基づきます。 特に、Windows デバイスでは、トークンにわずかな違いを類似のユーザー エージェント文字列があります。 次の Windows PowerShell の例は、シームレスな WIA をサポートする今日の市場にあるデバイスの現在のセットの最善のガイダンスを提供します。

    Set-AdfsProperties -WIASupportedUserAgents @("MSIE 6.0", "MSIE 7.0; Windows NT", "MSIE 8.0", "MSIE 9.0", "MSIE 10.0; Windows NT 6", "Windows NT 6.3; Trident/7.0", "Windows NT 6.3; Win64; x64; Trident/7.0", "Windows NT 6.3; WOW64; Trident/7.0", "Windows NT 6.2; Trident/7.0", "Windows NT 6.2; Win64; x64; Trident/7.0", "Windows NT 6.2; WOW64; Trident/7.0", "Windows NT 6.1; Trident/7.0", "Windows NT 6.1; Win64; x64; Trident/7.0", "Windows NT 6.1; WOW64; Trident/7.0", "MSIPC", "Windows Rights Management Client")

上記のコマンドは AD FS は、WIA の次のユース ケースをのみ説明を確認します。

ユーザー エージェント|使用事例|
-----|-----|
MSIE 6.0|IE 6.0|
MSIE 7.0; Windows NT|IE 7、IE イントラネット ゾーンでします。 デスクトップ オペレーティング システムでは、"Windows NT"フラグメントが送信されます。|
MSIE 8.0|IE 8.0 (デバイスがありませんこのを送信するより具体的にするため必要があります)|
MSIE 9.0|IE の 9.0 (デバイスがありません送信、詳細を確認する必要がありません)|
MSIE 10.0; Windows NT 6|Windows XP およびデスクトップ オペレーティング システムの新しいバージョンの IE 10.0</br></br>送信するため、(使用してモバイル設定を優先) Windows Phone 8.0 デバイスは除外されます。</br></br>ユーザー エージェント:Mozilla/5.0 (互換性があります。MSIE 10.0 です。Windows Phone 8.0。Trident/6.0。発行元の IEMobile/10.0 です。ARM;タッチです。NOKIA;Lumia 920)|
Windows NT 6.3;Trident または 7.0</br></br>Windows NT 6.3;Win64;x64。Trident または 7.0</br></br>Windows NT 6.3; WOW64; Trident/7.0| Windows 8.1 デスクトップ オペレーティング システム、さまざまなプラットフォーム|
Windows NT 6.2;Trident または 7.0</br></br>Windows NT 6.2;Win64;x64。Trident または 7.0</br></br>Windows NT 6.2; WOW64; Trident/7.0|Windows 8 デスクトップ オペレーティング システム、さまざまなプラットフォーム|
Windows NT 6.1;Trident または 7.0</br></br>Windows NT 6.1;Win64;x64。Trident または 7.0</br></br>Windows NT 6.1;これは、WOW64Trident または 7.0|Windows 7 デスクトップ オペレーティング システム、さまざまなプラットフォーム|
MSIPC を右クリックし| Microsoft Information Protection とクライアントの制御|
Windows Rights Management クライアント|Windows Rights Management クライアント|

WIASupportedUserAgents 文字列に示されている以外のユーザー エージェントのフォーム ベース認証へのフォールバックを有効にするには、WindowsIntegratedFallbackEnabled フラグを true に設定します。

    Set-AdfsGlobalAuthenticationPolicy -WindowsIntegratedFallbackEnabled $true

また、イントラネットのフォーム ベース認証が有効になっていることを確認します。

## <a name="configuring-wia-for-chrome"></a>Chrome WIA を構成します。
WIA をサポートする AD FS の構成には、Chrome またはその他のユーザー エージェントを追加できます。 これにより、AD FS によって保護されたリソースにアクセスするときに、資格情報を手動で入力しなくてもアプリケーションにシームレスにログオンします。 Chrome で WIA を有効にするのには、次の手順に従います。

AD FS の構成で Chrome のユーザー エージェント文字列を追加します。

    Set-AdfsProperties -WIASupportedUserAgents ((Get-ADFSProperties | Select -ExpandProperty WIASupportedUserAgents) + “Chrome”)
    
Chrome のユーザー エージェント文字列は、AD FS のプロパティで設定されたことを確認します。

    Get-AdfsProperties | Select -ExpandProperty WIASupportedUserAgents

![認証を構成します。](media/Configure-intranet-forms-based-authentication-for-devices-that-do-not-support-WIA/chrome1.png) 

>[!NOTE]   
> 新しいブラウザーとデバイスがリリースされるは、ユーザー エージェントの機能を調整し、ブラウザーとデバイスを使用して言ったときに、ユーザーの認証エクスペリエンスを最適化するために、AD FS の構成を適宜更新することをお勧めします。 具体的にはお勧め再評価すること、 **WIASupportedUserAgents** WIA のサポート マトリックスに、新しいデバイスまたはブラウザーの種類を追加するときに、AD FS で設定します。


