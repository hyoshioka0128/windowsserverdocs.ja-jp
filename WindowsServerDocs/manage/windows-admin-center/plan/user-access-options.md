---
title: Windows Admin center のユーザー アクセス オプション
description: ユーザー アクセス オプションと Windows Admin center (Project Honolulu) の id プロバイダー
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 03/07/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 9adea736d6e7ae181bdfe50289564083146f5b30
ms.sourcegitcommit: 4961576f2891600ef9a760ca7df650d14332e057
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/09/2019
ms.locfileid: "9151997"
---
# Windows Admin center のユーザー アクセス オプション

>適用対象: Windows Admin Center、Windows Admin Center Preview

Windows Server に展開されると、Windows Admin Center がサーバー環境の管理の一元的なポイントを提供します。 Windows Admin Center へのアクセスを制御するには、管理、ランドス ケープのセキュリティを向上させることができます。

## ゲートウェイへのアクセスの役割

Windows Admin Center ゲートウェイ サービスへのアクセス用の 2 つのロールの定義: ゲートウェイ ユーザーとゲートウェイの管理者です。

> [!NOTE]
> ゲートウェイへのアクセスは、ゲートウェイによって表示されている対象サーバーへのアクセスを意味しません。 ターゲット サーバーを管理するには、ユーザーを対象のサーバー上の管理者特権を持つ資格情報を関連付ける必要があります。

**ゲートウェイのユーザー**がそのゲートウェイを介してサーバーを管理するために Windows Admin Center ゲートウェイ サービスに接続できますが、アクセス許可もゲートウェイへの認証に使用される認証メカニズムは変更できません。

**ゲートウェイの管理者**は、ゲートウェイにユーザーを認証する方法と同様のアクセスを取得した構成できます。

>[!NOTE]
> Windows Admin Center で定義されているアクセス グループがない場合は、ロールには、Windows アカウント ゲートウェイ サーバーへのアクセスが反映されます。 

[Windows Admin Center でゲートウェイのユーザーと管理者のアクセスを構成します。](../configure/user-access-control.md)

## Id プロバイダーのオプション

ゲートウェイの管理者は、次のいずれかを選択できます。

 - [Active Directory/ローカル マシン グループ](../configure/user-access-control.md#active-directory-or-local-machine-groups)
 - [Windows Admin Center の id プロバイダーとして azure Active Directory](../configure/user-access-control.md#azure-active-directory)


### スマート カード認証

Active Directory またはローカル コンピューターのグループの id プロバイダーとしてを使用する場合は、追加のスマート カード ベースのセキュリティ グループのメンバーである Windows Admin Center にアクセスするユーザーを必要とするスマート カード認証を適用できます。 [Windows Admin Center では、スマート カード認証を構成します。](../configure/user-access-control.md#active-directory-or-local-machine-groups)

### 条件付きアクセスし、多要素認証

ゲートウェイの Azure AD 認証を要求することで、条件付きアクセスと Azure AD によって提供される多要素認証などの追加のセキュリティ機能を活用できます。 [Azure Active Directory の条件付きアクセスの構成について説明します。](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal-get-started)

## ロール ベースのアクセス制御

既定では、ユーザーには、Windows Admin Center を使用して管理するコンピューターで完全なローカルの管理者特権が必要です。
これにより、リモート コンピューターに接続することされを表示してシステムの設定を変更するための十分なアクセス許可があります。
ただし、一部のユーザーでが無制限マシンにアクセスし、ジョブの実行には必要ありません。
Windows Admin Center で**役割ベースのアクセス制御**を使用して、それらの完全なローカル管理者を作成するのではなく、コンピューターへのアクセス制限でこのようなユーザーに提供することができます。

Windows Admin Center で役割ベースのアクセス制御は、PowerShell [Just Enough Administration](https://aka.ms/jeadocs)エンドポイントと各管理対象サーバーを構成することで動作します。
このエンドポイントは、どのような側面システムの各ロールの管理を許可するユーザーは、ロールに割り当てられているなど、ロールを定義します。
ユーザーは、制限付きのエンドポイントに接続するときは、代わりにシステムを管理する一時的なローカル管理者アカウントが作成されます。
これによりがないため、独自の委任モデルもツールは Windows Admin Center で引き続き管理できます。
Windows Admin Center を通じてコンピューターを管理するために、ユーザーが停止したとき、一時的なアカウントが自動的に削除されます。

ユーザーは、役割ベースのアクセス制御で構成されているコンピューターに接続するかどうかは、ローカル管理者を Windows Admin Center が確認まずされます。
その場合は、制限なしで Windows Admin Center の完全なエクスペリエンスを受け取ります。
それ以外の場合、Windows Admin Center は、ユーザーが定義済みのロールのいずれかに属しているか確認されます。
ユーザーと呼びます*アクセスを制限*がある場合は、Windows Admin Center のロールに属しているが、完全な管理者ではありません。
最後に、管理者とロールのメンバーのどちらも、ユーザーがある場合、アクセスが拒否されますコンピューターを管理します。

役割ベースのアクセス制御は、サーバー マネージャーおよびフェールオーバー クラスター ソリューション利用できます。

### 利用可能なロール

Windows Admin Center は、次のエンドユーザーの役割をサポートしています。

ロールの名前 | 使用目的
----------|-------------
管理者 | リモート デスクトップまたは PowerShell へのアクセス権を付与することがなく、Windows Admin Center でほとんどの機能を使用することができます。 この役割は、コンピューター上の管理のエントリ ポイントを制限する「サーバーをジャンプ」のシナリオに適しています。
リーダー | サーバーでの情報と設定の表示が変更することができます。
HYPER-V 管理者 | HYPER-V 仮想マシンとスイッチに変更を加えることができますが、読み取り専用アクセスするには、その他の機能を制限します。

次の組み込みの拡張機能では、制限付きのアクセス権を持つユーザーが接続するときは、機能が制限します。

- ファイル (ファイルのアップロードまたはダウンロード)
- PowerShell (利用不可)
- リモート デスクトップ (利用不可)
- 記憶域レプリカ (利用不可)

この時点で、組織のカスタムの役割を作成することはできませんが、各ロールへのアクセスを許可されているユーザーを選択できます。

### 役割ベースのアクセス制御のための準備

一時的なローカル アカウントを活用するには、各ターゲット コンピューターを Windows Admin Center で役割ベースのアクセス制御をサポートするように構成する必要があります。
構成プロセスでは、PowerShell スクリプトと Just Enough Administration エンドポイントを Desired State Configuration を使用して、コンピューターにインストールする必要があります。

場合は、数台のコンピューターのみがある、簡単に構成を適用できます、個別に Windows Admin Center で役割ベースのアクセス制御のページを使用して各コンピューターにします。
個々 のコンピューターで役割ベースのアクセス制御を設定すると、各ロールへのアクセスを制御するローカル セキュリティ グループが作成されます。
ロールのセキュリティ グループのメンバーとして追加することで、ユーザーまたはその他のセキュリティ グループにアクセスを付与できます。

複数のコンピューターでの全社的な展開には、ゲートウェイから構成スクリプトをダウンロードし、Desired State Configuration プル サーバー、Azure オートメーションでは、または、優先する管理ツールを使用してコンピューターに配布できます。
