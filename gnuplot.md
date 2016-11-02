### In the console

To plot data points store in 'datafile', the data should be organized in columns. The first row can include words labeling the content of the columns, and these can be automatically set to be in the legend. Separation between columns is arbitrary.

#### General comments

At any moment, if you need help just type `help` and choose the topic, and the subtopic if needed. Pressing Enter without typing anything will exit from the help pages. Every setting that can be `set` can also be `unset`. **All commands can be abbreviated by the first unique letters**, if there is ambiguity, gnuplot will complain.
Typing `quit` will exit from the gnuplot shell. Typing `reset` will `unset` **all** settings to their default values. Typing `save 'filename'` will save everything to disk, and `load 'filename'` will restore everything back. Typing `history` will show you the history of all your typed in commands. Typing `test` will show an overview of the line styles and line types set. Typing `show <setting>` will print the value assigned to that particular `<setting>`.
Note that all commands given below which specify an axis, such as `xrange` or `xlabel` are also valid for the y and z axis (when applicable) and are thus not written explicitly.

#### Set the terminal

    set terminal                    # shows the available terminals
    set terminal qt <n>             # plot to the qt gui number <n>, different numbers -> different windows!
    set terminal dumb               # plot to the terminal (awesome!!)
    set terminal pdf                # render the plot in a pdf file (using cairo)
    set terminal eps                # render the plot in an eps (using cairo)
    set terminal postscript         # render the plot in a postscript file (no cairo)
    set terminal epslatex           # plot (w/o text) in an eps file and create a tex file which render the text using Latex
    set terminal cairolatex pdf     # same as above but creates a pdf. (Note however that I was not able to use it..)

#### Output stream

    set output                      # set the default output / close a file if there is one open
    set output 'outfile'            # open file 'outfile' and write the output in it

After we have opened a file with `set output 'outfile'` and written in it, it is important **to close it** again with `set output`, otherwise the file will just remain empty. Note that when using `cairolatex`, we need to specify the latex file with `set output 'file.tex'`, and cairolatex will automatically create `file.pdf` with the figure.

#### Functions

    f(x) = x^2                                  # define a function called f(x)
    g(x,y) = 2.0*sin(x)+exp(y)                  # more than one variable, there are predefined functions too!
    h(x) = a*4.0 + b*sin(pi*x)                  # functions can have variables not yet set (i.e. a in this case)

#### Plot

    plot 'datafile' using 1:2                   # plot the first column in datafile as x and the second as y
    plot 'datafile' u 1:3 title columnhead      # plot the 1st and the 3rd column and use the text in the first row in the legend
    plot f(x)                                   # plot the function f(x)
    splot g(x,y)                                # plot the g(x,y) with lines
    splot g(x,y) with pm3d                      # plot the g(x,y) as a surface
    plot [xmin:xmax] [ymin:ymax] 'datafile'     # plot within a certain range
    replot f(x)                                 # superimpose the plot of f(x) to the previous plot (only in interactive mode!!)
    plot 'datafile' u 1:2, '' u 1:3             # plot simultaneously two sets of data points (preferred way!! Required for Latex!)
    plot 'datafile' u 1:2 with linespoints      # plot data points with points and lines
    plot 'datafile' u 1:2 with lp ls 2          # plot data points with points and lines of style number 2 (ls = linestyle)
    plot 'datafile' u 1:2 with lp lt 2          # plot data points with points and lines of type number 2 (lt = linetype)
    plot 'datafile' u 1:2 with lines lw 3       # plot data points with lines of width 3
    plot 'datafile' u 1:2 lc rgb '#e69f00'      # plot data points with lines of color #e69f00
    plot 'datafile' u 1:2 with points ps 4      # plot data points with points of size 4
    plot 'datafile' u 1:2 with p pt 7           # plot data points with points of type 7
    plot 'datafile' u 1:2 with p lc rgb 'blue'  # plot data points with points of blue color
    plot 'datafile' u 1:(27.21*$2)              # plot data points, scaling the y data by 27.21

#### Fitting

    fit h(x) 'datafile' u 1:5 via a,b           # fit h(x) to the points in 'datafile', finding the best values for a and b -> assigns the values to a and b

#### Axes, grids, ranges, labels, tics, ...

    set grid                                    # set a grid in the background of the plot
	set size square								# set square ratio for the plot
    set xzeroaxis                               # set a dotted line as the x-axis
    set xzeroaxis linetype -1                   # adding linetype -1 makes it the same as the border lines
    set xrange [xmin:xmax]                      # set x range from xmin to xmax
    set xlabel 'Can contain \Latex code'        # set the axis label (Latex available using cairolatex term)
    set xtics xmin,dx,xmax                      # set tics from xmin to xmax every dx
    set xtics add (8,12,14,20)                  # set tics at those specific positions
    set xtics nomirror                          # remove tics on the opposite border
    set xtics ('lab' 0, 'lab2' 2, ...)          # set tics with specific labels (strings!)

