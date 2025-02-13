<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Live News</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0/dist/css/bootstrap.min.css" rel="stylesheet">
    <style>
        .news-card {
            margin: 15px; 
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        .news-image {
            height: 200px;
            object-fit: cover;
        }
    </style>
</head>
<body>
    <div class="container my-5">
        <h1 class="text-center mb-4">📰 Latest News</h1>
        <div id="news-container" class="row"></div>
    </div>

    <script>
        // Replace with your NewsAPI key
        const API_KEY = '9dcd66ce7af8412589242680503200d1';
        const NEWS_API = `https://newsapi.org/v2/top-headlines?country=us&apiKey=${API_KEY}`;

        async function loadNews() {
            try {
                const response = await fetch(NEWS_API);
                const data = await response.json();
                
                let html = '';
                data.articles.forEach(article => {
                    html += `
                        <div class="col-md-4">
                            <div class="news-card">
                                <img src="${article.urlToImage || 'https://via.placeholder.com/300x200'}" 
                                     class="news-image w-100">
                                <h3 class="mt-3">${article.title}</h3>
                                <p>${article.description || ''}</p>
                                <a href="${article.url}" target="_blank" class="btn btn-primary">
                                    Read More →
                                </a>
                            </div>
                        </div>
                    `;
                });
                
                document.getElementById('news-container').innerHTML = html;
            } catch (error) {
                console.error('Error:', error);
            }
        }

        // Auto-refresh every 5 minutes
        loadNews();
        setInterval(loadNews, 300000);
    </script>
</body>
</html>
