Pyllica
=======

Pyllica is a small python tool to retrieve the text-version of newspapers in <a href="http://gallica.bnf.fr/">gallica</a>, the main french digital library. It works also for books and other single documents (and, soon perhaps, for periodicals). 

It will not retrieve documents that are only accessible in image version (that is, that have not been <a href="https://en.wikipedia.org/wiki/Optical_character_recognition">OCRized</a>).

<h3>Installation and requirements</h3>

It is based on python 2.7.5 and requires the module <em>beautiful soup</em> (<a href="http://www.crummy.com/software/BeautifulSoup/)">more info</a>).

To initiate pyllica, put pyllica.py in the directory where you want to archive the texts and open a new python file (you can also write directly your commands into pyllica.py, but it is much practical to work with a clean file). It should begin with:

<blockquote>
from pyllica import *
</blockquote>

A typical command file would look like this :
<blockquote>
from pyllica import *<br /> <br />
textpress(url="http://gallica.bnf.fr/ark:/12148/cb39294634r/date", title="debats", year=1900, month=2, day=28, rate=1, item=1, firstpage=2, lastpage=2)
</blockquote>

On my computer, the download rate was approximately 10-15 pages per minute for newspapers (much quicker for usual books, as pages are lighter and there is less calculus involved). The rate could go higher or lower depending on the efficiency of your laptop the quality of your internet connection.

The tool currently includes two functions, texpress and textbook.

<h3>Textpress</h3>

textpress(url, title, year, month, day, item, rate, firstpage, lastpage, sep1, sep2) is an advanced function to deal with newspapers in gallica. It allows to fetch a given number of newspaper, from a startdate. The rate of fetching (one newspaper out of 7, for example) ou the number of pages retrieved can also be customised. 

To use textpress, you have to specify the following information:<ul>
<li><b>url</b> = url id for the newspaper (for instance, "http://gallica.bnf.fr/ark:/12148/cb34431794k/" for "Le Temps"). The information must be a string (and put into brackets).</li>
<li><b>title</b> = title of the retrieved file (preferably the name of the newspaper, but it can be anything). The information must be a string (and put into brackets).</li>
<li><b>year</b> = year of the startdate file</li>
<li><b>month</b> = month of the startdate file</li>
<li><b>day</b> = day of the stardate file</li>
<li><b>item</b> = number of newspapers retrieved</li> 
<li><b>rate</b> = rate of fetching. For instance, a rate of 7, will give you a newspaper every week. This is especially useful if you look for journalistic texts that appears on a non-daily basis (a weekly chronicle…).</li>
<li><b>firstpage</b> = the first page you are looking for.</li>
<li><b>lastpage</b> = the last page you are looking for. If you only fetch one page, put the same number as firstpage. Till the end of the XIXth century, french newspapers usually cormprises 4 pages: if you are looking for the whole newspaper lastpage=4 should do the trick.</li>
<li><b>sep1</b> = the first separator in order to isolate the beginning of a press section from the early part of a page. This parameter is optional</li>
<li><b>sep2</b> = the last separator in order to isolate the end of a press section from the late part of a page. This parameter is optional</li>
</ul>

If you want first two pages of all the issues published on monday of the "journal des débats" of the year 1862, you can use the following:

<blockquote>
textpress(url="http://gallica.bnf.fr/ark:/12148/cb39294634r/date", title="lesdebats", year=1862, month=1, day=6, rate=7, item=52, firstpage=1, lastpage=2)
</blockquote>

pyllica also provindes you a brief index of the gallica url of the mains french newspaper archived in gallica.

<h3>Textbook</h3>

textbook(url, title, firstpage, lastpage) is a much simpler function than textpress. It allows you to get a set of pages from any text-version of a document on gallica.

To use textbook, you have to specify the following information:<ul>
<li><b>url</b> = url id for the book. The information must be a string (and put into brackets).</li>
<li><b>title</b> = title of the retrieved file (preferably the name of the book, but it can be anything). The information must be a string (and put into brackets).</li>
<li><b>firstpage</b> = the first page you are looking for.</li>
<li><b>lastpage</b> = the last page you are looking for. If you only fetch one page, put the same number as firstpage.</li>
</ul>

If you're looking the pages 13 to 15 of the <a href="http://gallica.bnf.fr/ark:/12148/bpt6k6290660h">1837 edition</a> of the <a href="http://gallica.bnf.fr/ark:/12148/cb32688404r/date">Almanach du commerce</a> of Sébastien Bottin (a splendid corpus for vintage data mining, by the way), you can use the following:

<blockquote>
textbook(url="http://gallica.bnf.fr/ark:/12148/bpt6k6290660h", title="bottin", firstpage=13, lastpage=15)
</blockquote>

<h3>What's next?</h3>

If all works fine you should see your directory should list the retrieved files in the following manneer:
<blockquote>
lesdebats-18630103.txt<br />
lesdebats-18630102.txt<br />
lesdebats-18630101.txt<br />
lesdebats-18621231.txt<br />
</blockquote>

As the OCR recognition of Gallica is not perfect (about 5-10% of misread words for standard journalistic text, as much as 40% when the original copy is in a bad shape), the texts are better suited for large quantitative data analysis.

While you can do some convenient data analysis with python, I would recommend using a more powerful statistic language. <a href="http://www.r-project.org/">R</a> includes an <a hrefh="http://cran.r-project.org/web/packages/tm/index.html">effective library</a> for text and data mining, tm. This <a href="http://cran.r-project.org/web/packages/tm/vignettes/tm.pdf">introduction</a> to the tm package is quite accessible.

<h3>Future development</h3>

I'm planning to do the following things:<ul>
<li><b>Rewrite the code for older version of python</b> (and using regex to avoid the installation of beautiful soup).</li>
<li><b>Adding a new function to retrieve issues of periodicals</b> (<a href="http://gallica.bnf.fr/ark:/12148/cb32688404r/date">like this one</a>).</li>
<li><b>Adding a set of functions to deal with image and pdf versions</b> (an adaptation of the <a href="https://fr.wikisource.org/wiki/Wikisource:Gallica/gallica.ml">fine script</a> of <a href="https://fr.wikisource.org/wiki/Utilisateur:Pmx">Pmx</a> for Wikisource for python might seem nice).</li>
<li><b>Inclusion of tabular content recognition</b>. Instead of being read like texts, tables would be recognised as data structure</li>
<li><b>Adding gallica metadata to the retrieved files</b> (authors, editors and so forth…).</li>
<li><b>Developing of repository of section separators for several old french newspapers</b>, so that the content of a specific section can be retrieved. I've made up a function to fetch all the business sections of the "Journal des débats" in the 1860s: the results were not perfect (one issue out of two were properly retrieved), as this function relies on excellent OCR recognition. This is still an improvement from all-manual processes.</li>
</ul>
