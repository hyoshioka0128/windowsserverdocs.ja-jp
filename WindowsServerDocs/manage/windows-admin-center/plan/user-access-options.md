---
title: Windows Admin Center でのユーザー アクセス オプション
description: ユーザー アクセス オプションと id プロバイダーと Windows Admin Center (プロジェクト ホノルル)
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 03/07/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 9adea736d6e7ae181bdfe50289564083146f5b30
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825893"
---
# <a name="user-access-options-with-windows-admin-center"></a>Windows Admin Center でのユーザー アクセス オプション

>適用先:Windows Admin Center、Windows Admin Center プレビュー

Windows Server で展開されると、Windows Admin Center は、サーバー環境の管理の一元化されたポイントを提供します。 Windows Admin Center へのアクセスを制御することで、管理のランドス ケープのセキュリティを向上できます。

## <a name="gateway-access-roles"></a>ゲートウェイへのアクセスの役割

Windows Admin Center、ゲートウェイ サービスにアクセスするための 2 つのロールを定義します。 ゲートウェイのユーザーとゲートウェイの管理者。

> [!NOTE]
> ゲートウェイへのアクセスは、ゲートウェイが表示されているターゲット サーバーへのアクセスを意味しません。 ターゲット サーバーを管理するには、ユーザーは、対象サーバーで管理者特権のある資格情報を関連付ける必要があります。

**ゲートウェイのユーザー**そのゲートウェイを使用してサーバーを管理するために、Windows Admin Center ゲートウェイ サービスに接続できますが、アクセス許可も、ゲートウェイへの認証に使用する認証メカニズムは変更できません。

**ゲートウェイ管理者**へのアクセスを取得したゲートウェイにユーザーが認証方法を構成することができます。

>[!NOTE]
> Windows Admin Center で定義されているアクセス グループがない場合、Windows アカウントでゲートウェイ サーバーへのアクセスがロールに反映されます。 

[Windows Admin Center では、ゲートウェイのユーザーと管理者のアクセスを構成します。](../configure/user-access-control.md)

## <a name="identity-provider-options"></a>Id プロバイダーのオプション

ゲートウェイの管理者には、次のいずれかを選択できます。

 - [Active Directory/ローカルのコンピューター グループ](../configure/user-access-control.md#active-directory-or-local-machine-groups)
 - [Windows Admin Center の id プロバイダーとしての azure Active Directory](../configure/user-access-control.md#azure-active-directory)


### <a name="smartcard-authentication"></a>スマート カード認証

Id プロバイダーとして Active Directory またはローカル コンピューターのグループを使用して、その他のスマート カード ベースのセキュリティ グループのメンバーである Windows Admin Center にアクセスするユーザーを要求することで、スマート カード認証を適用できます。 [Windows Admin Center では、スマート カード認証を構成します。](../configure/user-access-control.md#active-directory-or-local-machine-groups)

### <a name="conditional-access-and-multi-factor-authentication"></a>条件付きアクセスと多要素認証

ゲートウェイの Azure AD 認証を必要とすると、条件付きアクセスと Azure AD によって提供される多要素認証などの追加のセキュリティ機能を活用できます。 [Azure Active Directory で条件付きアクセスの構成に関する詳細について説明します。](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal-get-started)

## <a name="role-based-access-control"></a>役割ベースのアクセス制御

既定では、ユーザーには、Windows Admin Center を使用して管理するコンピューターの完全なローカル管理者特権が必要があります。
これは、マシンにリモートで接続を許可され表示およびシステム設定を変更するための十分なアクセス許可があります。
ただし、一部のユーザーには、ジョブを実行するコンピューターへの無制限アクセスの必要はありません。
使用することができます**ロール ベース access control**それらの完全なローカル管理者ではなく、マシンにアクセスが制限されたこのようなユーザーに提供する Windows Admin Center でします。

Windows Admin Center でのロールベースのアクセス制御は、PowerShell を使用した各管理対象サーバーを構成することによって動作[Just Enough Administration](https://aka.ms/jeadocs)エンドポイント。
このエンドポイントは、システムのどのような側面を管理する各ロールが許可されている、ユーザーがロールに割り当てられているなど、ロールを定義します。
ユーザーは、制限付きのエンドポイントに接続するときは、ユーザーに代わってシステムを管理する一時的なローカル管理者アカウントが作成されます。
これにより、独自の委任モデルがないもツールは Windows Admin Center で引き続き管理できます。
ユーザーは、Windows Admin Center 経由でコンピューターの管理を停止すると、一時的なアカウントが自動的に削除します。

ユーザーは、ロールベースのアクセス制御で構成されたマシンに接続するときに Windows Admin Center は、ローカル管理者であるを確認は最初にします。
その場合は、制限なしで完全な Windows Admin Center エクスペリエンスを受け取ります。
それ以外の場合、Windows Admin Center では、ユーザーが定義済みのロールのいずれかに属しているかどうかは確認します。
ユーザーがあると言います*制限付きアクセス*場合は、Windows Admin Center のロールに属しているが、完全な管理者ではありません。
最後に、ユーザーが管理者でも、ロールのメンバーの場合は、拒否されますマシンの管理にアクセスします。

ロール ベース access control は、サーバー マネージャーとフェールオーバー クラスター ソリューションを使用できます。

### <a name="available-roles"></a>［利用できる役割］

Windows Admin Center では、次のエンド ユーザー ロールがサポートされています。

ロール名 | 使用目的
----------|-------------
管理者 | リモート デスクトップまたは PowerShell へのアクセスを許可せず、Windows Admin Center でのほとんどの機能を使用することができます。 このロールは、コンピューターの管理のエントリ ポイントを制限する「ジャンプ サーバー」のシナリオに適してします。
Readers | サーバーで、情報および設定を表示、変更することができます。
Hyper-V 管理者 | HYPER-V 仮想マシンとスイッチを変更することができますが、読み取り専用アクセスを他の機能を制限します。

次の組み込みの拡張機能が機能を制限付きアクセスが制限されたユーザーが接続します。

- ファイル (ファイルのアップロードまたはダウンロード)
- PowerShell (使用不可)
- リモート デスクトップ (利用不可)
- 記憶域レプリカ (利用不可)

この時点で、組織のカスタム ロールを作成することはできませんが、各ロールへのアクセスを付与するユーザーを選択することができます。

### <a name="preparing-for-role-based-access-control"></a>ロールベースのアクセス制御のための準備

一時的なローカル アカウントを活用するには、各ターゲット コンピューターが Windows Admin Center でロールベースのアクセス制御をサポートするように構成する必要があります。
構成プロセスでは、Desired State Configuration を使用してマシンに PowerShell スクリプトと Just Enough Administration のエンドポイントをインストールする必要があります。

数台のコンピューターだけの場合は簡単に構成を適用する個別に Windows Admin Center でロールベースのアクセス制御のページを使用して各コンピューターにします。
個々 のコンピューターでのロールベースのアクセス制御を設定するときは、各ロールへのアクセスを制御するローカル セキュリティ グループが作成されます。
ロールのセキュリティ グループのメンバーとして追加することで、ユーザーまたは他のセキュリティ グループにアクセスを付与できます。

全社展開は複数のコンピューターは、ゲートウェイから構成スクリプトをダウンロードして、Desired State Configuration プル サーバー、Azure Automation の場合、または優先管理ツールを使用してコンピューターに配布できます。
