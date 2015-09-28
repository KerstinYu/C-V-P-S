Latex Fonts
===========

Introduction to fonts
---------------------

There are many font families e.g. Computer Modern, Times, Arial and
Courier. Those families can be grouped into three main categories: roman
(rm) or serif, sans serif (sf) and monospace (tt).Computer Modern Roman
is the default font family for LaTeX.

The three families are defined by their respective variables:

-   \rmdefault
-   \sfdefault
-   \ttdefault

The default family is contained in the \familydefault variable, and it
is meant to have one of the three aforementioned variables as value. The
default is defined like the following assignment:

    \renewcommand*{\familydefault}{\sfdefault}

This will turn all the part of the document using the default font to
the default sans serif, which is Computer Modern Sans Serif if you did
not change the default font.

Changing font families usually works in two steps:

1.  First specify which family you want to change (rm, sf or tt).
2.  Second specify the new default family if it is not rm.

Fonts may come with a package that will take care of defining all three
families plus the math fonts. You can do it by yourself, in which case
you do not have to load any package.

Below is an example that demonstrates how to change a specific family.

    % Default font (\familydefault = \rmdefault = Computer Modern Roman)
    Lorem ipsum dolor sit amet, consectitur adipiscing elit.

    % Palatino font (ppl must be installed).
    \renewcommand*\rmdefault{ppl}
    Lorem ipsum dolor sit amet, consectitur adipiscing elit.

    % Iwona font (iwona must be installed).
    \renewcommand*\rmdefault{iwona}
    Lorem ipsum dolor sit amet, consectitur adipiscing elit.

Font encoding
-------------

The default LaTeX font encoding is OT1, the encoding of the original
*Computer Modern* TeX text fonts. It contains only 128 characters, many
from ASCII.

The default Computer Modern font does *not* support T1. You will need
Computer Modern Super (cm-super) or *Latin Modern* (lmodern), which are
Computer Modern-like fonts with T1 support. There is nothing to change
in your document to use *CM Super* fonts (assuming they are installed),
they will get loaded *automatically* if you use *T1* encoding. For
*lmodern*, you will need to load the package after the T1 encoding has
been set:

    \usepackage['encoding']{fontenc}

    \usepackage[T1]{fontenc} %its default is cm-super
    \usepackage{lmodern}

Font Styles
-----------

### Shapes

    \textnormal{...}    document font family    This is the default or normal font.
    \emph{...}  emphasis    Typically italics. Using emph{} inside of italic text removes the italics on the emphasized text.
    \textrm{...}    roman font family   
    \textsf{...}    sans serif font family  
    \texttt{...}    teletypefont family     This is a fixed-width or monospace font.
    \textup{...}    upright shape   The same as the normal typeface.
    \textsl{...}    slanted shape   A skewed version of the normal typeface (similar to, but slightly different from, italics).
    \textsc{...}    Small Capitals  
    \textmd{...}    medium weight   A font weight in between normal and bold.
    \uppercase{...}         uppercase (all caps)    Also \lowercase. There are some caveats, though; see here.
    \lowercase{}
    \textit{...}    italic shape    
    \textbf{...}    bold    

For underline, use package rather than default command:

    \usepackage[normalem]{ulem}

-   To underline, use `\uline{...}`
-   To add a wavy underline, use `\uwave{...}`
-   For a strike-out (strikethrough), use `\sout{...}`
-   For a slash through each individual character `\xout{...}`

### Font Size

`\normalsize` is 10 point (option 10pt), but it may differ for some
Document Styles or their options, in which 1 pt is approximately 0.35136
mm.

1.  \tiny
2.  \scriptsize
3.  \footnotesize
4.  \small
5.  \normalsize
6.  \large
7.  \Large
8.  \LARGE
9.  \huge
10. \Huge

You may choose a particular font size with the
`\fontsize{<size>}{<line space>}` command. Example:

      {\fontsize{5cm}{1em}\selectfont This is big!}

### Local font selection

You can change font for a specific part of the text. There are four font
properties you can change.

-   \fontencoding
        The font encoding, such as OT1 (TeX default) or T1 (extended
    characters support, better PDF support, widely used).

-   \fontfamily
        The font family.

-   \fontseries
        The series: l=light, m=medium, b=bold, bx=very bold.

-   \fontshape
        The shape: it=italic, n=normal, sl=slanted, sc=small capitals.

    { \fontfamily{anttlc}\selectfont
      Some text in anttlc... }

The `\selectfont` command is *mandatory*, otherwise the font will not be
changed. It is highly recommended to enclose the command in a group to
cleanly return to the previous font selection when desired.

