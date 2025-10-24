# Last.fm Exploratory Data Analysis

**Authors:** Hanzhe Jiang (hj2614), Jae Huang (jh9004)

**Course:** Data Bootcamp - Midterm Project

**Data Source:** Last.fm API

**Endpoints Used:** geo.getTopArtists, geo.getTopTracks, tag.getTopArtists, artist.getSimilar, artist.getTopTags

# IMPORTANT
Note: Our original notebook includes interactive widgets for genre and recommendation exploration, which works on Colab, but fails to load completely on Github. If the notebook fails to render on GitHub due to widget metadata errors, simply download the .ipynb file and open it locally in Jupyter or Colab to view the full interactive features. Otherwise, a .py file has been also attached for your reference. 

---

## Project Overview

This project explores global music-listening patterns based on data collected via the Last.fm API. Our goal was to conduct an exploratory data analysis to examine how music preferences vary across countries and genres. We also wanted to highlight how recommendation systems and tagging behavior affect the modern music landscape. By combining data from multiple API endpoints, we analyzed country-level trends, genre characteristics, and artist similarity connections, patterns regarding global and local parts of consumption.
<img width="1384" height="790" alt="image" src="https://github.com/user-attachments/assets/da3cdb4d-e208-49cb-bdd5-e723dada7b08" />
*(World map or bar chart comparing top artists by country)*

Our project demonstrates practical use of Python-based data science workflows, including API integration, data cleaning, visualization, and analysis. Throughout this notebook, we incorporated key Python libraries (pandas, matplotlib, seaborn, requests, and ipywidgets) to support both our analysis objectives and also for interactivity.

---

## Driving Questions

* How do popular artists and tracks differ across countries, and what does this reveal about cultural listening preferences?
* Which genres and tags dominate global music scenes, and how do they overlap or remain distinct?
* Can frequency-based recommendations reveal clusters of artists with similar audiences across genres?
* How consistent are popular tags across genres, and what does this imply about evolving genre boundaries?

---

## Methodology

Our data comes directly from the Last.fm API, a public interface that aggregates listener activity from millions of users by connecting to music platforms such as Spotify and Apple Music. The API provides access to information such as top artists, most-played tracks, genre tags, and artist similarities. For this analysis, we combined multiple API endpoints to build a well-rounded dataset.

To ensure data variety, we selected twelve countries across multiple continents, including the United States, Brazil, Germany, South Korea, and India. For each country, we retrieved both the top artists and top tracks using geo.getTopArtists and geo.getTopTracks. At the same time, we gathered genre-level data using the tag.getTopArtists endpoint, which returned artist lists for genres such as pop, rock, hip-hop, electronic, jazz, and R&B. Using these artists as seeds, we then used artist.getSimilar to find related artists and measure their similarity scores. Finally, we analyzed artist tags using artist.getTopTags to observe how listeners classify music. (We also added brief pauses between API requests using time.sleep() to avoid rate limits and integrated error handling to maintain data consistency.)

---

## Country-Level Analysis

In the first part of our analysis, we focused on understanding listening trends across countries. Using data from the geo.getTopArtists endpoint, we visualized the most popular artists by listener count. The results featured an interesting balance between global and regional preferences. Artists like Taylor Swift, The Weeknd, and Kendrick Lamar consistently ranked among the top in multiple countries, suggesting substantial international reach and universal appeal. Yet each country also exhibited local preferences, with domestic artists often dominating their respective charts.

When we examined track-level data using geo.getTopTracks, an interesting pattern emerged: individual songs often cross borders more easily than their artists do. For example, a single hit song may gain international traction even if the artist is not a global household name.
<img width="1381" height="790" alt="image" src="https://github.com/user-attachments/assets/efaf5d93-d614-4efd-89c2-a1f721feac16" />
*(Bar chart of top tracks by country)*

Overall, this part of our analysis highlights the duality of global music consumption. It appears that while the internet and streaming services have made international music more accessible than ever, cultural and linguistic preferences continue to shape what people listen to at home.

---

## Artist Similarity and Recommendation Patterns

In the next section, we analyzed artist relationships using the artist.getSimilar endpoint. By querying similar artists for top genre performers, we identified how frequently specific names appeared across different similarity lists. These artists, who appear multiple times, often act as "genre bridges," connecting diverse audiences through stylistic versatility. For example, Drake, The Weeknd, and Taylor Swift frequently surfaced across both pop and R&B or hip-hop lists, suggesting broad listener overlap.
<img width="672" height="455" alt="image" src="https://github.com/user-attachments/assets/ebc74dfe-1276-435a-997f-234641fb7740" />
*("Artists similar to Taylor Swift" bar chart)*

