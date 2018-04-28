### <a name="entity-framework-version-must-match-the-net-framework-version"></a><span data-ttu-id="3de5c-101">Entity Framework バージョンは .NET Framework バージョンに一致する必要がある</span><span class="sxs-lookup"><span data-stu-id="3de5c-101">Entity Framework version must match the .NET Framework version</span></span>

|   |   |
|---|---|
|<span data-ttu-id="3de5c-102">説明</span><span class="sxs-lookup"><span data-stu-id="3de5c-102">Details</span></span>|<span data-ttu-id="3de5c-103">Entity Framework のバージョンは .NET Framework のバージョンに一致する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3de5c-103">The entity framework version should be matched with the .NET framework version.</span></span> <span data-ttu-id="3de5c-104">.NET 4.5 には、Entity Framework 5 をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="3de5c-104">Entity Framework 5 is recommended for .NET 4.5.</span></span> <span data-ttu-id="3de5c-105">.NET 4.5 プロジェクトの EF 4.x に <xref:System.ComponentModel.DataAnnotations> に関する既知の問題がいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="3de5c-105">There are some known issues with EF 4.x in a .NET 4.5 project around <xref:System.ComponentModel.DataAnnotations>.</span></span> <span data-ttu-id="3de5c-106">.NET 4.5 では、別のアセンブリに移動したので、どの注釈を使用するのか判断するという問題があります。</span><span class="sxs-lookup"><span data-stu-id="3de5c-106">In .NET 4.5, these were moved to a different assembly, so there are issues determining which annotations to use.</span></span>|
|<span data-ttu-id="3de5c-107">提案される解決策</span><span class="sxs-lookup"><span data-stu-id="3de5c-107">Suggestion</span></span>|<span data-ttu-id="3de5c-108">.NET Framework 4.5 の場合、Entity Framework 5 にアップグレードする</span><span class="sxs-lookup"><span data-stu-id="3de5c-108">Upgrade to Entity Framework 5 for .NET Framework 4.5</span></span>|
|<span data-ttu-id="3de5c-109">スコープ</span><span class="sxs-lookup"><span data-stu-id="3de5c-109">Scope</span></span>|<span data-ttu-id="3de5c-110">Major</span><span class="sxs-lookup"><span data-stu-id="3de5c-110">Major</span></span>|
|<span data-ttu-id="3de5c-111">バージョン</span><span class="sxs-lookup"><span data-stu-id="3de5c-111">Version</span></span>|<span data-ttu-id="3de5c-112">4.5</span><span class="sxs-lookup"><span data-stu-id="3de5c-112">4.5</span></span>|
|<span data-ttu-id="3de5c-113">型</span><span class="sxs-lookup"><span data-stu-id="3de5c-113">Type</span></span>|<span data-ttu-id="3de5c-114">再ターゲット中</span><span class="sxs-lookup"><span data-stu-id="3de5c-114">Retargeting</span></span>|
