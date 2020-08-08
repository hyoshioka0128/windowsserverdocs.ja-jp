---
title: MultiPoint Services をドメインに参加させる (オプション)
Description: MultiPoint Services をドメインに参加させる手順について説明します。
ms.date: 07/22/2016
ms.topic: article
ms.assetid: 623b7c21-dcbb-402e-8b5a-8e434cd225bd
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 8e1f1249ac3670a550e70cc09a9862306fd85658
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87995948"
---
# <a name="join-the-multipoint-services-computer-to-a-domain-optional"></a>MultiPoint Services コンピューターのドメインへの参加 (オプション)
Active Directory ドメインを介して MultiPoint Services コンピューターにアクセスする場合は、次の手順として、コンピューターをドメインに追加します。

> [!IMPORTANT]
> コンピューターをドメインに参加させる前に、タイムゾーンを確認する必要があります。 手順については、「[日付、時刻、およびタイムゾーンを設定する](./set-the-date-time.md)」を参照してください。

1.  **スタート**画面で、**コントロール パネル**を開きます。 [**システムとセキュリティ**] をクリックし、[**システム**] をクリックします。

2.  [**コンピューター名、ドメインおよびワークグループの設定**] で [**設定の変更**] をクリックします。

3.  [**コンピューター名**] タブで、[**変更**] をクリックします。

4.  [**コンピューター名/ドメイン**名の変更] ダイアログボックスで、[**ドメイン**] を選択し、ドメインの名前を入力して [ **OK**] をクリックし、ウィザードの手順に従ってプロセスを完了します。

5.  コンピューターが再起動したら、管理者としてログオンし、MultiPoint マネージャーが開かれるのを待ちます。

> [!IMPORTANT]
> MultiPoint Services ドメインの展開が正常に機能するようにするには、いくつかのグループポリシーを構成し、レジストリを更新する必要があります。 詳細については、「[ドメイン展開のグループポリシーを構成する](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn265982(v=ws.11))」を参照してください。