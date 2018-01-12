---
uid: mvc/videos/mvc-2/how-do-i/how-do-i-create-a-custom-html-helper-for-an-mvc-application
title: "I: MVC 응용 프로그램에 대 한 사용자 지정 HTML 도우미를 만드는 방법 | Microsoft 문서"
author: rick-anderson
description: "이 비디오에서는 Chris Pels에 MVC 응용 프로그램의 표준 집합에서 사용할 수 있는 사용자 지정 HtmlHelper를 만드는 방법을 보여 줍니다. 첫 번째 샘플 MVC 응용 프로그램..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 12/11/2009
ms.topic: article
ms.assetid: 58b5eb15-4160-4ce2-ae70-6ba94262ea73
ms.technology: dotnet-mvc
ms.prod: .net-framework
msc.legacyurl: /mvc/videos/mvc-2/how-do-i/how-do-i-create-a-custom-html-helper-for-an-mvc-application
msc.type: video
ms.openlocfilehash: 96e58c706101c8b304636947b723fc50cae7f3bc
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="how-do-i-create-a-custom-html-helper-for-an-mvc-application"></a><span data-ttu-id="399cb-105">I: MVC 응용 프로그램에 대 한 사용자 지정 HTML 도우미를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="399cb-105">How Do I: Create a Custom HTML Helper for an MVC Application?</span></span>
====================
<span data-ttu-id="399cb-106">으로 [Chris Pels](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="399cb-106">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="399cb-107">이 비디오에서는 Chris Pels에 MVC 응용 프로그램의 표준 집합에서 사용할 수 있는 사용자 지정 HtmlHelper를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="399cb-107">In this video Chris Pels shows how to create a custom HtmlHelper that is not available in the standard set in an MVC application.</span></span> <span data-ttu-id="399cb-108">먼저 예제 MVC 응용 프로그램 데모 컨트롤러와 뷰 사용자 지정 HtmlHelper 테스트를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="399cb-108">First, a sample MVC application is created with a demo controller and view to test the custom HtmlHelper.</span></span> <span data-ttu-id="399cb-109">그런 다음 확장 메서드를 나타내는 사용자 지정 HtmlHelper 구현 하는 공개 함수 모듈을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="399cb-109">Next, a module is created with a public function that is an extension method which represents the implementation of the custom HtmlHelper.</span></span> <span data-ttu-id="399cb-110">만들기 위한 사용자 지정 도우미는 &amp;lt; img&amp;gt; 페이지에서 태그를 삽입 하 고 id, url 및 이미지 태그에 대 한 대체 텍스트를 포함 하 여 여러 인바운드 매개 변수를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="399cb-110">The custom helper is for creating &amp;lt;img&amp;gt; tags in a page and receives several inbound parameters including the id, url, and alt text for the image tag.</span></span> <span data-ttu-id="399cb-111">논리 함수는 전체 반환 하는 데에 추가 되 &amp;lt; img&amp;gt; 지정 된 정보로 태그 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="399cb-111">The logic is then added to the function for returning the completed &amp;lt;img&amp;gt; tag with the specified information.</span></span> <span data-ttu-id="399cb-112">그런 다음 사용자 지정 HtmlHelper 이미지를 표시 하는 데모 페이지에서 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="399cb-112">Then the custom HtmlHelper is used on the demo page to display an image.</span></span> <span data-ttu-id="399cb-113">사용자 지정 HtmlHelper 정보 쉽게 다른를 만들기에 대 한 유연성을 제공 하는 생성자 재정의 여러 개 포함 하도록 확장 되는 마지막으로, &amp;lt; img&amp;gt; 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="399cb-113">Finally, the custom HtmlHelper is expanded to include multiple constructor overrides which provide flexibility for more easily creating different &amp;lt;img&amp;gt; tags.</span></span>

[<span data-ttu-id="399cb-114">&#9654; (18 분) 비디오를 시청 하세요</span><span class="sxs-lookup"><span data-stu-id="399cb-114">&#9654; Watch video (18 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-create-a-custom-html-helper-for-an-mvc-application)

>[!div class="step-by-step"]
<span data-ttu-id="399cb-115">[이전](how-do-i-implement-view-models-to-manage-data-for-aspnet-mvc-views.md)
[다음](how-do-i-work-with-model-binders-in-an-mvc-application.md)</span><span class="sxs-lookup"><span data-stu-id="399cb-115">[Previous](how-do-i-implement-view-models-to-manage-data-for-aspnet-mvc-views.md)
[Next](how-do-i-work-with-model-binders-in-an-mvc-application.md)</span></span>