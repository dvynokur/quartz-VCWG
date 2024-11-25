---
title: <%* 
	let title = tp.file.title
	if (title.startsWith("Untitled")) {
		title = await tp.system.prompt("Title"); 
		await tp.file.rename(`${title}`); 
	}
%> <%* tR += `${title}` %>
draft: true
socialImage: logo.png
socialDescription:
---
 
---
[Home Page](index.md)
