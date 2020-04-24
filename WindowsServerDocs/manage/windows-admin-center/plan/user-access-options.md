---
title: Windows Admin Center でのユーザー アクセス オプション
description: Windows Admin Center でのユーザー アクセス オプションと ID プロバイダー (Project Honolulu)
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 03/07/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 084cdae0bf8ca0eb3aff1f4679d30978b860efef
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "71356916"
---
# <a name="user-access-options-with-windows-admin-center"></a>Windows Admin Center でのユーザー アクセス オプション

>適用先:Windows Admin Center、Windows Admin Center Preview

Windows Server に展開されている場合、Windows Admin Center ではサーバー環境を一元的に管理することができます。 Windows Admin Center へのアクセスを制御することにより、管理環境のセキュリティを向上できます。

## <a name="gateway-access-roles"></a>ゲートウェイ アクセスのロール

Windows Admin Center では、ゲートウェイ サービスにアクセスするための 2 つのロール (ゲートウェイ ユーザーとゲートウェイ管理者) が定義されています。

> [!NOTE]
> ゲートウェイへのアクセスは、そのゲートウェイが参照できるターゲット サーバーへのアクセスを意味するものではありません。 ターゲット サーバーを管理するには、ユーザーは、ターゲット サーバーの管理者特権を持つ資格情報を使用して接続する必要があります。

**ゲートウェイ ユーザー**は、Windows Admin Center ゲートウェイ サービスに接続し、そのゲートウェイを介してサーバーを管理できますが、ゲートウェイに対する認証に使用されるアクセス許可や認証メカニズムを変更することはできません。

**ゲートウェイ管理者**は、誰がゲートウェイにアクセスできるかと、ゲートウェイにアクセスするユーザーの認証方法を構成できます。

>[!NOTE]
> Windows Admin Center にアクセス グループが定義されていない場合、ロールにはゲートウェイ サーバーへの Windows アカウントのアクセス権が反映されます。 

[Windows Admin Center でゲートウェイ ユーザーと管理者のアクセス権を構成します](../configure/user-access-control.md)。

## <a name="identity-provider-options"></a>ID プロバイダーのオプション

ゲートウェイ管理者は、次のいずれかを選択できます。

 - [Active Directory またはローカル コンピューターのグループ](../configure/user-access-control.md#active-directory-or-local-machine-groups)
 - [Windows Admin Center の ID プロバイダーとしての Azure Active Directory](../configure/user-access-control.md#azure-active-directory)


### <a name="smartcard-authentication"></a>スマートカード認証

Active Directory またはローカル マシンのグループを ID プロバイダーとして使用する場合、Windows Admin Center にアクセスするユーザーに対し、追加のスマートカードベースのセキュリティ グループのメンバーになるよう要求することによって、スマートカード認証を実施できます。 [Windows Admin Center でスマートカード認証を構成します](../configure/user-access-control.md#active-directory-or-local-machine-groups)。

### <a name="conditional-access-and-multi-factor-authentication"></a>条件付きアクセスと多要素認証

ゲートウェイに対して Azure AD 認証を要求することにより、Azure AD で提供されている条件付きアクセスや多要素認証などの追加のセキュリティ機能を利用できます。 [Azure Active Directory を使用した条件付きアクセスの構成の詳細については、こちらを参照してください。](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal-get-started)

## <a name="role-based-access-control"></a>ロール基準のアクセス制御

既定では、ユーザーは、Windows Admin Center を使用して管理するマシンに対して完全なローカル管理者特権を必要とします。
これにより、マシンへのリモート接続が可能となり、システム設定を表示および変更するために必要なアクセス許可を持つことができます。
ただし、ユーザーによっては、ジョブを実行するためにマシンへの無制限のアクセス権を必要としない場合があります。
Windows Admin Center で**ロールベースのアクセス制御**を使用すると、そのようなユーザーに対して、完全なローカル管理者としてのアクセス権ではなく、マシンへの制限付きアクセス権を付与できます。

Windows Admin Center でのロールベースのアクセス制御は、PowerShell の [Just Enough Administration](https://aka.ms/jeadocs) エンドポイントを使用して各管理対象サーバーを構成することにより機能します。
このエンドポイントでは、各ロールが管理できるシステムの側面や、ロールに割り当てられているユーザーなど、ロール定義を行います。
ユーザーが制限付きエンドポイントに接続すると、代わりにシステムを管理するための一時的なローカル管理者アカウントが作成されます。
これにより、独自の委任モデルを持たないツールでも、引き続き Windows Admin Center を使用して管理できます。
この一時アカウントは、ユーザーが Windows Admin Center を使用したマシン管理を行わなくなると、自動的に削除されます。

ユーザーがロールベースのアクセス制御を使用して構成されたマシンに接続すると、Windows Admin Center では、ローカル管理者であるかどうかを最初に確認します。
そうである場合は、Windows Admin Center のフル機能を制限なしで使用できます。
そうでない場合、Windows Admin Center は、ユーザーが定義済みロールのいずれかに属しているかどうかを確認します。
Windows Admin Center のロールに属していても、完全な管理者でない場合、ユーザーには "*制限付きアクセス権*" が与えられることになります。
最後に、ユーザーが管理者でもロールのメンバーでもない場合は、マシンを管理するためのアクセスは拒否されます。

ロールベースのアクセス制御は、サーバー マネージャーおよびフェールオーバー クラスターのソリューションで使用できます。

### <a name="available-roles"></a>［利用できる役割］

Windows Admin Center では、次のエンドユーザー ロールがサポートされています。

ロール名 | 使用目的
----------|-------------
Administrators | ユーザーは Windows Admin Center のほとんどの機能を使用できます。リモート デスクトップおよび PowerShell へのアクセス権は付与されません。 このロールは、マシン上の管理エントリ ポイントを制限する "ジャンプ サーバー" のシナリオに適しています。
Readers | ユーザーはサーバー上の情報や設定を表示できますが、変更することはできません。
Hyper-V 管理者 | ユーザーは Hyper-V 仮想マシンとスイッチに変更を加えることができますが、他の機能は読み取り専用アクセスに制限されます。

次の組み込みの拡張機能では、ユーザーが制限付きアクセスで接続した場合、機能が制限されます。

- ファイル (ファイルのアップロードまたはダウンロードはできない)
- PowerShell (利用不可)
- リモート デスクトップ (利用不可)
- 記憶域レプリカ (利用不可)

現時点では、組織のカスタム ロールを作成することはできませんが、どのユーザーに各ロールへのアクセスを付与するかを選択することはできます。

### <a name="preparing-for-role-based-access-control"></a>ロールベースのアクセス制御の準備

一時的ローカル アカウントを利用するには、Windows Admin Center でロールベースのアクセス制御をサポートするように各ターゲット マシンを構成する必要があります。
構成プロセスでは、Desired State Configuration を使用して、PowerShell スクリプトと Just Enough Administration エンドポイントをマシンにインストールする必要があります。

コンピューターが数台しかない場合は、Windows Admin Center にあるロールベースのアクセス制御ページを使用することで、個々のコンピューターに構成を簡単に適用できます。
個々のコンピューターにロールベースのアクセス制御を設定すると、各ロールへのアクセスを制御するローカル セキュリティ グループが作成されます。
ユーザーまたは他のセキュリティ グループには、ロール セキュリティ グループのメンバーとして追加することによって、アクセスを許可できます。

複数のコンピューターにわたるエンタープライズ全体の展開では、ゲートウェイから構成スクリプトをダウンロードし、Desired State Configuration プル サーバー、Azure Automation、または必要に応じて管理ツールを使用して、お使いのコンピューターに配布できます。
