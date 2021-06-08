The question: what do speakers of English and of Chinese write about and find interesting?
Secondarily, what patterns can be seen in the structure of this knowledge base? 

Data Sources:

The English and Chinese language versions of Wikipedia.  While there are several dialects behind its development, the Chinese site has been standardized into Mandarin, and the character set into the modern 'Simplified' Chinese writing system.  My focus began on the indexes of article titles and the structure of subcategories, but quickly expanded to article content (just main content at this stage - not including embedded lists, etc.)

The Wikipedia platform has a couple hundred ‘versions’ which are unique encyclopedias of identical basic structure in other languages (although they are not necessarily congruent in their topics of interest and fullest exploration).  Some languages rival the original English, while some have only a handful of articles and are just getting started.  I have used web scraping of indexes/article titles/content between these two language versions, and compare areas of activity based on categories (from general to specific based on each site’s own structure).  

Known Issues and Challenges:

The overall challenge of translation in conjuction with scraping stood out - I began by generating categories from the English index into a set of possible topics (then translated that into a set to search through the Chinese), so that as topics were found in the Chinese version, they could be linked to their English translation row-wise.  One problem with this was including topics that only appear in versions other than English, and this was at least partially addressed by taking a separate approach with data generated from the Chinese version based on it's own unique categories and subcategories (described below in 'Implementation').

Conceptually, the imbalance in total articles (English having around 6.3M, and Chinese with around 1.2M) presents a difficulty in comparing levels of interest between the populations of contributors, as those drawn to contribute may correlate with certain interests.  Additionally, as many articles and edits may be made by individuals belonging to both populations, accounting for this may be highly complex.  For this phase, I have simply addressed this per each method of analysis.

Implementation:

The vast majority of Wikipedia scraping projects that I found are in Python, with a few in R.

The translation process was determined as the googletrans Python library.  The second question was whether the structure of the topics and comprehensive crawling would be realistic for this scope of project, but it was determined that a crawl through the subcategories to simply retrieve the content behind the article links made for a good level of depth.  The scraping was done with the requests library and BeautifulSoup.

The most general categories of each language I've called 'level 1,' and the next layer - most general subtopics - 'level 2,' etc.

Matched Title Comparison - Generate a list of keywords from English levels 1 and 2, identify matching titles on Chinese side, and compare the pairs in terms of article length (post-translation), article text similarity (using Jaccard Similarity in scikitlearn).  As defined in the documentation, "The Jaccard index [1], or Jaccard similarity coefficient, defined as the size of the intersection divided by the size of the union of two label sets, is used to compare set of predicted labels for a sample to the corresponding set of labels in y_true."

Independent analysis - On corpora generated from each version's unique level 1 and 2 topics and the resulting article text (a given level 2 topic produces a broad article typically by the same name), performed Latent Dirichlet Allocation using Gensim and pyLDAvis, and word frequency distributions and treemaps with the Natural Language Toolkit and plotly.  Then look more deeply into the LDA topic models as interesting insights arise.

A simple interactive space, which also includes some interpretations and takeaways was created using Google Sites, and can be found at https://sites.google.com/view/atlas-of-articles.

Related projects of others:
(a flip on the question) https://en.wikipedia.org/wiki/Wikipedia:Wikipedia_articles_written_in_the_greatest_number_of_languages
(the traffic approach) https://stackoverflow.com/questions/5323589/how-to-use-wikipedia-api-to-get-the-page-view-statistics-of-a-particular-page-in
