<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Cricket Times - Your Cricket News Source</title>
<link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap" rel="stylesheet">
<style>
    body { font-family: 'Roboto', sans-serif; margin: 0; padding: 0; background: #f4f4f4; }
    header { background: #0a2f5d; color: white; padding: 10px 20px; display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; }
    header h1 { margin: 0; font-size: 28px; }
    nav a { color: white; text-decoration: none; margin: 0 10px; font-weight: bold; }
    nav a:hover { text-decoration: underline; }
    .search-box input { padding: 5px; border-radius: 3px; border: none; }
    .breaking-news { background: #ff0000; color: white; padding: 10px; overflow: hidden; position: relative; height: 30px; }
    .ticker { position: absolute; white-space: nowrap; will-change: transform; }
    .container { display: flex; flex-wrap: wrap; margin: 20px; }
    .main-content { flex: 3; margin-right: 20px; min-width: 300px; }
    .sidebar { flex: 1; min-width: 250px; }
    .section { margin-bottom: 30px; }
    .section h2 { border-bottom: 2px solid #0a2f5d; padding-bottom: 5px; color: #0a2f5d; }
    .article { display: flex; margin-bottom: 15px; background: white; padding: 10px; border-radius: 5px; }
    .article img { width: 150px; height: 100px; object-fit: cover; margin-right: 10px; border-radius: 5px; }
    .article div { flex: 1; }
    .article h3 { margin: 0 0 5px 0; }
    .article p { margin: 0; font-size: 14px; color: #333; }
    .sidebar .widget { background: white; padding: 10px; margin-bottom: 20px; border-radius: 5px; }
    footer { background: #0a2f5d; color: white; text-align: center; padding: 15px; margin-top: 20px; }
    button.category-btn { margin: 5px; padding: 5px 10px; background: #0a2f5d; color: white; border: none; cursor: pointer; border-radius: 3px; }
    button.category-btn:hover { background: #053153; }
    /* Slider */
    .slider { position: relative; overflow: hidden; height: 200px; margin-bottom: 20px; border-radius: 5px; }
    .slides { display: flex; transition: transform 0.5s ease-in-out; }
    .slide { min-width: 100%; box-sizing: border-box; position: relative; }
    .slide img { width: 100%; height: 200px; object-fit: cover; border-radius: 5px; }
    .slide h3 { position: absolute; bottom: 10px; left: 10px; color: white; background: rgba(0,0,0,0.6); padding: 5px 10px; border-radius: 3px; margin: 0; }
</style>
</head>
<body>

<header>
    <h1>Cricket Times</h1>
    <nav>
        <a href="#" class="category-btn" data-category="All">Home</a>
        <a href="#" class="category-btn" data-category="Matches">Matches</a>
        <a href="#" class="category-btn" data-category="Players">Players</a>
        <a href="#" class="category-btn" data-category="IPL">IPL</a>
        <a href="#" class="category-btn" data-category="World Cups">World Cups</a>
        <a href="#" class="category-btn" data-category="Stats">Stats</a>
    </nav>
    <div class="search-box">
        <input type="text" placeholder="Search news..." id="searchInput">
    </div>
</header>

<div class="breaking-news">
    <div class="ticker" id="ticker"></div>
</div>

<div class="container">
    <div class="main-content">
        <div class="slider" id="topSlider">
            <div class="slides" id="slidesContainer"></div>
        </div>

        <div class="section" id="newsSection">
            <h2>All News</h2>
            <!-- Articles will be injected here by JS -->
        </div>
    </div>

    <div class="sidebar">
        <div class="widget">
            <h3>Trending News</h3>
            <ul id="trendingList"></ul>
        </div>
        <div class="widget">
            <h3>Subscribe to Newsletter</h3>
            <input type="email" placeholder="Your email" style="width: 100%; padding: 5px;">
            <button style="margin-top: 5px; padding: 5px 10px; background: #0a2f5d; color: white; border: none; cursor: pointer;">Subscribe</button>
        </div>
    </div>
</div>

<footer>
    &copy; 2025 Cricket Times | All rights reserved | <a href="#" style="color: white;">Privacy Policy</a> | <a href="#" style="color: white;">Contact Us</a>
</footer>

<script>
// Breaking news ticker (cricket-focused)
const tickerNews = [
    "Live: India vs Australia 3rd ODI updates!",
    "IPL 2025: RR defeats CSK in thrilling last-over finish",
    "Player Injuries: Virat Kohli doubtful for next series",
    "World Cup 2027 preparations underway"
];

let tickerIndex = 0;
const tickerElement = document.getElementById('ticker');

function updateTicker() {
    tickerElement.textContent = tickerNews[tickerIndex];
    tickerIndex = (tickerIndex + 1) % tickerNews.length;
}
updateTicker();
setInterval(updateTicker, 4000);

// Top stories slider (cricket-focused)
const topStories = [
    {title: "India Wins T20 Series Against Australia", img: "https://source.unsplash.com/800x200/?cricket"},
    {title: "IPL 2025: Exciting Matches This Week", img: "https://source.unsplash.com/800x200/?cricket-stadium"},
    {title: "Virat Kohli Scores Record 1200th Run in ODIs", img: "https://source.unsplash.com/800x200/?cricket-player"}
];

const slidesContainer = document.getElementById('slidesContainer');
topStories.forEach(story => {
    const slide = document.createElement('div');
    slide.className = 'slide';
    slide.innerHTML = `<img src="${story.img}" alt="Story"><h3>${story.title}</h3>`;
    slidesContainer.appendChild(slide);
});

let slideIndex = 0;
function showNextSlide() {
    slideIndex = (slideIndex + 1) % topStories.length;
    slidesContainer.style.transform = `translateX(-${slideIndex * 100}%)`;
}
setInterval(showNextSlide, 4000);

// Cricket news articles
const articles = [
    {title: "India vs Australia 3rd ODI Highlights", img: "https://source.unsplash.com/150x100/?cricket", category: "Matches", desc: "India beat Australia by 5 wickets in a thrilling match."},
    {title: "Virat Kohli Injured During Net Practice", img: "https://source.unsplash.com/150x100/?cricket-player", category: "Players", desc: "Star batsman Virat Kohli faces injury doubts for the upcoming series."},
    {title: "IPL 2025: RR vs CSK Review", img: "https://source.unsplash.com/150x100/?cricket-stadium", category: "IPL", desc: "Rajasthan Royals defeated Chennai Super Kings in a nail-biting last-over finish."},
    {title: "World Cup 2027: Teams and Venues Announced", img: "https://source.unsplash.com/150x100/?cricket-tournament", category: "World Cups", desc: "ICC announces venues and teams for the next Cricket World Cup."},
    {title: "Top 10 Batsmen Stats 2025", img: "https://source.unsplash.com/150x100/?cricket-score", category: "Stats", desc: "Check out the top performing batsmen of this year with full stats."},
];

function displayArticles(filter = "All") {
    const newsSection = document.getElementById('newsSection');
    newsSection.innerHTML = "<h2>All News</h2>";
    const filtered = filter === "All" ? articles : articles.filter(a => a.category === filter);
    filtered.forEach(article => {
        const div = document.createElement('div');
        div.className = "article";
        div.innerHTML = `<img src="${article.img}" alt="News"><div><h3>${article.title}</h3><p>${article.desc}</p></div>`;
        newsSection.appendChild(div);
    });
}
displayArticles();

// Category filter buttons
document.querySelectorAll('.category-btn').forEach(btn => {
    btn.addEventListener('click', (e) => {
        e.preventDefault();
        const category = btn.getAttribute('data-category');
        displayArticles(category);
    });
});

// Trending news
const trending = [
    "India beats Australia in ODI series",
    "KL Rahul scores century in IPL",
    "ICC rankings updated for 2025",
    "Next World Cup schedule released"
];
const trendingList = document.getElementById('trendingList');
trending.forEach(item => {
    const li = document.createElement('li');
    li.textContent = item;
    trendingList.appendChild(li);
});

// Simple search functionality
document.getElementById('searchInput').addEventListener('input', (e) => {
    const query = e.target.value.toLowerCase();
    const filtered = articles.filter(a => a.title.toLowerCase().includes(query) || a.desc.toLowerCase().includes(query));
    const newsSection = document.getElementById('newsSection');
    newsSection.innerHTML = "<h2>Search Results</h2>";
    filtered.forEach(article => {
        const div = document.createElement('div');
        div.className = "article";
        div.innerHTML = `<img src="${article.img}" alt="News"><div><h3>${article.title}</h3><p>${article.desc}</p></div>`;
        newsSection.appendChild(div);
    });
});
</script>

</body>
</html>