These results led us to develop a frequency-based recommendation approach. Our custom function, get_recommended_artists_by_genre, counts how often each artist is recommended across several top artist lists. We then visualized these results using two main plots: a bar chart ranking the most frequently recommended artists, and a scatter plot comparing frequency to average similarity score. Artists who appear often and have high match scores are likely to be globally influential and algorithmically favored.
<img width="1385" height="990" alt="image" src="https://github.com/user-attachments/assets/a3c7d61e-5ce0-4f0a-b002-5680e7b04a4b" />
*(Frequency vs. average match score scatter plot)*

The results confirm that recommendation systems tend to amplify already popular artists who blend multiple styles, further strengthening their dominance across genres. However, our research also identified niche artists who, despite lower frequency, had very high similarity scores, potentially indicating tightly connected communities around specific sounds.

---

## Tag Distribution and Genre Overlap

To explore how listeners categorize music, we collected the top tags associated with leading artists in six genres: pop, rock, hip-hop, electronic, jazz, and R&B. For each genre, the function get_top_tags_for_genre retrieved artist tags, aggregated their frequencies, and calculated the percentage distribution.
<img width="1789" height="1180" alt="image" src="https://github.com/user-attachments/assets/68a1cc1f-77d7-478b-8dd0-238877c2d6f9" />
*(Multi-panel bar charts showing tag distributions by genre)*

The results reveal both distinctive genre identities and cross-genre overlap. Pop and R&B share tags like "pop," "female vocalists," and "R&B," while electronic music overlaps with pop and indie. Jazz remains the most distinct, consistently defined by "blues," "vocal jazz," and "soul." These tag patterns reflect how listeners perceive genre boundaries. These overlapping identifiers support the idea of the growing fluidity of genre in today's streaming era. As recommendation algorithms prioritize sound-based and contextual similarity, artists increasingly transcend the traditionally strict stylistic categories, thus leading to the rise of hybrid genres and crossover collaborations.

---

## Findings and Interpretation

Our analysis yields several key insights, the first being that globalization and personalization coexist in music consumption. The same handful of international names dominate charts across multiple countries, yet regional artists still hold influence within their cultural contexts. This shows that while technology connects listeners globally, cultural heritage and language still play essential roles in shaping taste and influencing track rankings in each country.

Next, genre boundaries are becoming increasingly fluid. The overlap in tag distributions across pop, R&B, and electronic genres suggests that modern audiences value flexibility over rigid labels. Technically, this is reflected in how playlists and algorithmic recommendations have shifted the focus from genre loyalty to mood and style.

Additionally, recommendation algorithms reinforce the success of crossovers. Artists who appeal to multiple audiences are recommended more frequently, amplifying their visibility across platforms. However, this exact mechanism allows niche artists with high similarity scores to thrive within their own communities, highlighting the dual nature of algorithmic discovery.

Lastly, listener behavior and tagging patterns reflect cultural perception. The persistence of specific tags, such as "female vocalists" or "dance," across genres reveals how audiences associate identity, emotion, and movement with the music they enjoy.

---

## Limitations and Future Work

There are some constraints to this analysis. The Last.fm API imposes limits on the number of records returned per request, potentially reducing the dataset's representativeness. In addition, country data coverage is uneven; for example, some nations, such as South Korea, may return incomplete data due to smaller user bases or catalog restrictions. Lastly, Last.fm tags are community-generated and therefore subjective; they can vary widely based on cultural context or user interpretation. Not all music listeners are connected to Last.fm, so the data collected is not representative of the general population.

For future reference, expanding the dataset by combining Last.fm data with platforms such as Spotify and Apple Music could improve its accuracy. Additionally, incorporating time-series analysis could also reveal how music trends shift seasonally or over the years.

---

## Reproducibility and Setup

To reproduce our data and results this analysis:

1. Clone the repository and open the notebook file.
2. Insert your own Last.fm API key into the `api_key` variable.
3. Run all cells sequentially to fetch and analyze the data.
4. Ensure the following libraries are installed: pandas, matplotlib, seaborn, requests, ipywidgets, numpy, scipy.

---

## Conclusion

All in all, our exploratory data analysis reveals that both shared digital culture and distinct regional identities shape global music consumption. As streaming platforms and algorithms continue to evolve, they both reflect and influence listener behavior by encouraging diversity and amplifying cross-genre success. However, distinct cultural preferences persist, and while music may bring the world together, each audience still listens in its own unique way.