You can use all these commands in a row:

      {
      \fontencoding{T1}\fontfamily{anttlc}\fontseries{m}\fontshape{n}\selectfont
      Some text in anttlc...
      }

The default values are stored in \encodingdefault, \familydefault,
\seriesdefault and \shapedefault. Setting back the default font
properties can be done with

      \fontencoding{\encodingdefault}
      \fontfamily{\familydefault}
      \fontseries{\seriesdefault}
      \fontshape{\shapedefault}
      \selectfont

For short, you can use the
\usefont{<encoding>}{<family>}{<series>}{<shape>} command.

      \usefont{T1}{cmr}{m}{n} % Computer Modern Roman (TeX default) in T1 encoding. May lead to bad text quality if you do not have cm-super installed.
      \usefont{T1}{phv}{m}{sc} % phv family (sans serif) medium small capitals.
      \usefont{T1}{ptm}{b}{it} % ptm family bold italic
      \usefont{U}{pzd}{m}{n}   % ...

System fonts
------------

### XeTeX

#### fonts in XeTeX

If you use the *XeTeX* or *LuaTeX* engine and the fontspec package,
you'll be able to use any font installed in the system effortlessly.
XeTeX also uses *Unicode* by default, which might be helpful for font
issues.

To use the fonts, simply load the fontspec package and set the font:

    \documentclass{article}

    \usepackage{fontspec}
    \setmainfont{Arial}

    \begin{document}
    Lorem ipsum...
    \end{document}

Then compile the document with *xelatex* or *lualatex*. Note that you
can only generate .pdf file

Also you should *not* load the *inputenc* or *fontenc* package. Instead
make sure that your document is encoded as UTF-8 and load *fontspec*,
which will take care of the font encoding.

#### fontspec usage

    \fontspec [ font features ] { font name } % selects a font for one-time use 
    \setmainfont [ font features ] { font name }
    \setsansfont [ font features ] { font name }
    \setmonofont [ font features ] { font name }
    \newfontfamily cmd [ font features ] { font name }

Ligatures:

    \def\test#1#2{%
    #2 $\to$ {\addfontfeature{#1} #2}\\}
    \fontspec{Linux Libertine}
    \test{Ligatures=Historic}{strict}
    \test{Ligatures=Rare}{wurtzite}
    \test{Ligatures=NoCommon}{firefly}


    Ligatures=Required        ∗ rlig
              NoRequired      rlig (deactivate)
              Common          ∗ liga
              NoCommon        liga (deactivate)
              Contextual      ∗ clig
              NoContextual    clig (deactivate)
              Rare/Discretionary dlig
              Historic        hlig
              TeX             tlig/trep

##### BY FONT NAME

    \fontspec[ ... ]{Cambria}
    \fontspec[ ... ]{Adobe Garamond}

##### BY FILE NAME

XETEX and LuaTEX also allow fonts to be loaded by file name instead of
font name. When you have a very large collection of fonts, you will
sometimes not wish to have them all installed in your system’s font
directories. In this case, it is more convenient to load them from a
different location on your disk. This technique is also necessary in
XETEX when loading OpenType fonts that are present within your TEX
distribution, such as
`/usr/local/texlive/ 2013/texmf-dist/fonts/opentype/public`. Fonts in
such locations are visible to XETEX but cannot be loaded by font name,
only file name; LuaTEX does not have this restriction.

Fonts selected by filename must include bold and italic variants
explicitly.

    \fontspec
    [ BoldFont
    = texgyrepagella-bold.otf ,
    ItalicFont
    = texgyrepagella-italic.otf ,
    BoldItalicFont = texgyrepagella-bolditalic.otf ]
    {texgyrepagella-regular.otf}

or

    \fontspec
    [ Extension
    = .otf ,
    BoldFont
    = texgyrepagella-bold ,
    ... ]
    {texgyrepagella-regular}

or

    \fontspec
    [ Extension
    = .otf ,
    UprightFont
    = *-regular ,
    BoldFont
    = *-bold ,
    ... ]
    {texgyrepagella}

and to load a font that is not in one of the default search paths, its
location in the filesystem must be specified with the Path feature:

    \fontspec
    [ Path
    = /Users/will/Fonts/ ,
    UprightFont
    = *-regular ,
    BoldFont
    = *-bold ,
    ... ]
    {texgyrepagella}

