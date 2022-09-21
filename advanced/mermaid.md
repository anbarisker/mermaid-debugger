## Enabling Mermaid Alpha Two

Mermaid is an engine that enables you to draw beautiful, highly detailed SVG diagrams and flowcharts
using Markdown. It is supported out of the box on developer documentation portal.

Some examples of Mermaid diagrams can be found [below](#examples). For usage instructions
and the full range of supported diagrams,
visit [https://mermaid-js.github.io/mermaid](https://mermaid-js.github.io/mermaid).

To view Mermaid diagrams on your local Docsify server, import Mermaid
and edit your Docsify
configuration in your `index.html` file as shown below:

```html
<body>
	<!-- 1. Import mermaid.js, BEFORE the window.$docsify initialisation -->
	<script src="//cdn.jsdelivr.net/npm/mermaid/dist/mermaid.min.js"></script>

	<script>
		// 2. Add the two lines below before declaring the window.$docsify object:
		var num = 0;
		mermaid.initialize({ startOnLoad: false });

		// 3. Add the "markdown" option to window.$docsify in addition to the other config
		window.$docsify = {
			...otherDocsifyConfig,
			markdown: {
				renderer: {
					code: function (code, lang) {
						if (lang === "mermaid") {
							return (
								'<div class="mermaid">' +
								mermaid.render("mermaid-svg-" + num++, code) +
								"</div>"
							);
						}
						return this.origin.code.apply(this, arguments);
					},
				},
			},
		};
	</script>
	<!-- ...other imports -->
</body>
```

## Writing diagrams

To write a Mermaid diagram, simply use a code block with the language type set to `mermaid`:

````
```mermaid
graph TD;
	 A-->B;
	 A-->C;
	 B-->D;
	 C-->D;
```
````

Example 2

```mermaid
flowchart LR
	subgraph "Legend"
		direction LR
		n1(start) --- a1["user's task"] --> j1
		j1 -...-> j2
		j3 --> n2(end)
		subgraph "Compliance-Framework"
			subgraph "Stage"
				j2[optional-job*] --> j3[job]
			end
		end
		
		subgraph "File"
			direction LR
			j1[job]
		end
	end

	classDef J fill:#ffd,stroke:#cc7;
	class j1,j2,j3 J;
	classDef A fill:#ddd,stroke:#eee;
	class a1 A;
	classDef F fill:#fff,stroke:#226;
	class File,Legend F;
	classDef C fill:#fff,stroke:#226,stroke-dasharray: 5 5;
	class Compliance-Framework,Stage C;
	classDef N fill:#eef,stroke:#226;
	class n1,n2 N;
```
