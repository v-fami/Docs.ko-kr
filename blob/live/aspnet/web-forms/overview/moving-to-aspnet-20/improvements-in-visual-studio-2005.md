---
uid: web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
title: "Visual Studio 2005의 개선 사항 | Microsoft Docs"
author: microsoft
description: "Visual Studio 2005 웹 응용 프로그램 개발자에 향상 된 기능 및 향상 된 웹 프로젝트에 긴 목록 제공합니다."
ms.author: aspnetcontent
manager: wpickett
ms.date: 02/20/2005
ms.topic: article
ms.assetid: 72d90cd0-b3d9-454c-b2eb-ed0d9812f32c
ms.technology: dotnet-webforms
ms.prod: .net-framework
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/improvements-in-visual-studio-2005
msc.type: authoredcontent
ms.openlocfilehash: 2c1f9a7291d8eab675bac3e1c37d6922131e3761
ms.sourcegitcommit: 9a9483aceb34591c97451997036a9120c3fe2baf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/10/2017
---
<a name="improvements-in-visual-studio-2005"></a><span data-ttu-id="0787b-103">Visual Studio 2005의 향상 된 기능</span><span class="sxs-lookup"><span data-stu-id="0787b-103">Improvements in Visual Studio 2005</span></span>
====================
<span data-ttu-id="0787b-104">여 [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="0787b-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="0787b-105">Visual Studio 2005 웹 응용 프로그램 개발자에 향상 된 기능 및 향상 된 웹 프로젝트에 긴 목록 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-105">Visual Studio 2005 provides Web application developers with a long list of improvements and enhancements to Web projects.</span></span>


<span data-ttu-id="0787b-106">Visual Studio 2005 웹 응용 프로그램 개발자에 향상 된 기능 및 향상 된 웹 프로젝트에 긴 목록 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-106">Visual Studio 2005 provides Web application developers with a long list of improvements and enhancements to Web projects.</span></span> <span data-ttu-id="0787b-107">강력 하지만 Visual Studio.NET 2002 및 2003은, 많은 불만 사항에에서 있었습니다 웹 프로젝트 된 처리 하는 방식.</span><span class="sxs-lookup"><span data-stu-id="0787b-107">As powerful as Visual Studio .NET 2002 and 2003 are, there were many complaints in the way that Web projects were handled.</span></span> <span data-ttu-id="0787b-108">Visual Studio 2005 이러한 불만 사항 해결 하는 데 많은 새 기능을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-108">Visual Studio 2005 adds a significant number of new features in order to address these complaints.</span></span> <span data-ttu-id="0787b-109">Visual Studio.NET 2003 웹 응용 프로그램의 컴파일을 처리 하는 방식을 선호 하는, 참조 [웹 응용 프로그램 프로젝트](https://go.microsoft.com/fwlink/?LinkId=57870)합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-109">For those who prefer the way that Visual Studio .NET 2003 handled compilation of Web applications, see [Web Application Projects](https://go.microsoft.com/fwlink/?LinkId=57870).</span></span>

<span data-ttu-id="0787b-110">이 모듈에서는 잘 웹 프로젝트 생성, 관리 및 개발의 향상 된 기능을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-110">In this module, well cover improvements in Web project creation, management, and development.</span></span> <span data-ttu-id="0787b-111">이후 단원에서 웹 프로젝트를 빌드하고 배포 하기의 개선 사항도 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-111">In a later module, well cover improvements in building Web projects and deploying them.</span></span>

## <a name="frontpage-server-extensions"></a><span data-ttu-id="0787b-112">FrontPage Server Extensions</span><span class="sxs-lookup"><span data-stu-id="0787b-112">FrontPage Server Extensions</span></span>

<span data-ttu-id="0787b-113">Visual Studio.NET 2002 및 2003 FrontPage Server Extensions 상자에서 만들거나 웹 프로젝트를 작성 하기 위해 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-113">Visual Studio .NET 2002 and 2003 required FrontPage Server Extensions on the box in order to create or build Web projects.</span></span> <span data-ttu-id="0787b-114">개발자는 두 가지 서로 다른 액세스 모드 (FrontPage Server Extensions 또는 파일 액세스 모드) 사이 선택을, 모두 FrontPage Server Extensions IIS 등의 응용 프로그램 루트를 설정 하는 등 작업을 수행 하는 데 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-114">Developers did have a choice between two different access modes (FrontPage Server Extensions or File access mode), both used FrontPage Server Extensions to perform tasks such as setting the application root in IIS, etc.</span></span>

<span data-ttu-id="0787b-115">Visual Studio 2005 로컬 프로젝트에 대 한 범주에 대 한 의존도 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-115">Visual Studio 2005 removes the reliance on FrontPage Server Extensions for local projects.</span></span> <span data-ttu-id="0787b-116">Visual Studio 2005는 이제 IIS 메타 베이스 FrontPage Server Extensions를 사용 하는 대신 직접 액세스 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-116">Visual Studio 2005 now accesses the IIS metabase directly instead of using the FrontPage Server Extensions.</span></span> <span data-ttu-id="0787b-117">Visual Studio 2005는 또한 FrontPage Server Extensions를 요구 하지 않고 원격 프로젝트 액세스를 허용 하는 FTP에 대 한 지원을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-117">Visual Studio 2005 also adds support for FTP which allows for remote project access without requiring FrontPage Server Extensions.</span></span>

<span data-ttu-id="0787b-118">해당 프로젝트에서 FrontPage Server Extensions를 사용 하려는 개발자는 옵션은 계속 사용할 수입니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-118">For those developers who want to use FrontPage Server Extensions in their projects, the option is still available.</span></span> <span data-ttu-id="0787b-119">그러나 강력한 ASP.NET 개발자 커뮤니티 피드백에 따라는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-119">However, based upon strong feedback from the ASP.NET developer community, it is not a requirement.</span></span>

> [!NOTE]
> <span data-ttu-id="0787b-120">FrontPage Server Extensions가 원격 프로젝트 만들기, 열기 등 여전히 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-120">FrontPage Server Extensions are still required for remote project creation, opening, etc.</span></span>


## <a name="aspnet-development-server"></a><span data-ttu-id="0787b-121">ASP.NET Development Server</span><span class="sxs-lookup"><span data-stu-id="0787b-121">ASP.NET Development Server</span></span>

<span data-ttu-id="0787b-122">Visual Studio 2005 ASP.NET 개발 서버를 호출 하는 새 웹 서버와 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-122">Visual Studio 2005 ships with a new Web server called ASP.NET Development Server.</span></span> <span data-ttu-id="0787b-123">(이 웹 서버를 이전에 Cassini.)</span><span class="sxs-lookup"><span data-stu-id="0787b-123">(This Web server was previously known as Cassini.)</span></span>

<span data-ttu-id="0787b-124">ASP.NET Development Server의 다양 한 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-124">There are several benefits of the ASP.NET Development Server.</span></span>

- <span data-ttu-id="0787b-125">관리자가 아닌 사용자도 개발 하 고 웹 서버 디버깅에 대 한 가능한 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-125">It is now possible for non-Administrators to develop and debug against a Web server.</span></span>
- <span data-ttu-id="0787b-126">ASP.NET 개발 서버는 동적으로 유연한 프로젝트 위치에 대 한 허용 하는 파일 시스템의 모든 위치에 가상 디렉터리를 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-126">The ASP.NET Development Server dynamically maps virtual directories to any location in the file system allowing for flexible project locations.</span></span>
- <span data-ttu-id="0787b-127">Windows XP Professional에 IIS를 이미 사용 중인 사용자는 이제 IIS에서 기본 웹 사이트의 파일 또는 폴더 구조에 영향을 주지 않는 새 웹 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-127">Users on Windows XP Professional who are already using IIS will now be able to create new Web applications that will not affect the file or folder structure of their Default Web Site in IIS.</span></span>

<span data-ttu-id="0787b-128">ASP.NET 개발 서버를 활용 하기 위해 특별 한 구성이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-128">No special configuration is required to take advantage of the ASP.NET Development Server.</span></span> <span data-ttu-id="0787b-129">파일 시스템에서 호스팅되는 웹 프로젝트를 디버깅 하거나 검색할 때 Visual Studio 2005는 임의의 포트에서 요청 서비스에서 ASP.NET 개발 서버 인스턴스의 자동 시작 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-129">When a Web project that is hosted on the file system is debugged or browsed, Visual Studio 2005 will automatically start an instance of the ASP.NET Development Server on a random port to service the request.</span></span>

<span data-ttu-id="0787b-130">이 모듈의 뒷부분에 나오는 ASP.NET 개발 서버에서 자세한 정보를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-130">More information will be covered on the ASP.NET Development Server later in this module.</span></span>

## <a name="improved-file-management"></a><span data-ttu-id="0787b-131">향상 된 파일 관리</span><span class="sxs-lookup"><span data-stu-id="0787b-131">Improved File Management</span></span>

<span data-ttu-id="0787b-132">Visual Studio 2002 및 2003에서 프로젝트 파일 (VB.NET에 대 한.vbproj) 및 C#에 대 한.csproj 웹 응용 프로그램의 모든 파일에 정보를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-132">In Visual Studio 2002 and 2003, a project file (.vbproj for VB.NET and .csproj for C#) stored information on all files in the Web application.</span></span> <span data-ttu-id="0787b-133">솔루션 탐색기 표시 프로젝트 파일의 파일 정보를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-133">The Solution Explorer display is based upon the file information in the project file.</span></span> <span data-ttu-id="0787b-134">이 인해 솔루션 탐색기 외부 편집기 사용 된 경우에 종종 잘못 된 정보가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-134">Because of this, the Solution Explorer would often display inaccurate information in cases where external editors were used.</span></span> <span data-ttu-id="0787b-135">Visual Studio 2002 및 2003은 종종 파일 변경 내용을 덮어쓰거나 파일의 최신 버전을 표시 하지.</span><span class="sxs-lookup"><span data-stu-id="0787b-135">Visual Studio 2002 and 2003 would often overwrite file changes or not display the most recent version of files.</span></span>

<span data-ttu-id="0787b-136">Visual Studio 2005에서는 프로젝트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-136">Visual Studio 2005 does away with the project file.</span></span> <span data-ttu-id="0787b-137">대신, 파일 및 폴더 정보는 정확 하 게 프로젝트의 파일 표시에 디스크에서 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-137">Instead, it reads the file and folder information directly from the disk, resulting in an accurate display of the files in your project.</span></span> <span data-ttu-id="0787b-138">Visual Studio 2002 및 2003의 참조 폴더는 웹 응용 프로그램에서 실제 폴더를 나타내지 않습니다 때문에 Visual Studio 2005 솔루션 탐색기에서 References 폴더를도 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-138">Because the References folder in Visual Studio 2002 and 2003 does not represent an actual folder in your Web application, Visual Studio 2005 also removes the References folder from Solution Explorer.</span></span> <span data-ttu-id="0787b-139">Visual Studio 2005에서 프로젝트에 대 한 참조에 액세스 하려면 프로젝트에 대 한 속성 페이지를 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-139">To access the references for your project in Visual Studio 2005, you should use the Property pages for the project.</span></span>

## <a name="creating-web-projects"></a><span data-ttu-id="0787b-140">웹 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="0787b-140">Creating Web Projects</span></span>

<span data-ttu-id="0787b-141">웹 개발자가 Visual Studio 2005에서 프로젝트를 만드는 데 사용할 수 있는 여러 가지 새로운 옵션 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-141">Web developers have many new options available for project creation in Visual Studio 2005.</span></span> <span data-ttu-id="0787b-142">웹 사이트는 파일 시스템에서 아무 곳 이나 지금 만들 수 있습니다 및 다음 디버깅할 수 있습니다 또는 새 ASP.NET 개발 서버를 사용 하 여 찾아볼 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-142">Web sites can now be created anywhere in the file system and can then be debugged or browsed using the new ASP.NET Development Server.</span></span> <span data-ttu-id="0787b-143">개발자는 FTP를 사용 하 여 새 웹 사이트를 만들 수도 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-143">Developers can also create new Web sites using FTP.</span></span>

<span data-ttu-id="0787b-144">Visual Studio 2005에서 웹 프로젝트를 만드는 연습 동영상을 보려면 여기를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-144">Click here to view a video walkthrough of creating Web projects in Visual Studio 2005.</span></span>


![](improvements-in-visual-studio-2005/_static/image1.png)


[<span data-ttu-id="0787b-145">전체 화면 비디오 열기</span><span class="sxs-lookup"><span data-stu-id="0787b-145">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/creating_projects1.wmv)


### <a name="file-system-projects"></a><span data-ttu-id="0787b-146">파일 시스템 프로젝트</span><span class="sxs-lookup"><span data-stu-id="0787b-146">File System Projects</span></span>

<span data-ttu-id="0787b-147">동영상 연습에서 살펴본 것 처럼 또는 로컬 컴퓨터에서 파일 공유를 통해 원격 위치에서 파일 시스템에 웹 사이트를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-147">As you saw in the video walkthrough, you can choose to create Web sites on the file system either on the local machine or on a remote location via a file share.</span></span> <span data-ttu-id="0787b-148">파일 시스템에서 생성 된 웹 사이트를 찾는 및 ASP.NET 개발 서버를 사용 하 여 디버깅 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-148">Web sites that are created on the file system are browsed and debugged using the ASP.NET Development Server.</span></span>

> [!NOTE]
> <span data-ttu-id="0787b-149">ASP.NET 개발 서버는 고객에 대 한 일부 혼란이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-149">The ASP.NET Development Server may cause some confusion for customers.</span></span> <span data-ttu-id="0787b-150">웹 프로젝트를 IISs 디렉터리 구조 (예: c:\inetpub\wwwroot)에 파일 시스템에 생성 하는 경우 웹 사이트 여전히 Visual Studio 2005 내에서 시작 하는 경우 ASP.NET 개발 서버를 통해 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-150">If a Web project is created on the file system in IISs directory structure (i.e. c:\inetpub\wwwroot), the Web site will still be browsed via the ASP.NET Development Server when launched from within Visual Studio 2005.</span></span> <span data-ttu-id="0787b-151">따라서 모든 IIS 구성 (즉, 인증 방법) 적용 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-151">Therefore, any IIS configuration (i.e. authentication methods) is not applicable.</span></span>


<span data-ttu-id="0787b-152">기본 웹 프로젝트도 많이 제거 하 여 오버 헤드의 포함 Default.aspx 페이지, default.cs 파일 및 앱\_데이터 폴더.</span><span class="sxs-lookup"><span data-stu-id="0787b-152">The default web project also removes a lot of the overhead by only includes a Default.aspx page, default.cs file, and an App\_Data folder.</span></span> <span data-ttu-id="0787b-153">Web.config 및 특수 폴더 (예: 앱\_코드) 필요에 따라 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-153">The web.config and special folders (i.e. app\_code) are added as they are needed.</span></span> <span data-ttu-id="0787b-154">웹 프로젝트 파일 및 필요한 폴더에만 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-154">Your web project only includes the files and folders that you need.</span></span>

### <a name="http-projects"></a><span data-ttu-id="0787b-155">HTTP 프로젝트</span><span class="sxs-lookup"><span data-stu-id="0787b-155">HTTP Projects</span></span>

<span data-ttu-id="0787b-156">HTTP 프로젝트 원격 웹 사이트 또는 로컬 IIS 웹 사이트에서 만들어진 프로젝트에 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-156">HTTP projects can either be projects that are created on a local IIS Web site or on a remote Web site.</span></span> <span data-ttu-id="0787b-157">기본 프로젝트 위치는 `http://localhost`합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-157">The default project location is `http://localhost`.</span></span> <span data-ttu-id="0787b-158">찾아보기 단추를 누르면 방법은 두 가지 HTTP: 로컬 IIS 및 원격 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-158">If you click the Browse button, there are two HTTP options: Local IIS and Remote Site.</span></span> <span data-ttu-id="0787b-159">이러한 두 옵션의 주요 차이점은 웹 사이트 정보 파일이 웹 서버에 복사 되는 방법 및 위치 선택 대화 상자에서 표시 되는 메서드.</span><span class="sxs-lookup"><span data-stu-id="0787b-159">The main difference in these two options is the method in which the web site information is displayed in the Choose Location dialog and in how the files are copied to the Web server.</span></span>

<span data-ttu-id="0787b-160">로컬 IIS 옵션 로컬 컴퓨터에서 메타 베이스에서 사이트 정보를 읽고 및 파일 시스템을 사용 하 여 파일이 복사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-160">The Local IIS option reads the site information from the metabase on the local machine and files are copied using the file system.</span></span> <span data-ttu-id="0787b-161">원격 사이트 옵션 FrontPage Server Extensions 이름과 사이트 정보를 사용 하 고 HTTP를 사용 하 여 파일은 복사 하 고 FrontPage Server Extensions RPC 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-161">The Remote Site option uses the FrontPage Server Extensions and the site information and files are copied using HTTP and FrontPage Server Extensions RPC calls.</span></span>

> [!NOTE]
> <span data-ttu-id="0787b-162">Vs #\_tmp.htm 파일 및 get\_aspx\_ver.aspx는 더 이상 버전 정보를 확인 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-162">The vs###\_tmp.htm file and get\_aspx\_ver.aspx are no longer used to determine version information.</span></span>


<span data-ttu-id="0787b-163">기본 HTTP 방법은 로컬 IIS입니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-163">The default HTTP option is Local IIS.</span></span> <span data-ttu-id="0787b-164">이 옵션을 사용할 수 있는 사이트를 확인 하려면 IIS 메타 베이스 및 콘텐츠 생성 될 위치 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-164">This option reads the IIS Metabase to determine which sites are available and the location in which to create content.</span></span> <span data-ttu-id="0787b-165">트리 뷰에서 선택 하 여 다른 폴더 또는 가상 디렉터리를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-165">You can select a different folder or virtual directory by selecting it in the tree view.</span></span> <span data-ttu-id="0787b-166">있습니다 수도 새 가상 디렉터리 만들기, 폴더, 응용 프로그램으로 표시으로이 대화 상자에서 기존 가상 디렉터리를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-166">You can also create a new virtual directory, mark folders as applications, as well as delete existing virtual directories from this dialog box.</span></span>


![위치 대화 상자를 선택 합니다.](improvements-in-visual-studio-2005/_static/image1.gif)

<span data-ttu-id="0787b-168">**그림 1**:는 위치 대화 상자를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-168">**Figure 1**: The Choose Location Dialog</span></span>


<span data-ttu-id="0787b-169">와 달리 이전 버전의 Visual Studio를 선택 하는 경우에 **Secure Sockets Layer** 경우 요청 하는 보안 경고 대화 상자가 표시 됩니다, 확인란을 선택 하 고 SSL 인증서를 찾는 URL을 일치 하지 않습니다 계속 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-169">Unlike in earlier versions of Visual Studio, if you check the **Use Secure Sockets Layer** checkbox and the SSL certificate does not match the URL you are browsing, you will be presented with a Security Alert dialog asking you if you would like to proceed.</span></span> <span data-ttu-id="0787b-170">Visual Studio.NET 2003을 사용 하 여 사용 된 인증서 나와 일치 하는 경우, 프로젝트 만들기 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-170">Using Visual Studio .NET 2003, if the certificate was not a matching one, creating the project would fail.</span></span>


![보안 경고에 대 한 SSL 인증서](improvements-in-visual-studio-2005/_static/image2.gif)

<span data-ttu-id="0787b-172">**그림 2**: SSL 인증서에 대 한 보안 경고</span><span class="sxs-lookup"><span data-stu-id="0787b-172">**Figure 2**: Security Alert Regarding SSL Certificate</span></span>


### <a name="note-on-host-headers"></a><span data-ttu-id="0787b-173">호스트 헤더에 대 한 참고</span><span class="sxs-lookup"><span data-stu-id="0787b-173">Note on Host Headers</span></span>

<span data-ttu-id="0787b-174">특정 IP에 바인딩된 사이트에서 웹 응용 프로그램을 만드는 경우에 호스트 헤더 구성 되어 있는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-174">If you are creating a Web application on a site bound to a specific IP, you will need to ensure that a host header is configured.</span></span> <span data-ttu-id="0787b-175">그렇지 않으면 Visual Studio에서 사이트 만듭니다 `http://localhost`, 하지만 사이트는를 탐색 하거나 IDE 내에서 디버깅 하는 경우 IP 주소가 올바르게 확인 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-175">Otherwise, Visual Studio will create the site at `http://localhost`, but the IP address will not resolve correctly when the site is browsed or debugged from within the IDE.</span></span>

<span data-ttu-id="0787b-176">원격 사이트 옵션을 선택 하면 대화 상자를 새 웹 사이트에 대 한 대상 URL을 입력할 수로 변경 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-176">If you select the Remote Site option, the dialog changes to allow you to enter the destination URL for the new Web site.</span></span> <span data-ttu-id="0787b-177">이 URL에 FrontPage Server Extensions 사용 하도록 설정 하는 서버에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-177">This URL must be on a server that has the FrontPage Server Extensions enabled.</span></span> <span data-ttu-id="0787b-178">FrontPage Server Extensions를 사용 하 여 로컬 웹 서버와 함께 작업 하려는 경우 원격 사이트 옵션을 사용할 수 있으며 로컬 URL을 지정.</span><span class="sxs-lookup"><span data-stu-id="0787b-178">If you want to work with your local Web server using the FrontPage Server Extensions, you can use the Remote Site option and specify a local URL.</span></span>


![원격 서버에 웹 사이트 만들기](improvements-in-visual-studio-2005/_static/image1.jpg)

<span data-ttu-id="0787b-180">**그림 3**: 원격 서버에 웹 사이트 만들기</span><span class="sxs-lookup"><span data-stu-id="0787b-180">**Figure 3**: Creating a Web Site on a Remote Server</span></span>


<span data-ttu-id="0787b-181">를 만들 때 응용 프로그램 SSL 통해 원격 사이트에 SSL 인증서와 일치 하지 않으면 확인 대화 상자에서 로컬 IIS 옵션을 사용 하는 경우 표시 대화 상자 보다 약간 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-181">When creating an application on a remote site via SSL, if the SSL certificate does not match, the confirmation dialog is slightly different than the dialog displayed when using the Local IIS option.</span></span>


![원격 사이트 보안 경고](improvements-in-visual-studio-2005/_static/image3.gif)

<span data-ttu-id="0787b-183">**그림 4**: 원격 사이트 보안 경고</span><span class="sxs-lookup"><span data-stu-id="0787b-183">**Figure 4**: The Remote Site Security Alert</span></span>


<a id="_Toc116100243"></a>

#### <a name="ftp"></a><span data-ttu-id="0787b-184">FTP</span><span class="sxs-lookup"><span data-stu-id="0787b-184">FTP</span></span>

<span data-ttu-id="0787b-185">Visual Studio 2005에서는 FTP 통해 웹 사이트를 만드는 옵션을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-185">Visual Studio 2005 introduces the option to create Web sites via FTP.</span></span> <span data-ttu-id="0787b-186">이 옵션을 사용 하면 IDE는 사용자가 임시 폴더에 파일을 로컬로 만듭니다 하 고 FTP를 사용 하 여 FTP 위치에 파일을 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-186">When you use this option, the IDE creates the files locally in the users temp folder and then uses FTP to move the files to the FTP location.</span></span>

> [!NOTE]
> <span data-ttu-id="0787b-187">임시 폴더 위치는 c:\Documents and Settings\&lt; 사용자&gt;\Local Settings\Temp\VWDWebCache\&lt; 서버&gt;\_&lt;응용 프로그램 이름&gt;</span><span class="sxs-lookup"><span data-stu-id="0787b-187">The temp folder location is c:\Documents and Settings\&lt;User&gt;\Local Settings\Temp\VWDWebCache\&lt;Server&gt;\_&lt;application name&gt;</span></span>


<span data-ttu-id="0787b-188">FTP 옵션을 사용할 경우 위치 선택 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-188">When using the FTP option, you will be presented with a Choose Location dialog.</span></span> <span data-ttu-id="0787b-189">아래와 같이이 대화 상자에 필요한 FTP 연결 정보를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-189">You enter the required FTP connection information into this dialog as shown below.</span></span>


![FTP에 대 한 위치 대화 상자를 선택 합니다.](improvements-in-visual-studio-2005/_static/image2.jpg)

<span data-ttu-id="0787b-191">**그림 5**:는 FTP에 대 한 위치 대화 상자를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-191">**Figure 5**: The Choose Location Dialog for FTP</span></span>


## <a name="lab-setup-ftp-site-and-create-a-project"></a><span data-ttu-id="0787b-192">랩: 설정 FTP 사이트 및 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="0787b-192">Lab: Setup FTP site and create a project</span></span>

<span data-ttu-id="0787b-193">다음 단계는 사용자만은 FTP를 통해를 업로드할 수 있는 위치에 있도록 FTP 사이트를 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-193">The following steps configure the FTP site so that a user has a location that only they can upload to via FTP.</span></span>

### <a name="install-the-ftp-service"></a><span data-ttu-id="0787b-194">FTP 서비스를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-194">Install the FTP Service</span></span>

1. <span data-ttu-id="0787b-195">프로그램 추가 / 제거를 열고, Windows 구성 요소 추가/제거를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-195">Open Add Remove Programs, select Add/Remove Windows Components</span></span>
2. <span data-ttu-id="0787b-196">인터넷 정보 서비스 (Windows 2003에서 응용 프로그램 서버)를 선택 하 고 클릭 **세부 정보**합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-196">Select Internet Information Services (Application Server on Windows 2003) and click **Details**.</span></span>
3. <span data-ttu-id="0787b-197">확인 **파일 전송 프로토콜 (FTP) 서비스** 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-197">Check **File Transfer Protocol (FTP) Service** and click **OK**.</span></span>
4. <span data-ttu-id="0787b-198">클릭 **다음** FTP 서비스를 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-198">Click **Next** to install the FTP service.</span></span>

### <a name="create-a-new-folder-for-content"></a><span data-ttu-id="0787b-199">콘텐츠에 대 한 새 폴더 만들기</span><span class="sxs-lookup"><span data-stu-id="0787b-199">Create a New Folder for Content</span></span>

1. <span data-ttu-id="0787b-200">Windows 탐색기에서 라는 새 폴더를 만든 **User1** c:\inetpub\wwwroot 안에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-200">In Windows Explorer, create a new folder called **User1** inside of c:\inetpub\wwwroot.</span></span>

#### <a name="configure-folders-and-permissions-on-folders"></a><span data-ttu-id="0787b-201">폴더에서 폴더와 사용 권한을 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-201">Configure folders and permissions on folders.</span></span>

1. <span data-ttu-id="0787b-202">관리 도구에서 인터넷 정보 서비스 스냅인을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-202">Open the Internet Information Services snap-in from Administrative Tools.</span></span> <span data-ttu-id="0787b-203">지금 컴퓨터 이름은 노드 아래에 FTP 사이트 폴더를 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-203">You will now have an FTP Sites folder under the computer name node.</span></span>
2. <span data-ttu-id="0787b-204">확장 **FTP 사이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-204">Expand **FTP Sites**.</span></span>
3. <span data-ttu-id="0787b-205">마우스 오른쪽 단추로 클릭는 **기본 FTP 사이트**선택, **새로**, 다음 **가상 디렉터리**, 클릭 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-205">Right-click the **Default FTP Site**, select **New**, then **Virtual Directory**, then click **Next**.</span></span>
4. <span data-ttu-id="0787b-206">입력 **User1** 가상 디렉터리 이름과 클릭에 대 한 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-206">Enter **User1** for the virtual directory name and click **Next**.</span></span>
5. <span data-ttu-id="0787b-207">입력 **c:\inetpub\wwwroot\User1** 경로 클릭에 대 한 **다음**합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-207">Enter **c:\inetpub\wwwroot\User1** for the path and click **Next**.</span></span>
6. <span data-ttu-id="0787b-208">클릭 **다음** 차례로 **마침** 마법사를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-208">Click **Next** and then **Finish** to complete the wizard.</span></span>
7. <span data-ttu-id="0787b-209">마우스 오른쪽 단추로 클릭는 **User1** 선택한 기본 FTP 사이트 가상 디렉터리 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-209">Right-click the **User1** virtual directory under Default FTP Site and select **Properties**.</span></span>
8. <span data-ttu-id="0787b-210">확인의 **쓰기** 확인란을 클릭 하 고 **확인** 는 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-210">Check the **Write** checkbox and click **OK** to close the dialog.</span></span>
9. <span data-ttu-id="0787b-211">마우스 오른쪽 단추로 클릭 **기본 FTP 사이트** 선택 **속성**합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-211">Right-click **Default FTP Site** and select **Properties**.</span></span>
10. <span data-ttu-id="0787b-212">에 **보안 계정** 탭을 선택 취소 **익명 연결 허용**합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-212">On the **Security Accounts** tab, uncheck **Allow Anonymous Connections**.</span></span>
11. <span data-ttu-id="0787b-213">클릭 **예** 계속할 것인지 묻는 대화 상자.</span><span class="sxs-lookup"><span data-stu-id="0787b-213">Click **Yes** in the dialog asking if you want to continue.</span></span>
12. <span data-ttu-id="0787b-214">클릭 **확인** 는 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-214">Click **OK** to close the dialog.</span></span>
13. <span data-ttu-id="0787b-215">확장 된 **기본 웹 사이트** 아래는 **웹 사이트** 노드.</span><span class="sxs-lookup"><span data-stu-id="0787b-215">Expand the **Default Web Site** under the **Web Sites** node.</span></span>
14. <span data-ttu-id="0787b-216">마우스 오른쪽 단추로 클릭는 **User1** 디렉터리 및 선택 **속성**</span><span class="sxs-lookup"><span data-stu-id="0787b-216">Right-click the **User1** directory and select **Properties**</span></span>
15. <span data-ttu-id="0787b-217">에 **응용 프로그램 설정** 섹션에서 클릭 **만들기** 응용 프로그램으로 폴더를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-217">In the **Application Settings** section, click **Create** to mark the folder as an application.</span></span>
16. <span data-ttu-id="0787b-218">클릭 **확인** 는 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-218">Click **OK** to close the dialog.</span></span>
17. <span data-ttu-id="0787b-219">인터넷 정보 서비스 스냅인을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-219">Close the Internet Information Services snap-in.</span></span>

### <a name="create-web-project"></a><span data-ttu-id="0787b-220">웹 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="0787b-220">Create web project</span></span>

1. <span data-ttu-id="0787b-221">Visual Studio 2005를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-221">Open Visual Studio 2005.</span></span>
2. <span data-ttu-id="0787b-222">**파일** 메뉴 선택 **새 웹 사이트**합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-222">From the **File** menu, select **New Web Site**.</span></span>
3. <span data-ttu-id="0787b-223">에 **위치** 드롭다운 **FTP**합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-223">In the **Location** dropdown, select **FTP**.</span></span>
4. <span data-ttu-id="0787b-224">**찾아보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-224">Click **Browse**.</span></span>
5. <span data-ttu-id="0787b-225">입력 **localhost** 에 **서버** 텍스트 상자에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-225">Enter **localhost** in the **Server** textbox.</span></span>
6. <span data-ttu-id="0787b-226">입력 **User1** 디렉터리 텍스트 상자에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-226">Enter **User1** in the Directory textbox.</span></span>
7. <span data-ttu-id="0787b-227">클릭 **열려**합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-227">Click **Open**.</span></span> <span data-ttu-id="0787b-228">FTP 위치는 새 웹 사이트 대화 상자에 입력 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-228">The FTP location will be entered into the New Web Site dialog.</span></span>
8. <span data-ttu-id="0787b-229">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-229">Click **OK**.</span></span>
9. <span data-ttu-id="0787b-230">선택을 취소 **익명 로그온** FTP 로그온 대화 상자에서 자격 증명을 입력 하 고 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-230">Uncheck **Anonymous log on** in the FTP Log On dialog, enter your credentials, and click **OK**.</span></span>
10. <span data-ttu-id="0787b-231">프로젝트에 대 한 URL은 무엇입니까?</span><span class="sxs-lookup"><span data-stu-id="0787b-231">What is the URL for the project?</span></span> <span data-ttu-id="0787b-232">(프로젝트에 대 한 URL은 솔루션 탐색기 나타납니다.)</span><span class="sxs-lookup"><span data-stu-id="0787b-232">(The URL for the project will be displayed in Solution Explorer.)</span></span>
11. <span data-ttu-id="0787b-233">**빌드** 메뉴 선택 **웹 사이트 빌드** 또는 **솔루션 빌드**합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-233">From the **Build** menu, select **Build Web Site** or **Build Solution**.</span></span>
12. <span data-ttu-id="0787b-234">솔루션 탐색기에서 Default.aspx를 마우스 오른쪽 단추로 클릭 하 고 선택 **브라우저에서 보기**합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-234">Right-click on Default.aspx in Solution Explorer and select **View in Browser**.</span></span>
13. <span data-ttu-id="0787b-235">웹 사이트 URL 필요 대화 상자에 입력 `http://localhost/user1` URL 및 클릭 **확인**합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-235">In the Web Site URL Required dialog, enter `http://localhost/user1` for the URL and click **OK**.</span></span>

> [!NOTE]
> <span data-ttu-id="0787b-236">형식을 로드할 수 없음을 나타내는 오류가 발생 하는 경우 \_Default, ASP.NET 2.0를 웹 사이트와 이전 버전에서 실행 되 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-236">If you get a error indicating an inability to load the type \_Default, make sure that you are running ASP.NET 2.0 on your Web site and not an earlier version.</span></span> <span data-ttu-id="0787b-237">인터넷 정보 서비스에서 ASP.NET 탭에서 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-237">You can do that from the ASP.NET tab in Internet Information Services.</span></span>


## <a name="opening-web-projects"></a><span data-ttu-id="0787b-238">웹 프로젝트 열기</span><span class="sxs-lookup"><span data-stu-id="0787b-238">Opening Web Projects</span></span>

<span data-ttu-id="0787b-239">웹 프로젝트를 열면 프로젝트 만들기와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-239">Opening Web projects is similar to creating projects.</span></span> <span data-ttu-id="0787b-240">다음 섹션에서는 관심을 기울 아웃에 대 한 IDE 내에서 작업 하는 동안 영역을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-240">The following sections call out areas to keep an eye out for while working within the IDE.</span></span> <span data-ttu-id="0787b-241">또한 HTTP 및 FTP를 사용 하 여 웹 프로젝트를 사용한 작업에 대해서도 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-241">It also covers working with Web projects using HTTP and FTP.</span></span>

<span data-ttu-id="0787b-242">웹 프로젝트를 열려면 파일 메뉴에서 웹 사이트 열기를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-242">To open a Web project, select Open Web Site from the File menu.</span></span> <span data-ttu-id="0787b-243">이전에 대상 동일한 위치 선택 대화 상자와 라는 메시지가 되 고 같은 네 가지 옵션을 사용할 수 있는: 파일 시스템, 로컬 IIS, FTP 및 원격 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-243">You will be prompted with the same Choose Location dialog covered previously and you have the same four options available to you: File System, Local IIS, FTP, and Remote Site.</span></span>

<a id="_Toc116100245"></a>

## <a name="file-system"></a><span data-ttu-id="0787b-244">파일 시스템</span><span class="sxs-lookup"><span data-stu-id="0787b-244">File System</span></span>

<span data-ttu-id="0787b-245">앞에서 설명한 대로이 단원에서는 Visual Studio는 더 이상 프로젝트 파일을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-245">As indicated previously in this module, Visual Studio no longer uses a project file.</span></span> <span data-ttu-id="0787b-246">따라서 파일 시스템에서 웹 사이트를 열려고 하면 실제로 옵션이 있습니다 선택한 폴더는 웹 프로젝트를 Visual Studio에서 처음으로 만들어지지 않은 경우에 원하는 모든 폴더를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-246">Therefore, if you choose to open a Web site from the file system, you actually have the option of choosing any folder that you wish, even if the folder you choose was not created as a Web project initially in Visual Studio.</span></span> <span data-ttu-id="0787b-247">예를 들어 웹 사이트와 내 문서 폴더를 열지 선택할 수 있으며 Visual Studio는 기꺼이 열고 아래와 같이 파일을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-247">For example, you can choose to open the My Documents folder as a Web site and Visual Studio will happily open it and display your files as shown below.</span></span>


![웹 사이트로 열린 내 문서](improvements-in-visual-studio-2005/_static/image3.jpg)

<span data-ttu-id="0787b-249">**그림 6**: *내 문서* 웹 사이트로 열</span><span class="sxs-lookup"><span data-stu-id="0787b-249">**Figure 6**: *My Documents* Opened As a Web Site</span></span>


<span data-ttu-id="0787b-250">Visual Studio만을 만들기 때문에 필요한 경우 추가 파일 및 폴더에 추가 파일이 나 폴더가 없기 열 위치에 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-250">Because Visual Studio only creates additional files and folders when necessary, no additional files or folders are added to the location you open.</span></span> <span data-ttu-id="0787b-251">이 아키텍처의 부작용을 파일 시스템에 웹 사이트를 중첩에서 하지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-251">A side-effect of this architecture is that it prevents you from nesting Web sites on the file system.</span></span> <span data-ttu-id="0787b-252">예를 들어 다음과 같은 디렉터리 구조를 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-252">For example, consider the following directory structure.</span></span>

<span data-ttu-id="0787b-253">C:\MyWebSite에 웹 프로젝트</span><span class="sxs-lookup"><span data-stu-id="0787b-253">Web project at C:\MyWebSite</span></span>

<span data-ttu-id="0787b-254">C:\MyWebSite\Nested에 다른 웹 프로젝트</span><span class="sxs-lookup"><span data-stu-id="0787b-254">Another web project at C:\MyWebSite\Nested</span></span>

<span data-ttu-id="0787b-255">C:\MyWebSite에서 웹 사이트를 열 때 중첩 된 폴더는 해당 응용 프로그램의 하위 폴더로 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-255">When you open the Web site at c:\MyWebSite, the Nested folder will appear as a sub-folder of that application.</span></span>

<a id="_Toc116100246"></a>

## <a name="http"></a><span data-ttu-id="0787b-256">HTTP</span><span class="sxs-lookup"><span data-stu-id="0787b-256">HTTP</span></span>

<span data-ttu-id="0787b-257">IIS 메타 베이스 (로컬 IIS) 또는 FrontPage Server Extensions (원격 사이트)를 사용 하 여 설정은 읽어 HTTP 통해 웹 사이트를 열 때 중첩 된 웹 응용 프로그램에 있는 경우 응용 프로그램으로 식별 하는 아이콘으로도 표시 됩니다 이러한.</span><span class="sxs-lookup"><span data-stu-id="0787b-257">When opening Web sites via HTTP, settings are read either from the IIS metabase (Local IIS) or using FrontPage Server Extensions (Remote Site.) If there are nested web applications, these are displayed as well with an icon identifying them as an application.</span></span> <span data-ttu-id="0787b-258">Frontpage에서 웹 응용 프로그램으로 작업에 익숙한 Visual Studio 2005에서의 동작과가 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-258">If you are familiar with working with web applications in FrontPage, the behavior in Visual Studio 2005 is similar.</span></span>

<span data-ttu-id="0787b-259">Visual Studio IDE 내에서 현재 열려 있는 응용 프로그램 아래에 중첩 된 응용 프로그램에 대 한 아이콘이 표시 되는 경우에 것은 허용 되지 않습니다 확장할 자신의 콘텐츠를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-259">Even though Visual Studio will display an icon for applications that are nested beneath the application that is currently opened within the IDE, it will not allow you to expand them to see their content.</span></span> <span data-ttu-id="0787b-260">그러나 열에 두 번 클릭 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-260">You can, however, double-click on them to open them.</span></span> <span data-ttu-id="0787b-261">이렇게 하면 웹 응용 프로그램을 엽니다 (또는 현재 열려 있는 솔루션을 바꾸기) 묻는 대화 상자가 나타납니다 또는 현재 솔루션에 웹 응용 프로그램을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-261">When you do, you will be presented with a dialog prompting you to either open the web application (and replace the currently open solution) or add the Web application to your current solution.</span></span>


![중첩 된 응용 프로그램 아이콘을 두 번 클릭 하면이 대화 상자 표시](improvements-in-visual-studio-2005/_static/image4.jpg)

<span data-ttu-id="0787b-263">**그림 7**: 중첩 된 응용 프로그램 아이콘을 두 번 클릭 하면이 대화 상자 표시</span><span class="sxs-lookup"><span data-stu-id="0787b-263">**Figure 7**: Double-clicking a nested application icon presents you with this dialog</span></span>


<a id="_Toc116100247"></a>

## <a name="ftp-site"></a><span data-ttu-id="0787b-264">FTP 사이트</span><span class="sxs-lookup"><span data-stu-id="0787b-264">FTP Site</span></span>

<span data-ttu-id="0787b-265">FTP 통해 사이트를 열 때 파일은 모두 로컬로 복사 임시 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-265">When you open a site via FTP, the files are all copied locally to your temp folder.</span></span> <span data-ttu-id="0787b-266">로컬 저장소 위치에 대 한 전체 경로 프로젝트에 대 한 속성 창에 표시 되 고 다음 형식을 사용 하 여 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-266">The full path for the local storage location is displayed in the Properties pane for the project and is created using the following format.</span></span>

<span data-ttu-id="0787b-267">C:\Documents and Settings\&lt; 사용자&gt;\Local Settings\Temp\VWDWebCache\&lt; 서버&gt;\_&lt;응용 프로그램 이름&gt;</span><span class="sxs-lookup"><span data-stu-id="0787b-267">C:\Documents and Settings\&lt;User&gt;\Local Settings\Temp\VWDWebCache\&lt;Server&gt;\_&lt;application name&gt;</span></span>

<span data-ttu-id="0787b-268">FTP를 사용 하면 Visual Studio를 아래와 같이 찾아볼 수 있도록 프로젝트에 대 한 기본 URL을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-268">When using FTP, Visual Studio will need to specify the base URL for your project so that you can browse it as shown below.</span></span> <span data-ttu-id="0787b-269">기본 URL을 지정 하지 않으면 Visual Studio 라는 나타납니다에 대 한 웹 사이트의 페이지를 탐색 하려고 처음으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-269">If you do not specify a base URL, Visual Studio will ask you for it the first time you attempt to browse a page in the Web site.</span></span>


![FTP 사이트에 대 한 기본 URL을 지정](improvements-in-visual-studio-2005/_static/image5.jpg)

<span data-ttu-id="0787b-271">**그림 8**: FTP 사이트에 대 한 기본 URL 지정</span><span class="sxs-lookup"><span data-stu-id="0787b-271">**Figure 8**: Specifying a Base URL for FTP Sites</span></span>


## <a name="improvements-in-compilation"></a><span data-ttu-id="0787b-272">컴파일의 향상 된 기능</span><span class="sxs-lookup"><span data-stu-id="0787b-272">Improvements in Compilation</span></span>

<span data-ttu-id="0787b-273">작업에서 Visual Studio 2005 웹 응용 프로그램을 이전 버전 보다 훨씬 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-273">Working with Web applications in Visual Studio 2005 is noticeably faster than previous versions.</span></span> <span data-ttu-id="0787b-274">이 수는 없는 일부만 컴파일 아키텍처의 변경 내용에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-274">This is due in no small part to the changes in compilation architecture.</span></span>

<span data-ttu-id="0787b-275">Visual Studio 2002 및 2003에서 웹 응용 프로그램으로 /bin 폴더에 있는 하나의 주 어셈블리로 컴파일 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-275">In Visual Studio 2002 and 2003, Web applications were compiled into one primary assembly residing in the /bin folder.</span></span> <span data-ttu-id="0787b-276">Visual Studio 2005 응용 프로그램에서\_코드 폴더에 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-276">In Visual Studio 2005, an App\_Code folder was added.</span></span> <span data-ttu-id="0787b-277">클래스 및 기타 UI가 아닌 코드 응용 프로그램에 추가 됩니다\_코드 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-277">Classes and other non-UI code are added to the App\_Code folder.</span></span> <span data-ttu-id="0787b-278">Visual Studio는 프로젝트를 응용 프로그램의 모든 파일을 작성 하는 경우\_코드 폴더는 단일 앱으로 컴파일되는\_Code.dll 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-278">When Visual Studio builds the project, all files in the App\_Code folder are compiled into a single App\_Code.dll file.</span></span> <span data-ttu-id="0787b-279">이러한 변경의 결과 후속 빌드는 이전 버전 보다 훨씬 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-279">The result of this change is that subsequent builds are much faster than in previous versions.</span></span>

> [!NOTE]
> <span data-ttu-id="0787b-280">ASP.NET 웹 응용 프로그램을 빌드하 MSBuild 명령줄 유틸리티를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-280">The MSBuild command line utility can also be used to build ASP.NET Web applications.</span></span> <span data-ttu-id="0787b-281">모듈 9에에서 해당 도구를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-281">That tool will be covered in module 9.</span></span>


<span data-ttu-id="0787b-282">다른 컴파일 향상 된 빌드 메뉴에서 새 빌드 페이지 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-282">Another compilation enhancement is the new Build Page option on the Build menu.</span></span> <span data-ttu-id="0787b-283">이 기능을 사용 하면 개발자가 변경 내용을 보다 신속 하 게 컴파일될 수 있도록 현재 페이지만 (함께, 시의 종속성)를 다시 작성 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-283">This feature allows a developer to rebuild only the current page (along with, of course, and dependencies) so that changes can be compiled more quickly.</span></span> <span data-ttu-id="0787b-284">C# IntelliSense 등을 업데이트 하기 위해에 대 한 백그라운드 컴파일을 제공 하지 않으므로, 유익한 지 보내주신이 기능에서 intellisense가 단순히 단일 페이지를 다시 작성 하 여 신속 하 게 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-284">Because C# does not offer background compilation for purposes of updating IntelliSense, etc., they will benefit immensely from this feature because it will allow for IntelliSense to be updated quickly by simply rebuilding a single page.</span></span>

<span data-ttu-id="0787b-285">프로젝트에 대 한 빌드 속성을 사용 하 여 빌드 시작 페이지가 실행 되기 전에 발생 하는 형식을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-285">The Build properties for a project allow you to configure the type of build that occurs before the startup page is executed.</span></span> <span data-ttu-id="0787b-286">개발자는 Visual Studio 코드 변경 후 응용 프로그램을 보다 신속 하 게 디버깅을 시작할 수 있도록만 빌드 현재 페이지를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-286">Developers can choose to only build the current page so that Visual Studio can start debugging applications more quickly after code changes.</span></span>


![빌드 페이지 시작 작업](improvements-in-visual-studio-2005/_static/image6.jpg)

<span data-ttu-id="0787b-288">**그림 9**: 빌드 페이지 시작 작업</span><span class="sxs-lookup"><span data-stu-id="0787b-288">**Figure 9**: The Build Page Start Action</span></span>


<span data-ttu-id="0787b-289">Visual Studio 및 ASP.NET 아키텍처에 향상 된 또 다른 훌륭한 기능 편집 영역에 있으며 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-289">Another great enhancement to Visual Studio and the ASP.NET architecture is in the area of edit and continue.</span></span> <span data-ttu-id="0787b-290">Visual Studio 2005에서 개발자가 프로젝트 디버깅을 시작 디버거를 분리 하지 않고 프로젝트에서 코드 변경 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-290">In Visual Studio 2005, developers can start debugging a project and make code changes on the project without detaching the debugger.</span></span> <span data-ttu-id="0787b-291">사실, 새 클래스를 추가 하는 프로젝트 디버깅을 시작할 문자 그대로 수, 해당 클래스에 코드를 추가, 해당 클래스의 새 인스턴스를 만드는 사용자 페이지에 코드를 추가 및 디버거를 분리 하지 않고 모든 클래스의 메서드를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-291">In fact, you can literally start debugging a project, add a new class, add code to that class, add code to your page that creates a new instance of that class and execute a method of the class, all without detaching the debugger.</span></span> <span data-ttu-id="0787b-292">새 코드를 실행 하는 것은 말 그대로 브라우저 새로 고침 하는 것 만큼 쉽게!</span><span class="sxs-lookup"><span data-stu-id="0787b-292">Executing the new code is literally as easy as refreshing the browser!</span></span>

<span data-ttu-id="0787b-293">편집의 연습 동영상을 참조 하 고 Visual Studio 2005에서 기능을 계속 하려면 여기를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-293">Click here to see a video walkthrough of the edit and continue feature in Visual Studio 2005.</span></span>


![](improvements-in-visual-studio-2005/_static/image2.png)


[<span data-ttu-id="0787b-294">전체 화면 비디오 열기</span><span class="sxs-lookup"><span data-stu-id="0787b-294">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/editcontinue1.wmv)


<span data-ttu-id="0787b-295">강력한 편집 하며 계속 하기 기능 ASP.NET 2.0에서 및 ASP.NET 응용 프로그램에 대 한 아키텍처 변경으로 인해 Visual Studio 2005는 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-295">The robust edit and continue functionality in ASP.NET 2.0 and Visual Studio 2005 is due to an architectural change for ASP.NET applications.</span></span> <span data-ttu-id="0787b-296">ASP.NET에서 Visual Studio 2002/2003에서 만든 응용 프로그램 1.x /bin 폴더에 저장 된 기본 어셈블리로 컴파일된 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-296">In ASP.NET 1.x, applications created in Visual Studio 2002/2003 were compiled into a primary assembly that was stored in the /bin folder.</span></span> <span data-ttu-id="0787b-297">모든 클래스, 페이지, 등 해당 하나의 DLL에 컴파일된 응용 프로그램에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-297">All classes, pages, etc. for the application were compiled into that one DLL.</span></span> <span data-ttu-id="0787b-298">다음 런타임 시, ASP.NET 컨트롤, 태그 및 페이지 내의 ASP.NET 코드의 모든 컴파일 것 및 Dll에는 ASP.NET 임시 폴더에 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-298">Then at runtime, ASP.NET would compile all of the controls, markup, and ASP.NET code within pages and copy those DLLs into the ASP.NET temporary folder.</span></span>

<span data-ttu-id="0787b-299">두 개의 컴파일 모델 런타임에 (Visual Studio 용 하나) 및 ASP.NET에 대 한 위의 설명에 ASP.NET 2.0을 사용 하는 Visual Studio 2005에서 한 하나의 일반적인 컴파일 모델에 병합 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-299">In Visual Studio 2005 using ASP.NET 2.0, the two compilation models outline above (one for Visual Studio and one for ASP.NET at runtime) have been merged into one common compilation model.</span></span> <span data-ttu-id="0787b-300">즉, 런타임에 모든 컴파일 문제가 대신 개발 단계에서 이제 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-300">That means that all compilation issues are now caught during the development stage instead of at runtime.</span></span> <span data-ttu-id="0787b-301">디자이너와 사용자 정의 컨트롤 및 마스터 페이지 등의 기능에 대 한 IntelliSense 지원에 대 한 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-301">It also allows for designer and IntelliSense support for features such as user controls and master pages.</span></span>

<span data-ttu-id="0787b-302">사용자 정의 컨트롤에 대 한 디자이너 지원 연습 비디오를 보려면 여기를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-302">Click here to see a video walkthrough of designer support for user controls.</span></span>


![](improvements-in-visual-studio-2005/_static/image3.png)


[<span data-ttu-id="0787b-303">전체 화면 비디오 열기</span><span class="sxs-lookup"><span data-stu-id="0787b-303">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/usercontrols1.wmv)


> [!NOTE]
> <span data-ttu-id="0787b-304">사용자 정의 컨트롤은 페이지에서 제거 되 면는 @Register 지시문을 태그에 상태를 유지 하 고 웹 사이트에서 사용자 정의 컨트롤을 삭제 하는 파서 오류를 방지 하려면 수동으로 제거 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-304">When a user control is removed from a page, the @Register directive remains in the markup and should be removed manually in order to avoid parser errors if the user control is deleted from the Web site.</span></span>


<span data-ttu-id="0787b-305">다른 향상 된 Visual Studio 컴파일 모델은 웹 사이트 게시 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-305">Another improvement in the Visual Studio compilation model is the Publish Web Site feature.</span></span> <span data-ttu-id="0787b-306">게시 기능 웹 사이트를 미리 컴파일하고, 때문에 개발자가 요청에 있는 모든 내용을 컴파일할 필요가 없으므로 때문에 성능이 향상된 누릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-306">Because the Publish feature precompiles the Web site, developers can enjoy the added performance of not having to compile anything on demand.</span></span> <span data-ttu-id="0787b-307">앱에서 모든 소스 코드 미리 컴파일하고 사용자도\_소스 코드가 없는를 배포할 수 있도록 폴더를 DLL로 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-307">It also precompiles all source code in the App\_Code folder into a DLL so that no source code has to be deployed.</span></span>


![게시 웹 사이트 대화 상자](improvements-in-visual-studio-2005/_static/image7.jpg)

<span data-ttu-id="0787b-309">**그림 10**: 게시 웹 사이트 대화 상자</span><span class="sxs-lookup"><span data-stu-id="0787b-309">**Figure 10**: The Publish Web Site Dialog</span></span>


> [!NOTE]
> <span data-ttu-id="0787b-310">Aspnet\_compile.exe 유틸리티 미리 ASP.NET 웹 응용 프로그램을 컴파일하는 데 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-310">The aspnet\_compile.exe utility can also be used to pre-compile an ASP.NET Web application.</span></span> <span data-ttu-id="0787b-311">모듈 9에에서 해당 도구를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-311">That tool will be covered in module 9.</span></span>


<span data-ttu-id="0787b-312">경우 아래와 같이 Temporary ASP.NET Files 폴더에 저장 됩니다 게시 웹 사이트를 미리 컴파일된 파일 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-312">When you Publish a Web site, the precompiled files are stored in the Temporary ASP.NET Files folder as shown below.</span></span> <span data-ttu-id="0787b-313">사용 하 여 파일을 *.compiled* 파일 확장명은 특정 Dll에 대 한 종속성을 정의 하는 XML 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-313">Files with a *.compiled* file extension are XML files that define dependencies for particular DLLs.</span></span> <span data-ttu-id="0787b-314">모든 Webform 또는 사용자 정의 컨트롤으로 시작 하는 임의의 Dll로 컴파일되는 *앱\_웹\_*합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-314">Any Webform or user controls are compiled into random DLLs that begin with *App\_Web\_*.</span></span>

<span data-ttu-id="0787b-315">두면는 *미리 컴파일된이 사이트를 업데이트할 수 있도록 허용* checkbox가 선택 태그 Webforms 및 사용자 컨트롤 내에서 배포 후 변경할 수 있도록 하는 DLL로 미리 컴파일된 되지 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-315">If you leave the *Allow this precompiled site to be updatable* checkbox checked, markup inside of your Webforms and user controls will not be pre-compiled into a DLL allowing you to make changes after deployment.</span></span> <span data-ttu-id="0787b-316">배포 된 콘텐츠에 대 한 변경이 허용 되지 않습니다 수 있도록 태그 고정 하지 않으려면이 확인란의 선택을 취소 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-316">If you would prefer to lock down the markup so that changes to the deployed content are not allowed, uncheck this box.</span></span>

<span data-ttu-id="0787b-317">*사용 하 여 고정 명명 고 페이지당 하나의 어셈블리만* 확인란을 사용 하 여 각 페이지는 고정 이름의 어셈블리에 컴파일됩니다 일괄 컴파일을 사용 하지 않도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-317">The *Use fixed naming and single page assemblies* checkbox allows you to disable batch compilation so that each page is compiled into a fixed-named assembly.</span></span> <span data-ttu-id="0787b-318">이 상자를 선택 되지 않은 상태로 일괄 컴파일을 활용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-318">Leaving this box unchecked allows you to take advantage of batch compilation.</span></span>

<span data-ttu-id="0787b-319">*미리 컴파일된 어셈블리에서 강력한 이름 사용* 확인란을 선택 하면 강력한 이름을 지정 하 여 미리 컴파일된 어셈블리입니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-319">The *Enable strong naming on precompiled assemblies* checkbox allows you to strong-name your precompiled assemblies.</span></span>

> [!NOTE]
> <span data-ttu-id="0787b-320">ASP.NET에서 1.x 강력한 이름의 어셈블리를 전역 어셈블리 캐시 (GAC)에 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-320">In ASP.NET 1.x, strong-named assemblies had to be installed into the Global Assembly Cache (GAC).</span></span> <span data-ttu-id="0787b-321">ASP.NET 2.0에서는 강력한 이름의 어셈블리를 GAC에 설치 하는 데 필요 없는 경우</span><span class="sxs-lookup"><span data-stu-id="0787b-321">In ASP.NET 2.0, you are not required to install strong-named assemblies into the GAC.</span></span>


![ASP.NET 응용 프로그램 미리 컴파일된 파일](improvements-in-visual-studio-2005/_static/image8.jpg)

<span data-ttu-id="0787b-323">**그림 11**: ASP.NET 응용 프로그램 미리 컴파일된 파일</span><span class="sxs-lookup"><span data-stu-id="0787b-323">**Figure 11**: An ASP.NET Applications Pre-Compiled Files</span></span>


> [!NOTE]
> <span data-ttu-id="0787b-324">위의 응용 프로그램에 web.config 파일이 있었습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-324">In the application above, there was no web.config file.</span></span> <span data-ttu-id="0787b-325">있었다면, 것은 호출 된 *PrecompiledApp.config* 웹 게시 한 후 사이트 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-325">If there had been, it would have been called *PrecompiledApp.config* after the Publish Web site process.</span></span>


## <a name="improvements-in-deployment"></a><span data-ttu-id="0787b-326">배포 향상 기능</span><span class="sxs-lookup"><span data-stu-id="0787b-326">Improvements in Deployment</span></span>

<span data-ttu-id="0787b-327">으로 Visual Studio 2002 및 2003을 사용 하 여 Visual Studio 2005에서는 프로젝트 복사 기능을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-327">As with Visual Studio 2002 and 2003, Visual Studio 2005 offers a Copy Project feature.</span></span> <span data-ttu-id="0787b-328">그러나이 기능은 Visual Studio 2005에서 강화 되었습니다 않으며은 이제 이라는 웹 사이트 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-328">However, the feature has been beefed up in Visual Studio 2005 and is now called Copy Web Site.</span></span>

<span data-ttu-id="0787b-329">웹 사이트 복사 대화는 왼쪽된 프레임 및 오른쪽 프레임으로 분할 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-329">The Copy Web Site dialog is split into a left frame and a right frame.</span></span> <span data-ttu-id="0787b-330">왼쪽된 프레임은 소스 웹 사이트, 오른쪽 프레임은 원격 웹 사이트 라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-330">The left frame is called the Source Web Site and the right frame is called the Remote Web Site.</span></span> <span data-ttu-id="0787b-331">일부 개발자가 혼동을 줄 수 있는 한 가지 없다는 오른쪽 프레임에 표시 되는 사이트 반드시 원격 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-331">One thing that may confuse some developers is that the site displayed in the right frame is not necessarily a remote site.</span></span> <span data-ttu-id="0787b-332">IIS의 로컬 인스턴스 또는 로컬 파일 시스템에서 사이트 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-332">It could be a site on the local file system or on the local instance of IIS.</span></span> <span data-ttu-id="0787b-333">또한 왼쪽된 프레임에 표시 되는 사이트 아닐 소스 웹 사이트 대화 상자를 사용 하면 원격 웹 사이트에서 게시할 수 있으므로 *를* 소스 웹 사이트입니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-333">Additionally, the site displayed in the left frame is not necessarily the source Web site because the dialog allows you to publish from the remote Web site *to* the source Web site.</span></span>

<span data-ttu-id="0787b-334">원격 웹 사이트에는 프로젝트를 복사 하는 경우 해당 사이트에 설치 된 FrontPage Server Extensions 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-334">If you are copying a project to a remote Web site, that site must have the FrontPage Server Extensions installed on it.</span></span> <span data-ttu-id="0787b-335">그렇지 않은 경우 FTP를 사용 하 여 연결 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-335">If it does not, you will need to connect using FTP.</span></span> <span data-ttu-id="0787b-336">반면에 로컬 IIS 인스턴스에 프로젝트를 복사 하는 경우 FrontPage Server Extensions 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-336">On the other hand, if you are copying a project to the local IIS instance, FrontPage Server Extensions are not required.</span></span>

> [!NOTE]
> <span data-ttu-id="0787b-337">로컬 IIS 인스턴스에서 새 웹 사이트를 만들려고 시도 하는 경우 FrontPage 2002 Server Extensions가 설치 된 SharePoint 서버에서 웹 사이트 만들기가 지원 되지 않습니다는 라는 오류 메시지가 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-337">If you try to create a new Web site on the local IIS instance and the FrontPage 2002 Server Extensions are installed, you will get an error message telling you that creating Web sites is not supported on a SharePoint server.</span></span> <span data-ttu-id="0787b-338">이 경우 FrontPage 2000 Server Extensions를 설치 하거나 FrontPage Server Extensions 제거 옵션도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-338">In that case, you have the option of installing the FrontPage 2000 Server Extensions or removing the FrontPage Server Extensions.</span></span>


<span data-ttu-id="0787b-339">웹 사이트 복사 기능을 연습 동영상을 보려면 여기를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-339">Click here for a video walkthrough of the Copy Web Site feature.</span></span>


![](improvements-in-visual-studio-2005/_static/image4.png)


[<span data-ttu-id="0787b-340">전체 화면 비디오 열기</span><span class="sxs-lookup"><span data-stu-id="0787b-340">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/copysite1.wmv)


## <a name="improvements-in-debugging"></a><span data-ttu-id="0787b-341">디버깅의 향상 된 기능</span><span class="sxs-lookup"><span data-stu-id="0787b-341">Improvements in Debugging</span></span>

<span data-ttu-id="0787b-342">Visual Studio 2005에서 디버깅 하는 네 가지 주요 향상 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-342">There are four key improvements in debugging in Visual Studio 2005.</span></span>

- <span data-ttu-id="0787b-343">기본적으로 관리자가 아닌 로컬로 디버깅 불가능 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-343">Debugging locally as a non-administrator is possible out of the box.</span></span>
- <span data-ttu-id="0787b-344">컴파일 요소에 대 한 디버그 특성은 기본적으로 false 이제입니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-344">The Debug attribute for the Compilation element is now false by default.</span></span>
- <span data-ttu-id="0787b-345">원격 디버깅 설치 및 구성 하는 이전 보다 훨씬 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-345">Remote debugging setup and configuration is easier than before.</span></span>
- <span data-ttu-id="0787b-346">이제 FTP 위치를 통해 연 웹 사이트를 디버깅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-346">You can now debug a Web site opened via an FTP location.</span></span>

## <a name="debugging-as-a-non-administrator"></a><span data-ttu-id="0787b-347">관리자가 아닌 방식으로 디버깅</span><span class="sxs-lookup"><span data-stu-id="0787b-347">Debugging as a Non-Administrator</span></span>

<span data-ttu-id="0787b-348">ASP.NET 개발 서버를 추가 관리자 이외의 사용자가을 쉽게 즉시 ASP.NET 응용 프로그램을 디버깅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-348">The addition of the ASP.NET Development Server allows non-administrators to easily debug ASP.NET applications right out of the box.</span></span> <span data-ttu-id="0787b-349">로컬 파일 시스템에서 실행 중인 ASP.NET 응용 프로그램을 디버깅할 때 Visual Studio는 로그온 한 사용자의 컨텍스트 내에서 ASP.NET 개발 서버를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-349">When an ASP.NET application running on the local file system is debugged, Visual Studio launches the ASP.NET Development Server under the context of the logged-on user.</span></span> <span data-ttu-id="0787b-350">그러면 해당 사용자 추가 구성 없이 해당 응용 프로그램을 디버깅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-350">That user can then debug that application without any additional configuration.</span></span>

## <a name="debug-is-false-by-default"></a><span data-ttu-id="0787b-351">디버그 False가 기본적으로</span><span class="sxs-lookup"><span data-stu-id="0787b-351">Debug is False by Default</span></span>

<span data-ttu-id="0787b-352">ASP.NET에서 1.x는 *디버그* 특성에 *컴파일* web.config 파일의 요소를 설정한 *true* 기본적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-352">In ASP.NET 1.x, the *debug* attribute in the *compilation* element of the web.config file was set to *true* by default.</span></span> <span data-ttu-id="0787b-353">그 항상 추천한 개발자가이 특성을 설정 *false* 프로덕션 환경에 응용 프로그램을 배포 하기 전에 있지만 대부분의 개발자로 설정 된 디버그 특성 종료 작업의 결과 완전히 이해 하지 때문에 true 이면 단순히 마지막로-됩니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-353">It has always been recommended that developers set this attribute to *false* before deploying an application to production, but because most developers don't fully understand the consequences of leaving the debug attribute set to true, they simply left it as-is.</span></span>

<span data-ttu-id="0787b-354">가장 심각한 문제 디버그 특성이 true로 설정 된 ASP.NETs 컴파일 모델을 일괄 처리를 해제 함을 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-354">The most severe problem with having the debug attribute set to true is that it disables ASP.NETs batch compilation model.</span></span> <span data-ttu-id="0787b-355">따라서 각 페이지는 별도 DLL로 컴파일됩니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-355">Therefore, each page is compiled into a separate DLL.</span></span> <span data-ttu-id="0787b-356">의미 있는 웹 응용 프로그램이 수천 페이지 (하지 드러나지의 어떤 방법으로)는 구성 하는 경우 해당 응용 프로그램에서 여러 개의 작은 Dll이 천 만들어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-356">If a Web application consists of thousands of pages (not unheard of by any means), that means several thousand small DLLs will be created by that application.</span></span> <span data-ttu-id="0787b-357">이러한 Dll은 크기가 작으며, 메모리의 특정 위치에 로드 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-357">While these DLLs are small in size, they are not loaded into any particular location in memory.</span></span> <span data-ttu-id="0787b-358">따라서 이들은 시스템 메모리에서 조각화가 발생 하며 OutOfMemoryException 발생 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-358">Therefore, they cause fragmentation in system memory and can contribute to OutOfMemoryException occurrences.</span></span>

<span data-ttu-id="0787b-359">ASP.NET 2.0에서 debug 특성은 기본적으로 false로 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-359">In ASP.NET 2.0, the debug attribute is set to false by default.</span></span> <span data-ttu-id="0787b-360">이미 확인 한 것 처럼, 개발자는 Visual Studio 2005에서 ASP.NET 응용 프로그램을 디버깅 하는 경우 디버깅 하도록 설정한 web.config 파일을 추가 하려면 메시지가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-360">As you have already seen, when a developer debugs an ASP.NET application in Visual Studio 2005, they are prompted to add a web.config file with debugging enabled.</span></span> <span data-ttu-id="0787b-361">ASP.NET에 있던 동일한 단점 그로 인해 이렇게 1.x 하지만 이제 개발자는 특성을 프로덕션 환경에 응용 프로그램을 이동 하기 전에 false로 다시 설정할지를 경고 명확 하 게 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-361">Doing so incurs the same drawbacks that were present in ASP.NET 1.x, but now the developer is clearly warned that the attribute should be reset to false before moving the application to production.</span></span>

## <a name="remote-debugging-setup-and-configuration"></a><span data-ttu-id="0787b-362">원격 디버깅 설치 및 구성</span><span class="sxs-lookup"><span data-stu-id="0787b-362">Remote Debugging Setup and Configuration</span></span>

<span data-ttu-id="0787b-363">Visual Studio 2002/2003에서 컴퓨터 디버그 관리자 (mdm.exe) 및 vs7jit.exe 프로세스에 사용한 원격 디버깅 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-363">In Visual Studio 2002/2003, remote debugging relied on the Machine Debug Manager (mdm.exe) and the vs7jit.exe process.</span></span> <span data-ttu-id="0787b-364">즉, 원격 디버깅 문제 해결 종종 고객에 대 한 검은색 상자 인시던트 였으며 PSS에 대 한 훨씬 더 자주 하지 못했습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-364">Because of that, troubleshooting remote debugging problems was often a black box for customers and it was often not much better for PSS.</span></span>

<span data-ttu-id="0787b-365">Visual Studio 2005 mdm.exe 및 vs7jit.exe 프로세스에 대 한 의존도 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-365">Visual Studio 2005 removes the reliance on the mdm.exe and vs7jit.exe processes.</span></span> <span data-ttu-id="0787b-366">대신 사용 한다는 점을 원격 디버그 모니터 (msvsmon.exe) 서비스</span><span class="sxs-lookup"><span data-stu-id="0787b-366">Instead, it now uses the Remote Debug Monitor service (msvsmon.exe.)</span></span>

<span data-ttu-id="0787b-367">Visual Studio 2005의 원격 디버깅에 대 한 요구 사항은 매우 간단 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-367">The requirement for debugging in Visual Studio 2005 remotely is quite simple.</span></span> <span data-ttu-id="0787b-368">디버깅 하기 전에 원격 서버에서 msvsmon.exe를 실행 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-368">You need to run msvsmon.exe on the remote server prior to debugging.</span></span> <span data-ttu-id="0787b-369">Visual Studio CD에서 원격 디버그 모니터를 설치할 수 있습니다 또는 웹 서버에 전혀 아무것도 설치 하지 않고 공유에서 msvsmon.exe를 간단히 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-369">You can install the Remote Debug Monitor from the Visual Studio CD or you can simply run msvsmon.exe from a share without installing anything at all on the Web server.</span></span>

<span data-ttu-id="0787b-370">Msvsmon.exe를 실행 하면 원격 디버깅 차단 되 고 포트에 대 한 것에서 문제가 발생할 수도 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-370">When you run msvsmon.exe, it is likely that it will complain about ports being blocked for remote debugging.</span></span> <span data-ttu-id="0787b-371">다행히 쉽게 차단 해제할 수 있습니다 포트 오른쪽 경고 대화 상자 내에서 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-371">Fortunately, you can easily unblock the ports from right within the warning dialog as shown below.</span></span>


![Windows 방화벽이 원격 디버깅 차단 인지 알림](improvements-in-visual-studio-2005/_static/image9.jpg)

<span data-ttu-id="0787b-373">**그림 12**: 알림 Windows 방화벽이 원격 디버깅 차단 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-373">**Figure 12**: Notification that Windows Firewall is Blocking Remote Debugging</span></span>


<span data-ttu-id="0787b-374">디버깅에 필요한 포트를 차단이 해제 되 면 아래와 같이 원격 디버깅 모니터 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-374">Once you have unblocked the ports necessary for debugging, you will see the Remote Debugging Monitor as shown below.</span></span> <span data-ttu-id="0787b-375">이 인터페이스에서 연결을 모니터링 하 고 디버깅 권한이 쉽게 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-375">From this interface, you can monitor connections and change debugging permissions easily.</span></span>


![원격 디버깅 모니터](improvements-in-visual-studio-2005/_static/image10.jpg)

<span data-ttu-id="0787b-377">**그림 13**: 원격 디버깅 모니터</span><span class="sxs-lookup"><span data-stu-id="0787b-377">**Figure 13**: The Remote Debugging Monitor</span></span>


<span data-ttu-id="0787b-378">에 원격으로 FTP를 통해 열린 웹 응용 프로그램을 디버깅할 수 이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-378">It is also possible to remotely debug a Web application opened via FTP.</span></span> <span data-ttu-id="0787b-379">단계 이전에 설명 된와 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-379">The steps are the same as those previously covered.</span></span> <span data-ttu-id="0787b-380">그러나이 모듈의 앞부분에 설명 된 대로 FTP 프로젝트 검색에 대 한 기본 URL을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-380">However, you will need to specify a base URL for browsing the FTP project as outlined earlier in this module.</span></span>

## <a name="lab-2"></a><span data-ttu-id="0787b-381">랩 2</span><span class="sxs-lookup"><span data-stu-id="0787b-381">Lab 2</span></span>

## <a name="remote-debugging-with-visual-studio-2005"></a><span data-ttu-id="0787b-382">Visual Studio 2005를 사용 하 여 원격 디버깅</span><span class="sxs-lookup"><span data-stu-id="0787b-382">Remote Debugging with Visual Studio 2005</span></span>

<span data-ttu-id="0787b-383">이 실습에서는 Visual Studio 2005를 사용 하 여 원격 디버깅을 통해 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-383">This lab will walk you through remote debugging with Visual Studio 2005.</span></span>

<span data-ttu-id="0787b-384">이 랩의 연습 동영상을 보려면 여기를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-384">Click here for a video walkthrough of this lab.</span></span>


![](improvements-in-visual-studio-2005/_static/image5.png)


[<span data-ttu-id="0787b-385">전체 화면 비디오 열기</span><span class="sxs-lookup"><span data-stu-id="0787b-385">Open Full-Screen Video</span></span>](improvements-in-visual-studio-2005/_static/remdebug1.wmv)


<span data-ttu-id="0787b-386">이 랩에서 사용 하면 하나의 Visual Studio 2005를 실행 하 고 다른 실행 중인 IIS 5 이상 두 컴퓨터를 포함 하도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-386">This lab requires you to have two machines, one running Visual Studio 2005 and the other running IIS 5 or greater.</span></span>

1. <span data-ttu-id="0787b-387">Visual Studio 2005를 열고 원격 서버에서 새 웹 사이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-387">Open Visual Studio 2005 and create a new Web site on the remote server.</span></span>

> [!NOTE]
> <span data-ttu-id="0787b-388">원격 IIS 인스턴스 또는 FTP를 통해 웹 사이트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-388">You can create the Web site on a remote IIS instance or via FTP.</span></span>


1. <span data-ttu-id="0787b-389">원격 웹 서버에서 UNC 경로 사용 하 여 개발 컴퓨터에서 msvsmon.exe를 찾아 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-389">From the remote Web server, locate msvsmon.exe on the development machine using a UNC path and execute it.</span></span>  
 <span data-ttu-id="0787b-390">Msvsmon.exe의 기본 위치는 \\server\c$ files\microsoft Visual Studio 8\Common7\IDE\Remote Debugger\x86 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-390">The default location for msvsmon.exe is \\server\c$\Program Files\Microsoft Visual Studio 8\Common7\IDE\Remote Debugger\x86.</span></span>
2. <span data-ttu-id="0787b-391">원격 디버깅을 위해 포트 차단을 해제 하 라는 메시지가 나타나면 그렇게 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-391">If prompted to unblock ports for remote debugging, do so.</span></span>
3. <span data-ttu-id="0787b-392">개발 컴퓨터에서 Default.aspx에 대 한 코드 숨김 열고 페이지에 중단점을 설정\_메서드를 로드 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-392">From the development machine, open the code-behind for Default.aspx and set a breakpoint in the Page\_Load method.</span></span>
4. <span data-ttu-id="0787b-393">개발 컴퓨터에서 디버깅을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-393">Start debugging from the development machine.</span></span>

<span data-ttu-id="0787b-394">예상 대로 중단점이 적중 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-394">You should hit the breakpoint as expected.</span></span>

## <a name="aspnet-development-server"></a><span data-ttu-id="0787b-395">ASP.NET Development Server</span><span class="sxs-lookup"><span data-stu-id="0787b-395">ASP.NET Development Server</span></span>

<span data-ttu-id="0787b-396">앞에서 설명한 마십시오,으로 Visual Studio 2005 ASP.NET 개발 서버를 호출 하는 웹 서버와 함께 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-396">As weve already discussed, Visual Studio 2005 ships with a Web server called the ASP.NET Development Server.</span></span> <span data-ttu-id="0787b-397">(ASP.NET 개발 서버는 라고도 Cassini.) 이 웹 서버가을 찾아서 다음 파일 시스템에서 실행 되는 웹 응용 프로그램을 디버깅 하는 편리한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-397">(The ASP.NET Development Server is sometimes referred to as Cassini.) This Web server is a convenient means to browse and debug Web applications running on the file system.</span></span>

<span data-ttu-id="0787b-398">ASP.NET 개발 서버는 제한 된 웹 서버.</span><span class="sxs-lookup"><span data-stu-id="0787b-398">The ASP.NET Development Server is a restricted Web server.</span></span> <span data-ttu-id="0787b-399">원격 연결을 허용 하지 않습니다, 그리고 웹 서버를 시작한 사용자 이외의 모든 사용자의 모든 요청을 허용 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-399">It does not allow remote connections, it does not allow any requests from any user other than the user who started the Web server.</span></span> <span data-ttu-id="0787b-400">ASP 페이지를 처리 하는 기능이 있는 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-400">It also does not have the capability of serving ASP pages.</span></span> <span data-ttu-id="0787b-401">ASP.NET 리소스 및 HTML 리소스 (이미지, CSS 파일 등 포함)만 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-401">Only ASP.NET resources and HTML resources (including images, CSS files, etc.) are served.</span></span>

<span data-ttu-id="0787b-402">C:\Windows\Microsoft.NET\Framework\v2.0에 있는 WebDev.WebServer.exe 파일을 실행 하 여 명령줄을 통해 ASP.NET 개발 서버를 시작할 수 있습니다. \*\*\*\*\*.</span><span class="sxs-lookup"><span data-stu-id="0787b-402">The ASP.NET Development Server can be launched via the command line by running the WebDev.WebServer.exe file located at c:\Windows\Microsoft.NET\Framework\v2.0.\*\*\*\*\*.</span></span> <span data-ttu-id="0787b-403">다음과 같은 대화 상자가 사용할 수 있는 매개 변수를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-403">The following dialog displays the parameters that are available.</span></span>


![](improvements-in-visual-studio-2005/_static/image11.jpg)

<span data-ttu-id="0787b-404">**그림 14**</span><span class="sxs-lookup"><span data-stu-id="0787b-404">**Figure 14**</span></span>


> [!NOTE]
> <span data-ttu-id="0787b-405">명령줄을 통해 명시적으로 시작 될 때 ASP.NET 개발 서버 지원 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0787b-405">The ASP.NET Development Server is not supported when launched explicitly via the command line.</span></span>