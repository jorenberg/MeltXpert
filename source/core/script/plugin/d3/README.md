# Data Visualization in MeltXpert®
## Definition
Data visualization or data visualisation is viewed by many disciplines as a modern equivalent of visual communication. (e.g. it is viewed as a branch of descriptive statistics by some, but also as a grounded theory development tool by others). It involves the creation and study of the visual representation of data, meaning "information that has been abstracted in some schematic form, including attributes or variables for the units of information".

A primary goal of data visualization is to communicate information clearly and efficiently to users via the statistical graphics, plots, information graphicscharts selected. Effective visualization helps users analyze and reason about data and evidence. It makes complex data more accessible, understandable and usable. Users may have particular analytical tasks, such as making comparisons or understanding causality, and the design principle of the graphic (i.e., showing comparisons or showing causality) follows the task. Tables are generally used where users will look-up a specific measurement, while charts of various types are used to show patterns or relationships in the data for one or more variables.

## Why in MeltXpert®
Data visualization is both an art and a science. It's a general term that describes any effort to help people understand the significance of data by placing it in a visual context, by help of Graph Theory. Patterns, trends and correlations that might go undetected in text-based data can be exposed and recognized easier with data visualization software.

That's why, for <b>Scientific Data Visualization</b> we're using many algorithms, methods and principles of it in <b>MeltXpert®</b>.

## D3 [Data-Driven Documents]
D3.js (or just D3 for Data-Driven Documents) is a JavaScript library for producing dynamic, interactive data visualizations in web browsers. It makes use of the widely implemented HTML5, CSS and SVG standards. It allows great control over the final visual result. D3 emphasizes web standards and combines powerful visualization components with a data-driven approach to DOM manipulation, giving the full capabilities of modern browsers without tying to use a proprietary framework.

URL: https://github.com/mbostock/d3 | https://d3js.org/.

## Graph Theory
In mathematics and computer science, graph theory is the study of graphs, which are mathematical structures used to model pairwise relations between objects. A graph in this context is made up of <i>vertices</i>, <i>nodes</i>, or <i>points</i> which are connected by <i>edges</i>, <i>arcs</i>, or <i>lines</i>.

### Definition
The following are some of the more basic ways of defining graphs and related mathematical structures.

<b>Graph:</b>

In the most common sense of the term, a <i>graph</i> is an ordered pair <i>G = (V, E)</i> comprising a set <i>V</i> of <i>vertices</i> or <i>nodes</i> or <i>points</i> together with a set <i>E</i> of <i>edges</i> or <i>arcs</i> or <i>lines</i>, which are 2-element subsets of <i>V</i> (i.e. an edge is related with two vertices, and the relation is represented as an unordered pair of the vertices with respect to the particular edge).

<b>Mathematical Expression:</b> <i>E</i> ⊆ [<i>V</i>]<sup>2</sup>;
  
  thus, the elements of <i>E</i> are 2-element subsets of <i>V</i>.

<b>Note:</b> To avoid notational ambiguities, always assume tacitly that <i>V</i> ∩ <i>E</i> = Ø.

<a name="degree" href="#degree">#</a>&nbsp;<b>The degree of a vertex:</b>

Let <i>G</i> = (<i>V</i>, <i>E</i>) be a (non-empty) graph.

The <i>degree</i> (or <i>valency</i>) <i>d<sub>G</sub></i>(<i>u</i>) = <i>d</i>(<i>u</i>) of a vertex <i>u</i> is the number |<i>E</i>(<i>u</i>)| of edges at <i>u</i>; by the definition of a graph, this is equal to the number of neighbours of <i>u</i>.

<b>Note:</b> A vertex of degree 0 is <i>isolated</i>.

- The number ∂(<i>G</i>) := min { <i>d</i>(<i>u</i>) | <i>u</i> ∈ V }, is the <i>minimum degree</i> of <i>G</i>,
- the number ∆(<i>G</i>) := max { <i>d</i>(<i>u</i>) | <i>u</i> ∈ V }, is the <i>maximum degree</i> of <i>G</i>.

<b>Note:</b>
- If all the vertices of <i>G</i> have the same degree <i>k</i>, then <i>G</i> is <i>k-regular</i>, or simply <i>regular</i>.
- A 3-regular graph is called <i>cubic</i>.
