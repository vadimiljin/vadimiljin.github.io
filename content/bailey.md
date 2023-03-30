# Keyword Clusterer

1. Create a virtual environment and install necessary packages:

```bash
python3 -m venv venv
source venv/bin/activate
pip install flask pandas numpy requests python-dotenv scikit-learn
```
2. Create a .env file to store your DataForSEO API credentials:

```makefile
DATAFORSEO_API_USERNAME=your_username
DATAFORSEO_API_PASSWORD=your_password
```
3. Create app.py with the following code:

```python
import os
import csv
import json
import tempfile
import itertools
from collections import defaultdict
from dotenv import load_dotenv
from flask import Flask, render_template, request, send_file
import requests
import pandas as pd
import numpy as np
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.metrics.pairwise import cosine_similarity

load_dotenv()
app = Flask(__name__)

API_ENDPOINT = "https://api.dataforseo.com/v3/serp/google/organic/live/regular"
USERNAME = os.environ['DATAFORSEO_API_USERNAME']
PASSWORD = os.environ['DATAFORSEO_API_PASSWORD']


def get_serp_data(keyword, location_name, language_name):
    response = requests.post(API_ENDPOINT, auth=(USERNAME, PASSWORD), json={
        "keyword": keyword,
        "location_name": location_name,
        "language_name": language_name,
        "depth": 1,
    })

    if response.status_code == 200:
        return response.json()
    else:
        raise Exception(f"API request failed with status code {response.status_code}")


def extract_top_urls(data):
    items = data.get("items", [])
    urls = [item["url"] for item in items if item["type"] == "organic" and 1 <= item["rank_group"] <= 10]
    return urls[:10]


def cluster_keywords(df, threshold=0.3):
    vectorizer = TfidfVectorizer()
    X = vectorizer.fit_transform(df["urls"].apply(lambda urls: " ".join(urls)))
    similarity_matrix = cosine_similarity(X)

    groups = defaultdict(set)
    for i, j in itertools.combinations(range(len(df)), 2):
        if similarity_matrix[i, j] >= threshold:
            groups[df.loc[i, "group_name"]].add(df.loc[j, "Keyword"])
            groups[df.loc[j, "group_name"]].add(df.loc[i, "Keyword"])

    return groups


def process_file(file, location_name, language_name, domain_name):
    df = pd.read_csv(file)
    df["urls"] = ""

    for idx, row in df.iterrows():
        keyword = row["Keyword"]
        data = get_serp_data(keyword, location_name, language_name)
        top_urls = extract_top_urls(data)
        df.at[idx, "urls"] = json.dumps(top_urls)

    df["group_name"] = df.apply(lambda row: row["Keyword"] if row["Search Volume"] == max(df["Search Volume"]) else "", axis=1)
    groups = cluster_keywords(df)

    with tempfile.NamedTemporaryFile(mode="w+", delete=False, newline="", suffix=".csv") as output_file:
        writer = csv.writer(output_file)
        writer.writerow(["Group Name", "Keyword", "Search Volume", "Matched URL", "Position"])

        for group_name, keywords in groups.items():
            for keyword in keywords:
                row = df[df["Keyword"] == keyword].iloc[0]
                urls = json.loads(row["urls"])
                matched_url, position = "", ""
                for idx, url in enumerate(urls):
                    if domain_name.lower() in url.lower():
                        matched_url = url
                    position = idx + 1
                    break

            writer.writerow([group_name, row["Keyword"], row["Search Volume"], matched_url, position])

    return output_file.name


@app.route("/", methods=["GET", "POST"])
def index():
    if request.method == "POST":
        file = request.files["csv_file"]
        location_name = request.form["location_name"]
        language_name = request.form["language_name"]
        domain_name = request.form["domain_name"]
    try:
        output_file_path = process_file(file, location_name, language_name, domain_name)
        return send_file(output_file_path, as_attachment=True, attachment_filename="output.csv", cache_timeout=0)
    except Exception as e:
        return f"Error: {str(e)}", 400

return render_template("index.html")

if __name__ == '__main__':
	app.run(debug=True)
```
4. Create a `templates` folder and add an `index.html` file with the following code:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Keyword Clustering</title>
</head>
<body>
    <h1>Keyword Clustering</h1>
    <form method="post" enctype="multipart/form-data">
        <label for="location_name">Location Name:</label>
        <select name="location_name">
            <!-- Add country names as options here -->
        </select><br><br>

        <label for="language_name">Language Name:</label>
        <select name="language_name">
            <!-- Add Google languages as options here -->
        </select><br><br>

        <label for="domain_name">Domain Name:</label>
        <input type="text" name="domain_name" required><br><br>

        <label for="keywords_file">Keywords File (CSV):</label>
        <input type="file" name="keywords_file" required><br><br>

        <input type="submit" value="Cluster Keywords">
    </form>
</body>
</html>
```
Replace the `<!-- Add country names as options here -->` and `<!-- Add Google languages as options here -->` comments with the appropriate `<option>` elements for countries and languages.

5. Run the Flask app:

```bash
export FLASK_APP=app.py
export FLASK_ENV=production
flask run --host=0.0.0.0 --port=8000
```

Access the web application in your browser at http://0.0.0.0:8000/ and upload a CSV file with the required columns.

The app will process the CSV file, cluster the keywords, and return a new CSV file with the specified columns.