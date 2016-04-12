# Data Visualization in MeltXpert®
## Definition
Data visualization or data visualisation is viewed by many disciplines as a modern equivalent of visual communication. (e.g. it is viewed as a branch of descriptive statistics by some, but also as a grounded theory development tool by others). It involves the creation and study of the visual representation of data, meaning "information that has been abstracted in some schematic form, including attributes or variables for the units of information".

A primary goal of data visualization is to communicate information clearly and efficiently to users via the statistical graphics, plots, information graphics and charts. Effective visualization helps users analyze and reason about data and evidence. It makes complex data more accessible, understandable and usable. Users may have particular analytical tasks, such as making comparisons or understanding causality, and the design principle of the graphic (i.e., showing comparisons or showing causality) follows the task. Tables are generally used where users will look-up a specific measurement, while charts of various types are used to show patterns or relationships in the data for one or more variables.

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

<a name="cycles" href="#cycles">#</a>&nbsp;<b>Paths and Cycles:</b>

A <i>path</i> is a (non-empty) graph <i>P</i> = (<i>V</i>, <i>E</i>) of the form,

<i>V</i> = { x<sub>0</sub>, x<sub>1</sub>,..., x<i><sub>k</sub></i> }

<i>E</i> = { x<sub>0</sub>x<sub>1</sub>, x<sub>1</sub>x<sub>2</sub>,..., x<i><sub>k-1</sub></i> - x<i><sub>k</sub></i> },

Where the x<i><sub>i</sub></i> are all distinct.

The vertices x<sub>0</sub> and x<sub>k</sub> are <i>linked</i> by <i>P</i> and are called it's <i>ends</i>; the vertices x<sub>1</sub>,..., x<sub>k-1</sub> are the <i>inner</i> vertices of <i>P</i>.

The number of edges of a path is it's <i>length</i>, and the path of length <i>k</i> is denoted by <i>P<sup>k</sup></i>.

Note, that <i>k</i> is allowed to be zero; thus, <i>P<sup>0</sup></i> = <i>K<sup>1</sup></i>.

<a name="connectivity" href="#connectivity">#</a>&nbsp;<b>Connectivity:</b>

A (non-empty) graph <i>G</i> is called <i>connected</i>, if any two of it's vertices are linked by a path in <i>G</i>. If <i>U</i> ⊆<i>V</i>(<i>G</i>) and <i>G</i>[<i>U</i>] is connected, also called <i>U</i> itself connected (in <i>G</i>).

<b>Note:</b> Instead of 'not connected', usually can say 'disconnected'.

<a name="trees" href="#trees">#</a>&nbsp;<b>Trees and Forests:</b>

An <i>acyclic</i> graph, one not containing any cycles, is called <i>forest</i>. A connected forest is called a <i>tree</i>. (Thus, a forest is a graph whose components are trees). The <i>vertices</i> of <i>degree</i> 1 in a tree are it's <i>leaves</i>. Every non-trivial tree has a leaf - consider, for example, the ends of a longest path.

<b>Theorem:</b>

<i>The following assertions are equivalent for a graph T</i>:
- <i>T is a tree</i>;
- <i>Any two vertices of T are linked by a unique path in T</i>;
- <i>T is minimally connected, i.e. T is connected but T - e is disconnected for every edge e ∈ T</i>;
- <i>T is maximally acyclic, i.e., T contains no cycle but T + xy does, for any two non-adjacent vertices x,y ∈ T</i>.

<a name="eulertour" href="#eulertour">#</a>&nbsp;<b>Euler Tour:</b>

In <i>graph theory</i>, an <i>Eulerian trail</i> (or <i>Eulerian path</i>) is a trail in a graph which visits every <i>edge</i> exactly once.

The term <i>Eulerian graph</i> has two common meanings in graph theory. One meaning is a graph with an <i>Eulerian circuit</i>, and the other is a graph with every <i>vertex</i> of even <i>degree</i>. These definitions coincide for connected graphs.

<b>Definition:</b>

An <i>Eulerian cycle</i>, <i>Eulerian circuit</i> or <i>Euler tour</i> in an <i>undirected graph</i> is a cycle that uses each <i>edge</i> exactly once. If such a cycle exists, the graph is called <i>Eulerian</i> or <i>unicursal</i>.

<b>Note:</b> A graph is <i>Eulerian</i>, if it admits an <b>Euler Tour</b>.

<b>Theorem:</b>

<i>A connected graph is <b>Eulerian</b> if and only if every vertex has even degree</i>.

## Visualising MeltXpert®
In <b>MeltXpert®</b>, we're using [d3](https://github.com/mbostock/d3) as a core library and their following plugins for Data Visualization:

01. [d3-array](https://github.com/d3/d3-array): <i>Array manipulation, ordering, searching, summarizing, etc</i>.
02. [d3-collection](https://github.com/d3/d3-collection): <i>Handy data structures for elements keyed by string</i>.
03. [d3-color](https://github.com/d3/d3-color): <i>Color spaces! RGB, HSL, Cubehelix, Lab (CIELAB) and HCL (CIELCH)</i>.
04. [d3-dispatch](https://github.com/d3/d3-dispatch): <i>Register named callbacks and call them with arguments.</i>.
05. [d3-ease](https://github.com/d3/d3-ease): <i>Easing functions for smooth animation</i>.
06. [d3-force](https://github.com/d3/d3-force): <i>Force-directed graph layout using velocity Verlet integration</i>.
07. [d3-hierarchy](https://github.com/d3/d3-hierarchy): <i>Layout algorithms for visualizing hierarchical data</i>.
08. [d3-hive](https://github.com/d3/d3-plugins): <i>A plugin for rendering Hive Plots</i>.
09. [d3-interpolate](https://github.com/d3/d3-interpolate): <i>Interpolate numbers, colors, strings, arrays, objects, whatever</i>.
10. [d3-keybinding](https://github.com/d3/d3-plugins): <i>Keybindings for d3</i>.
11. [d3-path](https://github.com/d3/d3-path): <i>Serialize Canvas path commands to SVG</i>.
12. [d3-queue](https://github.com/d3/d3-queue): <i>Evaluate asynchronous tasks with configurable concurrency</i>.
13. [d3-random](https://github.com/d3/d3-random): <i>Generate random numbers from various distributions</i>.
14. [d3-selection](https://github.com/d3/d3-selection): <i>Transform the DOM by selecting elements and joining to data</i>.
15. [d3-stack](https://github.com/mbostock/stack): <i>A presentation library with intuitive, scroll-based navigation</i>.

### Using d3

<a name="usingd3" href="#usingd3">#</a>&nbsp;<b>Browser/Platform Support:</b>

D3 supports so-called “modern” browsers, which generally means everything except IE8 and older versions. D3 is can work against Firefox, Chrome, Safari, Opera, IE9+, Android and iOS. Parts of D3 may work in older browsers, as the core D3 library has minimal requirements: JavaScript and the [W3C DOM](http://www.w3.org/DOM/) API. D3 uses the [Selectors API](http://www.w3.org/TR/selectors-api/) Level 1, but can work with preloading [Sizzle](http://sizzlejs.com/) for compatibility. We'll need a modern browser to use [SVG](http://www.w3.org/TR/SVG/) and [CSS3 Transitions](http://www.w3.org/TR/css3-transitions/). D3 is not a compatibility layer, so if any browser doesn't support standards, you're out of luck. Sorry!

D3 also runs on [Node.js](http://nodejs.org/)®. Use ```npm install d3``` to <i>install</i> it.

Note, that because Node itself lacks a DOM and multiple DOM implementations exist for it (e.g., [JSDOM](https://github.com/tmpvar/jsdom)), we'll need to explicitly pass in a DOM element to our d3 methods like so:

```js
  var d3 = require("d3"),
      jsdom = require("jsdom");
  
  var document = jsdom.jsdom(),
      svg = d3.select(document.body).append("svg");
```

D3 can also run within a [WebWorker](http://www.whatwg.org/specs/web-apps/current-work/multipage/workers.html) by creating a [custom build](https://github.com/mbostock/smash/wiki) containing only the desired (non-DOM) features.

<a name="installingd3" href="#installingd3">#</a>&nbsp;<b>Installing:</b>

Download the latest version from here:

- [https://github.com/mbostock/d3/releases](https://github.com/mbostock/d3/releases)

Or, to link directly to the latest release, copy this snippet:

```js
  <script type="text/javascript" src="https://d3js.org/d3.v3.min.js" charset="utf-8"></script>
```

<b>Note:</b> The non-minified source code contains non-ASCII characters and must be served with `UTF-8` encoding, either via the `charset="utf-8"` attribute on the script tag or by adding `<meta charset="utf-8">` to the top of the page.

If we see a SyntaxError: Unexpected token ILLEGAL at ```var Ï€ = Math.PI```, it is because we are serving the non-minified source with the incorrect `ISO-8859-1` encoding. See this [StackOverflow](http://stackoverflow.com/a/14301241) answer for more information.

<a name="using-d3" href="#using-d3">#</a>&nbsp;<b>Using D3:</b>

When developing locally, note that our browser may enforce strict permissions for reading files out of the local file system. If we're using [<b>d3.xhr</b>](https://github.com/mbostock/d3/wiki/Requests) locally (including d3.json <i>et al</i>.), must have a local web server.

D3 supports the asynchronous module definition (AMD) API. For example, while using [RequireJS](http://requirejs.org/), it may load as follows:

```js
  require.config({
    paths: {
      d3: "https://d3js.org/d3.v3.min"
    }
  });

  require(["d3"], function(d3) {
    console.log(d3.version);
  });
```
