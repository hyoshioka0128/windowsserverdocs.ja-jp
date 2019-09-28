---
title: ディスク保護を有効または無効にする
description: MultiPoint Services でディスク保護を使用する方法について説明します。
ms.custom: na
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 00aba4c4-0244-4b39-8c85-c46fd96e1d6a
author: lizap
manager: dongill
ms.author: elizapo
ms.openlocfilehash: ad5f12a3901a3faf3559abae76e0ba924dce2eb9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71389752"
---
# <a name="enable-or-disable-disk-protection"></a>ディスク保護を有効または無効にする
ディスク保護機能を使用すると、MultiPoint Services システムを再起動するたびに指定した状態にリセットできます。 ディスク保護を使用することにより、ユーザーは MultiPoint Services システムを一時的に変更することができ、変更はサーバーを再起動すると破棄されます。 サーバーの再起動時に破棄される変更の例としては、ユーザーのプロファイルのカスタマイズ、ファイルの保存、設定の変更、アプリケーションのインストールなどがあります。  
  
## <a name="enable-disk-protection"></a>ディスク保護を有効にする  
  
1.  MultiPoint マネージャーで、**ホーム** タブをクリックし、*コンピューター名* **タスク** の **ディスク保護を有効にする** をクリックします。  
  
2.  情報を確認して、 **[OK]** をクリックします。  
  
システムを再起動した後でシステムに対して行った変更 (インストールした新しいアプリケーションも含みます) は、その後で再起動するたびに破棄されます。  
  
## <a name="disable-disk-protection"></a>ディスクの保護を無効にする  
  
1.  MultiPoint マネージャーで、**ホーム** タブをクリックし、*コンピューター名* **タスク** の **ディスク保護を無効にする** をクリックします。  
  
2.  情報を確認して、 **[OK]** をクリックします。  
  
システムを再起動した後でシステムに対して行った変更は、サーバーにインストールしたアプリケーションも含めて、すべて永続的であり、次にシステムを再起動したときも破棄されません。  
  
