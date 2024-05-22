
# Reccomender-system
articles = [
    {"id": 1, "title": "Economic Growth in 2024", "description": "An in-depth analysis of the projected economic growth in 2024.", "tags": ["economy", "growth", "2024"]},

    
    {"id": 2, "title": "Climate Change and its Impact", "description": "Exploring the effects of climate change on global weather patterns.", "tags": ["climate change", "environment", "weather"]},

    
    {"id": 3, "title": "Advancements in Artificial Intelligence", "description": "A look at the latest advancements in AI and their applications.", "tags": ["AI", "technology", "innovation"]},

    
    {"id": 4, "title": "The Future of Renewable Energy", "description": "How renewable energy sources are shaping the future of energy.", "tags": ["renewable energy", "environment", "technology"]},

    
    {"id": 5, "title": "Global Political Trends in 2024", "description": "An analysis of the major political trends expected in 2024.", "tags": ["politics", "2024", "global"]},

    
    {"id": 6, "title": "Health Benefits of a Balanced Diet", "description": "Understanding the health benefits of maintaining a balanced diet.", "tags": ["health", "nutrition", "diet"]},

    
    {"id": 7, "title": "Technological Innovations in Healthcare", "description": "The impact of technological innovations on healthcare delivery.", "tags": ["healthcare", "technology", "innovation"]},

    
    {"id": 8, "title": "Economic Policies and their Impact", "description": "How different economic policies affect growth and development.", "tags": ["economy", "policies", "growth"]},

    
    {"id": 9, "title": "The Rise of Electric Vehicles", "description": "How electric vehicles are transforming the automotive industry.", "tags": ["electric vehicles", "technology", "innovation"]},

    
    {"id": 10, "title": "Mental Health Awareness in 2024", "description": "The importance of mental health awareness and initiatives in 2024.", "tags": ["mental health", "awareness", "2024"]}
]
from collections import defaultdict

def get_recommendations(current_article_id, articles):
    # Find the current article based on ID
    current_article = next((article for article in articles if article["id"] == current_article_id), None)
    if not current_article:
        return []

    current_tags = set(current_article["tags"])
    
    # Calculate similarity based on common tags
    similarity_scores = []
    for article in articles:
        if article["id"] != current_article_id:
            common_tags = current_tags.intersection(article["tags"])
            similarity_scores.append((article["id"], len(common_tags)))

    # Sort articles based on the number of common tags (similarity score)
    similarity_scores.sort(key=lambda x: x[1], reverse=True)
    
    # Get the top 3 recommendations
    recommended_article_ids = [article_id for article_id, score in similarity_scores[:3]]

    # Fetch the recommended articles
    recommended_articles = [article for article in articles if article["id"] in recommended_article_ids]

    return recommended_articles
