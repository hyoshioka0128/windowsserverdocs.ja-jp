---
title: ローカル ユーザー アカウントを作成する
description: MultiPoint Services でのユーザー アカウントの abou の 3 つの種類について説明します
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 33321932-4266-4961-9924-2cb4620bfcb4
author: evaseydl
ms.author: evas
manager: scottman
ms.openlocfilehash: e2e5a6c79e6dcd603d19ca868df1d11fce2bf746
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823673"
---
# <a name="create-local-user-accounts"></a>ローカル ユーザー アカウントを作成する
MultiPoint マネージャーを使用して、3 つのレベルのローカル ユーザー アカウントを作成できます。標準ユーザー アカウントです。MultiPoint ダッシュ ボード ユーザーは、管理権限のあるユーザー完全な管理者のユーザー アカウント。  
  
MultiPoint サーバー上のローカル ユーザー アカウントを作成するのにには、次の手順を使用します。 環境内に複数の MultiPoint サーバーが含まれています、任意のサーバー上のすべてのステーションにログオンできるユーザーをする場合は、各サーバーでローカル ユーザー アカウントを作成する必要があります。 セットアップでは、いくつかの制限があります。 ドメイン環境でユーザーは自分のドメイン アカウントを使用して設定することもできます。 オプションの概要については、次を参照してください。 [Windows MultiPoint サービス環境内のユーザー アカウントを計画](Plan-user-accounts-for-your-MultiPoint-services-environment.md)します。  
   
1.  管理者は、サーバーにログオンし、MultiPoint マネージャーを開きます。  
  
2.  をクリックして、**ユーザー**タブをクリックし、をクリックし、**ユーザー アカウントを追加**します。  
  
    ユーザー アカウントの追加ウィザードが開きます。  
  
3.  新しいユーザー アカウントのアカウント名とパスワードを入力し、クリックして**次**します。  
  
4.  作成するユーザー アカウントの種類を選択します。  
  
    -   **標準ユーザー** - できますステーションにログオンし、ユーザーのタスクの実行が MultiPoint マネージャーや、MultiPoint Server ダッシュ ボードへのアクセスがないと、システムをシャット ダウンできません。  
  
    -   **MultiPoint ダッシュ ボード ユーザー** -管理者権限が限られています。 ダッシュ ボード ユーザーはダッシュ ボードを開くし、システムからのユーザーの記録や、MultiPoint Server コンピューターをシャット ダウンなどのタスクを実行しますが、ユーザーは MultiPoint マネージャーへのアクセスがありません。  
  
    -   **管理ユーザー** MultiPoint Server の完全な管理者権限を持っています。 たとえば、管理ユーザーことができます MultiPoint マネージャーを実行、追加し削除ユーザー、システムの設定を変更やドライバーを更新します。  
  
5.  をクリックして**次**、順にクリックします**完了**ユーザー アカウントを作成します。