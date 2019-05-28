---
title: Windows Server に関連する記事に必要なメタデータ タグを追加します。
description: 情報の一覧する必要がありますとして追加するメタデータ タグ、Windows Server に関連する記事の先頭にします。 必要なタグは、レポートとチームの両方の要件に基づいて変更される可能性が。
author: eross-msft
ms.author: lizross
ms.date: 05/06/2019
ms.openlocfilehash: f7c514def1353d44386b1bc53c8cabffe1e31fda
ms.sourcegitcommit: 7e54a1bcd31cd2c6b18fd1f21b03f5cfb6165bf3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/09/2019
ms.locfileid: "65461640"
---
# <a name="add-the-required-metadata-tags-to-your-windows-server-related-article"></a>Windows Server に関連する記事に必要なメタデータ タグを追加します。

すべての記事の上部にあるは、特定のメタデータを追跡および SEO の目的を含める必要があります。 必要なタグは、レポートの要件に基づいて変更される可能性が。 ただし、すべてのフィールドの追加または削除する必要がある場合、このするを通知する必要があります。

これは、ようになります、上部と下部に 3 つのハイフン (-) を含みます。

```markdown

---
title: The title of the article should go here. This is used in SEO and search results.

description: A description for the article should go here. This is used in search results, to provide users with information about whether the article has the information they’re looking for.

ms.prod: Use this specific text, windows-server-threshold

ms.reviewer: The Microsoft alias for the primary PM for the feature/functionality

author: Your GitHub alias

ms.author: Your Microsoft alias

manager: Your manager’s Microsoft alias

ms.topic: Type of article, including article, landing-page, get-started-article, or reference

ms.date: Date of change (MM/DD/YYYY)

---

```

## <a name="example"></a>例

```markdown

---
title: What is Windows Admin Center?
description: Learn about the Windows Admin Center, a locally-deployed, browser-based management tool set that lets you manage your Windows Servers with no Azure or cloud dependency.
ms.prod: windows-server-threshold
ms.reviewer: alainch
author: danielle-github
ms.author: danielle
manager: alainch
ms.topic: article
ms.date: 07/06/2019
---

```