#### Title, legend, labels

    set title 'The title of the figure'         # set the title
    set key off                                 # turn legend off (on by default)
    set key Left                                # left justify text in the legend (there is discrepancy between qt and eps terminals)
    set key Left width -<k>                     # reduces the spacing between the text and the symbol/line
    set key samplen <k>                         # controls length of lines/symbols in the legend (default is 4!)
    set key at <x>,<y>                          # put the legend exactly where you want it
    set label 'bla bla' at <x>,<y>              # put a label at <x>,<y> where x,y, refers to values in the plot

#### Multiplot: tip & tricks

	set multiplot layout <n>,<m>				# set <n> rows with <m> plots each
	set lmargin <val>							# set a fixed size margin
	set rmargin <val>							# this is helpful if we want to put tics or label
	set bmargin <val>							# only on one axis, it keep the plot size constant!
	unset label									# if labels are set on one plot, need to be unset otherwise appear on next plot too!

#### Various helpful commands

    help set style                              # to see all possible things that can be set to modify line, points, ...
    show linetype <n>                           # show the settings for linetype <n>
    test                                        # show capabilities of actual terminal, useful for deciding point type

#### Colors

    show colors                                 # show all the predefined colors

###### Built-in colors pairings (dark / bright)

    forest-green / web-green
    dark-orange / light-red
    royalblue / skyblue
	dark-goldenrod / light-goldenrod

###### Numix darkest palette
Dark colors

    linecolor rgb '#555555'                     # black  
    linecolor rgb '#9c3528'                     # red    
    linecolor rgb '#61bc3b'                     # green  
    linecolor rgb '#f3b43a'                     # yellow
    linecolor rgb '#0d68a8'                     # blue   
    linecolor rgb '#744560'                     # magenta
    linecolor rgb '#288e9c'                     # cyan   
    linecolor rgb '#a2a2a2'                     # white  
Bright colors

    linecolor rgb '#888888'                     # black  
    linecolor rgb '#d64937'                     # red    
    linecolor rgb '#86df5d'                     # green  
    linecolor rgb '#fdd75a'                     # yellow
    linecolor rgb '#0f75bd'                     # blue   
    linecolor rgb '#9e5e83'                     # magenta
    linecolor rgb '#37c3d6'                     # cyan   
    linecolor rgb '#f9f9f9'                     # white  

### Guidelines for publication quality plots

For (simple) plots, using vector graphics (i.e. eps, ps, pdf) is the best choice, for images one would usually prefer raster graphics (tiff format above all, or alternatively **high quality** png or jpeg). The size of the picture is very important, because the editor will probably rescale it to fit it into the article, hence the closer the image is to the *correct* size, the more likely it will be as we expect it to be in the final version of the article. For a one-column figure the max width is around 8.25 cm, while for a two-column figure the min width is around 10.5 cm and the max around 16 cm. To set the size, either use `set size <x>cm,<y>cm` or in the terminal line `terminal ... size <x>cm,<y>cm`. For colored figures, use `set terminal epslatex color colortext`.  
Always check the journal website for other format recommendations!
Another useful tip: Use different line styles (dashed, dotted, ...) in addition to colors for the curves, in a print-out in black and white, colors are not distinguishable! Moreover, in the captions, do not refer to colors but to positions or line styles, for the same reason!

### How to include the created figures in a Latex document

Let us assume in the folder containing the main Latex document there is a 'figures' subfolder. We put there both the eps and tex files generated by gnuplot and in the main Latex document we add in the preamble the following lines of code

    \usepackage{color}                          # enables the use of colors in the plot
    \usepackage{graphicx}                       # enable to include figures in your document
    \graphicspath{{./figures/}}                 # add to the path the subfolder such that it can find the figure
                                                # note that the extra braces {} are necessary as well as the last slash /

Now, inside the document environment, to include the figure without rescaling, use

    \begin{figure}
        \centering
        \input{figures/my_figure.tex}
        \caption{Bla bla bla.}
        \label{fig:my_fig}
    \end{figure}

If we want to scale the figure, we need to do a small trick in order to maintain the font size consistent with the rest of the document

    \begin{figure}
        \centering
        \fontsize{16}{16}           % adjust it according to how much we scale the figure
        \resizebox{8cm}{!}{\input{figures/my_figure.tex}}   % the {!} maintains the aspect ratio
        \caption{Bla bla bla.}
        \label{fig:my_fig}
    \end{figure}

However, as explained above, it is strongly advice to generate the figure using gnuplot already with the right dimension, such that there is no need to rescale it, or if there is rescaling is minimal and there is no need to adapting the font size accordingly.

#### Some external resources (from where most of the content has been taken)

<http://vergil.chemistry.gatech.edu/resources/figures.html>  
<https://github.com/damarquezg/Tools-Cheat-Sheet/wiki/Gnuplot>  
<http://alvinalexander.com/technology/gnuplot-charts-graphs-examples>  
<https://chemistry.osu.edu/~foster.281/gnuplot/gnuplot_tutorial3_files/gp_manip.html>  
