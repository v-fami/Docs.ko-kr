---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/performing-batch-updates-vb
title: "일괄 처리 업데이트 (VB)를 수행 합니다. | Microsoft Docs"
author: rick-anderson
description: "완벽 하 게 편집할 만드는 방법을 설명에 해당 항목이 모두 있는 DataList 편집 모드와 해당 값에서 ' 모두 업데이트 ' 단추를 클릭 하 여 저장할 수 있습니다는 중..."
ms.author: aspnetcontent
manager: wpickett
ms.date: 10/30/2006
ms.topic: article
ms.assetid: 8dac22a7-91de-4e3b-888f-a4c438b03851
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/performing-batch-updates-vb
msc.type: authoredcontent
ms.openlocfilehash: cc7b90c06b2d99b6c540e9650bb4d8515f5c3702
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="performing-batch-updates-vb"></a><span data-ttu-id="41cf2-103">일괄 처리 업데이트 (VB)를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-103">Performing Batch Updates (VB)</span></span>
====================
<span data-ttu-id="41cf2-104">으로 [Scott Mitchell](https://twitter.com/ScottOnWriting)</span><span class="sxs-lookup"><span data-stu-id="41cf2-104">by [Scott Mitchell](https://twitter.com/ScottOnWriting)</span></span>

<span data-ttu-id="41cf2-105">[샘플 앱을 다운로드](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_37_VB.exe) 또는 [PDF 다운로드](performing-batch-updates-vb/_static/datatutorial37vb1.pdf)</span><span class="sxs-lookup"><span data-stu-id="41cf2-105">[Download Sample App](http://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_37_VB.exe) or [Download PDF](performing-batch-updates-vb/_static/datatutorial37vb1.pdf)</span></span>

> <span data-ttu-id="41cf2-106">완벽 하 게 편집할 만드는 방법을 설명에 해당 항목이 모두 있는 DataList 편집 모드와 페이지에는 "업데이트 모두" 단추를 클릭 하 여 해당 값을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-106">Learn how to create a fully-editable DataList where all of its items are in edit mode and whose values can be saved by clicking an "Update All" button on the page.</span></span>


## <a name="introduction"></a><span data-ttu-id="41cf2-107">소개</span><span class="sxs-lookup"><span data-stu-id="41cf2-107">Introduction</span></span>

<span data-ttu-id="41cf2-108">에 [이전 자습서](an-overview-of-editing-and-deleting-data-in-the-datalist-vb.md) 항목 수준 DataList를 만드는 방법을 검사 했습니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-108">In the [preceding tutorial](an-overview-of-editing-and-deleting-data-in-the-datalist-vb.md) we examined how to create an item-level DataList.</span></span> <span data-ttu-id="41cf2-109">표준 편집 가능한 GridView DataList의 각 항목에 포함 된 같은 편집 단추를 클릭 하면 항목 편집할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-109">Like the standard editable GridView, each item in the DataList included an Edit button that, when clicked, would make the item editable.</span></span> <span data-ttu-id="41cf2-110">특정 사용 사례 시나리오가 필요한 반면이 항목 수준의 편집에서 잘 작동 가끔 업데이트 되는 데이터를 많은 레코드를 편집 하려면 사용자가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-110">While this item-level editing works well for data that is only updated occasionally, certain use case scenarios require the user to edit many records.</span></span> <span data-ttu-id="41cf2-111">수십 개의 레코드를 편집 해야 하 고 편집을 클릭 하 고 해당 대로 변경한 각 하나에 대 한 업데이트를 클릭 하는 강제 적용 하는 사용자, 클릭 하면 양을 그녀의 생산성 방해가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-111">If a user needs to edit dozens of records and is forced to click Edit, make their changes, and click Update for each one, the amount of clicking can hamper her productivity.</span></span> <span data-ttu-id="41cf2-112">이러한 경우에는 편이 더 나은지 제공 하는 것을 완벽 하 게 편집할 DataList 곳 *모든* 해당 항목은 편집 모드 및 페이지에서 모두 업데이트 단추를 클릭 하 여 해당 값을 편집할 수 있습니다 (그림 1 참조).</span><span class="sxs-lookup"><span data-stu-id="41cf2-112">In such situations, a better option is to provide a fully-editable DataList, one where *all* of its items are in edit mode and whose values can be edited by clicking an Update All button on the page (see Figure 1).</span></span>


<span data-ttu-id="41cf2-113">[![완벽 하 게 편집 가능한 DataList의 각 항목을 수정할 수 있습니다.](performing-batch-updates-vb/_static/image2.png)](performing-batch-updates-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="41cf2-113">[![Each Item in a Fully Editable DataList can be Modified](performing-batch-updates-vb/_static/image2.png)](performing-batch-updates-vb/_static/image1.png)</span></span>

<span data-ttu-id="41cf2-114">**그림 1**: 완벽 하 게 편집 가능한 DataList의 각 항목을 수정할 수 있습니다 ([전체 크기 이미지를 보려면 클릭](performing-batch-updates-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="41cf2-114">**Figure 1**: Each Item in a Fully Editable DataList can be Modified ([Click to view full-size image](performing-batch-updates-vb/_static/image3.png))</span></span>


<span data-ttu-id="41cf2-115">이 자습서에서는 사용자가 완벽 하 게 편집할 DataList를 사용 하 여 공급 업체 주소 정보를 업데이트할 수 있도록 하는 방법을 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-115">In this tutorial we'll examine how to enable users to update suppliers address information using a fully editable DataList.</span></span>

## <a name="step-1-create-the-editable-user-interface-in-the-datalist-s-itemtemplate"></a><span data-ttu-id="41cf2-116">1 단계: s DataList의 ItemTemplate에 편집 가능한 사용자 인터페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="41cf2-116">Step 1: Create the Editable User Interface in the DataList s ItemTemplate</span></span>

<span data-ttu-id="41cf2-117">여기서 만드는 표준, 항목 수준 편집 가능한 DataList म 사용 두 템플릿이 이전 자습서:</span><span class="sxs-lookup"><span data-stu-id="41cf2-117">In the preceding tutorial, where we creating a standard, item-level editable DataList, we used two templates:</span></span>

- <span data-ttu-id="41cf2-118">`ItemTemplate`읽기 전용 사용자 인터페이스 (각 제품 s 이름과 가격을 표시 하기 위한 레이블 웹 컨트롤)를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-118">`ItemTemplate` contained the read-only user interface (the Label Web controls for displaying each product s name and price).</span></span>
- <span data-ttu-id="41cf2-119">`EditItemTemplate`편집 모드 사용자 인터페이스 (두 개의 TextBox 웹 컨트롤)를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-119">`EditItemTemplate` contained the edit mode user interface (the two TextBox Web controls).</span></span>

<span data-ttu-id="41cf2-120">DataList s `EditItemIndex` 속성은 어떤 나타냅니다 `DataListItem` (있는 경우)를 사용 하 여 렌더링 되는 `EditItemTemplate`합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-120">The DataList s `EditItemIndex` property dictates what `DataListItem` (if any) is rendered using the `EditItemTemplate`.</span></span> <span data-ttu-id="41cf2-121">특히는 `DataListItem` 인 `ItemIndex` 값과 s DataList 일치 `EditItemIndex` 속성은 사용 하 여 렌더링는 `EditItemTemplate`합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-121">In particular, the `DataListItem` whose `ItemIndex` value matches the DataList s `EditItemIndex` property is rendered using the `EditItemTemplate`.</span></span> <span data-ttu-id="41cf2-122">이 모델에는 완벽 하 게 편집할 DataList를 만들 때 시간만 떨어져 있는 폭포에 하나의 항목을 편집할 수 있습니다 하는 경우에 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-122">This model works well when only one item can be edited at a time, but falls apart when creating a fully-editable DataList.</span></span>

<span data-ttu-id="41cf2-123">원하는 완벽 하 게 편집할 DataList에 대 한 *모든* 의 `DataListItem` 편집 가능한 인터페이스를 사용 하 여 렌더링 하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-123">For a fully editable DataList, we want *all* of the `DataListItem` s to render using the editable interface.</span></span> <span data-ttu-id="41cf2-124">편집 가능한 인터페이스를 정의 하는이 수행 하는 가장 간단한 방법은 `ItemTemplate`합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-124">The simplest way to accomplish this is to define the editable interface in the `ItemTemplate`.</span></span> <span data-ttu-id="41cf2-125">공급 업체 주소 정보를 수정 하는 것에 대 한 편집 가능한 인터페이스에는 주소, 도시와 국가 값에 대 한 텍스트와 텍스트 상자와 공급 업체 이름을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-125">For modifying the suppliers address information, the editable interface contains the supplier name as text and then TextBoxes for the address, city, and country values.</span></span>

<span data-ttu-id="41cf2-126">열어 시작는 `BatchUpdate.aspx` 페이지 DataList 컨트롤을 추가 하 고 설정의 `ID` 속성을 `Suppliers`합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-126">Start by opening the `BatchUpdate.aspx` page, add a DataList control, and set its `ID` property to `Suppliers`.</span></span> <span data-ttu-id="41cf2-127">DataList s 스마트 태그에서 이라는 새 ObjectDataSource 컨트롤을 추가 하도록 선택할 `SuppliersDataSource`합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-127">From the DataList s smart tag, opt to add a new ObjectDataSource control named `SuppliersDataSource`.</span></span>


<span data-ttu-id="41cf2-128">[![SuppliersDataSource 라는 새 ObjectDataSource 만들기](performing-batch-updates-vb/_static/image5.png)](performing-batch-updates-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="41cf2-128">[![Create a New ObjectDataSource Named SuppliersDataSource](performing-batch-updates-vb/_static/image5.png)](performing-batch-updates-vb/_static/image4.png)</span></span>

<span data-ttu-id="41cf2-129">**그림 2**: 명명 된 새 ObjectDataSource 만드는 `SuppliersDataSource` ([전체 크기 이미지를 보려면 클릭](performing-batch-updates-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="41cf2-129">**Figure 2**: Create a New ObjectDataSource Named `SuppliersDataSource` ([Click to view full-size image](performing-batch-updates-vb/_static/image6.png))</span></span>


<span data-ttu-id="41cf2-130">구성 ObjectDataSource를 사용 하 여 데이터를 검색 하는 `SuppliersBLL` s 클래스 `GetSuppliers()` 메서드 (그림 3 참조).</span><span class="sxs-lookup"><span data-stu-id="41cf2-130">Configure the ObjectDataSource to retrieve data using the `SuppliersBLL` class s `GetSuppliers()` method (see Figure 3).</span></span> <span data-ttu-id="41cf2-131">이전 자습서는 ObjectDataSource 통해 공급 업체 정보 업데이트를 대신와 마찬가지로 비즈니스 논리 계층와 직접 협업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-131">As with the preceding tutorial, rather than updating the supplier information through the ObjectDataSource, we'll work directly with the Business Logic Layer.</span></span> <span data-ttu-id="41cf2-132">따라서 업데이트 탭에서 드롭 다운 목록을 (없음)을 설정 (그림 4 참조).</span><span class="sxs-lookup"><span data-stu-id="41cf2-132">Therefore, set the drop-down list to (None) in the UPDATE tab (see Figure 4).</span></span>


<span data-ttu-id="41cf2-133">[![GetSuppliers() 메서드를 사용 하 여 공급 업체 정보를 검색 합니다.](performing-batch-updates-vb/_static/image8.png)](performing-batch-updates-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="41cf2-133">[![Retrieve Supplier Information Using the GetSuppliers() Method](performing-batch-updates-vb/_static/image8.png)](performing-batch-updates-vb/_static/image7.png)</span></span>

<span data-ttu-id="41cf2-134">**그림 3**: 검색 공급자 정보를 사용 하 여 `GetSuppliers()` 메서드 ([전체 크기 이미지를 보려면 클릭](performing-batch-updates-vb/_static/image9.png))</span><span class="sxs-lookup"><span data-stu-id="41cf2-134">**Figure 3**: Retrieve Supplier Information Using the `GetSuppliers()` Method ([Click to view full-size image](performing-batch-updates-vb/_static/image9.png))</span></span>


<span data-ttu-id="41cf2-135">[![(없음) 드롭 다운 목록을 업데이트 탭에서 설정](performing-batch-updates-vb/_static/image11.png)](performing-batch-updates-vb/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="41cf2-135">[![Set the Drop-Down List to (None) in the UPDATE Tab](performing-batch-updates-vb/_static/image11.png)](performing-batch-updates-vb/_static/image10.png)</span></span>

<span data-ttu-id="41cf2-136">**그림 4**: (None) 드롭 다운 목록을 업데이트 탭에서 설정 ([전체 크기 이미지를 보려면 클릭](performing-batch-updates-vb/_static/image12.png))</span><span class="sxs-lookup"><span data-stu-id="41cf2-136">**Figure 4**: Set the Drop-Down List to (None) in the UPDATE Tab ([Click to view full-size image](performing-batch-updates-vb/_static/image12.png))</span></span>


<span data-ttu-id="41cf2-137">마법사를 완료 한 후 Visual Studio를 자동으로 생성 s DataList `ItemTemplate` 레이블 웹 컨트롤에 데이터 소스에서 반환 된 각 데이터 필드를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-137">After completing the wizard, Visual Studio automatically generates the DataList s `ItemTemplate` to display each data field returned by the data source in a Label Web control.</span></span> <span data-ttu-id="41cf2-138">편집 인터페이스를 대신 제공 하도록이 서식 파일을 수정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-138">We need to modify this template so that it provides the editing interface instead.</span></span> <span data-ttu-id="41cf2-139">`ItemTemplate` DataList s 스마트 태그에서 템플릿 편집 옵션을 사용 하 여 디자이너를 통해 또는 직접 선언 구문을 통해 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-139">The `ItemTemplate` can be customized through the Designer using the Edit Templates option from the DataList s smart tag or directly through the declarative syntax.</span></span>

<span data-ttu-id="41cf2-140">잠시 시간을 텍스트로 제공 업체의 이름을 표시 하지만 공급 업체의 주소, 도시, 및 국가 값에 대 한 입력란을 포함 하는 편집 인터페이스를 만들려면.</span><span class="sxs-lookup"><span data-stu-id="41cf2-140">Take a moment to create an editing interface that displays the supplier s name as text, but includes TextBoxes for the supplier s address, city, and country values.</span></span> <span data-ttu-id="41cf2-141">다음과 같이 변경한 후 페이지 s 선언적 구문 다음과 비슷하게 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-141">After making these changes, your page s declarative syntax should look similar to the following:</span></span>


[!code-aspx[Main](performing-batch-updates-vb/samples/sample1.aspx)]

> [!NOTE]
> <span data-ttu-id="41cf2-142">이전 자습서와 함께이 자습서에서는 DataList 사용에서 뷰 상태를가지고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-142">As with the preceding tutorial, the DataList in this tutorial must have its view state enabled.</span></span>


<span data-ttu-id="41cf2-143">에 `ItemTemplate` I 두 가지 새 CSS 클래스를 사용 하 여 m `SupplierPropertyLabel` 및 `SupplierPropertyValue`에 추가 된는 `Styles.css` 클래스와 같은 스타일 설정을 사용 하도록 구성 된는 `ProductPropertyLabel` 및 `ProductPropertyValue` CSS 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-143">In the `ItemTemplate` I m using two new CSS classes, `SupplierPropertyLabel` and `SupplierPropertyValue`, which have been added to the `Styles.css` class and configured to use the same style settings as the `ProductPropertyLabel` and `ProductPropertyValue` CSS classes.</span></span>


[!code-css[Main](performing-batch-updates-vb/samples/sample2.css)]

<span data-ttu-id="41cf2-144">다음과 같이 변경한 후 브라우저를 통해이 페이지를 방문 합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-144">After making these changes, visit this page through a browser.</span></span> <span data-ttu-id="41cf2-145">그림 5에서 볼 수 있듯이 각 DataList 항목은 텍스트로 공급 업체 이름을 표시 하 고 텍스트 상자를 사용 하 여 주소, 도시와 국가 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-145">As Figure 5 shows, each DataList item displays the supplier name as text and uses TextBoxes to display the address, city, and country.</span></span>


<span data-ttu-id="41cf2-146">[![DataList에 각 공급 업체는 편집 가능](performing-batch-updates-vb/_static/image14.png)](performing-batch-updates-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="41cf2-146">[![Each Supplier in the DataList is Editable](performing-batch-updates-vb/_static/image14.png)](performing-batch-updates-vb/_static/image13.png)</span></span>

<span data-ttu-id="41cf2-147">**그림 5**: DataList에 각 공급 업체는 편집 가능 ([전체 크기 이미지를 보려면 클릭](performing-batch-updates-vb/_static/image15.png))</span><span class="sxs-lookup"><span data-stu-id="41cf2-147">**Figure 5**: Each Supplier in the DataList is Editable ([Click to view full-size image](performing-batch-updates-vb/_static/image15.png))</span></span>


## <a name="step-2-adding-an-update-all-button"></a><span data-ttu-id="41cf2-148">2 단계: 업데이트를 모두 단추 추가</span><span class="sxs-lookup"><span data-stu-id="41cf2-148">Step 2: Adding an Update All Button</span></span>

<span data-ttu-id="41cf2-149">그림 5에 각 공급 업체에 해당 주소, 도시, 및 텍스트 상자에 표시 되는 국가 필드에, 현재 업데이트 단추가 없는 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-149">While each supplier in Figure 5 has its address, city, and country fields displayed in a TextBox, there currently is no Update button available.</span></span> <span data-ttu-id="41cf2-150">항목당 업데이트 단추를 대신 완벽 하 게 편집할 DataLists 생깁니다 일반적으로 단일 모두 업데이트 단추 페이지는 클릭 하면 업데이트 *모든* DataList의 레코드입니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-150">Rather than having an Update button per item, with fully editable DataLists there is typically a single Update All button on the page that, when clicked, updates *all* of the records in the DataList.</span></span> <span data-ttu-id="41cf2-151">이 자습서에 대 한 s (단추 중 하나를 클릭 하는 동일한 효과가) 하지만 두 개의 모두 업데이트 단추-맨 아래에 여러 개 있는 페이지의 위쪽에 한 추가 사용 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-151">For this tutorial, let s add two Update All buttons - one at the top of the page and one at the bottom (although clicking either button will have the same effect).</span></span>

<span data-ttu-id="41cf2-152">DataList 창과 집합 위로 단추 웹 컨트롤을 추가 하 여 시작 해당 `ID` 속성을 `UpdateAll1`합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-152">Start by adding a Button Web control above the DataList and set its `ID` property to `UpdateAll1`.</span></span> <span data-ttu-id="41cf2-153">다음으로 설정 DataList, 아래에 두 번째 단추 웹 컨트롤 추가 해당 `ID` 를 `UpdateAll2`합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-153">Next, add the second Button Web control beneath the DataList, setting its `ID` to `UpdateAll2`.</span></span> <span data-ttu-id="41cf2-154">설정의 `Text` 모두 업데이트 하는 두 개의 단추에 대 한 속성.</span><span class="sxs-lookup"><span data-stu-id="41cf2-154">Set the `Text` properties for the two Buttons to Update All.</span></span> <span data-ttu-id="41cf2-155">마지막으로, 두 단추에 대 한 이벤트 처리기를 만들 `Click` 이벤트입니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-155">Lastly, create event handlers for both Buttons `Click` events.</span></span> <span data-ttu-id="41cf2-156">각 이벤트 처리기에서 업데이트 논리를 복제 하는 대신 let s 리팩터링 논리는 세 번째 메서드에 `UpdateAllSupplierAddresses`,이 세 번째 메서드를 단순히 호출할 이벤트 처리기에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-156">Rather than duplicating the update logic in each of the event handlers, let s refactor that logic to a third method, `UpdateAllSupplierAddresses`, having the event handlers simply invoking this third method.</span></span>


[!code-vb[Main](performing-batch-updates-vb/samples/sample3.vb)]

<span data-ttu-id="41cf2-157">그림 6 모두 업데이트 단추를 추가한 후에 페이지를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-157">Figure 6 shows the page after the Update All buttons have been added.</span></span>


<span data-ttu-id="41cf2-158">[![페이지에 추가 된 두 업데이트 모두 단추](performing-batch-updates-vb/_static/image17.png)](performing-batch-updates-vb/_static/image16.png)</span><span class="sxs-lookup"><span data-stu-id="41cf2-158">[![Two Update All Buttons have been Added to the Page](performing-batch-updates-vb/_static/image17.png)](performing-batch-updates-vb/_static/image16.png)</span></span>

<span data-ttu-id="41cf2-159">**그림 6**: 페이지에 두 업데이트 모두 단추가 추가 되었습니다 ([전체 크기 이미지를 보려면 클릭](performing-batch-updates-vb/_static/image18.png))</span><span class="sxs-lookup"><span data-stu-id="41cf2-159">**Figure 6**: Two Update All Buttons have been Added to the Page ([Click to view full-size image](performing-batch-updates-vb/_static/image18.png))</span></span>


## <a name="step-3-updating-all-of-the-suppliers-address-information"></a><span data-ttu-id="41cf2-160">3 단계: 모든 공급 업체 주소 정보를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-160">Step 3: Updating All of the Suppliers Address Information</span></span>

<span data-ttu-id="41cf2-161">모든 DataList의 항목 편집 인터페이스를 표시 하 고 모든 업데이트 단추를 추가 하 여 계속이 일괄 처리 업데이트를 수행 하는 코드를 기록 하는 모든 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-161">With all of the DataList s items displaying the editing interface and with the addition of the Update All buttons, all that remains is writing the code to perform the batch update.</span></span> <span data-ttu-id="41cf2-162">특히, 해야 DataList의 항목 및 호출을 반복 하는 `SuppliersBLL` s 클래스 `UpdateSupplierAddress` 메서드 각각에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-162">Specifically, we need to loop through the DataList s items and call the `SuppliersBLL` class s `UpdateSupplierAddress` method for each one.</span></span>

<span data-ttu-id="41cf2-163">컬렉션 `DataListItem` DataList의 DataList를 통해 액세스할 수는 해당 구성을 인스턴스 [ `Items` 속성](https://msdn.microsoft.com/en-us/library/system.web.ui.webcontrols.datalist.items.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-163">The collection of `DataListItem` instances that makeup the DataList can be accessed via the DataList s [`Items` property](https://msdn.microsoft.com/en-us/library/system.web.ui.webcontrols.datalist.items.aspx).</span></span> <span data-ttu-id="41cf2-164">에 대 한 참조는 `DataListItem`, 해당을 잡고 수 `SupplierID` 에서 `DataKeys` 컬렉션 및 프로그래밍 방식으로 텍스트 웹 컨트롤 내 참조는 `ItemTemplate` 다음 코드와 같이:</span><span class="sxs-lookup"><span data-stu-id="41cf2-164">With a reference to a `DataListItem`, we can grab the corresponding `SupplierID` from the `DataKeys` collection and programmatically reference the TextBox Web controls within the `ItemTemplate` as the following code illustrates:</span></span>


[!code-vb[Main](performing-batch-updates-vb/samples/sample4.vb)]

<span data-ttu-id="41cf2-165">사용자가 모두 업데이트 단추 중 하나를 클릭는 `UpdateAllSupplierAddresses` 메서드는 각 반복 `DataListItem` 에 `Suppliers` DataList 및 호출은 `SuppliersBLL` s 클래스 `UpdateSupplierAddress` 메서드를 해당 값에서을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-165">When the user clicks one of the Update All buttons, the `UpdateAllSupplierAddresses` method iterates through each `DataListItem` in the `Suppliers` DataList and calls the `SuppliersBLL` class s `UpdateSupplierAddress` method, passing in the corresponding values.</span></span> <span data-ttu-id="41cf2-166">주소, 도시 또는 표준 국가 전달에 대 한 입력이 아닌 값의 값은 `Nothing` 를 `UpdateSupplierAddress` 는 데이터베이스의 결과입니다 (빈 문자열의 경우) 하는 대신 `NULL` 기본 s 레코드 필드에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-166">A non-entered value for address, city, or country passes is a value of `Nothing` to `UpdateSupplierAddress` (rather than a blank string), which results in a database `NULL` for the underlying record s fields.</span></span>

> [!NOTE]
> <span data-ttu-id="41cf2-167">향상 된 기능으로 일괄 처리 업데이트가 수행 된 후 몇 가지 확인 메시지가 제공 하는 페이지에 상태 Label 웹 컨트롤을 추가 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-167">As an enhancement, you may want to add a status Label Web control to the page that provides some confirmation message after the batch update is performed.</span></span>


## <a name="updating-only-those-addresses-that-have-been-modified"></a><span data-ttu-id="41cf2-168">수정 된 주소에만 업데이트</span><span class="sxs-lookup"><span data-stu-id="41cf2-168">Updating Only Those Addresses That Have Been Modified</span></span>

<span data-ttu-id="41cf2-169">이 자습서 호출에 사용 되는 일괄 처리 업데이트 알고리즘은 `UpdateSupplierAddress` 방법을 *모든* 자신의 주소 정보가 변경 되었는지 여부에 관계 없이 DataList의 공급 업체.</span><span class="sxs-lookup"><span data-stu-id="41cf2-169">The batch update algorithm used for this tutorial calls the `UpdateSupplierAddress` method for *every* supplier in the DataList, regardless of whether their address information has been changed.</span></span> <span data-ttu-id="41cf2-170">이러한 blind 클라우드에 없는 t 일반적으로 성능 문제를 업데이트 하는 동안 감사 된 데이터베이스 테이블에 변경 되 면 불필요 한 레코드를 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-170">While such blind updates aren t usually a performance issue, they can lead to superfluous records if you re auditing changes to the database table.</span></span> <span data-ttu-id="41cf2-171">예를 들어, 트리거를 사용 하 여 모든 기록 `UPDATE` s는 `Suppliers` 사용자 모든 했는지 여부에 관계 없이 시스템의 각 공급 업체에 대 한 새 감사 레코드를 만들 수는 모두 업데이트 단추를 클릭할 때마다 감사 테이블에 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-171">For example, if you use triggers to record all `UPDATE` s to the `Suppliers` table to an auditing table, every time a user clicks the Update All button a new audit record will be created for each supplier in the system, regardless of whether the user made any changes.</span></span>

<span data-ttu-id="41cf2-172">ADO.NET DataTable 및 데이터 어댑터 클래스는 여기서만 수정, 삭제 및 새 레코드 데이터베이스 통신으로 인해 일괄 처리 업데이트를 지원 하도록 설계 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-172">The ADO.NET DataTable and DataAdapter classes are designed to support batch updates where only modified, deleted, and new records results in any database communication.</span></span> <span data-ttu-id="41cf2-173">DataTable의 각 행에는 [ `RowState` 속성](https://msdn.microsoft.com/en-us/library/system.data.datarow.rowstate.aspx) 하는 행에서 수정, 삭제 하는 DataTable에 추가 되었습니다 그대로 유지 하는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-173">Each row in the DataTable has a [`RowState` property](https://msdn.microsoft.com/en-us/library/system.data.datarow.rowstate.aspx) that indicates whether the row has been added to the DataTable, deleted from it, modified, or remains unchanged.</span></span> <span data-ttu-id="41cf2-174">처음 DataTable 채워지면, 모든 행 변경 되지 않은 상태로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-174">When a DataTable is initially populated, all rows are marked unchanged.</span></span> <span data-ttu-id="41cf2-175">수정 된 행을 표시 행 s 열의 모든 값을 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-175">Changing the value of any of the row s columns marks the row as modified.</span></span>

<span data-ttu-id="41cf2-176">에 `SuppliersBLL` 클래스에 단일 공급 업체 레코드에 대 한 첫 번째 읽기 하 여 지정 된 공급자의 주소 정보 업데이트는 `SuppliersDataTable` 로 설정한는 `Address`, `City`, 및 `Country` 다음 코드를 사용 하 여 열 값:</span><span class="sxs-lookup"><span data-stu-id="41cf2-176">In the `SuppliersBLL` class we update the specified supplier s address information by first reading in the single supplier record into a `SuppliersDataTable` and then set the `Address`, `City`, and `Country` column values using the following code:</span></span>


[!code-vb[Main](performing-batch-updates-vb/samples/sample5.vb)]

<span data-ttu-id="41cf2-177">이 코드에서는 아무렇게나 전달 된 주소, 도시와 국가 값을 할당는 `SuppliersRow` 에 `SuppliersDataTable` 값이 변경 되었는지 여부에 관계 없이 합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-177">This code naively assigns the passed-in address, city, and country values to the `SuppliersRow` in the `SuppliersDataTable` regardless of whether or not the values have changed.</span></span> <span data-ttu-id="41cf2-178">이러한 수정 된 `SuppliersRow` s `RowState` 속성을 수정 하는 것으로 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-178">These modifications cause the `SuppliersRow` s `RowState` property to be marked as modified.</span></span> <span data-ttu-id="41cf2-179">때 데이터 액세스 계층 s `Update` 메서드를 호출 하 게 표시는 `SupplierRow` 수정 된 하 고 따라서 보냅니다는 `UPDATE` 명령을 데이터베이스에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-179">When the Data Access Layer s `Update` method is called, it sees that the `SupplierRow` has been modified and therefore sends an `UPDATE` command to the database.</span></span>

<span data-ttu-id="41cf2-180">그러나 가정,만에서 다를 경우 전달 된 주소, 도시, 및 국가 값을 할당 하려면이 메서드를 코드를 추가 했습니다는 `SuppliersRow` s 기존 값입니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-180">Imagine, however, that we added code to this method to only assign the passed-in address, city, and country values if they differ from the `SuppliersRow` s existing values.</span></span> <span data-ttu-id="41cf2-181">주소, 도시와 국가 동일한 있는 기존 데이터와의 경우 변경 되지 것입니다 수 및 `SupplierRow` s `RowState` 왼쪽으로 표시 된 그대로 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-181">In the case where the address, city, and country are the same as the existing data, no changes will be made and the `SupplierRow` s `RowState` will be left marked as unchanged.</span></span> <span data-ttu-id="41cf2-182">결과 하는 경우 DAL s `Update` 메서드가 호출 되 면 없는 데이터베이스 전화 걸 수 때문에 `SuppliersRow` 수정 되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-182">The net result is that when the DAL s `Update` method is called, no database call will be made because the `SuppliersRow` has not been modified.</span></span>

<span data-ttu-id="41cf2-183">이 변경을 적용할 맹목적으로 전달 된 주소, 도시, 및 다음 코드를 사용 하 여 국가 값을 할당 하는 문을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-183">To enact this change, replace the statements that blindly assign the passed-in address, city, and country values with the following code:</span></span>


[!code-vb[Main](performing-batch-updates-vb/samples/sample6.vb)]

<span data-ttu-id="41cf2-184">이 코드에서는 DAL s 추가 `Update` 메서드 보냅니다는 `UPDATE` 주소와 관련 된 값이 변경 된 레코드에 대 한 데이터베이스에 문의 합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-184">With this added code, the DAL s `Update` method sends an `UPDATE` statement to the database for only those records whose address-related values have changed.</span></span>

<span data-ttu-id="41cf2-185">또는 우리 수 추적 데이터베이스 데이터 및 전달 된 주소 필드 사이 차이가 있는지 여부를 확인 하 고, none, 없는 경우 DAL s에 대 한 호출을 무시 하기만 하면 `Update` 메서드.</span><span class="sxs-lookup"><span data-stu-id="41cf2-185">Alternatively, we could keep track of whether there are any differences between the passed-in address fields and the database data and, if there are none, simply bypass the call to the DAL s `Update` method.</span></span> <span data-ttu-id="41cf2-186">이 방법을 사용 하면 DB를 사용 하 여 다시 직접적인 방법, DB 직접적인 방법 되지 않으면 전달 된 경우에 적합 한 `SuppliersRow` 인스턴스입니다 `RowState` 데이터베이스 호출에 실제로 필요한 지 여부를 확인 하려면 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-186">This approach works well if you re using the DB direct method, since the DB direct method isn t passed a `SuppliersRow` instance whose `RowState` can be checked to determine whether a database call is actually needed.</span></span>

> [!NOTE]
> <span data-ttu-id="41cf2-187">될 때마다는 `UpdateSupplierAddress` 메서드가 호출 되 면 업데이트 된 레코드에 대 한 정보를 검색할 데이터베이스에 대 한 호출 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-187">Each time the `UpdateSupplierAddress` method is invoked, a call is made to the database to retrieve information about the updated record.</span></span> <span data-ttu-id="41cf2-188">그런 다음 데이터의 변경 사항이 데이터베이스에 대 한 호출이 테이블 행을 업데이트 하기 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-188">Then, if there are any changes in data, another call to the database is made to update the table row.</span></span> <span data-ttu-id="41cf2-189">이 워크플로 만들어 최적화할 수 있습니다는 `UpdateSupplierAddress` 허용 하는 메서드 오버 로드는 `EmployeesDataTable` 있는 인스턴스에 *모든* 로부터 변경 내용는 `BatchUpdate.aspx` 페이지.</span><span class="sxs-lookup"><span data-stu-id="41cf2-189">This workflow could be optimized by creating an `UpdateSupplierAddress` method overload that accepts an `EmployeesDataTable` instance that has *all* of the changes from the `BatchUpdate.aspx` page.</span></span> <span data-ttu-id="41cf2-190">그런 다음 레코드를 모두 가져오려면 데이터베이스에 한 번의 호출을 만들 수는 것은 `Suppliers` 테이블입니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-190">Then, it could make one call to the database to get all of the records from the `Suppliers` table.</span></span> <span data-ttu-id="41cf2-191">두 개의 결과 집합을 열거할 수 다음 하 고 변경 레코드에만 업데이트할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-191">The two resultsets could then be enumerated and only those records where changes have occurred could be updated.</span></span>


## <a name="summary"></a><span data-ttu-id="41cf2-192">요약</span><span class="sxs-lookup"><span data-stu-id="41cf2-192">Summary</span></span>

<span data-ttu-id="41cf2-193">이 자습서에서는 사용자가 신속 하 게 여러 공급자에 대 한 주소 정보를 수정 하는 완벽 하 게 편집할 DataList를 만드는 방법에 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-193">In this tutorial we saw how to create a fully editable DataList, allowing a user to quickly modify the address information for multiple suppliers.</span></span> <span data-ttu-id="41cf2-194">DataList s에서에서 공급 업체의 주소, 도시, 및 국가 값에 대 한 TextBox 웹 컨트롤 편집 인터페이스를 정의 하 여을 시작 했습니다. `ItemTemplate`합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-194">We started by defining the editing interface a TextBox Web control for the supplier s address, city, and country values in the DataList s `ItemTemplate`.</span></span> <span data-ttu-id="41cf2-195">다음으로, 위쪽 및 아래쪽 DataList 모두 업데이트 단추를 추가 했습니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-195">Next, we added Update All buttons above and below the DataList.</span></span> <span data-ttu-id="41cf2-196">사용자가 자신의 변경 작업을 수행 하 고 모두 업데이트 단추 중 하나를 클릭 한 후는 `DataListItem` s 열거를 호출 하는 `SuppliersBLL` s 클래스 `UpdateSupplierAddress` 메서드 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-196">After a user has made his changes and clicked one of the Update All buttons, the `DataListItem` s are enumerated and a call to the `SuppliersBLL` class s `UpdateSupplierAddress` method is made.</span></span>

<span data-ttu-id="41cf2-197">만족도 매우 프로그래밍!</span><span class="sxs-lookup"><span data-stu-id="41cf2-197">Happy Programming!</span></span>

## <a name="about-the-author"></a><span data-ttu-id="41cf2-198">작성자 정보</span><span class="sxs-lookup"><span data-stu-id="41cf2-198">About the Author</span></span>

<span data-ttu-id="41cf2-199">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), 7 ASP/ASP.NET 서적과의 창립자의 작성자 [4GuysFromRolla.com](http://www.4guysfromrolla.com), 1998 이후 Microsoft 웹 기술과 함께 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-199">[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), author of seven ASP/ASP.NET books and founder of [4GuysFromRolla.com](http://www.4guysfromrolla.com), has been working with Microsoft Web technologies since 1998.</span></span> <span data-ttu-id="41cf2-200">Scott 독립 컨설턴트, 강사, 기술 및 작성기 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-200">Scott works as an independent consultant, trainer, and writer.</span></span> <span data-ttu-id="41cf2-201">그의 최신 서적은 [ *Sam 업무량이 직접 ASP.NET 2.0 24 시간 동안에서*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-201">His latest book is [*Sams Teach Yourself ASP.NET 2.0 in 24 Hours*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco).</span></span> <span data-ttu-id="41cf2-202">에 연결할 수 그 [ mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) 에서 찾을 수 있는 그의 블로그를 통해 또는 [http://ScottOnWriting.NET](http://ScottOnWriting.NET)합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-202">He can be reached at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) or via his blog, which can be found at [http://ScottOnWriting.NET](http://ScottOnWriting.NET).</span></span>

## <a name="special-thanks-to"></a><span data-ttu-id="41cf2-203">특별히 감사</span><span class="sxs-lookup"><span data-stu-id="41cf2-203">Special Thanks To</span></span>

<span data-ttu-id="41cf2-204">이 자습서 시리즈 많은 유용한 검토자가 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-204">This tutorial series was reviewed by many helpful reviewers.</span></span> <span data-ttu-id="41cf2-205">이 자습서에 대 한 선행 검토자 Zack Jones 및 켄 Pespisa 했습니다.</span><span class="sxs-lookup"><span data-stu-id="41cf2-205">Lead reviewers for this tutorial were Zack Jones and Ken Pespisa.</span></span> <span data-ttu-id="41cf2-206">향후 내 MSDN 문서를 검토에 관심이 있으십니까?</span><span class="sxs-lookup"><span data-stu-id="41cf2-206">Interested in reviewing my upcoming MSDN articles?</span></span> <span data-ttu-id="41cf2-207">이 경우 drop me에 한 줄씩 [ mitchell@4GuysFromRolla.com합니다.](mailto:mitchell@4GuysFromRolla.com)</span><span class="sxs-lookup"><span data-stu-id="41cf2-207">If so, drop me a line at [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)</span></span>

>[!div class="step-by-step"]
<span data-ttu-id="41cf2-208">[이전](an-overview-of-editing-and-deleting-data-in-the-datalist-vb.md)
[다음](handling-bll-and-dal-level-exceptions-vb.md)</span><span class="sxs-lookup"><span data-stu-id="41cf2-208">[Previous](an-overview-of-editing-and-deleting-data-in-the-datalist-vb.md)
[Next](handling-bll-and-dal-level-exceptions-vb.md)</span></span>