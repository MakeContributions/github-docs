---
title: 关于任务列表
intro: 您可以使用任务列表将议题或拉取请求的工作分解为较小的任务，然后跟踪要完成的整套工作。
redirect_from:
  - /github/managing-your-work-on-github/managing-your-work-with-issues-and-pull-requests/about-task-lists
  - /articles/about-task-lists
  - /github/managing-your-work-on-github/about-task-lists
  - /issues/tracking-your-work-with-issues/creating-issues/about-task-lists
  - /issues/tracking-your-work-with-issues/about-task-lists
versions:
  fpt: '*'
  ghes: '*'
  ghae: '*'
  ghec: '*'
topics:
  - Pull requests
  - Issues
ms.openlocfilehash: dcb8d7972e83d8d35ed2425d57e2950d64ef1352
ms.sourcegitcommit: e8c012864f13f9146e53fcb0699e2928c949ffa8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2022
ms.locfileid: '148159458'
---
{% ifversion projects-v2-tasklists %} {% note %}

注意：有关 Tasklists（当前为专用 beta 版）的新迭代的详细信息，请参阅“[关于 Tasklists](/issues/tracking-your-work-with-issues/about-tasklists)”。

{% endnote %} {% endif %}

## 关于任务列表

任务列表是一组任务，每个任务都在单独的行上呈现，带有可点击的复选框。 您可以选中或取消选中复选框来将任务标记为完成或未完成。 

您可以使用 Markdown 在 {% data variables.product.product_name %} 上的任何评论中创建任务列表。 {% ifversion fpt or ghec %}如果在列表中引用议题、拉取请求或讨论，则引用将展开以显示标题和状态。{% endif %} 

{% ifversion not fpt or ghec %} 当任务列表在初始评论中时，可以查看议题和拉取请求列表中的任务列表摘要信息。
{% else %}

## 关于议题任务列表

如果您将任务列表添加到议题正文中，列表具有添加的功能。

- 为了帮助您跟踪团队在议题上的操作，议题任务列表的进度出现在 {% data variables.product.product_name %} 的不同位置，例如仓库的议题列表。
- 如果任务引用另一个议题，并且有人关闭该议题，则任务的复选框将自动标记为完整。 
- 如果任务需要进一步跟踪或讨论，您可以通过在任务上方悬停并单击任务右上角的 {% octicon "issue-opened" aria-label="The issue opened icon" %} 将任务转换为议题。 要在创建议题之前添加更多详细信息，您可以使用键盘快捷方式打开新议题表单。 有关详细信息，请参阅“[键盘快捷方式](/github/getting-started-with-github/using-github/keyboard-shortcuts#issues-and-pull-requests)”。
- 任务列表中提及的任何议题都将指定在引用议题中跟踪它们。

![渲染的任务列表](/assets/images/help/writing/task-list-rendered.png)

{% endif %}

## 创建任务列表

{% data reusables.repositories.task-list-markdown %}

{% tip %}

**提示：** 不能在已关闭的议题或包含链接的拉取请求的议题中创建任务列表项目。

{% endtip %}

## 对任务重新排序

您可以单击任务左边的复选框并将任务拖放至新位置，对任务列表中的项目重新排序。 您可以在相同的评论中对不同列表中的任务重新排序，但是不能在不同的评论中重新排序任务。

{% ifversion fpt %} ![重新排序的任务列表](/assets/images/help/writing/task-list-reordered.gif) {% else %} ![重新排序的任务列表](/assets/images/enterprise/writing/task-lists-reorder.gif) {% endif %}

{% ifversion fpt %}

## 导航跟踪的议题

任务列表中引用的任何议题都指定它们被包含任务列表的议题跟踪。 要从已跟踪的议题导航到正在跟踪的议题，请单击议题状态旁边的“已跟踪”中的跟踪议题编号。

![跟踪示例](/assets/images/help/writing/task_list_tracked.png)

{% endif %}

## 延伸阅读

{% ifversion code-scanning-task-lists %}
* “[使用任务列表跟踪议题中的 {% data variables.product.prodname_code_scanning %} 警报](/code-security/code-scanning/automatically-scanning-your-code-for-vulnerabilities-and-errors/tracking-code-scanning-alerts-in-issues-using-task-lists)”{% endif %}
