---
title: Windows Server (バージョン 1709 以降) で削除された機能と置換が計画されている機能
description: リリースで削除済みまたは削除予定の機能です。
ms.prod: windows-server-threshold
ms.technology: server-general
ms.topic: article
ms.date: 08/22/2019
author: jasongerend
ms.author: jgerend
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: b4303d05a87fe06e84df0cc55e2c1af8b34047e6
ms.sourcegitcommit: 6f8993e2180c4d3c177e3e1934d378959396b935
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/23/2019
ms.locfileid: "70000631"
---
# <a name="features-removed-or-planned-for-replacement-starting-with-windows-server-version-1709"></a>Windows Server バージョン 1709 以降で削除された機能と置換が計画されている機能

>適用先:Windows Server バージョン 1709

次の一覧に、Windows Server バージョン 1709 の機能のうち、このリリースで製品から削除された機能および今後のリリースで置換が検討されるようになった機能を示します。 商用環境でオペレーティング システムを更新する IT 担当者を対象としています。 **この一覧は、今後のリリースで変更される可能性があります。また、影響を受ける機能でこの一覧に含まれていないものもあります。** 

> [!TIP]
> - [Windows Insider プログラム](https://insider.windows.com)に参加することで Windows Server ビルドにいち早くアクセスできます。これは、機能の変更をテストするための最適な方法です。
> - その他のリリースに関する質問がある場合 「[Windows Server で削除された機能と置換が計画されている機能](../get-started-19/removed-features.md)」をご覧ください。

## <a name="features-removed-from-windows-server-version-1709"></a>Windows Server バージョン 1709 から削除された機能

Windows Server バージョン 1709 には、Windows Server 2016 と同じ機能が含まれています。 ただし、このリリースでは、Windows Server 2016 とは異なるインストール オプションが提供されます。

- 半期チャネルのリリースでは、Windows Server バージョン 1709 は Server Core インストール オプションのみを提供します。 詳細については、[サービス チャネルの比較](../get-started-19/servicing-channels-19.md)に関するページをご覧ください。
- このリリース以降、Nano Server はインストール可能なホスト オペレーティング システムとして使用できません。 代わりに、Nano Server は、コンテナー オペレーティング システムとして使用できます。 「[Windows Server バージョン 1709 で Nano Server に加えられる変更](nano-in-semi-annual-channel.md)」をご覧ください。
- このリリース以降、サーバー メッセージ ブロック (SMB) バージョン 1 は既定でインストールされません。 詳細については、「[SMBv1 is not installed by default in Windows 10 Fall Creators Update and Windows Server, version 1709 and later versions (Windows 10 Fall Creators Update および Windows Server バージョン 1709 以降では SMBv1 は既定でインストールされない)](https://support.microsoft.com/help/4034314/smbv1-is-not-installed-by-default-in-windows)」をご覧ください。


## <a name="features-being-considered-for-replacement-starting-with-subsequent-releases"></a>今後のリリースで置換が検討されている機能

以下の機能は、Windows Server バージョン 1709 以降のリリースでは置換が検討されています。 最終的には、インストールされる製品イメージから完全に削除され、他の機能によって置き換えられます (または他のソースからインストール可能になります)。このリリースでは引き続き使用できますが、特定の機能が削除されている場合があります。 これらの機能に依存するアプリケーション、コード、使用法については、別の方法の使用や将来的な置き換えを今から計画する必要があります。

提案されているこれらの機能の置換について共有する必要があるフィードバックがある場合は、[フィードバック Hub アプリ](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app)を使用できます。 このアプリは、Windows 10 で実行している場合でも、Windows Server 製品 (とドキュメント) に関するフィードバックの送信に使用することもできます。

### <a name="iis-6-management-compatibility"></a>IIS 6 管理互換
置換が検討されている特定の機能は次のとおりです。

- IIS 6 メタベース互換 (Web メタベース)
- IIS 6 管理コンソール (Web-Lgcy-Mgmt-Console)
- IIS 6 スクリプトのツール (Web-Lgcy-Scripting)
- IIS 6 WMI 互換 (Web-WMI)

IIS 6 メタベース互換 (IIS 6 ベースのメタベース スクリプトと IIS 7 以降のバージョンで使用されるファイル ベースの構成の間でエミュレーション レイヤーとして機能する) の代わりに、Microsoft.Web.Administration 名前空間などのツールを使用することによって、IIS ファイル ベースの構成を直接ターゲットにする管理スクリプトの移行を開始する必要があります。

また、IIS 6.0 またはそれ以前のバージョンから移行を開始し、最新バージョンの IIS に移行する必要があります。これは、Windows Server の最新のリリースで常に利用することができます。


### <a name="iis-digest-authentication"></a>IIS のダイジェスト認証
この認証方法は置き換えられる予定です。 代わりに、クライアント証明書マッピング ([1 対 1 のクライアント証明書マッピングの構成に関するトピック](https://docs.microsoft.com/iis/manage/configuring-security/configuring-one-to-one-client-certificate-mappings)を参照) や Windows 認証 ([アプリケーションの設定に関するトピック](https://docs.microsoft.com/iis-administration/configuration/appsettings.json)を参照) など、他の認証方法を使用する必要があります。

### <a name="internet-storage-name-service-isns"></a>インターネット記憶域ネーム サービス (iSNS)
iSNS は置き換えが検討されています。 サーバー メッセージ ブロック (SMB) 機能は、基本的に同じ機能と追加機能を提供しています。 この機能の背景情報については、「[サーバー メッセージ ブロックの概要](https://technet.microsoft.com/library/hh831795(v=ws.11).aspx)」を参照してください。

### <a name="rsaaes-encryption-for-iis"></a>IIS 用の RSA/AES 暗号化 
この暗号化方法は置き換えが検討されています。より優れた Cryptography API:Next Generation (CNG) による方法が既に利用できるためです。 CNG 暗号化について詳しくは、[CNG の概要に関するトピック](https://msdn.microsoft.com/library/windows/desktop/aa375276(v=vs.85).aspx)をご覧ください。

### <a name="windows-powershell-20"></a>Windows PowerShell 2.0
この初期バージョンの Windows PowerShell は、いくつかのより新しいバージョンで置き換えられています。 最適な機能とパフォーマンスを実現するには、Windows PowerShell 5.0 以降に移行してください。 詳細については、[PowerShell ドキュメント](https://docs.microsoft.com/powershell/index?view=powershell-5.1)をご覧ください。

