<h2>The File System Promises API</h2>
<p>
  In the following code snippet, I'll be using the fs Promises API.<br>
  It's available to you if you're rocking at least Node.js v10.
</p>

<h2>The reason you're here</h2>
<code>const { promises: fs } = require("fs");

async function getFiles(path = "./") {
    // Get files within the current directory and add a path key to the file objects
    const files = (await fs.readdir(path, { withFileTypes: true }))
        .filter(file => !file.isDirectory())
        .map(file => ({ ...file, path: path + file.name }));
	
    // Get folders in within the current directory
    const folders = (await fs.readdir(path, { withFileTypes: true })).filter(folder => folder.isDirectory());

    for (const folder of folders)
        /*
          Add the found files within the subdirectory to the files array by calling the
          current function itself
        */
        files.push(...await getFiles(`${path}${folder.name}/`));

    return files;
}</code>

<h2>Example output</h2>
<code>[
    { name: 'index.js', path: './index.js', [Symbol(type)]: 1 },
    { name: 'test2_index.html', path: './test2/test2_index.html', [Symbol(type)]: 1 }
]</code>
