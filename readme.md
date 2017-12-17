#Sample HarpJs site

###Introduction
This is a simple site made as an exercise to demonstrate the HarpJS Static Site Generator. The text and illustrations from **The Rime of the Ancient Mariner** are used as example text, with poem chapters taking the role of blog posts.

http://harpjs.com/

The structure of pages is defined in templates (layouts) and the content is defined in either EJS templates markup, or Markdown files. The Harp server then uses these to build the HTML pages, either compiling static pages or serving HTML in real time.

###Structure
Any files to be watched, compiled and served are in the *public* directory. You can add the top-level pages into the public directory. You can add content into sub-folders, for example in this project, having the *chapters* pages inside the chapters sub-directory. 

###URLS
URLs are built based on the directories and filenames. Harp looks for a file called *index* in the project root or the public folder, to load as the homepage.
The URLs for the pages in the *chapters* subdirectory will take the form www.domain.com/chapters/file-name.

**Each sub-folder needs its own _data.json file**

###MetaData
Custom meta data for the project is defined in JSON files. Generally each page is represented by a JSON object, with key:values for each piece of metadata.
Each page or post needs to have metadata defined in the JSON. So if you added a new page, you would need to add another object to the metadata with the relevant key:values.

####Globals
The harp.json file in the project root defines global variables, available across all templates. You can access these variables in the templates using the key values, e.g the *title* in the header partial.

####Folder specific metadata
You can define a _data.json file in each sub-folder, to define custom metadata for these sections. E.g in the chapters/_data.json file, we define the path to the header images. These are exposed to the templates as an object in **public.folder-name._data**

####Templating
Harp looks for a _layout file to use as the template. This can be ejs, jade or just html.
We call *yield* in the template to bring in the content.
We can use a different layout file for each sub-folder, and we can define different templates for specific pages, from within the metadata.

####Partials
You can call the partial() function within the templates, to load in other sub-templates. In this project, we keep them in a folder *partials*. Paths to partials need are relative to the current file.

####Looping over Metadata
Since the templates are based on javascript, we can loop over the metadata JSON, to build custom site elements. For example the *chapter-links.ejs* partial loops over the list of chapters, and generates a nav link for each one.

####Inheritance
Metadata values cascade down through the directory structure, in effect making the globally defined ones 'defaults' and the sub-folder metadata overwrites of these defaults. Therefore, we can refer to the title property in the template of the chapters, and if a title is not defined in the subdirectory _data.json, the global value will be used.

####Compiling CSS
Harp watches and compiles SASS and other CSS-like languages. In this case we use a single custom SASS file, main.scss in the public/css folder. This gets automatically compiled to main.css by the Harp server, into the same folder, so we don't need to worry about watching the directory via an separate build tool/NPM script.

###Running
NPM install to get HarpJS installed, or install it globally.
To run the project, open a command line in the project root and do *harp server*. This will run the site locally on port 9000.

###Deploying
A simple procfile is included, so the site can be easily deployed to Heroku. The harp server can run on the Heroku container, serving the compiled pages.