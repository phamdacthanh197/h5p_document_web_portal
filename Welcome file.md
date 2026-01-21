---


---

<h1 id="h5p-rest-server---integration-guide">H5P REST Server - Integration Guide</h1>
<p>This document provides a comprehensive guide for integrating the <code>h5p-rest-server</code> into your existing projects, including architecture overview, sequence diagrams, database schemas, and step-by-step instructions.</p>
<hr>
<h2 id="table-of-contents">Table of Contents</h2>
<ol>
<li>
<p><a href="#architecture-overview">Architecture Overview</a></p>
</li>
<li>
<p><a href="#system-components">System Components</a></p>
</li>
<li>
<p><a href="#database-schema">Database Schema</a></p>
</li>
<li>
<p><a href="#authentication-flow">Authentication Flow</a></p>
</li>
<li>
<p><a href="#content-management-flow">Content Management Flow</a></p>
</li>
<li>
<p><a href="#integration-steps">Integration Steps</a></p>
</li>
<li>
<p><a href="#external-api-integration">External API Integration</a></p>
</li>
<li>
<p><a href="#configuration-reference">Configuration Reference</a></p>
</li>
</ol>
<hr>
<h2 id="architecture-overview">Architecture Overview</h2>
<p>The H5P REST Server follows a layered architecture pattern with clear separation of concerns:</p>
<pre class=" language-mermaid"><svg id="mermaid-svg-SAlz3rsmwhNR4rW2" width="100%" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" height="1217.5205078125" style="max-width: 694.78515625px;" viewBox="0 0 694.78515625 1217.5205078125"><style>#mermaid-svg-SAlz3rsmwhNR4rW2{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#000000;}#mermaid-svg-SAlz3rsmwhNR4rW2 .error-icon{fill:#552222;}#mermaid-svg-SAlz3rsmwhNR4rW2 .error-text{fill:#552222;stroke:#552222;}#mermaid-svg-SAlz3rsmwhNR4rW2 .edge-thickness-normal{stroke-width:2px;}#mermaid-svg-SAlz3rsmwhNR4rW2 .edge-thickness-thick{stroke-width:3.5px;}#mermaid-svg-SAlz3rsmwhNR4rW2 .edge-pattern-solid{stroke-dasharray:0;}#mermaid-svg-SAlz3rsmwhNR4rW2 .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-svg-SAlz3rsmwhNR4rW2 .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-svg-SAlz3rsmwhNR4rW2 .marker{fill:#666;stroke:#666;}#mermaid-svg-SAlz3rsmwhNR4rW2 .marker.cross{stroke:#666;}#mermaid-svg-SAlz3rsmwhNR4rW2 svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-svg-SAlz3rsmwhNR4rW2 .label{font-family:"trebuchet ms",verdana,arial,sans-serif;color:#000000;}#mermaid-svg-SAlz3rsmwhNR4rW2 .cluster-label text{fill:#333;}#mermaid-svg-SAlz3rsmwhNR4rW2 .cluster-label span{color:#333;}#mermaid-svg-SAlz3rsmwhNR4rW2 .label text,#mermaid-svg-SAlz3rsmwhNR4rW2 span{fill:#000000;color:#000000;}#mermaid-svg-SAlz3rsmwhNR4rW2 .node rect,#mermaid-svg-SAlz3rsmwhNR4rW2 .node circle,#mermaid-svg-SAlz3rsmwhNR4rW2 .node ellipse,#mermaid-svg-SAlz3rsmwhNR4rW2 .node polygon,#mermaid-svg-SAlz3rsmwhNR4rW2 .node path{fill:#eee;stroke:#999;stroke-width:1px;}#mermaid-svg-SAlz3rsmwhNR4rW2 .node .label{text-align:center;}#mermaid-svg-SAlz3rsmwhNR4rW2 .node.clickable{cursor:pointer;}#mermaid-svg-SAlz3rsmwhNR4rW2 .arrowheadPath{fill:#333333;}#mermaid-svg-SAlz3rsmwhNR4rW2 .edgePath .path{stroke:#666;stroke-width:1.5px;}#mermaid-svg-SAlz3rsmwhNR4rW2 .flowchart-link{stroke:#666;fill:none;}#mermaid-svg-SAlz3rsmwhNR4rW2 .edgeLabel{background-color:white;text-align:center;}#mermaid-svg-SAlz3rsmwhNR4rW2 .edgeLabel rect{opacity:0.5;background-color:white;fill:white;}#mermaid-svg-SAlz3rsmwhNR4rW2 .cluster rect{fill:hsl(210,66.6666666667%,95%);stroke:#26a;stroke-width:1px;}#mermaid-svg-SAlz3rsmwhNR4rW2 .cluster text{fill:#333;}#mermaid-svg-SAlz3rsmwhNR4rW2 .cluster span{color:#333;}#mermaid-svg-SAlz3rsmwhNR4rW2 div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:12px;background:hsl(-160,0%,93.3333333333%);border:1px solid #26a;border-radius:2px;pointer-events:none;z-index:100;}#mermaid-svg-SAlz3rsmwhNR4rW2:root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}#mermaid-svg-SAlz3rsmwhNR4rW2 flowchart{fill:apa;}</style><g><g class="output"><g class="clusters"><g class="cluster" id="flowchart-subGraph4-563" transform="translate(361.22265625,1143.9946556091309)" style="opacity: 1;"><rect width="651.125" height="131.05181121826172" x="-325.5625" y="-65.52590560913086"></rect><g class="label" transform="translate(0, -51.525901794433594)" id="mermaid-svg-SAlz3rsmwhNR4rW2Text"><g transform="translate(-38.5703125,-13.359375)"><foreignObject width="77.140625" height="26.71875"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Data Layer</div></foreignObject></g></g></g><g class="cluster" id="flowchart-subGraph3-564" transform="translate(176.56640625,931.75)" style="opacity: 1;"><rect width="337.1328125" height="193.4375" x="-168.56640625" y="-96.71875"></rect><g class="label" transform="translate(0, -82.71875)" id="mermaid-svg-SAlz3rsmwhNR4rW2Text"><g transform="translate(-54.7890625,-13.359375)"><foreignObject width="109.578125" height="26.71875"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Core H5P Layer</div></foreignObject></g></g></g><g class="cluster" id="flowchart-subGraph2-565" transform="translate(324.69140625,543.234375)" style="opacity: 1;"><rect width="523.03125" height="483.59375" x="-261.515625" y="-241.796875"></rect><g class="label" transform="translate(0, -227.796875)" id="mermaid-svg-SAlz3rsmwhNR4rW2Text"><g transform="translate(-62.640625,-13.359375)"><foreignObject width="125.28125" height="26.71875"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Application Layer</div></foreignObject></g></g></g><g class="cluster" id="flowchart-subGraph1-566" transform="translate(335.255859375,203.078125)" style="opacity: 1;"><rect width="445.30859375" height="96.71875" x="-222.654296875" y="-48.359375"></rect><g class="label" transform="translate(0, -34.359375)" id="mermaid-svg-SAlz3rsmwhNR4rW2Text"><g transform="translate(-67.1484375,-13.359375)"><foreignObject width="134.296875" height="26.71875"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">API Gateway Layer</div></foreignObject></g></g></g><g class="cluster" id="flowchart-subGraph0-567" transform="translate(347.23828125,56.359375)" style="opacity: 1;"><rect width="550.65625" height="96.71875" x="-275.328125" y="-48.359375"></rect><g class="label" transform="translate(0, -34.359375)" id="mermaid-svg-SAlz3rsmwhNR4rW2Text"><g transform="translate(-43.4140625,-13.359375)"><foreignObject width="86.828125" height="26.71875"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Client Layer</div></foreignObject></g></g></g></g><g class="edgePaths"><g class="edgePath LS-WEB LE-NGINX" id="L-WEB-NGINX" style="opacity: 1;"><path class="path" d="M192.34765625,79.71875L192.34765625,104.71875L192.34765625,129.71875L192.34765625,154.71875L270.7260892063813,179.71875" marker-end="url(https://stackedit.io/app#arrowhead74)" style="fill:none"></path><defs><marker id="arrowhead74" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath LS-MOBILE LE-NGINX" id="L-MOBILE-NGINX" style="opacity: 1;"><path class="path" d="M376.81640625,79.71875L376.81640625,104.71875L376.81640625,129.71875L376.81640625,154.71875L359.831349707189,179.71875" marker-end="url(https://stackedit.io/app#arrowhead75)" style="fill:none"></path><defs><marker id="arrowhead75" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath LS-LMS LE-NGINX" id="L-LMS-NGINX" style="opacity: 1;"><path class="path" d="M531.70703125,79.71875L531.70703125,104.71875L531.70703125,129.71875L531.70703125,154.71875L428.453125,181.31474607546346" marker-end="url(https://stackedit.io/app#arrowhead76)" style="fill:none"></path><defs><marker id="arrowhead76" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath LS-NGINX LE-EXPRESS" id="L-NGINX-EXPRESS" style="opacity: 1;"><path class="path" d="M343.9609375,226.4375L343.9609375,251.4375L343.9609375,276.4375L343.9609375,301.4375L343.9609375,326.4375" marker-end="url(https://stackedit.io/app#arrowhead77)" style="fill:none"></path><defs><marker id="arrowhead77" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath LS-EXPRESS LE-ROUTES" id="L-EXPRESS-ROUTES" style="opacity: 1;"><path class="path" d="M343.9609375,373.15625L343.9609375,398.15625L343.9609375,423.15625" marker-end="url(https://stackedit.io/app#arrowhead78)" style="fill:none"></path><defs><marker id="arrowhead78" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath LS-ROUTES LE-MIDDLEWARE" id="L-ROUTES-MIDDLEWARE" style="opacity: 1;"><path class="path" d="M343.9609375,469.875L343.9609375,494.875L343.9609375,519.875" marker-end="url(https://stackedit.io/app#arrowhead79)" style="fill:none"></path><defs><marker id="arrowhead79" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath LS-MIDDLEWARE LE-CONTROLLERS" id="L-MIDDLEWARE-CONTROLLERS" style="opacity: 1;"><path class="path" d="M343.9609375,566.59375L343.9609375,591.59375L343.9609375,616.59375" marker-end="url(https://stackedit.io/app#arrowhead80)" style="fill:none"></path><defs><marker id="arrowhead80" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath LS-CONTROLLERS LE-SERVICES" id="L-CONTROLLERS-SERVICES" style="opacity: 1;"><path class="path" d="M343.9609375,663.3125L343.9609375,688.3125L343.9609375,713.3125" marker-end="url(https://stackedit.io/app#arrowhead81)" style="fill:none"></path><defs><marker id="arrowhead81" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath LS-SERVICES LE-H5P_EDITOR" id="L-SERVICES-H5P_EDITOR" style="opacity: 1;"><path class="path" d="M304.875,744.521908358479L103.17578125,785.03125L103.17578125,810.03125L103.17578125,835.03125L103.17578125,860.03125" marker-end="url(https://stackedit.io/app#arrowhead82)" style="fill:none"></path><defs><marker id="arrowhead82" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath LS-SERVICES LE-H5P_PLAYER" id="L-SERVICES-H5P_PLAYER" style="opacity: 1;"><path class="path" d="M304.875,756.689411352542L249.53515625,785.03125L249.53515625,810.03125L249.53515625,835.03125L249.53515625,860.03125" marker-end="url(https://stackedit.io/app#arrowhead83)" style="fill:none"></path><defs><marker id="arrowhead83" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath LS-SERVICES LE-EXTERNAL_API" id="L-SERVICES-EXTERNAL_API" style="opacity: 1;"><path class="path" d="M383.046875,745.1767331817383L566.20703125,785.03125L566.20703125,810.03125L566.20703125,835.03125L566.20703125,883.390625L566.20703125,931.75L566.20703125,980.109375L566.20703125,1028.46875L566.20703125,1053.46875L566.20703125,1078.46875L566.20703125,1120.6352806091309" marker-end="url(https://stackedit.io/app#arrowhead84)" style="fill:none"></path><defs><marker id="arrowhead84" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath LS-H5P_EDITOR LE-H5P_STORAGE" id="L-H5P_EDITOR-H5P_STORAGE" style="opacity: 1;"><path class="path" d="M103.17578125,906.75L103.17578125,931.75L146.70566816437804,956.75" marker-end="url(https://stackedit.io/app#arrowhead85)" style="fill:none"></path><defs><marker id="arrowhead85" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath LS-H5P_PLAYER LE-H5P_STORAGE" id="L-H5P_PLAYER-H5P_STORAGE" style="opacity: 1;"><path class="path" d="M249.53515625,906.75L249.53515625,931.75L217.4026845214055,956.75" marker-end="url(https://stackedit.io/app#arrowhead86)" style="fill:none"></path><defs><marker id="arrowhead86" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath LS-H5P_STORAGE LE-MONGO" id="L-H5P_STORAGE-MONGO" style="opacity: 1;"><path class="path" d="M151.32848470315025,1003.46875L112.74609375,1028.46875L112.74609375,1053.46875L112.74609375,1078.46875L112.74609375,1105.545078277588" marker-end="url(https://stackedit.io/app#arrowhead87)" style="fill:none"></path><defs><marker id="arrowhead87" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath LS-H5P_STORAGE LE-S3" id="L-H5P_STORAGE-S3" style="opacity: 1;"><path class="path" d="M212.77986798263328,1003.46875L239.96484375,1028.46875L239.96484375,1053.46875L239.96484375,1078.46875L239.96484375,1107.1410446166992" marker-end="url(https://stackedit.io/app#arrowhead88)" style="fill:none"></path><defs><marker id="arrowhead88" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath LS-SERVICES LE-REDIS" id="L-SERVICES-REDIS" style="opacity: 1;"><path class="path" d="M360.3370292306139,760.03125L377.86328125,785.03125L377.86328125,810.03125L377.86328125,835.03125L377.86328125,883.390625L377.86328125,931.75L377.86328125,980.109375L377.86328125,1028.46875L377.86328125,1053.46875L377.86328125,1078.46875L377.86328125,1103.46875" marker-end="url(https://stackedit.io/app#arrowhead89)" style="fill:none"></path><defs><marker id="arrowhead89" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g></g><g class="edgeLabels"><g class="edgeLabel" transform="" style="opacity: 1;"><g transform="translate(0,0)" class="label"><rect rx="0" ry="0" width="0" height="0"></rect><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span id="L-L-WEB-NGINX" class="edgeLabel L-LS-WEB' L-LE-NGINX"></span></div></foreignObject></g></g><g class="edgeLabel" transform="" style="opacity: 1;"><g transform="translate(0,0)" class="label"><rect rx="0" ry="0" width="0" height="0"></rect><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span id="L-L-MOBILE-NGINX" class="edgeLabel L-LS-MOBILE' L-LE-NGINX"></span></div></foreignObject></g></g><g class="edgeLabel" transform="" style="opacity: 1;"><g transform="translate(0,0)" class="label"><rect rx="0" ry="0" width="0" height="0"></rect><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span id="L-L-LMS-NGINX" class="edgeLabel L-LS-LMS' L-LE-NGINX"></span></div></foreignObject></g></g><g class="edgeLabel" transform="" style="opacity: 1;"><g transform="translate(0,0)" class="label"><rect rx="0" ry="0" width="0" height="0"></rect><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span id="L-L-NGINX-EXPRESS" class="edgeLabel L-LS-NGINX' L-LE-EXPRESS"></span></div></foreignObject></g></g><g class="edgeLabel" transform="" style="opacity: 1;"><g transform="translate(0,0)" class="label"><rect rx="0" ry="0" width="0" height="0"></rect><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span id="L-L-EXPRESS-ROUTES" class="edgeLabel L-LS-EXPRESS' L-LE-ROUTES"></span></div></foreignObject></g></g><g class="edgeLabel" transform="" style="opacity: 1;"><g transform="translate(0,0)" class="label"><rect rx="0" ry="0" width="0" height="0"></rect><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span id="L-L-ROUTES-MIDDLEWARE" class="edgeLabel L-LS-ROUTES' L-LE-MIDDLEWARE"></span></div></foreignObject></g></g><g class="edgeLabel" transform="" style="opacity: 1;"><g transform="translate(0,0)" class="label"><rect rx="0" ry="0" width="0" height="0"></rect><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span id="L-L-MIDDLEWARE-CONTROLLERS" class="edgeLabel L-LS-MIDDLEWARE' L-LE-CONTROLLERS"></span></div></foreignObject></g></g><g class="edgeLabel" transform="" style="opacity: 1;"><g transform="translate(0,0)" class="label"><rect rx="0" ry="0" width="0" height="0"></rect><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span id="L-L-CONTROLLERS-SERVICES" class="edgeLabel L-LS-CONTROLLERS' L-LE-SERVICES"></span></div></foreignObject></g></g><g class="edgeLabel" transform="" style="opacity: 1;"><g transform="translate(0,0)" class="label"><rect rx="0" ry="0" width="0" height="0"></rect><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span id="L-L-SERVICES-H5P_EDITOR" class="edgeLabel L-LS-SERVICES' L-LE-H5P_EDITOR"></span></div></foreignObject></g></g><g class="edgeLabel" transform="" style="opacity: 1;"><g transform="translate(0,0)" class="label"><rect rx="0" ry="0" width="0" height="0"></rect><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span id="L-L-SERVICES-H5P_PLAYER" class="edgeLabel L-LS-SERVICES' L-LE-H5P_PLAYER"></span></div></foreignObject></g></g><g class="edgeLabel" transform="" style="opacity: 1;"><g transform="translate(0,0)" class="label"><rect rx="0" ry="0" width="0" height="0"></rect><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span id="L-L-SERVICES-EXTERNAL_API" class="edgeLabel L-LS-SERVICES' L-LE-EXTERNAL_API"></span></div></foreignObject></g></g><g class="edgeLabel" transform="" style="opacity: 1;"><g transform="translate(0,0)" class="label"><rect rx="0" ry="0" width="0" height="0"></rect><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span id="L-L-H5P_EDITOR-H5P_STORAGE" class="edgeLabel L-LS-H5P_EDITOR' L-LE-H5P_STORAGE"></span></div></foreignObject></g></g><g class="edgeLabel" transform="" style="opacity: 1;"><g transform="translate(0,0)" class="label"><rect rx="0" ry="0" width="0" height="0"></rect><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span id="L-L-H5P_PLAYER-H5P_STORAGE" class="edgeLabel L-LS-H5P_PLAYER' L-LE-H5P_STORAGE"></span></div></foreignObject></g></g><g class="edgeLabel" transform="" style="opacity: 1;"><g transform="translate(0,0)" class="label"><rect rx="0" ry="0" width="0" height="0"></rect><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span id="L-L-H5P_STORAGE-MONGO" class="edgeLabel L-LS-H5P_STORAGE' L-LE-MONGO"></span></div></foreignObject></g></g><g class="edgeLabel" transform="" style="opacity: 1;"><g transform="translate(0,0)" class="label"><rect rx="0" ry="0" width="0" height="0"></rect><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span id="L-L-H5P_STORAGE-S3" class="edgeLabel L-LS-H5P_STORAGE' L-LE-S3"></span></div></foreignObject></g></g><g class="edgeLabel" transform="" style="opacity: 1;"><g transform="translate(0,0)" class="label"><rect rx="0" ry="0" width="0" height="0"></rect><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span id="L-L-SERVICES-REDIS" class="edgeLabel L-LS-SERVICES' L-LE-REDIS"></span></div></foreignObject></g></g></g><g class="nodes"><g class="node default" id="flowchart-MONGO-519" label-offset-y="10.060132964816614" transform="translate(112.74609375,1143.9946556091309)" style="opacity: 1;"><path d="M 0,10.060132964816614 a 42.0859375,10.060132964816614 0,0,0 84.171875 0 a 42.0859375,10.060132964816614 0,0,0 -84.171875 0 l 0,56.77888296481662 a 42.0859375,10.060132964816614 0,0,0 84.171875 0 l 0,-56.77888296481662" transform="translate(-42.0859375,-38.44957444722492)" class="label-container" style="fill:#d4edda;"></path><g class="label" transform="translate(0,0)"><g transform="translate(-32.0859375,-13.359375)"><foreignObject width="64.171875" height="26.71875"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">MongoDB</div></foreignObject></g></g></g><g class="node default" id="flowchart-S3-520" label-offset-y="8.996159078178763" transform="translate(239.96484375,1143.9946556091309)" style="opacity: 1;"><path d="M 0,8.996159078178763 a 35.1328125,8.996159078178763 0,0,0 70.265625 0 a 35.1328125,8.996159078178763 0,0,0 -70.265625 0 l 0,55.71490907817876 a 35.1328125,8.996159078178763 0,0,0 70.265625 0 l 0,-55.71490907817876" transform="translate(-35.1328125,-36.853613617268145)" class="label-container" style="fill:#d4edda;"></path><g class="label" transform="translate(0,0)"><g transform="translate(-25.1328125,-13.359375)"><foreignObject width="50.265625" height="26.71875"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">AWS S3</div></foreignObject></g></g></g><g class="node default" id="flowchart-REDIS-521" label-offset-y="11.4443540734716" transform="translate(377.86328125,1143.9946556091309)" style="opacity: 1;"><path d="M 0,11.4443540734716 a 52.765625,11.4443540734716 0,0,0 105.53125 0 a 52.765625,11.4443540734716 0,0,0 -105.53125 0 l 0,58.1631040734716 a 52.765625,11.4443540734716 0,0,0 105.53125 0 l 0,-58.1631040734716" transform="translate(-52.765625,-40.5259061102074)" class="label-container" style="fill:#d4edda;"></path><g class="label" transform="translate(0,0)"><g transform="translate(-42.765625,-13.359375)"><foreignObject width="85.53125" height="26.71875"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Redis Cache</div></foreignObject></g></g></g><g class="node default" id="flowchart-EXTERNAL_API-522" transform="translate(566.20703125,1143.9946556091309)" style="opacity: 1;"><rect rx="0" ry="0" x="-85.578125" y="-23.359375" width="171.15625" height="46.71875" class="label-container"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-75.578125,-13.359375)"><foreignObject width="151.15625" height="26.71875"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">External Backend API</div></foreignObject></g></g></g><g class="node default" id="flowchart-H5P_EDITOR-516" transform="translate(103.17578125,883.390625)" style="opacity: 1;"><rect rx="0" ry="0" x="-47.7578125" y="-23.359375" width="95.515625" height="46.71875" class="label-container"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-37.7578125,-13.359375)"><foreignObject width="75.515625" height="26.71875"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">H5P Editor</div></foreignObject></g></g></g><g class="node default" id="flowchart-H5P_PLAYER-517" transform="translate(249.53515625,883.390625)" style="opacity: 1;"><rect rx="0" ry="0" x="-48.6015625" y="-23.359375" width="97.203125" height="46.71875" class="label-container"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-38.6015625,-13.359375)"><foreignObject width="77.203125" height="26.71875"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">H5P Player</div></foreignObject></g></g></g><g class="node default" id="flowchart-H5P_STORAGE-518" transform="translate(187.37890625,980.109375)" style="opacity: 1;"><rect rx="0" ry="0" x="-72.59375" y="-23.359375" width="145.1875" height="46.71875" class="label-container"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-62.59375,-13.359375)"><foreignObject width="125.1875" height="26.71875"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Storage Managers</div></foreignObject></g></g></g><g class="node default" id="flowchart-EXPRESS-511" transform="translate(343.9609375,349.796875)" style="opacity: 1;"><rect rx="0" ry="0" x="-61.8203125" y="-23.359375" width="123.640625" height="46.71875" class="label-container" style="fill:#fff3cd;"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-51.8203125,-13.359375)"><foreignObject width="103.640625" height="26.71875"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Express Server</div></foreignObject></g></g></g><g class="node default" id="flowchart-ROUTES-512" transform="translate(343.9609375,446.515625)" style="opacity: 1;"><rect rx="0" ry="0" x="-55.8515625" y="-23.359375" width="111.703125" height="46.71875" class="label-container"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-45.8515625,-13.359375)"><foreignObject width="91.703125" height="26.71875"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Routes Layer</div></foreignObject></g></g></g><g class="node default" id="flowchart-MIDDLEWARE-513" transform="translate(343.9609375,543.234375)" style="opacity: 1;"><rect rx="0" ry="0" x="-73.3046875" y="-23.359375" width="146.609375" height="46.71875" class="label-container"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-63.3046875,-13.359375)"><foreignObject width="126.609375" height="26.71875"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Middleware Layer</div></foreignObject></g></g></g><g class="node default" id="flowchart-CONTROLLERS-514" transform="translate(343.9609375,639.953125)" style="opacity: 1;"><rect rx="0" ry="0" x="-49.453125" y="-23.359375" width="98.90625" height="46.71875" class="label-container"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-39.453125,-13.359375)"><foreignObject width="78.90625" height="26.71875"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Controllers</div></foreignObject></g></g></g><g class="node default" id="flowchart-SERVICES-515" transform="translate(343.9609375,736.671875)" style="opacity: 1;"><rect rx="0" ry="0" x="-39.0859375" y="-23.359375" width="78.171875" height="46.71875" class="label-container" style="fill:#fff3cd;"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-29.0859375,-13.359375)"><foreignObject width="58.171875" height="26.71875"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Services</div></foreignObject></g></g></g><g class="node default" id="flowchart-NGINX-510" transform="translate(343.9609375,203.078125)" style="opacity: 1;"><rect rx="0" ry="0" x="-84.4921875" y="-23.359375" width="168.984375" height="46.71875" class="label-container"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-74.4921875,-13.359375)"><foreignObject width="148.984375" height="26.71875"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Nginx/Load Balancer</div></foreignObject></g></g></g><g class="node default" id="flowchart-WEB-507" transform="translate(192.34765625,56.359375)" style="opacity: 1;"><rect rx="0" ry="0" x="-85.4375" y="-23.359375" width="170.875" height="46.71875" class="label-container" style="fill:#e1f5ff;"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-75.4375,-13.359375)"><foreignObject width="150.875" height="26.71875"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Web Portal/Frontend</div></foreignObject></g></g></g><g class="node default" id="flowchart-MOBILE-508" transform="translate(376.81640625,56.359375)" style="opacity: 1;"><rect rx="0" ry="0" x="-49.03125" y="-23.359375" width="98.0625" height="46.71875" class="label-container" style="fill:#e1f5ff;"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-39.03125,-13.359375)"><foreignObject width="78.0625" height="26.71875"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Mobile App</div></foreignObject></g></g></g><g class="node default" id="flowchart-LMS-509" transform="translate(531.70703125,56.359375)" style="opacity: 1;"><rect rx="0" ry="0" x="-55.859375" y="-23.359375" width="111.71875" height="46.71875" class="label-container" style="fill:#e1f5ff;"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-45.859375,-13.359375)"><foreignObject width="91.71875" height="26.71875"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">External LMS</div></foreignObject></g></g></g></g></g></g></svg></pre>
<h3 id="key-features">Key Features</h3>
<ul>
<li>
<p>🔐 <strong>Shared Secret Key Auth</strong>: Uses shared JWT secret key from LMS (local login disabled)</p>
</li>
<li>
<p>📦 <strong>Scalable Storage</strong>: MongoDB for metadata, S3 for content files</p>
</li>
<li>
<p>⚡ <strong>Performance</strong>: Redis caching for sessions and frequently accessed data</p>
</li>
<li>
<p>🌐 <strong>i18n Ready</strong>: Multi-language support via i18next</p>
</li>
<li>
<p>📝 <strong>Auto-documented</strong>: Swagger/OpenAPI documentation</p>
</li>
<li>
<p>🐳 <strong>Container Ready</strong>: Docker and docker-compose included</p>
</li>
</ul>
<hr>
<h2 id="system-components">System Components</h2>
<h3 id="routes-layer">1. Routes Layer</h3>
<blockquote>
<p><strong>Note</strong>: Local authentication routes (<code>/login</code>, <code>/logout</code>, <code>/sso/login</code>) are currently <strong>disabled</strong>.</p>
</blockquote>
<blockquote>
<p>The server uses a shared secret key from the LMS for JWT token verification.</p>
</blockquote>
<blockquote>
<p>See <a href="./AUTHENTICATION.md">AUTHENTICATION.md</a> for details.</p>
</blockquote>
<pre class=" language-typescript"><code class="prism  language-typescript">
Routes

├── <span class="token operator">/</span>auth<span class="token operator">/</span>verify <span class="token operator">-</span> ✅ ACTIVE<span class="token punctuation">:</span> External  token  <span class="token function">verification</span> <span class="token punctuation">(</span>shared  secret  key<span class="token punctuation">)</span>

└── <span class="token operator">/</span>h5p<span class="token comment">/* - ✅ ACTIVE: H5P content operations

  

// Disabled routes (commented out):

// ├── /login - ❌ DISABLED: Local username/password authentication

// ├── /logout - ❌ DISABLED: Token invalidation

// └── /sso/login - ❌ DISABLED: Single sign-on with external user

</span></code></pre>
<h3 id="services-layer">2. Services Layer</h3>
<p>| Service | Responsibility |</p>
<p>|---------|---------------|</p>
<p>| <strong>AuthService</strong> | User authentication, token management, session handling |</p>
<p>| <strong>ContentService</strong> | H5P content CRUD operations, editor/player rendering |</p>
<p>| <strong>SessionCacheService</strong> | In-memory session caching with TTL |</p>
<p>| <strong>TokenVerificationService</strong> | External API token verification |</p>
<h3 id="storage-layer">3. Storage Layer</h3>
<p>| Storage Type | Technology | Purpose |</p>
<p>|-------------|-----------|---------|</p>
<p>| <strong>Content Storage</strong> | MongoDB + S3 | H5P content metadata and files |</p>
<p>| <strong>Library Storage</strong> | MongoDB + S3 | H5P libraries |</p>
<p>| <strong>User Data Storage</strong> | MongoDB | User progress and xAPI statements |</p>
<p>| <strong>Finished Data</strong> | MongoDB | Custom completion tracking |</p>
<p>| <strong>Session Cache</strong> | Redis / In-Memory | Session and permission caching |</p>
<hr>
<h2 id="database-schema">Database Schema</h2>
<h3 id="entity-relationship-diagram">Entity Relationship Diagram</h3>
<pre class=" language-mermaid"><svg id="mermaid-svg-7pl58wB2QENbaodZ" width="100%" xmlns="http://www.w3.org/2000/svg" height="40" style="max-width: 40px;" viewBox="-20 -20 40 40"><style>#mermaid-svg-7pl58wB2QENbaodZ{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#000000;}#mermaid-svg-7pl58wB2QENbaodZ .error-icon{fill:#552222;}#mermaid-svg-7pl58wB2QENbaodZ .error-text{fill:#552222;stroke:#552222;}#mermaid-svg-7pl58wB2QENbaodZ .edge-thickness-normal{stroke-width:2px;}#mermaid-svg-7pl58wB2QENbaodZ .edge-thickness-thick{stroke-width:3.5px;}#mermaid-svg-7pl58wB2QENbaodZ .edge-pattern-solid{stroke-dasharray:0;}#mermaid-svg-7pl58wB2QENbaodZ .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-svg-7pl58wB2QENbaodZ .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-svg-7pl58wB2QENbaodZ .marker{fill:#666;stroke:#666;}#mermaid-svg-7pl58wB2QENbaodZ .marker.cross{stroke:#666;}#mermaid-svg-7pl58wB2QENbaodZ svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-svg-7pl58wB2QENbaodZ .entityBox{fill:#eee;stroke:#999;}#mermaid-svg-7pl58wB2QENbaodZ .attributeBoxOdd{fill:#ffffff;stroke:#999;}#mermaid-svg-7pl58wB2QENbaodZ .attributeBoxEven{fill:#f2f2f2;stroke:#999;}#mermaid-svg-7pl58wB2QENbaodZ .relationshipLabelBox{fill:hsl(-160,0%,93.3333333333%);opacity:0.7;background-color:hsl(-160,0%,93.3333333333%);}#mermaid-svg-7pl58wB2QENbaodZ .relationshipLabelBox rect{opacity:0.5;}#mermaid-svg-7pl58wB2QENbaodZ .relationshipLine{stroke:#666;}#mermaid-svg-7pl58wB2QENbaodZ:root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}#mermaid-svg-7pl58wB2QENbaodZ er{fill:apa;}</style><g></g><defs><marker id="ONLY_ONE_START" refX="0" refY="9" markerWidth="18" markerHeight="18" orient="auto"><path stroke="gray" fill="none" d="M9,0 L9,18 M15,0 L15,18"></path></marker></defs><defs><marker id="ONLY_ONE_END" refX="18" refY="9" markerWidth="18" markerHeight="18" orient="auto"><path stroke="gray" fill="none" d="M3,0 L3,18 M9,0 L9,18"></path></marker></defs><defs><marker id="ZERO_OR_ONE_START" refX="0" refY="9" markerWidth="30" markerHeight="18" orient="auto"><circle stroke="gray" fill="white" cx="21" cy="9" r="6"></circle><path stroke="gray" fill="none" d="M9,0 L9,18"></path></marker></defs><defs><marker id="ZERO_OR_ONE_END" refX="30" refY="9" markerWidth="30" markerHeight="18" orient="auto"><circle stroke="gray" fill="white" cx="9" cy="9" r="6"></circle><path stroke="gray" fill="none" d="M21,0 L21,18"></path></marker></defs><defs><marker id="ONE_OR_MORE_START" refX="18" refY="18" markerWidth="45" markerHeight="36" orient="auto"><path stroke="gray" fill="none" d="M0,18 Q 18,0 36,18 Q 18,36 0,18 M42,9 L42,27"></path></marker></defs><defs><marker id="ONE_OR_MORE_END" refX="27" refY="18" markerWidth="45" markerHeight="36" orient="auto"><path stroke="gray" fill="none" d="M3,9 L3,27 M9,18 Q27,0 45,18 Q27,36 9,18"></path></marker></defs><defs><marker id="ZERO_OR_MORE_START" refX="18" refY="18" markerWidth="57" markerHeight="36" orient="auto"><circle stroke="gray" fill="white" cx="48" cy="18" r="6"></circle><path stroke="gray" fill="none" d="M0,18 Q18,0 36,18 Q18,36 0,18"></path></marker></defs><defs><marker id="ZERO_OR_MORE_END" refX="39" refY="18" markerWidth="57" markerHeight="36" orient="auto"><circle stroke="gray" fill="white" cx="9" cy="18" r="6"></circle><path stroke="gray" fill="none" d="M21,18 Q39,0 57,18 Q39,36 21,18"></path></marker></defs></svg></pre>
<h3 id="mongodb-collections">MongoDB Collections</h3>
<h4 id="h5p-content-collection">1. <strong>h5p-content</strong> Collection</h4>
<p>Stores H5P content metadata and parameters.</p>
<pre class=" language-typescript"><code class="prism  language-typescript">
<span class="token punctuation">{</span>

_id<span class="token punctuation">:</span> ObjectId<span class="token punctuation">,</span>

contentId<span class="token punctuation">:</span> <span class="token keyword">string</span><span class="token punctuation">,</span> <span class="token comment">// Unique content identifier</span>

metadata<span class="token punctuation">:</span> <span class="token punctuation">{</span>

title<span class="token punctuation">:</span> <span class="token keyword">string</span><span class="token punctuation">,</span>

authors<span class="token punctuation">:</span> <span class="token keyword">Array</span><span class="token punctuation">,</span>

license<span class="token punctuation">:</span> <span class="token keyword">string</span><span class="token punctuation">,</span>

mainLibrary<span class="token punctuation">:</span> <span class="token keyword">string</span><span class="token punctuation">,</span> <span class="token comment">// e.g., "H5P.InteractiveVideo"</span>

<span class="token comment">// ... other H5P metadata</span>

<span class="token punctuation">}</span><span class="token punctuation">,</span>

params<span class="token punctuation">:</span> <span class="token punctuation">{</span>

params<span class="token punctuation">:</span> object<span class="token punctuation">,</span> <span class="token comment">// Content-specific parameters</span>

metadata<span class="token punctuation">:</span> object

<span class="token punctuation">}</span><span class="token punctuation">,</span>

userId<span class="token punctuation">:</span> <span class="token keyword">string</span><span class="token punctuation">,</span> <span class="token comment">// Creator ID</span>

tenantId<span class="token operator">?</span><span class="token punctuation">:</span> <span class="token keyword">string</span><span class="token punctuation">,</span> <span class="token comment">// Multi-tenancy support</span>

branchId<span class="token operator">?</span><span class="token punctuation">:</span> <span class="token keyword">string</span><span class="token punctuation">,</span> <span class="token comment">// Organization/branch ID</span>

createdAt<span class="token punctuation">:</span> Date<span class="token punctuation">,</span>

updatedAt<span class="token punctuation">:</span> Date

<span class="token punctuation">}</span>

</code></pre>
<p><strong>Indexes:</strong></p>
<ul>
<li>
<p><code>{ contentId: 1, userId: 1 }</code></p>
</li>
<li>
<p><code>{ tenantId: 1, createdAt: -1 }</code></p>
</li>
<li>
<p><code>{ mainLibrary: 1 }</code></p>
</li>
</ul>
<h4 id="userdata-collection">2. <strong>userdata</strong> Collection</h4>
<p>Stores user interaction data and progress.</p>
<pre class=" language-typescript"><code class="prism  language-typescript">
<span class="token punctuation">{</span>

contentId<span class="token punctuation">:</span> <span class="token keyword">string</span><span class="token punctuation">,</span> <span class="token comment">// H5P content ID</span>

userId<span class="token punctuation">:</span> <span class="token keyword">string</span><span class="token punctuation">,</span> <span class="token comment">// User ID</span>

dataType<span class="token punctuation">:</span> <span class="token keyword">string</span><span class="token punctuation">,</span> <span class="token comment">// e.g., "state", "answered"</span>

subContentId<span class="token operator">?</span><span class="token punctuation">:</span> <span class="token keyword">string</span><span class="token punctuation">,</span> <span class="token comment">// Sub-content identifier</span>

data<span class="token punctuation">:</span> object<span class="token punctuation">,</span> <span class="token comment">// xAPI statement or state data</span>

timestamp<span class="token punctuation">:</span> <span class="token keyword">number</span><span class="token punctuation">,</span>

invalidate<span class="token punctuation">:</span> <span class="token keyword">boolean</span>

<span class="token punctuation">}</span>

</code></pre>
<p><strong>Indexes:</strong></p>
<ul>
<li><code>{ contentId: 1, userId: 1, dataType: 1, subContentId: 1 }</code></li>
</ul>
<h4 id="finisheddata-collection">3. <strong>finisheddata</strong> Collection</h4>
<p>Standard H5P completion tracking.</p>
<pre class=" language-typescript"><code class="prism  language-typescript">
<span class="token punctuation">{</span>

contentId<span class="token punctuation">:</span> <span class="token keyword">string</span><span class="token punctuation">,</span>

userId<span class="token punctuation">:</span> <span class="token keyword">string</span><span class="token punctuation">,</span>

score<span class="token punctuation">:</span> <span class="token keyword">number</span><span class="token punctuation">,</span>

maxScore<span class="token punctuation">:</span> <span class="token keyword">number</span><span class="token punctuation">,</span>

openedTimestamp<span class="token punctuation">:</span> <span class="token keyword">number</span><span class="token punctuation">,</span>

finishedTimestamp<span class="token punctuation">:</span> <span class="token keyword">number</span><span class="token punctuation">,</span>

completionTime<span class="token punctuation">:</span> <span class="token keyword">number</span>

<span class="token punctuation">}</span>

</code></pre>
<p><strong>Indexes:</strong></p>
<ul>
<li><code>{ contentId: 1, userId: 1 }</code> (unique)</li>
</ul>
<h4 id="custom-finisheddata-collection">4. <strong>custom-finisheddata</strong> Collection</h4>
<p>Extended completion tracking with custom metadata.</p>
<pre class=" language-typescript"><code class="prism  language-typescript">
<span class="token punctuation">{</span>

contentId<span class="token punctuation">:</span> <span class="token keyword">string</span><span class="token punctuation">,</span>

userId<span class="token punctuation">:</span> <span class="token keyword">string</span><span class="token punctuation">,</span>

score<span class="token punctuation">:</span> <span class="token keyword">number</span><span class="token punctuation">,</span>

maxScore<span class="token punctuation">:</span> <span class="token keyword">number</span><span class="token punctuation">,</span>

openedTimestamp<span class="token punctuation">:</span> <span class="token keyword">number</span><span class="token punctuation">,</span>

finishedTimestamp<span class="token punctuation">:</span> <span class="token keyword">number</span><span class="token punctuation">,</span>

completionTime<span class="token punctuation">:</span> <span class="token keyword">number</span><span class="token punctuation">,</span>

role<span class="token punctuation">:</span> ENUM_ROLE<span class="token punctuation">,</span> <span class="token comment">// User role at completion time</span>

branchId<span class="token operator">?</span><span class="token punctuation">:</span> <span class="token keyword">string</span><span class="token punctuation">,</span>

tenantId<span class="token operator">?</span><span class="token punctuation">:</span> <span class="token keyword">string</span><span class="token punctuation">,</span>

processedAt<span class="token punctuation">:</span> <span class="token keyword">number</span><span class="token punctuation">,</span> <span class="token comment">// Server processing timestamp</span>

scorePercentage<span class="token punctuation">:</span> <span class="token keyword">number</span><span class="token punctuation">,</span> <span class="token comment">// Calculated score percentage</span>

extraFields<span class="token operator">?</span><span class="token punctuation">:</span> object  <span class="token comment">// Client-provided custom data</span>

<span class="token punctuation">}</span>

</code></pre>
<p><strong>Indexes:</strong></p>
<ul>
<li>
<p><code>{ contentId: 1, userId: 1 }</code> (unique)</p>
</li>
<li>
<p><code>{ tenantId: 1, processedAt: -1 }</code></p>
</li>
<li>
<p><code>{ branchId: 1, processedAt: -1 }</code></p>
</li>
<li>
<p><code>{ processedAt: 1 }</code></p>
</li>
</ul>
<hr>
<h2 id="authentication-flow">Authentication Flow</h2>
<blockquote>
<p><strong>Current Configuration</strong>: Local authentication routes are <strong>disabled</strong>.</p>
</blockquote>
<blockquote>
<p>The H5P server uses a <strong>shared JWT secret key</strong> from the LMS for token verification.</p>
</blockquote>
<blockquote>
<p>For full details, see <a href="./AUTHENTICATION.md">AUTHENTICATION.md</a>.</p>
</blockquote>
<h3 id="token-verification-flow-active">Token Verification Flow (Active)</h3>
<p>This is the <strong>only active authentication flow</strong>. The LMS generates JWT tokens using a shared secret key, and the H5P server verifies them.</p>
<pre class=" language-mermaid"><svg id="mermaid-svg-plK8ChyHwVGOVAwx" width="100%" xmlns="http://www.w3.org/2000/svg" height="1395" style="max-width: 1342px;" viewBox="-50 -10 1342 1395"><style>#mermaid-svg-plK8ChyHwVGOVAwx{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#000000;}#mermaid-svg-plK8ChyHwVGOVAwx .error-icon{fill:#552222;}#mermaid-svg-plK8ChyHwVGOVAwx .error-text{fill:#552222;stroke:#552222;}#mermaid-svg-plK8ChyHwVGOVAwx .edge-thickness-normal{stroke-width:2px;}#mermaid-svg-plK8ChyHwVGOVAwx .edge-thickness-thick{stroke-width:3.5px;}#mermaid-svg-plK8ChyHwVGOVAwx .edge-pattern-solid{stroke-dasharray:0;}#mermaid-svg-plK8ChyHwVGOVAwx .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-svg-plK8ChyHwVGOVAwx .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-svg-plK8ChyHwVGOVAwx .marker{fill:#666;stroke:#666;}#mermaid-svg-plK8ChyHwVGOVAwx .marker.cross{stroke:#666;}#mermaid-svg-plK8ChyHwVGOVAwx svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-svg-plK8ChyHwVGOVAwx .actor{stroke:hsl(0,0%,83%);fill:#eee;}#mermaid-svg-plK8ChyHwVGOVAwx text.actor > tspan{fill:#333;stroke:none;}#mermaid-svg-plK8ChyHwVGOVAwx .actor-line{stroke:#666;}#mermaid-svg-plK8ChyHwVGOVAwx .messageLine0{stroke-width:1.5;stroke-dasharray:none;stroke:#333;}#mermaid-svg-plK8ChyHwVGOVAwx .messageLine1{stroke-width:1.5;stroke-dasharray:2,2;stroke:#333;}#mermaid-svg-plK8ChyHwVGOVAwx #arrowhead path{fill:#333;stroke:#333;}#mermaid-svg-plK8ChyHwVGOVAwx .sequenceNumber{fill:white;}#mermaid-svg-plK8ChyHwVGOVAwx #sequencenumber{fill:#333;}#mermaid-svg-plK8ChyHwVGOVAwx #crosshead path{fill:#333;stroke:#333;}#mermaid-svg-plK8ChyHwVGOVAwx .messageText{fill:#333;stroke:#333;}#mermaid-svg-plK8ChyHwVGOVAwx .labelBox{stroke:hsl(0,0%,83%);fill:#eee;}#mermaid-svg-plK8ChyHwVGOVAwx .labelText,#mermaid-svg-plK8ChyHwVGOVAwx .labelText > tspan{fill:#333;stroke:none;}#mermaid-svg-plK8ChyHwVGOVAwx .loopText,#mermaid-svg-plK8ChyHwVGOVAwx .loopText > tspan{fill:#333;stroke:none;}#mermaid-svg-plK8ChyHwVGOVAwx .loopLine{stroke-width:2px;stroke-dasharray:2,2;stroke:hsl(0,0%,83%);fill:hsl(0,0%,83%);}#mermaid-svg-plK8ChyHwVGOVAwx .note{stroke:hsl(60,100%,23.3333333333%);fill:#ffa;}#mermaid-svg-plK8ChyHwVGOVAwx .noteText,#mermaid-svg-plK8ChyHwVGOVAwx .noteText > tspan{fill:#333;stroke:none;}#mermaid-svg-plK8ChyHwVGOVAwx .activation0{fill:#f4f4f4;stroke:#666;}#mermaid-svg-plK8ChyHwVGOVAwx .activation1{fill:#f4f4f4;stroke:#666;}#mermaid-svg-plK8ChyHwVGOVAwx .activation2{fill:#f4f4f4;stroke:#666;}#mermaid-svg-plK8ChyHwVGOVAwx:root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}#mermaid-svg-plK8ChyHwVGOVAwx sequence{fill:apa;}</style><g></g><g><line id="actor105" x1="75" y1="5" x2="75" y2="1384" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="0" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="75" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="75" dy="0">User</tspan></text></g><g><line id="actor106" x1="275" y1="5" x2="275" y2="1384" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="200" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="275" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="275" dy="0">WebPortal</tspan></text></g><g><line id="actor107" x1="475" y1="5" x2="475" y2="1384" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="400" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="475" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="475" dy="0">LMS</tspan></text></g><g><line id="actor108" x1="675" y1="5" x2="675" y2="1384" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="600" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="675" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="675" dy="0">H5PServer</tspan></text></g><g><line id="actor109" x1="967" y1="5" x2="967" y2="1384" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="892" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="967" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="967" dy="0">SessionCache</tspan></text></g><g><line id="actor110" x1="1167" y1="5" x2="1167" y2="1384" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="1092" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="1167" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="1167" dy="0">ExternalAPI</tspan></text></g><defs><marker id="arrowhead" refX="9" refY="5" markerUnits="userSpaceOnUse" markerWidth="12" markerHeight="12" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z"></path></marker></defs><defs><marker id="crosshead" markerWidth="15" markerHeight="8" orient="auto" refX="16" refY="4"><path fill="black" stroke="#000000" stroke-width="1px" d="M 9,2 V 6 L16,4 Z" style="stroke-dasharray: 0, 0;"></path><path fill="none" stroke="#000000" stroke-width="1px" d="M 0,1 L 6,7 M 6,1 L 0,7" style="stroke-dasharray: 0, 0;"></path></marker></defs><defs><marker id="filled-head" refX="18" refY="7" markerWidth="20" markerHeight="28" orient="auto"><path d="M 18,7 L9,13 L14,7 L9,1 Z"></path></marker></defs><defs><marker id="sequencenumber" refX="15" refY="15" markerWidth="60" markerHeight="40" orient="auto"><circle cx="15" cy="15" r="6"></circle></marker></defs><text x="175" y="80" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">Enter credentials</text><line x1="75" y1="113" x2="275" y2="113" class="messageLine0" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="fill: none;"></line><text x="375" y="128" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">POST /login</text><line x1="275" y1="161" x2="475" y2="161" class="messageLine0" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="fill: none;"></line><text x="475" y="176" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">Verify credentials</text><path d="M 475,209 C 535,199 535,239 475,229" class="messageLine0" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="fill: none;"></path><text x="475" y="254" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">Generate JWT</text><text x="475" y="273" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">(shared secret key)</text><path d="M 475,306 C 535,296 535,336 475,326" class="messageLine0" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="fill: none;"></path><text x="375" y="351" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">JWT token</text><line x1="475" y1="384" x2="275" y2="384" class="messageLine1" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="stroke-dasharray: 3, 3; fill: none;"></line><text x="475" y="399" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">POST /auth/verify</text><text x="475" y="418" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">Header: Bearer {token}</text><line x1="275" y1="451" x2="675" y2="451" class="messageLine0" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="fill: none;"></line><text x="675" y="466" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">Extract token</text><path d="M 675,499 C 735,489 735,529 675,519" class="messageLine0" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="fill: none;"></path><text x="821" y="544" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">Check cache</text><line x1="675" y1="577" x2="967" y2="577" class="messageLine0" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="fill: none;"></line><text x="821" y="637" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">Cached user data</text><line x1="967" y1="670" x2="675" y2="670" class="messageLine1" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="stroke-dasharray: 3, 3; fill: none;"></line><text x="475" y="685" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">200 {valid: true, user}</text><line x1="675" y1="718" x2="275" y2="718" class="messageLine1" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="stroke-dasharray: 3, 3; fill: none;"></line><text x="821" y="778" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">null</text><line x1="967" y1="811" x2="675" y2="811" class="messageLine1" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="stroke-dasharray: 3, 3; fill: none;"></line><text x="675" y="826" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">Verify JWT signature</text><text x="675" y="845" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">(shared secret key)</text><path d="M 675,878 C 735,868 735,908 675,898" class="messageLine0" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="fill: none;"></path><text x="921" y="968" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">GET /auth/verify</text><text x="921" y="987" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">Header: Bearer {token}</text><line x1="675" y1="1020" x2="1167" y2="1020" class="messageLine0" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="fill: none;"></line><text x="921" y="1035" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">User data + permissions</text><line x1="1167" y1="1068" x2="675" y2="1068" class="messageLine1" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="stroke-dasharray: 3, 3; fill: none;"></line><g><line x1="665" y1="918" x2="1177" y2="918" class="loopLine"></line><line x1="1177" y1="918" x2="1177" y2="1078" class="loopLine"></line><line x1="665" y1="1078" x2="1177" y2="1078" class="loopLine"></line><line x1="665" y1="918" x2="665" y2="1078" class="loopLine"></line><polygon points="665,918 715,918 715,931 706.6,938 665,938" class="labelBox"></polygon><text x="690" y="931" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="labelText" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">opt</text><text x="946" y="936" text-anchor="middle" class="loopText" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;"><tspan x="946">[External API Verification]</tspan></text></g><text x="821" y="1093" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">Cache user session (TTL: 5min)</text><line x1="675" y1="1126" x2="967" y2="1126" class="messageLine0" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="fill: none;"></line><text x="475" y="1141" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">200 {valid: true, user}</text><line x1="675" y1="1174" x2="275" y2="1174" class="messageLine1" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="stroke-dasharray: 3, 3; fill: none;"></line><g><line x1="265" y1="587" x2="1187" y2="587" class="loopLine"></line><line x1="1187" y1="587" x2="1187" y2="1184" class="loopLine"></line><line x1="265" y1="1184" x2="1187" y2="1184" class="loopLine"></line><line x1="265" y1="587" x2="265" y2="1184" class="loopLine"></line><line x1="265" y1="733" x2="1187" y2="733" class="loopLine" style="stroke-dasharray: 3, 3;"></line><polygon points="265,587 315,587 315,600 306.6,607 265,607" class="labelBox"></polygon><text x="290" y="600" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="labelText" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">alt</text><text x="751" y="605" text-anchor="middle" class="loopText" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;"><tspan x="751">[Cache Hit]</tspan></text><text x="726" y="751" text-anchor="middle" class="loopText" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">[Cache Miss]</text></g><text x="475" y="1199" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">Access H5P content</text><text x="475" y="1218" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">Header: Bearer {token}</text><line x1="275" y1="1251" x2="675" y2="1251" class="messageLine0" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="fill: none;"></line><text x="475" y="1266" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">H5P content</text><line x1="675" y1="1299" x2="275" y2="1299" class="messageLine1" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="stroke-dasharray: 3, 3; fill: none;"></line><g><rect x="0" y="1319" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="75" y="1351.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="75" dy="0">User</tspan></text></g><g><rect x="200" y="1319" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="275" y="1351.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="275" dy="0">WebPortal</tspan></text></g><g><rect x="400" y="1319" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="475" y="1351.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="475" dy="0">LMS</tspan></text></g><g><rect x="600" y="1319" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="675" y="1351.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="675" dy="0">H5PServer</tspan></text></g><g><rect x="892" y="1319" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="967" y="1351.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="967" dy="0">SessionCache</tspan></text></g><g><rect x="1092" y="1319" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="1167" y="1351.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="1167" dy="0">ExternalAPI</tspan></text></g></svg></pre>
<h3 id="authentication-configuration">Authentication Configuration</h3>
<p>Both the LMS and H5P server must use the <strong>same secret key</strong>:</p>
<pre class=" language-env"><code class="prism  language-env">
# LMS .env

JWT_SECRET_KEY=your-shared-secret-key-here

  

# H5P Server .env

AUTH_JWT_ACCESS_TOKEN_SECRET_KEY=your-shared-secret-key-here

</code></pre>
<h3 id="disabled-authentication-flows">Disabled Authentication Flows</h3>
<p>The following authentication methods are <strong>currently disabled</strong> (routes commented out in code):</p>
<ul>
<li>
<p>❌ <strong>Local Login</strong> (<code>POST /login</code>) - Username/password authentication</p>
</li>
<li>
<p>❌ <strong>Local Logout</strong> (<code>POST /logout</code>) - Token invalidation</p>
</li>
<li>
<p>❌ <strong>SSO Login</strong> (<code>POST /sso/login</code>) - Single sign-on</p>
</li>
</ul>
<p>To re-enable these, uncomment the routes in <code>src/routes/auth.routes.ts</code> and implement the necessary user storage.</p>
<hr>
<h2 id="content-management-flow">Content Management Flow</h2>
<h3 id="content-listing-flow">1. Content Listing Flow</h3>
<pre class=" language-mermaid"><svg id="mermaid-svg-0rwVgi9L5iUNLq0H" width="100%" xmlns="http://www.w3.org/2000/svg" height="757" style="max-width: 2030px;" viewBox="-50 -10 2030 757"><style>#mermaid-svg-0rwVgi9L5iUNLq0H{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#000000;}#mermaid-svg-0rwVgi9L5iUNLq0H .error-icon{fill:#552222;}#mermaid-svg-0rwVgi9L5iUNLq0H .error-text{fill:#552222;stroke:#552222;}#mermaid-svg-0rwVgi9L5iUNLq0H .edge-thickness-normal{stroke-width:2px;}#mermaid-svg-0rwVgi9L5iUNLq0H .edge-thickness-thick{stroke-width:3.5px;}#mermaid-svg-0rwVgi9L5iUNLq0H .edge-pattern-solid{stroke-dasharray:0;}#mermaid-svg-0rwVgi9L5iUNLq0H .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-svg-0rwVgi9L5iUNLq0H .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-svg-0rwVgi9L5iUNLq0H .marker{fill:#666;stroke:#666;}#mermaid-svg-0rwVgi9L5iUNLq0H .marker.cross{stroke:#666;}#mermaid-svg-0rwVgi9L5iUNLq0H svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-svg-0rwVgi9L5iUNLq0H .actor{stroke:hsl(0,0%,83%);fill:#eee;}#mermaid-svg-0rwVgi9L5iUNLq0H text.actor > tspan{fill:#333;stroke:none;}#mermaid-svg-0rwVgi9L5iUNLq0H .actor-line{stroke:#666;}#mermaid-svg-0rwVgi9L5iUNLq0H .messageLine0{stroke-width:1.5;stroke-dasharray:none;stroke:#333;}#mermaid-svg-0rwVgi9L5iUNLq0H .messageLine1{stroke-width:1.5;stroke-dasharray:2,2;stroke:#333;}#mermaid-svg-0rwVgi9L5iUNLq0H #arrowhead path{fill:#333;stroke:#333;}#mermaid-svg-0rwVgi9L5iUNLq0H .sequenceNumber{fill:white;}#mermaid-svg-0rwVgi9L5iUNLq0H #sequencenumber{fill:#333;}#mermaid-svg-0rwVgi9L5iUNLq0H #crosshead path{fill:#333;stroke:#333;}#mermaid-svg-0rwVgi9L5iUNLq0H .messageText{fill:#333;stroke:#333;}#mermaid-svg-0rwVgi9L5iUNLq0H .labelBox{stroke:hsl(0,0%,83%);fill:#eee;}#mermaid-svg-0rwVgi9L5iUNLq0H .labelText,#mermaid-svg-0rwVgi9L5iUNLq0H .labelText > tspan{fill:#333;stroke:none;}#mermaid-svg-0rwVgi9L5iUNLq0H .loopText,#mermaid-svg-0rwVgi9L5iUNLq0H .loopText > tspan{fill:#333;stroke:none;}#mermaid-svg-0rwVgi9L5iUNLq0H .loopLine{stroke-width:2px;stroke-dasharray:2,2;stroke:hsl(0,0%,83%);fill:hsl(0,0%,83%);}#mermaid-svg-0rwVgi9L5iUNLq0H .note{stroke:hsl(60,100%,23.3333333333%);fill:#ffa;}#mermaid-svg-0rwVgi9L5iUNLq0H .noteText,#mermaid-svg-0rwVgi9L5iUNLq0H .noteText > tspan{fill:#333;stroke:none;}#mermaid-svg-0rwVgi9L5iUNLq0H .activation0{fill:#f4f4f4;stroke:#666;}#mermaid-svg-0rwVgi9L5iUNLq0H .activation1{fill:#f4f4f4;stroke:#666;}#mermaid-svg-0rwVgi9L5iUNLq0H .activation2{fill:#f4f4f4;stroke:#666;}#mermaid-svg-0rwVgi9L5iUNLq0H:root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}#mermaid-svg-0rwVgi9L5iUNLq0H sequence{fill:apa;}</style><g></g><g><line id="actor111" x1="75" y1="5" x2="75" y2="746" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="0" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="75" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="75" dy="0">Client</tspan></text></g><g><line id="actor112" x1="433" y1="5" x2="433" y2="746" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="358" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="433" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="433" dy="0">Express</tspan></text></g><g><line id="actor113" x1="703" y1="5" x2="703" y2="746" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="628" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="703" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="703" dy="0">Middleware</tspan></text></g><g><line id="actor114" x1="920" y1="5" x2="920" y2="746" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="845" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="920" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="920" dy="0">ContentController</tspan></text></g><g><line id="actor115" x1="1172" y1="5" x2="1172" y2="746" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="1097" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="1172" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="1172" dy="0">ContentService</tspan></text></g><g><line id="actor116" x1="1589" y1="5" x2="1589" y2="746" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="1514" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="1589" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="1589" dy="0">H5PEditor</tspan></text></g><g><line id="actor117" x1="1855" y1="5" x2="1855" y2="746" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="1780" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="1855" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="1855" dy="0">MongoDB</tspan></text></g><defs><marker id="arrowhead" refX="9" refY="5" markerUnits="userSpaceOnUse" markerWidth="12" markerHeight="12" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z"></path></marker></defs><defs><marker id="crosshead" markerWidth="15" markerHeight="8" orient="auto" refX="16" refY="4"><path fill="black" stroke="#000000" stroke-width="1px" d="M 9,2 V 6 L16,4 Z" style="stroke-dasharray: 0, 0;"></path><path fill="none" stroke="#000000" stroke-width="1px" d="M 0,1 L 6,7 M 6,1 L 0,7" style="stroke-dasharray: 0, 0;"></path></marker></defs><defs><marker id="filled-head" refX="18" refY="7" markerWidth="20" markerHeight="28" orient="auto"><path d="M 18,7 L9,13 L14,7 L9,1 Z"></path></marker></defs><defs><marker id="sequencenumber" refX="15" refY="15" markerWidth="60" markerHeight="40" orient="auto"><circle cx="15" cy="15" r="6"></circle></marker></defs><text x="254" y="80" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">GET /h5p/contents?page=1&amp;perPage=20</text><text x="254" y="99" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">Header: Authorization: Bearer {token}</text><line x1="75" y1="132" x2="433" y2="132" class="messageLine0" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="fill: none;"></line><text x="568" y="147" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">authenticate &amp; extract user</text><line x1="433" y1="180" x2="703" y2="180" class="messageLine0" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="fill: none;"></line><text x="812" y="195" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">listContent(req, res)</text><line x1="703" y1="228" x2="920" y2="228" class="messageLine0" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="fill: none;"></line><text x="1046" y="243" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">listContent(user, options)</text><line x1="920" y1="276" x2="1172" y2="276" class="messageLine0" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="fill: none;"></line><text x="1381" y="291" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">contentManager.listContentPaging(user, options)</text><line x1="1172" y1="324" x2="1589" y2="324" class="messageLine0" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="fill: none;"></line><text x="1722" y="339" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">find({tenantId, userId})</text><text x="1722" y="358" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">.skip().limit().sort()</text><line x1="1589" y1="391" x2="1855" y2="391" class="messageLine0" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="fill: none;"></line><text x="1722" y="406" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">content documents + count</text><line x1="1855" y1="439" x2="1589" y2="439" class="messageLine1" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="stroke-dasharray: 3, 3; fill: none;"></line><text x="1381" y="454" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">{items, pagination}</text><line x1="1589" y1="487" x2="1172" y2="487" class="messageLine1" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="stroke-dasharray: 3, 3; fill: none;"></line><text x="1172" y="502" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">transform to ListContentItem[]</text><path d="M 1172,535 C 1232,525 1232,565 1172,555" class="messageLine0" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="fill: none;"></path><text x="1046" y="580" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">{items, pagination}</text><line x1="1172" y1="613" x2="920" y2="613" class="messageLine1" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="stroke-dasharray: 3, 3; fill: none;"></line><text x="498" y="628" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">200 {items: [...], pagination: {...}}</text><line x1="920" y1="661" x2="75" y2="661" class="messageLine1" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="stroke-dasharray: 3, 3; fill: none;"></line><g><rect x="0" y="681" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="75" y="713.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="75" dy="0">Client</tspan></text></g><g><rect x="358" y="681" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="433" y="713.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="433" dy="0">Express</tspan></text></g><g><rect x="628" y="681" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="703" y="713.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="703" dy="0">Middleware</tspan></text></g><g><rect x="845" y="681" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="920" y="713.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="920" dy="0">ContentController</tspan></text></g><g><rect x="1097" y="681" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="1172" y="713.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="1172" dy="0">ContentService</tspan></text></g><g><rect x="1514" y="681" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="1589" y="713.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="1589" dy="0">H5PEditor</tspan></text></g><g><rect x="1780" y="681" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="1855" y="713.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="1855" dy="0">MongoDB</tspan></text></g></svg></pre>
<h3 id="content-play-flow">2. Content Play Flow</h3>
<pre class=" language-mermaid"><svg id="mermaid-svg-BJqi0UdTpJRteGsh" width="100%" xmlns="http://www.w3.org/2000/svg" height="845" style="max-width: 1918px;" viewBox="-50 -10 1918 845"><style>#mermaid-svg-BJqi0UdTpJRteGsh{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#000000;}#mermaid-svg-BJqi0UdTpJRteGsh .error-icon{fill:#552222;}#mermaid-svg-BJqi0UdTpJRteGsh .error-text{fill:#552222;stroke:#552222;}#mermaid-svg-BJqi0UdTpJRteGsh .edge-thickness-normal{stroke-width:2px;}#mermaid-svg-BJqi0UdTpJRteGsh .edge-thickness-thick{stroke-width:3.5px;}#mermaid-svg-BJqi0UdTpJRteGsh .edge-pattern-solid{stroke-dasharray:0;}#mermaid-svg-BJqi0UdTpJRteGsh .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-svg-BJqi0UdTpJRteGsh .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-svg-BJqi0UdTpJRteGsh .marker{fill:#666;stroke:#666;}#mermaid-svg-BJqi0UdTpJRteGsh .marker.cross{stroke:#666;}#mermaid-svg-BJqi0UdTpJRteGsh svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-svg-BJqi0UdTpJRteGsh .actor{stroke:hsl(0,0%,83%);fill:#eee;}#mermaid-svg-BJqi0UdTpJRteGsh text.actor > tspan{fill:#333;stroke:none;}#mermaid-svg-BJqi0UdTpJRteGsh .actor-line{stroke:#666;}#mermaid-svg-BJqi0UdTpJRteGsh .messageLine0{stroke-width:1.5;stroke-dasharray:none;stroke:#333;}#mermaid-svg-BJqi0UdTpJRteGsh .messageLine1{stroke-width:1.5;stroke-dasharray:2,2;stroke:#333;}#mermaid-svg-BJqi0UdTpJRteGsh #arrowhead path{fill:#333;stroke:#333;}#mermaid-svg-BJqi0UdTpJRteGsh .sequenceNumber{fill:white;}#mermaid-svg-BJqi0UdTpJRteGsh #sequencenumber{fill:#333;}#mermaid-svg-BJqi0UdTpJRteGsh #crosshead path{fill:#333;stroke:#333;}#mermaid-svg-BJqi0UdTpJRteGsh .messageText{fill:#333;stroke:#333;}#mermaid-svg-BJqi0UdTpJRteGsh .labelBox{stroke:hsl(0,0%,83%);fill:#eee;}#mermaid-svg-BJqi0UdTpJRteGsh .labelText,#mermaid-svg-BJqi0UdTpJRteGsh .labelText > tspan{fill:#333;stroke:none;}#mermaid-svg-BJqi0UdTpJRteGsh .loopText,#mermaid-svg-BJqi0UdTpJRteGsh .loopText > tspan{fill:#333;stroke:none;}#mermaid-svg-BJqi0UdTpJRteGsh .loopLine{stroke-width:2px;stroke-dasharray:2,2;stroke:hsl(0,0%,83%);fill:hsl(0,0%,83%);}#mermaid-svg-BJqi0UdTpJRteGsh .note{stroke:hsl(60,100%,23.3333333333%);fill:#ffa;}#mermaid-svg-BJqi0UdTpJRteGsh .noteText,#mermaid-svg-BJqi0UdTpJRteGsh .noteText > tspan{fill:#333;stroke:none;}#mermaid-svg-BJqi0UdTpJRteGsh .activation0{fill:#f4f4f4;stroke:#666;}#mermaid-svg-BJqi0UdTpJRteGsh .activation1{fill:#f4f4f4;stroke:#666;}#mermaid-svg-BJqi0UdTpJRteGsh .activation2{fill:#f4f4f4;stroke:#666;}#mermaid-svg-BJqi0UdTpJRteGsh:root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}#mermaid-svg-BJqi0UdTpJRteGsh sequence{fill:apa;}</style><g></g><g><line id="actor118" x1="75" y1="5" x2="75" y2="834" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="0" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="75" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="75" dy="0">Client</tspan></text></g><g><line id="actor119" x1="340" y1="5" x2="340" y2="834" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="265" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="340" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="340" dy="0">Express</tspan></text></g><g><line id="actor120" x1="540" y1="5" x2="540" y2="834" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="465" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="540" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="540" dy="0">ContentController</tspan></text></g><g><line id="actor121" x1="908" y1="5" x2="908" y2="834" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="833" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="908" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="908" dy="0">ContentService</tspan></text></g><g><line id="actor122" x1="1274" y1="5" x2="1274" y2="834" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="1199" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="1274" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="1274" dy="0">H5PPlayer</tspan></text></g><g><line id="actor123" x1="1543" y1="5" x2="1543" y2="834" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="1468" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="1543" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="1543" dy="0">MongoDB</tspan></text></g><g><line id="actor124" x1="1743" y1="5" x2="1743" y2="834" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="1668" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="1743" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="1743" dy="0">S3</tspan></text></g><defs><marker id="arrowhead" refX="9" refY="5" markerUnits="userSpaceOnUse" markerWidth="12" markerHeight="12" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z"></path></marker></defs><defs><marker id="crosshead" markerWidth="15" markerHeight="8" orient="auto" refX="16" refY="4"><path fill="black" stroke="#000000" stroke-width="1px" d="M 9,2 V 6 L16,4 Z" style="stroke-dasharray: 0, 0;"></path><path fill="none" stroke="#000000" stroke-width="1px" d="M 0,1 L 6,7 M 6,1 L 0,7" style="stroke-dasharray: 0, 0;"></path></marker></defs><defs><marker id="filled-head" refX="18" refY="7" markerWidth="20" markerHeight="28" orient="auto"><path d="M 18,7 L9,13 L14,7 L9,1 Z"></path></marker></defs><defs><marker id="sequencenumber" refX="15" refY="15" markerWidth="60" markerHeight="40" orient="auto"><circle cx="15" cy="15" r="6"></circle></marker></defs><text x="208" y="80" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">GET /h5p/{contentId}/play</text><line x1="75" y1="113" x2="340" y2="113" class="messageLine0" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="fill: none;"></line><text x="440" y="128" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">playContent</text><line x1="340" y1="161" x2="540" y2="161" class="messageLine0" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="fill: none;"></line><text x="724" y="176" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">renderContent(contentId, user, language)</text><line x1="540" y1="209" x2="908" y2="209" class="messageLine0" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="fill: none;"></line><text x="1091" y="224" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">render(contentId, user, language)</text><line x1="908" y1="257" x2="1274" y2="257" class="messageLine0" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="fill: none;"></line><text x="1409" y="272" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">getContent(contentId)</text><line x1="1274" y1="305" x2="1543" y2="305" class="messageLine0" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="fill: none;"></line><text x="1409" y="320" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">content metadata + params</text><line x1="1543" y1="353" x2="1274" y2="353" class="messageLine1" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="stroke-dasharray: 3, 3; fill: none;"></line><text x="1509" y="368" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">getContentFile(contentId)</text><line x1="1274" y1="401" x2="1743" y2="401" class="messageLine0" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="fill: none;"></line><text x="1509" y="416" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">content files</text><line x1="1743" y1="449" x2="1274" y2="449" class="messageLine1" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="stroke-dasharray: 3, 3; fill: none;"></line><text x="1274" y="464" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">build IPlayerModel</text><path d="M 1274,497 C 1334,487 1334,527 1274,517" class="messageLine0" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="fill: none;"></path><text x="1091" y="542" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">IPlayerModel (integration, scripts, styles)</text><line x1="1274" y1="575" x2="908" y2="575" class="messageLine1" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="stroke-dasharray: 3, 3; fill: none;"></line><text x="724" y="590" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">IPlayerModel</text><line x1="908" y1="623" x2="540" y2="623" class="messageLine1" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="stroke-dasharray: 3, 3; fill: none;"></line><text x="540" y="638" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">render to HTML</text><path d="M 540,671 C 600,661 600,701 540,691" class="messageLine0" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="fill: none;"></path><text x="308" y="716" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">200 text/html (playable H5P page)</text><line x1="540" y1="749" x2="75" y2="749" class="messageLine1" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="stroke-dasharray: 3, 3; fill: none;"></line><g><rect x="0" y="769" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="75" y="801.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="75" dy="0">Client</tspan></text></g><g><rect x="265" y="769" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="340" y="801.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="340" dy="0">Express</tspan></text></g><g><rect x="465" y="769" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="540" y="801.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="540" dy="0">ContentController</tspan></text></g><g><rect x="833" y="769" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="908" y="801.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="908" dy="0">ContentService</tspan></text></g><g><rect x="1199" y="769" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="1274" y="801.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="1274" dy="0">H5PPlayer</tspan></text></g><g><rect x="1468" y="769" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="1543" y="801.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="1543" dy="0">MongoDB</tspan></text></g><g><rect x="1668" y="769" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="1743" y="801.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="1743" dy="0">S3</tspan></text></g></svg></pre>
<h3 id="content-creationupdate-flow">3. Content Creation/Update Flow</h3>
<pre class=" language-mermaid"><svg id="mermaid-svg-Ut46Kel5N5pufyYa" width="100%" xmlns="http://www.w3.org/2000/svg" height="786" style="max-width: 1773px;" viewBox="-50 -10 1773 786"><style>#mermaid-svg-Ut46Kel5N5pufyYa{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#000000;}#mermaid-svg-Ut46Kel5N5pufyYa .error-icon{fill:#552222;}#mermaid-svg-Ut46Kel5N5pufyYa .error-text{fill:#552222;stroke:#552222;}#mermaid-svg-Ut46Kel5N5pufyYa .edge-thickness-normal{stroke-width:2px;}#mermaid-svg-Ut46Kel5N5pufyYa .edge-thickness-thick{stroke-width:3.5px;}#mermaid-svg-Ut46Kel5N5pufyYa .edge-pattern-solid{stroke-dasharray:0;}#mermaid-svg-Ut46Kel5N5pufyYa .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-svg-Ut46Kel5N5pufyYa .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-svg-Ut46Kel5N5pufyYa .marker{fill:#666;stroke:#666;}#mermaid-svg-Ut46Kel5N5pufyYa .marker.cross{stroke:#666;}#mermaid-svg-Ut46Kel5N5pufyYa svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-svg-Ut46Kel5N5pufyYa .actor{stroke:hsl(0,0%,83%);fill:#eee;}#mermaid-svg-Ut46Kel5N5pufyYa text.actor > tspan{fill:#333;stroke:none;}#mermaid-svg-Ut46Kel5N5pufyYa .actor-line{stroke:#666;}#mermaid-svg-Ut46Kel5N5pufyYa .messageLine0{stroke-width:1.5;stroke-dasharray:none;stroke:#333;}#mermaid-svg-Ut46Kel5N5pufyYa .messageLine1{stroke-width:1.5;stroke-dasharray:2,2;stroke:#333;}#mermaid-svg-Ut46Kel5N5pufyYa #arrowhead path{fill:#333;stroke:#333;}#mermaid-svg-Ut46Kel5N5pufyYa .sequenceNumber{fill:white;}#mermaid-svg-Ut46Kel5N5pufyYa #sequencenumber{fill:#333;}#mermaid-svg-Ut46Kel5N5pufyYa #crosshead path{fill:#333;stroke:#333;}#mermaid-svg-Ut46Kel5N5pufyYa .messageText{fill:#333;stroke:#333;}#mermaid-svg-Ut46Kel5N5pufyYa .labelBox{stroke:hsl(0,0%,83%);fill:#eee;}#mermaid-svg-Ut46Kel5N5pufyYa .labelText,#mermaid-svg-Ut46Kel5N5pufyYa .labelText > tspan{fill:#333;stroke:none;}#mermaid-svg-Ut46Kel5N5pufyYa .loopText,#mermaid-svg-Ut46Kel5N5pufyYa .loopText > tspan{fill:#333;stroke:none;}#mermaid-svg-Ut46Kel5N5pufyYa .loopLine{stroke-width:2px;stroke-dasharray:2,2;stroke:hsl(0,0%,83%);fill:hsl(0,0%,83%);}#mermaid-svg-Ut46Kel5N5pufyYa .note{stroke:hsl(60,100%,23.3333333333%);fill:#ffa;}#mermaid-svg-Ut46Kel5N5pufyYa .noteText,#mermaid-svg-Ut46Kel5N5pufyYa .noteText > tspan{fill:#333;stroke:none;}#mermaid-svg-Ut46Kel5N5pufyYa .activation0{fill:#f4f4f4;stroke:#666;}#mermaid-svg-Ut46Kel5N5pufyYa .activation1{fill:#f4f4f4;stroke:#666;}#mermaid-svg-Ut46Kel5N5pufyYa .activation2{fill:#f4f4f4;stroke:#666;}#mermaid-svg-Ut46Kel5N5pufyYa:root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}#mermaid-svg-Ut46Kel5N5pufyYa sequence{fill:apa;}</style><g></g><g><line id="actor125" x1="75" y1="5" x2="75" y2="775" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="0" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="75" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="75" dy="0">Client</tspan></text></g><g><line id="actor126" x1="344" y1="5" x2="344" y2="775" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="269" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="344" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="344" dy="0">Express</tspan></text></g><g><line id="actor127" x1="544" y1="5" x2="544" y2="775" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="469" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="544" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="544" dy="0">ContentController</tspan></text></g><g><line id="actor128" x1="811" y1="5" x2="811" y2="775" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="736" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="811" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="811" dy="0">ContentService</tspan></text></g><g><line id="actor129" x1="1153" y1="5" x2="1153" y2="775" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="1078" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="1153" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="1153" dy="0">H5PEditor</tspan></text></g><g><line id="actor130" x1="1398" y1="5" x2="1398" y2="775" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="1323" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="1398" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="1398" dy="0">MongoDB</tspan></text></g><g><line id="actor131" x1="1598" y1="5" x2="1598" y2="775" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="1523" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="1598" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="1598" dy="0">S3</tspan></text></g><defs><marker id="arrowhead" refX="9" refY="5" markerUnits="userSpaceOnUse" markerWidth="12" markerHeight="12" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z"></path></marker></defs><defs><marker id="crosshead" markerWidth="15" markerHeight="8" orient="auto" refX="16" refY="4"><path fill="black" stroke="#000000" stroke-width="1px" d="M 9,2 V 6 L16,4 Z" style="stroke-dasharray: 0, 0;"></path><path fill="none" stroke="#000000" stroke-width="1px" d="M 0,1 L 6,7 M 6,1 L 0,7" style="stroke-dasharray: 0, 0;"></path></marker></defs><defs><marker id="filled-head" refX="18" refY="7" markerWidth="20" markerHeight="28" orient="auto"><path d="M 18,7 L9,13 L14,7 L9,1 Z"></path></marker></defs><defs><marker id="sequencenumber" refX="15" refY="15" markerWidth="60" markerHeight="40" orient="auto"><circle cx="15" cy="15" r="6"></circle></marker></defs><text x="210" y="80" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">POST /h5p/contents</text><text x="210" y="99" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">{library, params, metadata}</text><line x1="75" y1="132" x2="344" y2="132" class="messageLine0" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="fill: none;"></line><text x="444" y="147" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">createContent</text><line x1="344" y1="180" x2="544" y2="180" class="messageLine0" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="fill: none;"></line><text x="678" y="195" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">saveContent(payload, user)</text><line x1="544" y1="228" x2="811" y2="228" class="messageLine0" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="fill: none;"></line><text x="982" y="243" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">saveOrUpdateContentReturnMetaData</text><line x1="811" y1="276" x2="1153" y2="276" class="messageLine0" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="fill: none;"></line><text x="1153" y="291" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">validate library + params</text><path d="M 1153,324 C 1213,314 1213,354 1153,344" class="messageLine0" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="fill: none;"></path><text x="1276" y="369" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">insert content metadata</text><line x1="1153" y1="402" x2="1398" y2="402" class="messageLine0" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="fill: none;"></line><text x="1276" y="417" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">{contentId}</text><line x1="1398" y1="450" x2="1153" y2="450" class="messageLine1" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="stroke-dasharray: 3, 3; fill: none;"></line><text x="1376" y="465" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">upload content files</text><line x1="1153" y1="498" x2="1598" y2="498" class="messageLine0" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="fill: none;"></line><text x="1376" y="513" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">success</text><line x1="1598" y1="546" x2="1153" y2="546" class="messageLine1" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="stroke-dasharray: 3, 3; fill: none;"></line><text x="982" y="561" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">{contentId, metadata}</text><line x1="1153" y1="594" x2="811" y2="594" class="messageLine1" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="stroke-dasharray: 3, 3; fill: none;"></line><text x="678" y="609" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">{contentId, metadata}</text><line x1="811" y1="642" x2="544" y2="642" class="messageLine1" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="stroke-dasharray: 3, 3; fill: none;"></line><text x="310" y="657" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">200 {contentId, metadata}</text><line x1="544" y1="690" x2="75" y2="690" class="messageLine1" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="stroke-dasharray: 3, 3; fill: none;"></line><g><rect x="0" y="710" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="75" y="742.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="75" dy="0">Client</tspan></text></g><g><rect x="269" y="710" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="344" y="742.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="344" dy="0">Express</tspan></text></g><g><rect x="469" y="710" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="544" y="742.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="544" dy="0">ContentController</tspan></text></g><g><rect x="736" y="710" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="811" y="742.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="811" dy="0">ContentService</tspan></text></g><g><rect x="1078" y="710" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="1153" y="742.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="1153" dy="0">H5PEditor</tspan></text></g><g><rect x="1323" y="710" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="1398" y="742.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="1398" dy="0">MongoDB</tspan></text></g><g><rect x="1523" y="710" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="1598" y="742.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="1598" dy="0">S3</tspan></text></g></svg></pre>
<h3 id="learner-progress-tracking-flow">4. Learner Progress Tracking Flow</h3>
<pre class=" language-mermaid"><svg id="mermaid-svg-HvQbrWu05Yp2CL1x" width="100%" xmlns="http://www.w3.org/2000/svg" height="841" style="max-width: 2077px;" viewBox="-50 -10 2077 841"><style>#mermaid-svg-HvQbrWu05Yp2CL1x{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#000000;}#mermaid-svg-HvQbrWu05Yp2CL1x .error-icon{fill:#552222;}#mermaid-svg-HvQbrWu05Yp2CL1x .error-text{fill:#552222;stroke:#552222;}#mermaid-svg-HvQbrWu05Yp2CL1x .edge-thickness-normal{stroke-width:2px;}#mermaid-svg-HvQbrWu05Yp2CL1x .edge-thickness-thick{stroke-width:3.5px;}#mermaid-svg-HvQbrWu05Yp2CL1x .edge-pattern-solid{stroke-dasharray:0;}#mermaid-svg-HvQbrWu05Yp2CL1x .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-svg-HvQbrWu05Yp2CL1x .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-svg-HvQbrWu05Yp2CL1x .marker{fill:#666;stroke:#666;}#mermaid-svg-HvQbrWu05Yp2CL1x .marker.cross{stroke:#666;}#mermaid-svg-HvQbrWu05Yp2CL1x svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-svg-HvQbrWu05Yp2CL1x .actor{stroke:hsl(0,0%,83%);fill:#eee;}#mermaid-svg-HvQbrWu05Yp2CL1x text.actor > tspan{fill:#333;stroke:none;}#mermaid-svg-HvQbrWu05Yp2CL1x .actor-line{stroke:#666;}#mermaid-svg-HvQbrWu05Yp2CL1x .messageLine0{stroke-width:1.5;stroke-dasharray:none;stroke:#333;}#mermaid-svg-HvQbrWu05Yp2CL1x .messageLine1{stroke-width:1.5;stroke-dasharray:2,2;stroke:#333;}#mermaid-svg-HvQbrWu05Yp2CL1x #arrowhead path{fill:#333;stroke:#333;}#mermaid-svg-HvQbrWu05Yp2CL1x .sequenceNumber{fill:white;}#mermaid-svg-HvQbrWu05Yp2CL1x #sequencenumber{fill:#333;}#mermaid-svg-HvQbrWu05Yp2CL1x #crosshead path{fill:#333;stroke:#333;}#mermaid-svg-HvQbrWu05Yp2CL1x .messageText{fill:#333;stroke:#333;}#mermaid-svg-HvQbrWu05Yp2CL1x .labelBox{stroke:hsl(0,0%,83%);fill:#eee;}#mermaid-svg-HvQbrWu05Yp2CL1x .labelText,#mermaid-svg-HvQbrWu05Yp2CL1x .labelText > tspan{fill:#333;stroke:none;}#mermaid-svg-HvQbrWu05Yp2CL1x .loopText,#mermaid-svg-HvQbrWu05Yp2CL1x .loopText > tspan{fill:#333;stroke:none;}#mermaid-svg-HvQbrWu05Yp2CL1x .loopLine{stroke-width:2px;stroke-dasharray:2,2;stroke:hsl(0,0%,83%);fill:hsl(0,0%,83%);}#mermaid-svg-HvQbrWu05Yp2CL1x .note{stroke:hsl(60,100%,23.3333333333%);fill:#ffa;}#mermaid-svg-HvQbrWu05Yp2CL1x .noteText,#mermaid-svg-HvQbrWu05Yp2CL1x .noteText > tspan{fill:#333;stroke:none;}#mermaid-svg-HvQbrWu05Yp2CL1x .activation0{fill:#f4f4f4;stroke:#666;}#mermaid-svg-HvQbrWu05Yp2CL1x .activation1{fill:#f4f4f4;stroke:#666;}#mermaid-svg-HvQbrWu05Yp2CL1x .activation2{fill:#f4f4f4;stroke:#666;}#mermaid-svg-HvQbrWu05Yp2CL1x:root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}#mermaid-svg-HvQbrWu05Yp2CL1x sequence{fill:apa;}</style><g></g><g><line id="actor132" x1="75" y1="5" x2="75" y2="830" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="0" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="75" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="75" dy="0">Client</tspan></text></g><g><line id="actor133" x1="551" y1="5" x2="551" y2="830" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="476" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="551" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="551" dy="0">Express</tspan></text></g><g><line id="actor134" x1="784" y1="5" x2="784" y2="830" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="709" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="784" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="784" dy="0">ContentController</tspan></text></g><g><line id="actor135" x1="1125" y1="5" x2="1125" y2="830" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="1050" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="1125" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="1125" dy="0">ContentService</tspan></text></g><g><line id="actor136" x1="1360" y1="5" x2="1360" y2="830" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="1285" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="1360" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="1360" dy="0">UserDataManager</tspan></text></g><g><line id="actor137" x1="1560" y1="5" x2="1560" y2="830" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="1485" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="1560" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="1560" dy="0">CustomStorage</tspan></text></g><g><line id="actor138" x1="1902" y1="5" x2="1902" y2="830" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="1827" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="1902" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="1902" dy="0">MongoDB</tspan></text></g><defs><marker id="arrowhead" refX="9" refY="5" markerUnits="userSpaceOnUse" markerWidth="12" markerHeight="12" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z"></path></marker></defs><defs><marker id="crosshead" markerWidth="15" markerHeight="8" orient="auto" refX="16" refY="4"><path fill="black" stroke="#000000" stroke-width="1px" d="M 9,2 V 6 L16,4 Z" style="stroke-dasharray: 0, 0;"></path><path fill="none" stroke="#000000" stroke-width="1px" d="M 0,1 L 6,7 M 6,1 L 0,7" style="stroke-dasharray: 0, 0;"></path></marker></defs><defs><marker id="filled-head" refX="18" refY="7" markerWidth="20" markerHeight="28" orient="auto"><path d="M 18,7 L9,13 L14,7 L9,1 Z"></path></marker></defs><defs><marker id="sequencenumber" refX="15" refY="15" markerWidth="60" markerHeight="40" orient="auto"><circle cx="15" cy="15" r="6"></circle></marker></defs><text x="313" y="80" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">POST /h5p/my-finished</text><text x="313" y="99" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">{contentId, score, maxScore, timestamps, customFields}</text><line x1="75" y1="132" x2="551" y2="132" class="messageLine0" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="fill: none;"></line><text x="668" y="147" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">recordFinishedContent</text><line x1="551" y1="180" x2="784" y2="180" class="messageLine0" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="fill: none;"></line><text x="955" y="195" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">recordFinishedContent(payload, user)</text><line x1="784" y1="228" x2="1125" y2="228" class="messageLine0" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="fill: none;"></line><text x="1243" y="243" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">setFinished(data, user)</text><line x1="1125" y1="276" x2="1360" y2="276" class="messageLine0" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="fill: none;"></line><text x="1631" y="291" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">upsert finisheddata collection</text><line x1="1360" y1="324" x2="1902" y2="324" class="messageLine0" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="fill: none;"></line><text x="1631" y="339" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">success</text><line x1="1902" y1="372" x2="1360" y2="372" class="messageLine1" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="stroke-dasharray: 3, 3; fill: none;"></line><text x="1343" y="432" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">mirrorCustomFinishedPayload(data)</text><line x1="1125" y1="465" x2="1560" y2="465" class="messageLine0" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="fill: none;"></line><text x="1560" y="480" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">decorate with processedAt, scorePercentage</text><path d="M 1560,513 C 1620,503 1620,543 1560,533" class="messageLine0" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="fill: none;"></path><text x="1731" y="558" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">upsert custom-finisheddata collection</text><line x1="1560" y1="591" x2="1902" y2="591" class="messageLine0" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="fill: none;"></line><text x="1731" y="606" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">success</text><line x1="1902" y1="639" x2="1560" y2="639" class="messageLine1" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="stroke-dasharray: 3, 3; fill: none;"></line><g><line x1="1115" y1="382" x2="1912" y2="382" class="loopLine"></line><line x1="1912" y1="382" x2="1912" y2="649" class="loopLine"></line><line x1="1115" y1="649" x2="1912" y2="649" class="loopLine"></line><line x1="1115" y1="382" x2="1115" y2="649" class="loopLine"></line><polygon points="1115,382 1165,382 1165,395 1156.6,402 1115,402" class="labelBox"></polygon><text x="1140" y="395" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="labelText" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">alt</text><text x="1538.5" y="400" text-anchor="middle" class="loopText" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;"><tspan x="1538.5">[Custom fields provided]</tspan></text></g><text x="955" y="664" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">void</text><line x1="1125" y1="697" x2="784" y2="697" class="messageLine1" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="stroke-dasharray: 3, 3; fill: none;"></line><text x="430" y="712" text-anchor="middle" dominant-baseline="middle" alignment-baseline="middle" class="messageText" dy="1em" style="font-family: &quot;trebuchet ms&quot;, verdana, arial, sans-serif; font-size: 16px; font-weight: 400;">200 {success: true}</text><line x1="784" y1="745" x2="75" y2="745" class="messageLine1" stroke-width="2" stroke="none" marker-end="url(#arrowhead)" style="stroke-dasharray: 3, 3; fill: none;"></line><g><rect x="0" y="765" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="75" y="797.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="75" dy="0">Client</tspan></text></g><g><rect x="476" y="765" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="551" y="797.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="551" dy="0">Express</tspan></text></g><g><rect x="709" y="765" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="784" y="797.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="784" dy="0">ContentController</tspan></text></g><g><rect x="1050" y="765" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="1125" y="797.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="1125" dy="0">ContentService</tspan></text></g><g><rect x="1285" y="765" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="1360" y="797.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="1360" dy="0">UserDataManager</tspan></text></g><g><rect x="1485" y="765" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="1560" y="797.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="1560" dy="0">CustomStorage</tspan></text></g><g><rect x="1827" y="765" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="1902" y="797.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle; font-size: 14px; font-weight: 400; font-family: Open-Sans, &quot;sans-serif&quot;;"><tspan x="1902" dy="0">MongoDB</tspan></text></g></svg></pre>
<hr>
<h2 id="integration-steps">Integration Steps</h2>
<h3 id="step-1-prerequisites">Step 1: Prerequisites</h3>
<p>Ensure you have the following installed:</p>
<ul>
<li>
<p>Node.js ≥ 16.x</p>
</li>
<li>
<p>MongoDB ≥ 4.4</p>
</li>
<li>
<p>Redis ≥ 6.x (optional, for caching)</p>
</li>
<li>
<p>AWS S3 bucket or S3-compatible storage</p>
</li>
<li>
<p>Docker (optional, for containerized deployment)</p>
</li>
</ul>
<h3 id="step-2-installation">Step 2: Installation</h3>
<h4 id="option-a-standalone-installation">Option A: Standalone Installation</h4>
<pre class=" language-bash"><code class="prism  language-bash">
<span class="token comment"># Clone the repository</span>

<span class="token function">git</span>  clone  https://github.com/Lumieducation/H5P-Nodejs-library.git

<span class="token function">cd</span>  H5P-Nodejs-library

  

<span class="token comment"># Install dependencies</span>

<span class="token function">npm</span>  <span class="token function">install</span>

  

<span class="token comment"># Navigate to h5p-rest-server</span>

<span class="token function">cd</span>  packages/h5p-rest-server

  

<span class="token comment"># Copy environment template</span>

<span class="token function">cp</span>  .env.example  .env

</code></pre>
<h4 id="option-b-add-as-package-dependency">Option B: Add as Package Dependency</h4>
<pre class=" language-bash"><code class="prism  language-bash">
<span class="token comment"># Add to your project</span>

<span class="token function">npm</span>  <span class="token function">install</span>  @lumieducation/h5p-rest-server

  

<span class="token comment"># Or with workspace (monorepo)</span>

<span class="token comment"># Add to packages/ directory and link via workspaces</span>

</code></pre>
<h3 id="step-3-environment-configuration">Step 3: Environment Configuration</h3>
<p>Edit <code>.env</code> file with your configuration:</p>
<pre class=" language-env"><code class="prism  language-env">
# ===== STORAGE CONFIGURATION =====

  

# MongoDB

MONGODB_URL=mongodb://localhost:27017

MONGODB_DB=h5p

MONGODB_USER=root

MONGODB_PASSWORD=yourpassword

  

# AWS S3

AWS_ACCESS_KEY_ID=your-access-key

AWS_SECRET_ACCESS_KEY=your-secret-key

AWS_REGION=ap-southeast-1

AWS_S3_ENDPOINT=https://s3.amazonaws.com

AWS_S3_MAX_FILE_LENGTH=100

  

# Content Storage

CONTENTSTORAGE=mongos3

CONTENT_AWS_S3_BUCKET=h5p-content

CONTENT_MONGO_COLLECTION=h5p-content

  

# Temporary Files

TEMPORARYSTORAGE=s3

TEMPORARY_AWS_S3_BUCKET=h5p-temp-content

  

# User Data

USERDATASTORAGE=mongo

USERDATA_MONGO_COLLECTION=userdata

FINISHED_MONGO_COLLECTION=finisheddata

  

# ===== AUTHENTICATION =====

  

# JWT Configuration

AUTH_JWT_ACCESS_TOKEN_SECRET_KEY=your-super-secret-key-change-this

AUTH_JWT_ACCESS_TOKEN_EXPIRED=7d

AUTH_JWT_REFRESH_TOKEN_SECRET_KEY=another-secret-key-change-this

AUTH_JWT_REFRESH_TOKEN_EXPIRED=30d

  

# ===== EXTERNAL API INTEGRATION =====

  

# External Backend (for SSO/Token Verification)

EXTERNAL_API_URL=https://your-backend-api.com

EXTERNAL_API_VERIFY_ENDPOINT=/auth/verify

EXTERNAL_API_TIMEOUT=5000

  

# Session Cache

SESSION_CACHE_TTL_MS=300000 # 5 minutes

  

# ===== OPTIONAL =====

  

# Redis Cache

CACHE=redis

REDIS_HOST=localhost

REDIS_PORT=6379

REDIS_DB=0

  

# Redis Lock

LOCK=redis

LOCK_REDIS_HOST=localhost

LOCK_REDIS_PORT=6379

LOCK_REDIS_DB=1

  

# Internationalization

I18N_PRELOAD_LANGUAGES=en,vi,zh

  

# Debug

DEBUG=h5p:*

LOG_LEVEL=debug

</code></pre>
<h3 id="step-4-database-setup">Step 4: Database Setup</h3>
<p>The server will automatically create collections and indexes on first run. However, you can run manual setup:</p>
<pre class=" language-bash"><code class="prism  language-bash">
<span class="token comment"># Start MongoDB</span>

mongod  --dbpath  /path/to/data

  

<span class="token comment"># (Optional) Run migration scripts if provided</span>

<span class="token function">npm</span>  run  db:migrate

</code></pre>
<h3 id="step-5-download-h5p-core-assets">Step 5: Download H5P Core Assets</h3>
<pre class=" language-bash"><code class="prism  language-bash">
<span class="token comment"># From packages/h5p-rest-server directory</span>

<span class="token function">npm</span>  run  download:core

</code></pre>
<p>This downloads the H5P core library files (JavaScript, CSS) needed for the editor and player.</p>
<h3 id="step-6-start-the-server">Step 6: Start the Server</h3>
<h4 id="development-mode">Development Mode</h4>
<pre class=" language-bash"><code class="prism  language-bash">
<span class="token function">npm</span>  run  start:dev

</code></pre>
<p>The server will run on <code>http://localhost:8080</code> with hot-reload enabled.</p>
<h4 id="production-mode">Production Mode</h4>
<pre class=" language-bash"><code class="prism  language-bash">
<span class="token function">npm</span>  run  build

<span class="token function">npm</span>  start

</code></pre>
<h3 id="step-7-docker-deployment-optional">Step 7: Docker Deployment (Optional)</h3>
<pre class=" language-bash"><code class="prism  language-bash">
<span class="token comment"># Build Docker image (from repository root)</span>

docker  build  -f  packages/h5p-rest-server/Dockerfile  -t  h5p-rest-server:latest  <span class="token keyword">.</span>

  

<span class="token comment"># Run container</span>

docker  run  --env-file  packages/h5p-rest-server/.env  \

-v h5p_data:/app/packages/h5p-rest-server/h5p \

-p  8080:8080  \

h5p-rest-server:latest

  

<span class="token comment"># Or use docker-compose</span>

<span class="token function">cd</span>  packages/h5p-rest-server

docker-compose  up  -d

</code></pre>
<h3 id="step-8-verify-installation">Step 8: Verify Installation</h3>
<ol>
<li>
<p><strong>Check API Health</strong>: Visit <code>http://localhost:8080/docs</code> for Swagger UI</p>
</li>
<li>
<p><strong>Authentication Test</strong>:</p>
</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash">
<span class="token comment"># Local login (requires seeded users or custom implementation)</span>

curl  -X  POST  http://localhost:8080/login  \

-H <span class="token string">"Content-Type: application/json"</span> \

-d  <span class="token string">'{"username": "admin", "password": "password"}'</span>

</code></pre>
<ol start="3">
<li><strong>SSO Test</strong>:</li>
</ol>
<pre class=" language-bash"><code class="prism  language-bash">
curl  -X  POST  http://localhost:8080/sso/login  \

-H <span class="token string">"Content-Type: application/json"</span> \

-d  <span class="token string">'{

"user": {

"username": "user1",

"name": "Test User",

"role": "SUPER_ADMIN"

},

"tenantId": "tenant-1",

"branchId": "branch-1"

}'</span>

</code></pre>
<hr>
<h2 id="external-api-integration">External API Integration</h2>
<h3 id="token-verification-endpoint">Token Verification Endpoint</h3>
<p>Your external backend should provide a token verification endpoint:</p>
<pre class=" language-typescript"><code class="prism  language-typescript">
<span class="token comment">// External API: GET /auth/verify</span>

<span class="token comment">// Headers: Authorization: Bearer {token}</span>

  

<span class="token comment">// Expected Response:</span>

<span class="token punctuation">{</span>

<span class="token string">"statusCode"</span><span class="token punctuation">:</span> <span class="token number">200</span><span class="token punctuation">,</span>

<span class="token string">"data"</span><span class="token punctuation">:</span> <span class="token punctuation">{</span>

<span class="token string">"id"</span><span class="token punctuation">:</span>  <span class="token string">"user-uuid"</span><span class="token punctuation">,</span>

<span class="token string">"username"</span><span class="token punctuation">:</span>  <span class="token string">"user@example.com"</span><span class="token punctuation">,</span>

<span class="token string">"email"</span><span class="token punctuation">:</span>  <span class="token string">"user@example.com"</span><span class="token punctuation">,</span>

<span class="token string">"role"</span><span class="token punctuation">:</span>  <span class="token string">"SUPER_ADMIN"</span><span class="token punctuation">,</span>

<span class="token string">"tenantId"</span><span class="token punctuation">:</span>  <span class="token string">"tenant-123"</span><span class="token punctuation">,</span>

<span class="token string">"branchId"</span><span class="token punctuation">:</span>  <span class="token string">"branch-456"</span>

<span class="token punctuation">}</span>

<span class="token punctuation">}</span>

</code></pre>
<h3 id="integration-flow">Integration Flow</h3>
<pre class=" language-mermaid"><svg id="mermaid-svg-xytfEakMgmvpg5zt" width="100%" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" height="194.515625" style="max-width: 1012.53125px;" viewBox="0 0 1012.53125 194.515625"><style>#mermaid-svg-xytfEakMgmvpg5zt{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;fill:#000000;}#mermaid-svg-xytfEakMgmvpg5zt .error-icon{fill:#552222;}#mermaid-svg-xytfEakMgmvpg5zt .error-text{fill:#552222;stroke:#552222;}#mermaid-svg-xytfEakMgmvpg5zt .edge-thickness-normal{stroke-width:2px;}#mermaid-svg-xytfEakMgmvpg5zt .edge-thickness-thick{stroke-width:3.5px;}#mermaid-svg-xytfEakMgmvpg5zt .edge-pattern-solid{stroke-dasharray:0;}#mermaid-svg-xytfEakMgmvpg5zt .edge-pattern-dashed{stroke-dasharray:3;}#mermaid-svg-xytfEakMgmvpg5zt .edge-pattern-dotted{stroke-dasharray:2;}#mermaid-svg-xytfEakMgmvpg5zt .marker{fill:#666;stroke:#666;}#mermaid-svg-xytfEakMgmvpg5zt .marker.cross{stroke:#666;}#mermaid-svg-xytfEakMgmvpg5zt svg{font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:16px;}#mermaid-svg-xytfEakMgmvpg5zt .label{font-family:"trebuchet ms",verdana,arial,sans-serif;color:#000000;}#mermaid-svg-xytfEakMgmvpg5zt .cluster-label text{fill:#333;}#mermaid-svg-xytfEakMgmvpg5zt .cluster-label span{color:#333;}#mermaid-svg-xytfEakMgmvpg5zt .label text,#mermaid-svg-xytfEakMgmvpg5zt span{fill:#000000;color:#000000;}#mermaid-svg-xytfEakMgmvpg5zt .node rect,#mermaid-svg-xytfEakMgmvpg5zt .node circle,#mermaid-svg-xytfEakMgmvpg5zt .node ellipse,#mermaid-svg-xytfEakMgmvpg5zt .node polygon,#mermaid-svg-xytfEakMgmvpg5zt .node path{fill:#eee;stroke:#999;stroke-width:1px;}#mermaid-svg-xytfEakMgmvpg5zt .node .label{text-align:center;}#mermaid-svg-xytfEakMgmvpg5zt .node.clickable{cursor:pointer;}#mermaid-svg-xytfEakMgmvpg5zt .arrowheadPath{fill:#333333;}#mermaid-svg-xytfEakMgmvpg5zt .edgePath .path{stroke:#666;stroke-width:1.5px;}#mermaid-svg-xytfEakMgmvpg5zt .flowchart-link{stroke:#666;fill:none;}#mermaid-svg-xytfEakMgmvpg5zt .edgeLabel{background-color:white;text-align:center;}#mermaid-svg-xytfEakMgmvpg5zt .edgeLabel rect{opacity:0.5;background-color:white;fill:white;}#mermaid-svg-xytfEakMgmvpg5zt .cluster rect{fill:hsl(210,66.6666666667%,95%);stroke:#26a;stroke-width:1px;}#mermaid-svg-xytfEakMgmvpg5zt .cluster text{fill:#333;}#mermaid-svg-xytfEakMgmvpg5zt .cluster span{color:#333;}#mermaid-svg-xytfEakMgmvpg5zt div.mermaidTooltip{position:absolute;text-align:center;max-width:200px;padding:2px;font-family:"trebuchet ms",verdana,arial,sans-serif;font-size:12px;background:hsl(-160,0%,93.3333333333%);border:1px solid #26a;border-radius:2px;pointer-events:none;z-index:100;}#mermaid-svg-xytfEakMgmvpg5zt:root{--mermaid-font-family:"trebuchet ms",verdana,arial,sans-serif;}#mermaid-svg-xytfEakMgmvpg5zt flowchart{fill:apa;}</style><g><g class="output"><g class="clusters"></g><g class="edgePaths"><g class="edgePath LS-A LE-B" id="L-A-B" style="opacity: 1;"><path class="path" d="M105.8125,87.85941366331383L178.4609375,73.8984375L263.515625,86.5326227861543" marker-end="url(https://stackedit.io/app#arrowhead90)" style="fill:none"></path><defs><marker id="arrowhead90" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath LS-B LE-A" id="L-B-A" style="opacity: 1;"><path class="path" d="M263.515625,107.9830022138457L178.4609375,120.6171875L105.8125,106.65621133668617" marker-end="url(https://stackedit.io/app#arrowhead91)" style="fill:none"></path><defs><marker id="arrowhead91" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath LS-A LE-C" id="L-A-C" style="opacity: 1;"><path class="path" d="M94.3173169711786,73.8984375L178.4609375,21.359375L335.71875,21.359375L498.6875,21.359375L600.3964190362841,73.8984375" marker-end="url(https://stackedit.io/app#arrowhead92)" style="fill:none"></path><defs><marker id="arrowhead92" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath LS-C LE-B" id="L-C-B" style="opacity: 1;"><path class="path" d="M577.046875,108.15935098965811L498.6875,120.6171875L407.921875,107.6071578379674" marker-end="url(https://stackedit.io/app#arrowhead93)" style="fill:none"></path><defs><marker id="arrowhead93" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath LS-B LE-C" id="L-B-C" style="opacity: 1;"><path class="path" d="M407.921875,86.9084671620326L498.6875,73.8984375L577.046875,86.35627401034189" marker-end="url(https://stackedit.io/app#arrowhead94)" style="fill:none"></path><defs><marker id="arrowhead94" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath LS-C LE-D" id="L-C-D" style="opacity: 1;"><path class="path" d="M714.1875,97.2578125L798.4609375,97.2578125L882.734375,97.2578125" marker-end="url(https://stackedit.io/app#arrowhead95)" style="fill:none"></path><defs><marker id="arrowhead95" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath LS-C LE-A" id="L-C-A" style="opacity: 1;"><path class="path" d="M600.3964190362841,120.6171875L498.6875,173.15625L335.71875,173.15625L178.4609375,173.15625L94.3173169711786,120.6171875" marker-end="url(https://stackedit.io/app#arrowhead96)" style="fill:none"></path><defs><marker id="arrowhead96" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g></g><g class="edgeLabels"><g class="edgeLabel" transform="translate(178.4609375,73.8984375)" style="opacity: 1;"><g transform="translate(-28.5546875,-13.359375)" class="label"><rect rx="0" ry="0" width="57.109375" height="26.71875"></rect><foreignObject width="57.109375" height="26.71875"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span id="L-L-A-B" class="edgeLabel L-LS-A' L-LE-B">1. Login</span></div></foreignObject></g></g><g class="edgeLabel" transform="translate(178.4609375,120.6171875)" style="opacity: 1;"><g transform="translate(-47.6484375,-13.359375)" class="label"><rect rx="0" ry="0" width="95.296875" height="26.71875"></rect><foreignObject width="95.296875" height="26.71875"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span id="L-L-B-A" class="edgeLabel L-LS-B' L-LE-A">2. JWT Token</span></div></foreignObject></g></g><g class="edgeLabel" transform="translate(335.71875,21.359375)" style="opacity: 1;"><g transform="translate(-84.609375,-13.359375)" class="label"><rect rx="0" ry="0" width="169.21875" height="26.71875"></rect><foreignObject width="169.21875" height="26.71875"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span id="L-L-A-C" class="edgeLabel L-LS-A' L-LE-C">3. Access H5P with JWT</span></div></foreignObject></g></g><g class="edgeLabel" transform="translate(498.6875,120.6171875)" style="opacity: 1;"><g transform="translate(-53.359375,-13.359375)" class="label"><rect rx="0" ry="0" width="106.71875" height="26.71875"></rect><foreignObject width="106.71875" height="26.71875"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span id="L-L-C-B" class="edgeLabel L-LS-C' L-LE-B">4. Verify Token</span></div></foreignObject></g></g><g class="edgeLabel" transform="translate(498.6875,73.8984375)" style="opacity: 1;"><g transform="translate(-44.3359375,-13.359375)" class="label"><rect rx="0" ry="0" width="88.671875" height="26.71875"></rect><foreignObject width="88.671875" height="26.71875"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span id="L-L-B-C" class="edgeLabel L-LS-B' L-LE-C">5. User Data</span></div></foreignObject></g></g><g class="edgeLabel" transform="translate(798.4609375,97.2578125)" style="opacity: 1;"><g transform="translate(-59.2734375,-13.359375)" class="label"><rect rx="0" ry="0" width="118.546875" height="26.71875"></rect><foreignObject width="118.546875" height="26.71875"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span id="L-L-C-D" class="edgeLabel L-LS-C' L-LE-D">6. Cache Session</span></div></foreignObject></g></g><g class="edgeLabel" transform="translate(335.71875,173.15625)" style="opacity: 1;"><g transform="translate(-64.203125,-13.359375)" class="label"><rect rx="0" ry="0" width="128.40625" height="26.71875"></rect><foreignObject width="128.40625" height="26.71875"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span id="L-L-C-A" class="edgeLabel L-LS-C' L-LE-A">7. Return Content</span></div></foreignObject></g></g></g><g class="nodes"><g class="node default" id="flowchart-A-582" transform="translate(56.90625,97.2578125)" style="opacity: 1;"><rect rx="0" ry="0" x="-48.90625" y="-23.359375" width="97.8125" height="46.71875" class="label-container"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-38.90625,-13.359375)"><foreignObject width="77.8125" height="26.71875"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Web Portal</div></foreignObject></g></g></g><g class="node default" id="flowchart-B-583" transform="translate(335.71875,97.2578125)" style="opacity: 1;"><rect rx="0" ry="0" x="-72.203125" y="-23.359375" width="144.40625" height="46.71875" class="label-container"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-62.203125,-13.359375)"><foreignObject width="124.40625" height="26.71875"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">External Backend</div></foreignObject></g></g></g><g class="node default" id="flowchart-C-587" transform="translate(645.6171875,97.2578125)" style="opacity: 1;"><rect rx="0" ry="0" x="-68.5703125" y="-23.359375" width="137.140625" height="46.71875" class="label-container"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-58.5703125,-13.359375)"><foreignObject width="117.140625" height="26.71875"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">H5P REST Server</div></foreignObject></g></g></g><g class="node default" id="flowchart-D-593" transform="translate(943.6328125,97.2578125)" style="opacity: 1;"><rect rx="0" ry="0" x="-60.8984375" y="-23.359375" width="121.796875" height="46.71875" class="label-container"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-50.8984375,-13.359375)"><foreignObject width="101.796875" height="26.71875"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Redis/Memory</div></foreignObject></g></g></g></g></g></g></svg></pre>
<h3 id="client-integration-example">Client Integration Example</h3>
<pre class=" language-typescript"><code class="prism  language-typescript">
<span class="token comment">// Frontend login flow</span>

<span class="token keyword">async</span>  <span class="token keyword">function</span>  <span class="token function">login</span><span class="token punctuation">(</span>username<span class="token punctuation">:</span> <span class="token keyword">string</span><span class="token punctuation">,</span> password<span class="token punctuation">:</span> <span class="token keyword">string</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>

<span class="token comment">// Step 1: Login to external backend</span>

<span class="token keyword">const</span>  response <span class="token operator">=</span> <span class="token keyword">await</span>  <span class="token function">fetch</span><span class="token punctuation">(</span><span class="token string">'https://your-backend.com/auth/login'</span><span class="token punctuation">,</span> <span class="token punctuation">{</span>

method<span class="token punctuation">:</span>  <span class="token string">'POST'</span><span class="token punctuation">,</span>

headers<span class="token punctuation">:</span> <span class="token punctuation">{</span> <span class="token string">'Content-Type'</span><span class="token punctuation">:</span>  <span class="token string">'application/json'</span> <span class="token punctuation">}</span><span class="token punctuation">,</span>

body<span class="token punctuation">:</span>  JSON<span class="token punctuation">.</span><span class="token function">stringify</span><span class="token punctuation">(</span><span class="token punctuation">{</span> username<span class="token punctuation">,</span> password <span class="token punctuation">}</span><span class="token punctuation">)</span>

<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token keyword">const</span> <span class="token punctuation">{</span> token <span class="token punctuation">}</span> <span class="token operator">=</span> <span class="token keyword">await</span>  response<span class="token punctuation">.</span><span class="token function">json</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token comment">// Step 2: Verify token with H5P server</span>

<span class="token keyword">const</span>  verifyResponse <span class="token operator">=</span> <span class="token keyword">await</span>  <span class="token function">fetch</span><span class="token punctuation">(</span><span class="token string">'http://h5p-server:8080/auth/verify'</span><span class="token punctuation">,</span> <span class="token punctuation">{</span>

method<span class="token punctuation">:</span>  <span class="token string">'POST'</span><span class="token punctuation">,</span>

headers<span class="token punctuation">:</span> <span class="token punctuation">{</span> <span class="token string">'Authorization'</span><span class="token punctuation">:</span>  <span class="token template-string"><span class="token string">`Bearer </span><span class="token interpolation"><span class="token interpolation-punctuation punctuation">${</span>token<span class="token interpolation-punctuation punctuation">}</span></span><span class="token string">`</span></span> <span class="token punctuation">}</span>

<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token keyword">const</span> <span class="token punctuation">{</span> user <span class="token punctuation">}</span> <span class="token operator">=</span> <span class="token keyword">await</span>  verifyResponse<span class="token punctuation">.</span><span class="token function">json</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token comment">// Step 3: Store token and make H5P requests</span>

localStorage<span class="token punctuation">.</span><span class="token function">setItem</span><span class="token punctuation">(</span><span class="token string">'authToken'</span><span class="token punctuation">,</span> token<span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token comment">// Now you can access H5P endpoints</span>

<span class="token keyword">await</span>  <span class="token function">fetchH5PContent</span><span class="token punctuation">(</span>token<span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token punctuation">}</span>

  

<span class="token keyword">async</span>  <span class="token keyword">function</span>  <span class="token function">fetchH5PContent</span><span class="token punctuation">(</span>token<span class="token punctuation">:</span> <span class="token keyword">string</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>

<span class="token keyword">const</span>  response <span class="token operator">=</span> <span class="token keyword">await</span>  <span class="token function">fetch</span><span class="token punctuation">(</span><span class="token string">'http://h5p-server:8080/h5p/contents'</span><span class="token punctuation">,</span> <span class="token punctuation">{</span>

headers<span class="token punctuation">:</span> <span class="token punctuation">{</span> <span class="token string">'Authorization'</span><span class="token punctuation">:</span>  <span class="token template-string"><span class="token string">`Bearer </span><span class="token interpolation"><span class="token interpolation-punctuation punctuation">${</span>token<span class="token interpolation-punctuation punctuation">}</span></span><span class="token string">`</span></span> <span class="token punctuation">}</span>

<span class="token punctuation">}</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token keyword">const</span> <span class="token punctuation">{</span> items <span class="token punctuation">}</span> <span class="token operator">=</span> <span class="token keyword">await</span>  response<span class="token punctuation">.</span><span class="token function">json</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>

<span class="token keyword">return</span>  items<span class="token punctuation">;</span>

<span class="token punctuation">}</span>

</code></pre>
<hr>
<h2 id="configuration-reference">Configuration Reference</h2>
<h3 id="storage-options">Storage Options</h3>
<p>| Option | Values | Description |</p>
<p>|--------|--------|-------------|</p>
<p>| <code>CONTENTSTORAGE</code> | <code>mongos3</code>, <code>mongo</code>, <code>s3</code>, <code>file</code> | Where to store H5P content |</p>
<p>| <code>LIBRARYSTORAGE</code> | <code>mongos3</code>, <code>mongo</code>, <code>s3</code>, <code>file</code> | Where to store H5P libraries |</p>
<p>| <code>TEMPORARYSTORAGE</code> | <code>s3</code>, <code>file</code> | Where to store temporary files |</p>
<p>| <code>USERDATASTORAGE</code> | <code>mongo</code> | Where to store user progress data |</p>
<h3 id="cache-options">Cache Options</h3>
<p>| Option | Values | Description |</p>
<p>|--------|--------|-------------|</p>
<p>| <code>CACHE</code> | <code>redis</code>, <code>memory</code> | Cache provider |</p>
<p>| <code>LOCK</code> | <code>redis</code> | Distributed lock provider |</p>
<h3 id="security-best-practices">Security Best Practices</h3>
<ol>
<li>
<p><strong>Use Strong JWT Secrets</strong>: Generate random, long secrets for production</p>
</li>
<li>
<p><strong>Enable HTTPS</strong>: Always use TLS in production</p>
</li>
<li>
<p><strong>Rate Limiting</strong>: Implement rate limiting on authentication endpoints</p>
</li>
<li>
<p><strong>CORS Configuration</strong>: Restrict CORS to your frontend domains</p>
</li>
<li>
<p><strong>Environment Variables</strong>: Never commit <code>.env</code> to version control</p>
</li>
<li>
<p><strong>Token Expiration</strong>: Use short-lived access tokens (15m - 1h)</p>
</li>
<li>
<p><strong>Refresh Tokens</strong>: Implement refresh token rotation</p>
</li>
</ol>
<h3 id="performance-tuning">Performance Tuning</h3>
<ol>
<li>
<p><strong>Redis Caching</strong>: Enable Redis for session caching in production</p>
</li>
<li>
<p><strong>CDN for Assets</strong>: Serve H5P core assets via CDN</p>
</li>
<li>
<p><strong>MongoDB Indexes</strong>: Ensure all collections have proper indexes</p>
</li>
<li>
<p><strong>Connection Pooling</strong>: Configure MongoDB connection pool size</p>
</li>
<li>
<p><strong>Upload Limits</strong>: Adjust <code>AWS_S3_MAX_FILE_LENGTH</code> based on your needs</p>
</li>
</ol>
<hr>
<h2 id="troubleshooting">Troubleshooting</h2>
<h3 id="common-issues">Common Issues</h3>
<p><strong>1. MongoDB Connection Refused</strong></p>
<pre class=" language-bash"><code class="prism  language-bash">
<span class="token comment"># Check MongoDB is running</span>

mongosh  mongodb://localhost:27017

  

<span class="token comment"># Check credentials in .env</span>

MONGODB_USER<span class="token operator">=</span>root

MONGODB_PASSWORD<span class="token operator">=</span>yourpassword

</code></pre>
<p><strong>2. S3 Upload Fails</strong></p>
<pre class=" language-bash"><code class="prism  language-bash">
<span class="token comment"># Verify AWS credentials</span>

aws  s3  <span class="token function">ls</span>  s3://your-bucket-name

  

<span class="token comment"># Check bucket permissions and CORS settings</span>

</code></pre>
<p><strong>3. Token Verification Fails</strong></p>
<pre class=" language-bash"><code class="prism  language-bash">
<span class="token comment"># Test external API manually</span>

curl  -H  <span class="token string">"Authorization: Bearer {token}"</span>  \

https://your-backend.com/auth/verify

  

<span class="token comment"># Check EXTERNAL_API_URL in .env</span>

</code></pre>
<p><strong>4. H5P Core Assets Not Found</strong></p>
<pre class=" language-bash"><code class="prism  language-bash">
<span class="token comment"># Re-download H5P core</span>

<span class="token function">npm</span>  run  download:core

  

<span class="token comment"># Check h5p/ directory exists</span>

<span class="token function">ls</span>  -la  packages/h5p-rest-server/h5p

</code></pre>
<hr>
<h2 id="api-reference">API Reference</h2>
<p>For detailed API documentation, run the server and visit:</p>
<p><strong>Swagger UI</strong>: <code>http://localhost:8080/docs</code></p>
<p><strong>OpenAPI JSON</strong>: <code>http://localhost:8080/docs/json</code></p>
<hr>
<h2 id="support--contributing">Support &amp; Contributing</h2>
<ul>
<li>
<p><strong>Issues</strong>: <a href="https://github.com/Lumieducation/H5P-Nodejs-library/issues">GitHub Issues</a></p>
</li>
<li>
<p><strong>Discussions</strong>: <a href="https://github.com/Lumieducation/H5P-Nodejs-library/discussions">GitHub Discussions</a></p>
</li>
<li>
<p><strong>Slack</strong>: <a href="https://join.slack.com/t/lumi-education/shared_invite/...">Lumi Education Slack</a></p>
</li>
</ul>
<hr>
<h2 id="license">License</h2>
<p>GNU General Public License v3.0 - See <a href="../../../LICENSE">LICENSE</a> file for details.</p>

