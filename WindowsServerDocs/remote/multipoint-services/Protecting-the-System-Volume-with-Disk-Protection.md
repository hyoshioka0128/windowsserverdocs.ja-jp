---
title: ディスクの保護を使用してシステム ボリュームを保護する
description: MultiPoint Services のディスク保護に関する情報を提供します。
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 18694665-ed65-4d84-8505-f460cf3df907
author: evaseydl
manager: scotman
ms.author: evas
ms.openlocfilehash: 27bcce68cfe5856e987f5ad93460abd12217c26b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71389508"
---
# <a name="protecting-the-system-volume-with-disk-protection"></a>ディスクの保護を使用してシステム ボリュームを保護する
MultiPoint Services には、コンピューターを起動するたびにシステムボリュームに対する変更を即座に消去するオプションが用意されています。 ディスク保護機能を有効にした場合、構成の破損やマルウェアの導入など、ドライブに加えられた変更は、次回コンピューターを再起動したときに元に戻されます。 これは、既知の "good" または "ゴールデン" ソフトウェアイメージが毎回読み込まれるようにする管理者にとって便利な機能です。 たとえば、夜間に自動更新やソフトウェアの修正プログラムの適用をスケジュールすることができます。 計画の考慮事項は、エンドユーザーがソフトウェアのインストールなどの変更をインターネットから行うことができるようにするかどうかです。 この機能を有効にすると、ユーザーがファイルを保存できるようにするには、ファイル共有をシステムボリュームの外部に配置する必要があります。  
  