##### e.g.

    \setmainfont{TeX Gyre Bonum}
    \setsansfont[Scale=MatchLowercase]{Latin Modern Sans}
    \setmonofont[Scale=MatchLowercase]{Inconsolata}
    \rmfamily Pack my box with five dozen liquor jugs\par
    \sffamily Pack my box with five dozen liquor jugs\par
    \ttfamily Pack my box with five dozen liquor jugs

### xelatex & pdflatex

To make your document support both pdflatex and xelatex/lualatex you can
use the \ifxetex/ \ifluatex macro from the *ifxetex*/ *ifluatex*
package. For example for xelatex

    \documentclass{article}
    \usepackage{ifxetex}

    \ifxetex
      \usepackage{fontspec}
      \defaultfontfeatures{Ligatures=TeX} % To support LaTeX quoting style
      \setromanfont{Hoefler Text}
    \else
      \usepackage[T1]{fontenc}
      \usepackage[utf8]{inputenc}
    \fi

    \begin{document}
    Lorem ipsum...
    \end{document}

Good fonts and their usage
==========================

Serif:
------

  -   Accanthis

        \usepackage[T1]{fontenc}
        \usepackage{accanthis}

  -   Baskervald

        \usepackage{baskervald}
        \usepackage[T1]{fontenc}

  -   Day Roman [S]

        \renewcommand*\rmdefault{dayrom[s]}
        \usepackage[T1]{fontenc}

  -   DejaVu Serif

        \usepackage{DejaVuSerif} 
        \usepackage[T1]{fontenc}

  -   Droid Serif

        \usepackage[default]{droidserif} 
        \usepackage[T1]{fontenc}

  -   Garamond

        \usepackage[urw-garamond]{mathdesign} 
        \usepackage[T1]{fontenc}

  -   EB Garamond

        \usepackage[lining,scaled=.95]{ebgaramond} % default:oldstyle %% set
        numbers:lining to display lining+oldstyle numbers
        \usepackage[T1]{fontenc}

  -   Libre Baskerville

        \usepackage{librebaskerville} 
        \usepackage[T1]{fontenc}

  -   Merriweather

        \usepackage[T1]{fontenc} 
        \usepackage{merriweather} %% Option 'black' gives heavier bold face

Sans:
-----

  -   Droid Sans

        \usepackage{droid}

  -   Droid Sans

        \usepackage[defaultsans]{droidsans}

  -   Venturis ADF Sans

        \usepackage[lf]{venturis} %% lf option gives lining figures

  -   Arev

        \usepackage{arev}

  -   Cantarell

        %% Use option "defaultsans" to use cantarell as sans serif only
        \usepackage[default]{cantarell} 

  -   Linux Libertine O

        \usepackage{libertine}

  -   Comfortaa

        \usepackage[default]{comfortaa}

  -   DejaVu Sans

        \usepackage{DejaVuSans}

  -   DejaVu Sans

        \usepackage{dejavu}

  -   DejaVu Sans Condensed

        \usepackage{DejaVuSansCondensed}

  -   Iwona

        \usepackage[math]{iwona}

  -   Helvetica

        \usepackage[scaled]{helvet}

  -   Lato

        \usepackage[default]{lato}

  -   Merriweather

        \usepackage[sfdefault]{merriweather} %

  -   Merriweather

        % Option 'black' gives heavier bold face
        \usepackage[black]{merriweather} 

  -   Merriweather

        \usepackage{merriweather} %% Option 'black' gives heavier bold face

  -   Open Sans

        \usepackage[default,osfigures,scale=0.95]{opensans}

  -   Open Sans

        \usepackage[defaultsans,osfigures,scale=0.95]{opensans}

  -   Paratype Sans

        \usepackage{paratype}

  -   Paratype Sans Caption

        \usepackage{PTSansCaption}

  -   Paratype Serif Caption

        \usepackage{PTSerifCaption}

  -   Source Code Pro

        \usepackage[default]{sourcecodepro}

  -   Source Sans Pro

        \usepackage[default]{sourcesanspro}

  -   TeX Gyre Adventor

        \usepackage{tgadventor}

  -   TeX Gyre Heroes

        \usepackage{tgheros} %enchanced HELVETICA font

  -   Venturis ADF Sans

        \usepackage[lf]{venturis} %% lf option gives lining figures as
    default;

Misc
----

 - see the tex path:

    kpsewhich --show-path=tex

 - keep every block of info in single seperate a.tex file, then `\input{a}` it from within main.tex. The main.tex uses all of the snipets all the time, and `\loremipsum` for the letter section. For letters, always use letter_where.tex and letter_where_pream.tex. The pream.tex only has the addr stuff.

