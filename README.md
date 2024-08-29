# Mapping Cultural Networks in the Global South Book Market

This repo contains the data obtained and processed as part of the research that conducted to the paper titled "Mapping Cultural Networks in the Global South Book Market".

The following tables were created and calculated using the free SNA software Gephi. The node and edge tables used to run these metrics in Gephi were obtained following the procedure explained in the Data Extraction and Compilation section. A brief explanation of the meaning of the metrics used and the relationship established between them and the Shanghai network can be found in The Shanghai Network through SNA: Approaches and Metrics section.

## Data Extraction and Compilation

The data analyzed in this study were collected from a corpus of cultural magazines in Argentina during the 1980s and 1990s. _Babel. Revista de Libros_ (1988-1991), _Diario de Poesía. Información, creación y ensayo_ (1986-2012), _Con V de Vian_ (1990-1999), as well as the cultural columns from newspapers such as _El Porteño_ (1982-1993) or _Página/12_ (1987-present), served as the primary sources for tracing the Shanghai network during
the last two decades of the twentieth century. Information about the network from the twenty-first century onward was obtained from personal interviews, memoirs, and publishers’ catalogs, demonstrating the network’s existence at least until 2010.

The process of data extraction proceeded as follows: Initially, I conducted a “distant reading” of each issue of the journals, accumulating a body of reviews, articles, interviews, and essays in which prominent authors belonged to the Shanghai group. Given that a majority of these documents were scanned magazines, I employed optical character recognition (OCR) software to convert images into searchable text. Once the text was digitized, a Python function was employed to identify all capitalized letters. I utilized the following function, wherein `file_path` was replaced with the actual path to my text file, and `capitalized_words` executed the search for capitalized words within the text file:

```
import re

def find_capitalized_words(file_path:str)->list:
    capitalized_words = []

    with open (file_path , 'r') as file:
    text = file.read()
    pattern = r'\b[A-Z][a-zA-Z ]*\b'
    capitalized_words = re.findall(pattern , text)

    return capitalized_words
```

The function generated an extensive roster of proper names linked with each text and author, encompassing names of individuals, geographic locations, institutions, and titles of artistic works—all of which are conventionally capitalized in the Spanish language. Subsequently, data cleaning was performed to eliminate names unrelated to human beings. Additionally, a distinction was made between individuals associated with the
Argentine cultural sphere and other international authors frequently referenced by Shanghai members. While the latter group could prove valuable in studying the global literary canon established by these authors, they did not contribute to insights regarding social interactions within the local literary arena.

This list played a key role in establishing the datasets for Shanghai’s network during the 1980s and 1990s. However, during the final stage of interactions (2002-2010), the dearth of periodic publications provoked the exploration of relations through local editorial catalogs, digital newspaper searches, and interviews. Due to the scarcity of information there, the data collection process was not automated and I manually introduced it into
the dataset. Once the initial database with the list of nodes was concluded, I constructed a relational database organized as shown in the Tables termed "Gephi_Edges/Nodes". Here “id” served as an enumeration for each relationship within the network. “source” indicated the author signing each text, while “target” represented the names of Argentinian writers extracted using the Python function. The “type” field classified relationships as either “directed” or “undirected”. The “relations” column described the specific nature of the connection between nodes, drawing from the type of text or textual reference found in the corpus. The “weight” attribute assigns a value to each relationship, where all the weights are normalized so that they sum to 1.0. Higher weights were assigned to inter-textual interactions like comments (𝐶 = 2.5) and mentions (𝑀 = 1.5), while social encounters (𝐸𝑛𝑐 = 0.3) and participation in the same issue of _Babel. Revista de Libros_ (𝐵 = 0.25) held lower significance. Finally, the “year” column encompassed the date of the relationship or, in the case of the magazine network dataset, the issue number (1-22) in which the interactions occurred. 

The fundamental dataset was formed by the “source” and “target” columns, while attributes like “relations”, “type”, “weight”, and “year” provided additional context. The research data has been divided into four tables to represent the network’s evolution over the years, accounting for fluctuations in the number of members and metrics such as density, centrality, clustering coefficient, and centralization specific to each period. As the primary focus was on investigating diachronic changes within the network, the tables indicating the years of exchanges offer a comprehensive view of how the metric changes are intertwined with literary and sociological developments in the Shanghai circle over time.

## The Shanghai Network through SNA: Approaches and Metrics

As announced, SNA metrics are used, and they can be viewed in the remaining tables, termed with the time interval of every phase on the Shanghai network across the years. Density is the ratio of existing connections to the total number of possible connections in a network, representing the degree of interconnectedness among actors. In a graph representation, it is calculated by dividing the total lines connecting nodes by the maximum number of possible lines, while a result closer to 1 indicates a more densely populated network. The clustering coefficient in social network theory assesses how well a node connects highly connected regions without considering its importance in terms of information flow. Centrality measures the extent to which certain nodes accumulate the highest number of interactions, inspired by the concept of “star” actors in Sociometry. Local centrality applies when nodes are central only to their closest contacts, while global centrality means they are central to the entire network. PageRank and weighted degree have also been used as measures indicating the centralization of the network. Both were calculated with Gephi (Page et al. 1999), and while the first one is an algorithm that measures the importance of nodes within a network based on the quantity and quality of connections to them, the second one shows the sum of the weights of edges connected to a node. The eigenvector centrality, also estimated by Gephi, measures the influence of a node in a network, determined by the centrality of its neighbors.
