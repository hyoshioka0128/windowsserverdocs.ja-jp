---
title: ディスクの保護を使用してシステム ボリュームを保護する
description: MultiPoint Services のディスク保護に関する情報を提供します。
ms.date: 07/22/2016
ms.topic: article
ms.assetid: 18694665-ed65-4d84-8505-f460cf3df907
author: evaseydl
manager: scotman
ms.author: evas
ms.openlocfilehash: aae561dc506ea75d25229a66b1e2a25ed41ccc17
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87953798"
---
# <a name="protecting-the-system-volume-with-disk-protection"></a>ディスクの保護を使用してシステム ボリュームを保護する
MultiPoint Services には、コンピューターを起動するたびにシステムボリュームに対する変更を即座に消去するオプションが用意されています。 ディスク保護機能を有効にした場合、構成の破損やマルウェアの導入など、ドライブに加えられた変更は、次回コンピューターを再起動したときに元に戻されます。 これは、既知の "good" または "ゴールデン" ソフトウェアイメージが毎回読み込まれるようにする管理者にとって便利な機能です。 たとえば、夜間に自動更新やソフトウェアの修正プログラムの適用をスケジュールすることができます。 計画の考慮事項は、エンドユーザーがソフトウェアのインストールなどの変更をインターネットから行うことができるようにするかどうかです。 この機能を有効にすると、ユーザーがファイルを保存できるようにするには、ファイル共有をシステムボリュームの外部に配置する必要があります。

