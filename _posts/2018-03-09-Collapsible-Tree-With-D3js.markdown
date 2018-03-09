---
layout: post
title:  "A Collapsible Tree with D3.js"
date:   2018-03-02 13:15:36 +0100
categories: javascript
permalink: "/Collapsible-Tree-With-D3js"
---

In this post I will try to describe as clearly as possible the generation of a tree-diagram using the javascript library D3.js.

The reason I stumbled over this in the first place is that when diving into Tableau we had stumbled over the possibility to create node-tree diagrams. In particular, Jeffrey Shaffer pioneered the generation of such node-tree diagrams in Tableau.


<div style="height: 800px; width: 1000;" id="example"></div>

<style>

.node {
  cursor: pointer;
}

.node circle {
  fill: #fff;
  stroke: steelblue;
  stroke-width: 1.5px;
}

.node text {
  font: 10px sans-serif;
}

.link {
  fill: none;
  stroke: #ccc;
  stroke-width: 1.5px;
}

</style>

<script src="http://d3js.org/d3.v3.min.js"></script>

<script>

var margin = {top: 20, right: 120, bottom: 20, left: 120},
    width = 960 - margin.right - margin.left,
    height = 800 - margin.top - margin.bottom;

var i = 0,
    duration = 750,
    root;

var tree = d3.layout.tree()
    .size([height, width]);

var diagonal = d3.svg.diagonal()
    .projection(function(d) { return [d.y, d.x]; });

var svg = d3.select("div#example").append("svg")
    .attr("width", width + margin.right + margin.left)
    .attr("height", height + margin.top + margin.bottom)
  .append("g")
    .attr("transform", "translate(" + margin.left + "," + margin.top + ")");

var data = '{ "name": "DE45245235", "children": [ { "name": "AT75124", "size": 17010 }, { "name": "DE0473947", "children": [ {"name": "LU3493424", "size": 3534} ] }, { "name": "AT845654", "size": 353 }, { "name": "DE1234", "children": [ {"name": "DE98533", "children": [ {"name": "DE5689", "size": 2138}, {"name": "DE1437934", "size": 3824},{"name": "AT93842", "size": 1353}, {"name": "AT1234083", "size": 4665}, {"name": "LU134739", "size": 2649}, {"name": "DE1243934", "children": [ {"name": "DE74153", "size": 2138}, {"name": "DE713", "size": 3824}, {"name": "DE14635", "size": 763}, {"name": "AT3542345", "size": 5222}, {"name": "DE8265", "size": 7862}, {"name": "AT9673", "size": 8435} ] }, {"name": "DE097134", "size": 4896}, {"name": "DE13493", "size": 763}, {"name": "AT130943", "size": 5222}, {"name": "DE0932439", "size": 7862}, {"name": "AT09234", "size": 8435} ] }, {"name": "LU964694", "size": 1675} ] }, { "name": "BE8562452", "size": 2313 }, { "name": "DE9834923894", "children": [ {"name": "DE085324", "size": 2042} ] }, { "name": "DE9459458", "size": 6314 }, { "name": "DE84294839", "size": 4614 }, { "name": "ES234", "size": 20859 }, { "name": "ES237849", "size": 4461 }, { "name": "FR32894", "children": [ {"name": "FR84394893", "children": [ {"name": "IT92347923", "size": 6725} ] }, {"name": "FR123", "size": 3727}, {"name": "FR9034", "size": 9317}, {"name": "IT2349", "children": [ {"name": "IT92347923", "size": 6725}, {"name": "IT347932", "size": 3727}, {"name": "IT65923", "children": [ {"name": "IT02397493", "size": 6725}, {"name": "IT143234", "size": 3727}, {"name": "IT023947293", "size": 9317} ] }, {"name": "IT134238", "size": 12003}, {"name": "IT9273492", "size": 4853}, {"name": "FR134793", "children": [ {"name": "IT6832046208", "size": 6725}, {"name": "IT298342398", "size": 9317} ] }, {"name": "IT5793", "size": 4864}, {"name": "ES237432", "size": 3174}, {"name": "FR43242", "children": [ {"name": "IT023974923", "size": 6725}, {"name": "IT1231738", "size": 9317} ] }, {"name": "IT239479234", "size": 12870}, {"name": "IT7937493", "size": 2728}, {"name": "IT20342", "size": 12348}, {"name": "IT028343", "size": 870}, {"name": "IT09237493", "size": 9121}, {"name": "IT092349", "size": 9191} ] }, {"name": "AT09348", "size": 4853}, {"name": "FR12983742", "size": 8411}, {"name": "IT8403", "size": 4864}, {"name": "ES729347", "size": 3174}, {"name": "FR9104", "size": 7881}, {"name": "FR05634", "size": 12870}, {"name": "FR18348932", "size": 2728}, {"name": "FR09384", "size": 12348}, {"name": "FR12493", "size": 870}, {"name": "US129439", "size": 9121}, {"name": "FR093043", "size": 9191} ] }, { "name": "FR32894", "size": 5219 }, { "name": "GR273847283", "size": 9956 }, { "name": "IE724893", "size": 1286 }, { "name": "IT72384923879", "children": [ {"name": "IT832942", "size": 1041}, {"name": "IT2384932", "size": 5593} ] }, { "name": "IT123123", "size": 870 }, { "name": "LU2352", "size": 9191 }, { "name": "LU65398", "size": 2490 }, { "name": "NL73492", "size": 2023 }, { "name": "PT1313", "size": 16540 } ] }';

  root = JSON.parse(data);
  root.x0 = height / 2;
  root.y0 = 0;

  function collapse(d) {
    if (d.children) {
      d._children = d.children;
      d._children.forEach(collapse);
      d.children = null;
    }
  }

