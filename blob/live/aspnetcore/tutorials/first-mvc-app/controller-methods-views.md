---
title: "컨트롤러 메서드 및 보기"
author: rick-anderson
description: "컨트롤러 메서드, 보기 및 DataAnnotations 작업"
ms.author: riande
manager: wpickett
ms.date: 03/07/2017
ms.topic: get-started-article
ms.technology: aspnet
ms.prod: asp.net-core
uid: tutorials/first-mvc-app/controller-methods-views
ms.openlocfilehash: cfe1838371226334d368dca13bba37c5b1f6fc39
ms.sourcegitcommit: 3e303620a125325bb9abd4b2d315c106fb8c47fd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/19/2018
---
# <a name="controller-methods-and-views"></a><span data-ttu-id="cec3f-103">컨트롤러 메서드 및 보기</span><span class="sxs-lookup"><span data-stu-id="cec3f-103">Controller methods and views</span></span>

<span data-ttu-id="cec3f-104">작성자: [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="cec3f-104">By [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="cec3f-105">동영상 앱을 적절하게 시작했지만 프레젠테이션은 이상적이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="cec3f-105">We have a good start to the movie app, but the presentation is not ideal.</span></span> <span data-ttu-id="cec3f-106">시간(아래 이미지에서 오전 12시)을 표시하지 않으려 하고 **ReleaseDate**는 두 단어이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cec3f-106">We don't want to see the time (12:00:00 AM in the image below) and **ReleaseDate** should be two words.</span></span>

![인덱스 뷰: 릴리스 날짜는 한 단어(공백 없음)이며 모든 동영상 릴리스 날짜는 오전 12시를 표시합니다.](working-with-sql/_static/m55.png)

<span data-ttu-id="cec3f-108">*Models/Movie.cs* 파일을 열고 아래 표시된 강조 표시된 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cec3f-108">Open the *Models/Movie.cs* file and add the highlighted lines shown below:</span></span>

[!code-csharp[Main](start-mvc/sample/MvcMovie/Models/MovieDateWithExtraUsings.cs?name=snippet_1&highlight=13-14)]

<span data-ttu-id="cec3f-109">빨간색 물결선 **> 빠른 작업 및 리팩터링**을 마우스 오른쪽 단추로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cec3f-109">Right click on a red squiggly line **> Quick Actions and Refactorings**.</span></span>

  ![바로 가기 메뉴는 **> 빠른 작업 및 리팩터링**을 표시합니다.](controller-methods-views/_static/qa.png)


<span data-ttu-id="cec3f-111">`using System.ComponentModel.DataAnnotations;` 누르기</span><span class="sxs-lookup"><span data-stu-id="cec3f-111">Tap `using System.ComponentModel.DataAnnotations;`</span></span>

  ![목록 위쪽의 System.ComponentModel.DataAnnotations 사용](controller-methods-views/_static/da.png)

  <span data-ttu-id="cec3f-113">Visual Studio는 `using System.ComponentModel.DataAnnotations;`를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="cec3f-113">Visual studio adds `using System.ComponentModel.DataAnnotations;`.</span></span>

<span data-ttu-id="cec3f-114">필요하지 않는 `using` 문을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="cec3f-114">Let's remove the `using` statements that are not needed.</span></span> <span data-ttu-id="cec3f-115">기본적으로 밝은 회색 글꼴로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cec3f-115">They show up by default in a light grey font.</span></span> <span data-ttu-id="cec3f-116">*Movie.cs* 파일에서 마우스 오른쪽 단추로 **> 제거 및 using 정렬**의 아무 위치나 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cec3f-116">Right click anywhere in the *Movie.cs* file **> Remove and Sort Usings**.</span></span>

![제거 및 using 정렬](controller-methods-views/_static/rm.png)

<span data-ttu-id="cec3f-118">업데이트된 코드:</span><span class="sxs-lookup"><span data-stu-id="cec3f-118">The updated code:</span></span>

[!code-csharp[Main](./start-mvc/sample/MvcMovie/Models/MovieDate.cs?name=snippet_1)]

<!-- include start -->

[!INCLUDE[adding-model](../../includes/mvc-intro/controller-methods-views.md)]

>[!div class="step-by-step"]
<span data-ttu-id="cec3f-119">[이전](working-with-sql.md)
[다음](search.md)</span><span class="sxs-lookup"><span data-stu-id="cec3f-119">[Previous](working-with-sql.md)
[Next](search.md)</span></span>  