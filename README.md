
# NLP-based Mind Map Generation to Support Brainstorming Sessions

### Abstract
<div style="text-align: justify">
Intelligent computer systems increasingly take on more tasks of humans, even in the context of creativity techniques. After an overview of current research approaches of support potentials of electronic creativity techniques and virtual moderators, this paper introduces natural language processing techniques to analyze brainstorming sessions. On this foundation, an artifact is developed that is able to generate mind maps in virtually real-time during electronic brainstorming sessions. The objective is to show mentioned terms to motivate the participants to continue own or foreign ideas and make user behavior visible.

### Main aspects

 - Tokenize statements, that are retrieved via Slack API calls
 - Compute the similarity of statements with respect to their semantic relationship
 - Generate a mind map, that group similar terms close to each other and show assoziation lines
 - Visualize the position of each participant in the mindmap (close to the menationed terms) and show the temporal dependencies.
 - Compute the similarity of persons w.r.t. the similarity of their statements to find persons that are important for each other.

## What I have learned

### Background
The background is the university lecture "Information retrieval and web search engines" in conjunction with a design thinking course about smart assistens. *Information retrieval* (IR) is the opposite goal of structuring semantic information in a way, that allows fast query processing. This results in high requirements for efficient data structures and algorithms. My goal was to deepen database knowledge in the context of strong runtime limitations (the mind map should be generated in almost real-time) while extract information of the data simultaneously.
Similar to the mind map, similar terms should be located close to each other (cluster hypothesis). This should provide a fast overview about the main topics of the brainstorming sessions and the opinion of each participant.

### Action

After implementation of my own distributed system via sockets, I switched to the [Slack](https://slack.com) environment to provide a trustworthuy and familiar user interface. Slack provies a chat platform with many automation capabilities and many componies use this to maintan their processes (e.g. onboarding).

To save and evaluate statements, I used the IR techniques (mostly mentioned in the book by [Manning et al.](https://nlp.stanford.edu/IR-book/pdf/irbookonlinereading.pdf)).
The data analysis gave me the opportunity to try several databases (in-memory, file-based and NoSQL).
To extract semantic information, I integrated the pretrained model by [SpaCy.io](https://spacy.io). Their solution allows a fast mapping of terms to a 300-dimensional vector space.
The term similarities were computed by the euclidian distance in this vector space. To project all terms into a two-dimensional mindmap, multiple dimensionality reduction techniques were evaluated.

### Lessons learned
A big challenge in this project was the real-time requirement in combination with the $O(n^2)$ for term similarity computation. Even if all data is stored in the main memory, for about one hour lasting brainstorming sessions, the mind map generation took a few minutes. A solutions could be a grouping of tokens, for example, that only the main topics are visualized and used for the similarity estimation. More detailed terms could be manually displayed on user commands, that integrates them into the computations when they are needed.

Also the dimensionality reduction by PCA provided the best results, but distorted the terms on the main components (large distances for similar terms, resulting in long association lines). The clustering in a way, that does prevent label overlapping is also a non-trivial problem. A focus on the main topics would address this limitation.

As a positive result, the mentioned topics and the position of the participants over the time could be recognized in the mind map. This shows the main functionality of such a system, but further optimizations are essential.
</div>