root.children.forEach(collapse);
update(root);

d3.select(self.frameElement).style("height", "800px");

function update(source) {

  // Compute the new tree layout.
  var nodes = tree.nodes(root).reverse(),
      links = tree.links(nodes);

  // Normalize for fixed-depth.
  nodes.forEach(function(d) { d.y = d.depth * 180; });

  // Update the nodes…
  var node = svg.selectAll("g.node")
      .data(nodes, function(d) { return d.id || (d.id = ++i); });

  // Enter any new nodes at the parent's previous position.
  var nodeEnter = node.enter().append("g")
      .attr("class", "node")
      .attr("transform", function(d) { return "translate(" + source.y0 + "," + source.x0 + ")"; })
      .on("click", click);

  nodeEnter.append("circle")
      .attr("r", 1e-6)
      .style("fill", function(d) { return d._children ? "lightsteelblue" : "#fff"; });

  nodeEnter.append("text")
      .attr("x", function(d) { return d.children || d._children ? -10 : 10; })
      .attr("dy", ".35em")
      .attr("text-anchor", function(d) { return d.children || d._children ? "end" : "start"; })
      .text(function(d) { return d.name; })
      .style("fill-opacity", 1e-6);

  // Transition nodes to their new position.
  var nodeUpdate = node.transition()
      .duration(duration)
      .attr("transform", function(d) { return "translate(" + d.y + "," + d.x + ")"; });

  nodeUpdate.select("circle")
      .attr("r", 4.5)
      .style("fill", function(d) { return d._children ? "lightsteelblue" : "#fff"; });

  nodeUpdate.select("text")
      .style("fill-opacity", 1);

  // Transition exiting nodes to the parent's new position.
  var nodeExit = node.exit().transition()
      .duration(duration)
      .attr("transform", function(d) { return "translate(" + source.y + "," + source.x + ")"; })
      .remove();

  nodeExit.select("circle")
      .attr("r", 1e-6);

  nodeExit.select("text")
      .style("fill-opacity", 1e-6);

  // Update the links…
  var link = svg.selectAll("path.link")
      .data(links, function(d) { return d.target.id; });

  // Enter any new links at the parent's previous position.
  link.enter().insert("path", "g")
      .attr("class", "link")
      .attr("d", function(d) {
        var o = {x: source.x0, y: source.y0};
        return diagonal({source: o, target: o});
      });

  // Transition links to their new position.
  link.transition()
      .duration(duration)
      .attr("d", diagonal);

  // Transition exiting nodes to the parent's new position.
  link.exit().transition()
      .duration(duration)
      .attr("d", function(d) {
        var o = {x: source.x, y: source.y};
        return diagonal({source: o, target: o});
      })
      .remove();

  // Stash the old positions for transition.
  nodes.forEach(function(d) {
    d.x0 = d.x;
    d.y0 = d.y;
  });
}

// Toggle children on click.
function click(d) {
  if (d.children) {
    d._children = d.children;
    d.children = null;
  } else {
    d.children = d._children;
    d._children = null;
  }
  update(d);
}

</script>
