---
title: ディスクの保護を使用してシステム ボリュームを保護する
description: MultiPoint Services のディスクの保護についての情報を提供します
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 18694665-ed65-4d84-8505-f460cf3df907
author: evaseydl
manager: scotman
ms.author: evas
ms.openlocfilehash: a663bb27a7480066c997844d68b33774f9032e92
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855213"
---
# <a name="protecting-the-system-volume-with-disk-protection"></a>ディスクの保護を使用してシステム ボリュームを保護する
MultiPoint Services では、コンピューターを起動するたびに、システム ボリュームに対する変更をすぐに消去 オプションを提供します。 ディスク保護機能、構成の破損や、マルウェアの導入など、ドライブへの変更を有効にすると元に戻されます、次回コンピューターを再起動します。 これは、既知の「優れた」または"golden"ソフトウェア イメージに毎回が読み込まれていることを確認する管理者向けの便利な機能です。 自動更新またはソフトウェアのパッチ適用をスケジュールできます、たとえば、真夜中。 計画の考慮事項は、エンドユーザーが、インターネットからソフトウェアのインストールなどの変更を加えることができるかどうか。 この機能を有効にすると、ファイルに格納できるようにする場合、ファイル共有は、システム ボリュームの外部にある必要があります。  
  
