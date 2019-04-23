---
title: (省略可能) ドメインに MultiPoint Services に参加します。
Description: MultiPoint サービスをドメインに参加させる手順を提供します。
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 623b7c21-dcbb-402e-8b5a-8e434cd225bd
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: af5dd1f16e011161bbcf72c21c21088721ac1243
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827043"
---
# <a name="join-the-multipoint-services-computer-to-a-domain-optional"></a>(省略可能) ドメインに MultiPoint Services コンピューターを参加させる
MultiPoint Services コンピューターは、Active Directory ドメイン経由でアクセスは、次の手順は、ドメインにコンピューターを追加するは。  
  
> [!IMPORTANT]  
> コンピューターをドメインに参加する前に、タイム ゾーンを確認する必要があります。 手順については、次を参照してください。[日付、時刻、タイム ゾーン設定](Set-the-date--time--and-time-zone.md)します。  
   
1.  **スタート**画面で、**コントロール パネル**を開きます。 クリックして**システムとセキュリティ**、 をクリックし、**システム**します。  
  
2.  **[コンピューター名、ドメインおよびワークグループの設定]** で **[設定の変更]** をクリックします。  
  
3.  **コンピューター名**] タブで [**変更**します。  
  
4.  **コンピューター名/ドメイン名の変更**ダイアログ ボックスで、**ドメイン**、ドメインの名前を入力し、クリックして、 **OK**、ウィザードを完了する手順に従います、プロセスです。  
  
5.  コンピューターの再起動後に管理者としてログオンし、MultiPoint マネージャーを開くまで待ちます。  
  
> [!IMPORTANT]  
> MultiPoint Services ドメインの展開が正しく動作することを確認するには、いくつかのグループ ポリシーを構成して、レジストリを更新する必要があります。 詳しくは、次を参照してください。[ドメイン展開用のグループ ポリシーを構成する](https://technet.microsoft.com/library/dn265982.aspx)します。  