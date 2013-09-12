Palabra
=======

Tools for leaving Microsoft Word behind.

Over the past several days I have read lots and lots and lots of blog posts from writers who say, basically: "I'm going to quit using a word processor and start using text files instead." It seems that most of these writers have chosen to use Markdown as a way to apply formatting to their text documents, without ever moving their fingers from the keys. How nice! These writers all extoll the virtues of text plain text files: it's future-proof, it'll help my experiments with version control for writers -- so I'm sold! From now on, for me, I'll save my writings as some sort of text file.

But what about everything I've already written? 

I've been writing in Microsoft Word since at least 1995 and in that time I have amassed quite the collection of files: .doc files, .docx files, .rtf files, .html files, you name it, but not one of these is a plain text file. 

## How do I Convert Many Microsoft Word files Into Plain Text

note: I should start by saying that this process is not as easy as it should be, for the average writer. I'm sharing what (barely) worked for me, in the hopes of finding a better solution. I'm just learning, here.

If you're going to try this at home, back everything up. If you're like me, and you've got a lifetime of writings to convert from one file format to another, you do not want to risk losing anything because you screwed something up, so make a backup copy. Hell, make three.

So, how do I convert so many files? Should I just open each one up and do "save as" over and over and over again? Well, I could do that, but that would take forever! I decided, instead, to try a different method, one that might be able to be repeated by others and improved upon.

##Tools to do the Work

[Pandoc](http://johnmacfarlane.net/pandoc/) is a powerful command-line tool for converting many types of written documents, from one file format to another. (Pandoc is for Windows, Mac or Linux.) So I'll just use Pandoc for this, right? There's a catch. Pandoc doesn't work very well with .doc files and I still have many .doc files. Before I can use Pandoc to convert all my files into a text-based format, I'll need to use something first, to convert everything to a format that Pandoc can read.

[Textutil](https://developer.apple.com/library/mac/documentation/Darwin/Reference/ManPages/man1/textutil.1.html) is a command line utility baked into OS X. (Windows users, please chime in with any tools for windows that might help!) Textutil is similar to Pandoc, in that it can convert written documents from several formats into other formats, but although it can convert to .txt, it doesn't understand the Markdown formatting syntax, so I can't use Textutil to create the final product, unless I want to lose all my formatting. I don't have much formatting to lose, but still, that's not an option.

The trick, then, is to use Textutil to convert .doc files into .html files, and then to use Pandoc to convert .html files into .txt files with Markdown. 

I saw some forum posts that suggest that the following Terminal command might work (on OS X) as a way to combine Textutil with Pandoc:

```find . -name '*.doc' -print0 | xargs -0 sh -c 'textutil -convert html "$0" -stdout | pandoc -f html -t markdown -o "${0%.*}.md"'```

…but I couldn't get that to work for one file, let alone for dozens. I saw another post that said that bash loops might do the trick, and they did, but the examples weren't written for Pandoc so I wrote some code...

##Text Conversion Workflow

1. [Install Pandoc](http://johnmacfarlane.net/pandoc/installing.html)
2. Grab [the two shell scripts that I wrote](https://github.com/dylan-k/Palabra). I've posted them to Github and cleverly named them "Palabra".
3. Install the two files convert1.sh and convert2.sh into a directory full of .doc files that you would like to convert into Markdown-flavoured .txt files.
4. Point your terminal to that directory and from the terminal type "sh convert1.sh" This will convert all the .doc files in the directory into html files. (edit the file to say .doc if that's the kind you want to change)
5. then type "sh convert2.sh". This will convert all the html files you just made in step 2 into Markdown-flavoured .txt files.
4. Done!

… well, almost done. At this point, you've converted all your .doc files into Markdown-flavoured .txt files. To handle the .docx files, just edit line 2 of `convert1.sh` to read .docx instead of .doc and repeat the steps. (You should be able to do the same thing with .rtf but I haven't tried it yet.)

## One Word Document, Many Texts

One of my word .docx files was special in that it contains a copy of every one of my poems (a couple hundred, maybe?). That has gotten to be cumbersome after a few years, so I've decided to convert it into a set of text files. For extra credit, I wanted to name each file according to the first line of text, which in my case happened to be the title of the poem. I've lost the order that the poems were in, for now, but that wasn't so important to me anyway.

Here are some tips and tricks that helped me along the way

- [split one text file into many](https://gist.github.com/dylan-k/6517987)
- [rename each text file according to its first line of text](https://gist.github.com/dylan-k/6531959)
- [how to add .txt file extension to a batch of files with no file extension.](https://gist.github.com/dylan-k/6518333)

## useful links

- [convert batch of files via textutil](http://hints.macworld.com/article.php?story=20060309220909384) 
- [My question about this to Metafilter](http://ask.metafilter.com/248126/Convert-Many-Word-Documents-to-Markdown#3604336)
- [using bash loops for bash conversion](http://blog.silentumbrella.com/2009/10/08/bash-loops-are-fun-for-batch-conversion.html)





